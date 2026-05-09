# SOC Automation Lab: Wazuh EDR & Active Response 🛡️

Projekt domowego laboratorium SOC (Security Operations Center) opartego na stosie Wazuh. Środowisko demonstruje pełny cykl życia incydentu: od monitorowania i wykrywania podatności, po automatyczną reakcję na niebezpieczne zdarzenia.

## 🏗️ Architektura Systemu
- **Manager:** Wazuh (wdrożony w kontenerach Docker)
- **Endpointy:** Agenty Wazuh zainstalowane na systemach Windows (LaptopDellM, WindowsMarek)
- **Główne moduły:** FIM (File Integrity Monitoring), Vulnerability Detector, Active Response

---

## 🔬 Etap 1: Monitorowanie Integralności Plików (FIM) & Whodata
Skonfigurowano zaawansowany moduł FIM do monitorowania krytycznych katalogów w czasie rzeczywistym.

### Kluczowe osiągnięcia:
- **Wykrywanie Real-time:** Natychmiastowe alerty o dodaniu, modyfikacji lub usunięciu plików w monitorowanych ścieżkach (np. `C:\SOC_Test`).
- **Analiza Whodata:** Dzięki integracji z audytem systemu Windows, system raportuje **kto** dokonał zmiany (użytkownik) oraz **jakim procesem** (np. `notepad.exe`, `powershell.exe`).

---

## 🔍 Etap 2: Zarządzanie Podatnościami (Vulnerability Management)
Uruchomiono moduł skanowania podatności w oparciu o bazy danych CVE (NVD, MSU).

### Analiza wyników:
- **Identyfikacja zagrożeń:** Wstępne skanowanie wykazało 32 podatności krytyczne (Critical) oraz 579 wysokich (High) na testowym hoście Windows.
- **Wniosek:** Większość luk wynikała z brakujących poprawek Microsoft Security (CVE-2023-XXXX). System pozwolił na priorytetyzację procesu Patch Managementu.

---

## ⚡ Etap 3: Active Response (Automatyczna Defensywa)
Najbardziej zaawansowany etap laba – konfiguracja systemu do aktywnej obrony przed intruzami.

### Mechanizm działania:
- **Wyzwalacz (Trigger):** Wykrycie zdarzenia o poziomie krytyczności >= 6 (np. usunięcie pliku systemowego lub Brute Force).
- **Akcja:** Automatyczne wywołanie skryptu `win-firewall-drop`.
- **Rezultat:** Agent dynamicznie dodaje regułę do **Windows Defender Firewall** przy użyciu polecenia `netsh`, odcinając adres IP napastnika na 180 sekund.

---

## 📸 Dowody Koncepcyjne (PoC)

### Wykrywanie zmian (FIM)
System poprawnie zidentyfikował użytkownika i program modyfikujący pliki:
![Wykrywanie zmian](https://raw.githubusercontent.com/greeygoosee/soc-lab/main/Zrzut%20ekranu%20(21).jpg)

### Wykryte Podatności
Brutalna prawda o stanie zabezpieczeń endpointa:
![Podatności](https://raw.githubusercontent.com/greeygoosee/soc-lab/main/Zrzut%20ekranu%20(25)_2.jpg)

### Skuteczna Blokada (Active Response)
Potwierdzenie automatycznego bana (Rule ID 601) po wykryciu incydentu:
![Active Response](https://raw.githubusercontent.com/greeygoosee/soc-lab/main/Zrzut%20ekranu%20(27)_2.jpg)

---

## 🚀 Wnioski
Projekt udowadnia skuteczność systemów EDR w automatyzacji bezpieczeństwa. Dzięki integracji wielu modułów, czas reakcji na incydent (MTTR) został skrócony z minut do sekund poprzez eliminację czynnika ludzkiego w pierwszej linii obrony.
