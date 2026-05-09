# SOC Automation Lab: Wazuh EDR & Active Response 🛡️

Projekt profesjonalnego środowiska SOC (Security Operations Center) opartego na systemie Wazuh. Laboratorium demonstruje pełny cykl życia incydentu: od monitorowania i wykrywania podatności, po automatyczną, programową reakcję na zagrożenia.

## 🏗️ Architektura Systemu
- **SIEM/EDR Manager:** Wazuh (Open-source Security Platform)
- **Deployment:** Konteneryzacja Docker (High Availability / Scalability)
- **Endpointy:** Agenty Wazuh wdrożone na systemach Windows
- **Główne funkcjonalności:** FIM (File Integrity Monitoring), Vulnerability Detector, Active Response

---

## 🔬 Moduł 1: Monitorowanie Integralności Plików (FIM) & Whodata
Wdrożono zaawansowany nadzór nad krytycznymi zasobami systemowymi.

### Kluczowe funkcjonalności:
- **Detekcja w czasie rzeczywistym:** Monitorowanie zdarzeń typu Add/Modify/Delete w zdefiniowanych ścieżkach krytycznych.
- **Wzbogacanie danych (Whodata):** Integracja z audytem Windows w celu identyfikacji sprawcy (User) oraz narzędzia (Process Name/ID) użytego do modyfikacji pliku. Pozwala to na szybką segregację zmian autoryzowanych od potencjalnych ataków.

---

## 🔍 Moduł 2: Zarządzanie Podatnościami (Vulnerability Management)
Konfiguracja automatycznego skanowania endpointów pod kątem znanych luk w zabezpieczeniach.

### Zakres działań:
- **Integracja z bazami CVE:** Automatyczne mapowanie zainstalowanego oprogramowania i poprawek systemowych z bazami NVD oraz Microsoft Security Update (MSU).
- **Priorytetyzacja ryzyka:** Klasyfikacja podatności (Critical, High, Medium) pozwalająca na efektywne zarządzanie procesem Patch Managementu.

---

## ⚡ Moduł 3: Active Response (Automatyczna Defensywa)
Implementacja mechanizmów aktywnej obrony, skracających czas reakcji (MTTR) do minimum.

### Logika działania:
- **Analiza zdarzeń:** Automatyczne filtrowanie alertów o wysokim priorytecie (Level 6+).
- **Programowa reakcja:** Integracja z Windows Defender Firewall za pomocą skryptów wywołujących polecenie `netsh`.
- **Wynik:** Dynamiczne izolowanie podejrzanych adresów IP na poziomie warstwy sieciowej w odpowiedzi na wykryte incydenty (np. próby nieautoryzowanego dostępu lub manipulacji plikami).

---

## 🗺️ Roadmap & Rozwój Projektu
Projekt jest stale rozwijany o kolejne moduły bezpieczeństwa:
- **Integracja z SOAR (TheHive):** Planowane wdrożenie platformy do zarządzania sprawami (Case Management) i automatyzacji workflow.
- **Analiza Malware (Cortex):** Połączenie z silnikami analizy statycznej i dynamicznej plików podejrzanych.
- **Monitorowanie Sieci:** Wdrożenie sensorów Suricata/Snort do analizy ruchu sieciowego w czasie rzeczywistym.

---

## 🚀 Wnioski Techniczne
Laboratorium udowadnia, że automatyzacja w SOC jest kluczem do nowoczesnej obrony. Dzięki połączeniu detekcji sygnaturowej z monitorowaniem zachowań procesów i automatyczną odpowiedzią, system jest w stanie neutralizować zagrożenia zanim przerodzą się w poważny wyciek danych.
