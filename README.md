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
