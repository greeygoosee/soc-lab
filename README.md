# 🛡️ Proxmox Home SOC Lab

Projekt laboratorium bezpieczeństwa opartego na wirtualizacji **Proxmox VE**. Celem tego laba jest monitorowanie zagrożeń, analiza incydentów oraz automatyzacja odpowiedzi (SOAR).

## 🏗️ Architektura Systemu
- **Hypervisor:** Proxmox VE 9.x
- **Sieć:** Izolowane segmenty sieciowe dla zarządzania i monitorowania.
- **Node:** `my-lab`

## 📦 Inwentarz Usług (LXC/VM)
| ID  | Usługa              | Rola                        | Status      |
| :-- | :------------------ | :-------------------------- | :---------- |
| 100 | DNS Security        | DNS Sinkhole (AdGuard)      | ✅ Active   |
| 101 | Reverse Proxy       | Ingress Control (NPM)       | ✅ Active   |
| 102 | SIEM/XDR            | Threat Detection (Wazuh)    | ✅ Active   |
| 103 | Incident Response   | Case Management (TheHive)   | 🕒 Planned  |

## 🛠️ Stack Technologiczny
- **SIEM:** [Wazuh](https://www.google.com/search?q=wazuh+siem+xdr+features) - Detekcja intruzów i log management.
- **Persistence:** Systemd Unit Files dla automatyzacji startu kontenerów Docker.
- **Network Security:** AdGuard Home - Blokowanie złośliwych domen i telemetrii.
- **Ingress:** Nginx Proxy Manager - Bezpieczne wystawianie usług i zarządzanie SSL.

## 🚀 Plan Rozwoju
- [x] Konfiguracja środowiska wirtualizacji.
- [x] Wdrożenie DNS Security.
- [x] Instalacja Wazuh Manager (Docker Single-Node).
- [x] Konfiguracja statycznej adresacji IP i autostartu usług.
- [x] Wdrożenie pierwszego agenta na systemie Windows (Endpoint Monitoring).
- [ ] Implementacja File Integrity Monitoring (FIM).
- [ ] Integracja TheHive z Wazuh przez Shuffle/n8n.

🛡️ Capabilities:
- **Endpoint Monitoring:** Zbieranie logów z systemów Windows przez agentów Wazuh.
- **Persistence:** Automatyczne wznawianie usług po restarcie hosta (Docker + Systemd).
- **Network Privacy:** Izolacja usług monitorujących od głównego segmentu sieci.

🧠 Key Learnings & Challenges Overcome
Podczas budowy laboratorium napotkałem kilka krytycznych wyzwań, których rozwiązanie pozwoliło mi na głębsze zrozumienie architektury sieciowej i bezpieczeństwa:

Network Infrastructure Shift: Pierwotna konfiguracja opierała się na podwójnym NAT (router dostawcy + własny router). Wyzwaniem była poprawna adresacja maszyn wirtualnych. Problem rozwiązany poprzez przełączenie routera brzegowego w Bridge Mode i rekonfigurację podsieci na 192.168.88.x, co umożliwiło uzyskanie pełnej kontroli nad ruchem i statyczną adresacją usług.

Wazuh Credentials & Docker Persistence: Napotkałem trudności z synchronizacją haseł między indexerem a dashboardem po zmianie adresacji IP. Rozwiązaniem było wdrożenie plików .env oraz ręczna modyfikacja docker-compose.yml, co wymusiło poprawne wczytanie poświadczeń przy jednoczesnym zachowaniu trwałości wolumenów (Docker Volumes).

Service Reliability (Systemd Integration): Aby zapewnić wysoką dostępność (High Availability) usług SOC po restarcie fizycznego hosta, opracowałem i wdrożyłem własne jednostki systemd (Unit Files). Dzięki temu stack kontenerowy startuje automatycznie w odpowiedniej kolejności, uwzględniając zależności sieciowe.

Endpoint Security Enforcement: Pierwsze próby wdrożenia agenta kończyły się błędami uprawnień (Access Denied). Nauczką była konieczność egzekwowania pełnych uprawnień administracyjnych w PowerShell oraz weryfikacja polityk zapory systemowej pod kątem komunikacji z Managerem.

## Etap 2: Monitorowanie Integralności Plików (FIM) & Whodata

Kolejnym krokiem było wdrożenie modułu **FIM**, który pozwala na natychmiastowe wykrywanie nieautoryzowanych zmian w kluczowych katalogach systemu Windows.

### Kluczowe funkcjonalności:
- **Real-time Monitoring:** System wykrywa dodanie, modyfikację lub usunięcie pliku w ciągu kilku sekund od zdarzenia.
- **Analiza Whodata:** Dzięki integracji z systemowym audytem Windows, Wazuh raportuje nie tylko **co** się zmieniło, ale także **kto** (użytkownik) i **jakim programem** (proces) dokonał zmiany.

### Scenariusz testowy:
1. Skonfigurowano monitorowanie katalogu `C:\SOC_Test` za pomocą konfiguracji grupowej (`agent.conf`).
2. Przeprowadzono symulację ataku polegającą na stworzeniu i edycji pliku `hasla.txt`.
3. System poprawnie wygenerował alerty poziomu 7 (File added/modified), wzbogacone o dane kryminalistyczne (nazwa użytkownika i nazwa procesu).

> **Konfiguracja:**
> `<directories check_all="yes" report_changes="yes" whodata="yes">C:\SOC_Test</directories>`
