# 🛡️ Proxmox Home SOC Lab

Projekt domowego laboratorium bezpieczeństwa opartego na wirtualizacji **Proxmox VE**. Celem laba jest monitorowanie zagrożeń, analiza incydentów oraz automatyzacja odpowiedzi (SOAR).

## 🏗️ Architektura Systemu
- **Hypervisor:** Proxmox VE 9.1.1
- **Sieć:** Izolowane VLANy dla segmentu zarządzania i monitorowania.
- **Node:** `my-lab`

## 📦 Inwentarz Usług (LXC/VM)

| ID  | Usługa              | Rola                        | Status      | Adresacja (Internal) |
| :-- | :------------------ | :-------------------------- | :---------- | :------------------- |
| 100 | DNS Security        | DNS Sinkhole (AdGuard)      | ✅ Active   | 192.168.x.x          |
| 101 | Reverse Proxy       | Ingress Control (NPM)       | ✅ Active   | 192.168.x.x          |
| 102 | SIEM/XDR            | Threat Detection (Wazuh)    | ✅ Active   | 192.168.x.x          |
| 103 | Incident Response   | Case Management (TheHive)   | 🕒 Planned  | -                    |

## 🛠️ Stack Technologiczny
- **SIEM:** [Wazuh](https://wazuh.com) - Detekcja intruzów i log management.
- **Incident Response:** [TheHive](https://thehive-project.org) - Zarządzanie sprawami i śledztwo.
- **Network Security:** [AdGuard Home](https://adguard.com) - Blokowanie złośliwych domen.
- **Ingress:** [Nginx Proxy Manager](https://nginxproxymanager.com) - Bezpieczne wystawianie usług.

## 🚀 Plan Rozwoju
- [x] Konfiguracja Proxmox VE 9.x.
- [x] Wdrożenie DNS Security.
- [x] Instalacja Wazuh Manager w architekturze kontenerowej (Docker).
- [x] Konfiguracja automatyzacji startu usług (Systemd Unit Files).
- [x] Wdrożenie pierwszego agenta na systemie Windows (Endpoint Monitoring).
- [ ] Implementacja monitorowania integralności plików (FIM).
- [ ] Integracja TheHive z Wazuh (SOAR workflow).

🛡️ Capabilities:
- **Endpoint Monitoring:** Zbieranie logów z systemów Windows przez agentów Wazuh.
- **Persistence:** Automatyczne wznawianie usług po restarcie hosta (Docker + Systemd).
- **Network Privacy:** Izolacja usług monitorujących od głównego segmentu sieci.
