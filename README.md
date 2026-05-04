# 🛡️ Proxmox Home SOC Lab

Projekt domowego laboratorium bezpieczeństwa opartego na wirtualizacji **Proxmox VE**. Celem laba jest monitorowanie zagrożeń, analiza incydentów oraz automatyzacja odpowiedzi (SOAR).

## 🏗️ Architektura Systemu
- **Hypervisor:** Proxmox VE 9.1.1
- **Sieć:** Izolowane VLANy dla segmentu zarządzania i monitorowania.
- **Node:** `my-lab`

## 📦 Inwentarz Usług (LXC/VM)
| ID  | Nazwa Usługi | Rola | Status |
| :--- | :--- | :--- | :--- |
| 100 | AdGuard Home | DNS Sinkhole & Security | ✅ Running |
| 101 | Nginx Proxy Manager | Reverse Proxy & SSL | ✅ Running |
| 102 | Wazuh Manager | SIEM / XDR | 🕒 Planowane |
| 103 | TheHive | Incident Response Platform | 🕒 Planowane |

## 🛠️ Stack Technologiczny
- **SIEM:** [Wazuh](https://wazuh.com) - Detekcja intruzów i log management.
- **Incident Response:** [TheHive](https://thehive-project.org) - Zarządzanie sprawami i śledztwo.
- **Network Security:** [AdGuard Home](https://adguard.com) - Blokowanie złośliwych domen.
- **Ingress:** [Nginx Proxy Manager](https://nginxproxymanager.com) - Bezpieczne wystawianie usług.

## 🚀 Plan Rozwoju
- [x] Konfiguracja Proxmox VE.
- [x] Wdrożenie DNS Security (AdGuard).
- [ ] Instalacja Wazuh Manager (Master Node).
- [ ] Integracja TheHive z Wazuh przez Shuffle/n8n.
- [ ] Wdrożenie agentów na stacjach roboczych.
