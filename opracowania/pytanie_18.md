# Pytanie 18: Omów miary bezpieczeństwa systemu komputerowego.

## Kluczowe pojęcia
- **Miary bezpieczeństwa (Security Metrics)**: Standardy i wartości liczbowe służące do ilościowej oceny poziomu bezpieczeństwa, odporności systemów oraz efektywności procesów obronnych.
- **Triada CIA (Poufność, Integralność, Dostępność)**: Trzy podstawowe cele ochrony danych, wokół których definiuje się miary bezpieczeństwa.
- **MTTD (Mean Time to Detect)**: Średni czas potrzebny na wykrycie incydentu bezpieczeństwa od momentu jego wystąpienia.
- **MTTR (Mean Time to Respond / Repair)**: Średni czas potrzebny na reakcję, powstrzymanie (mitigation) i usunięcie skutków incydentu.
- **CVSS (Common Vulnerability Scoring System)**: Standardowy system oceny powagi podatności w oprogramowaniu (skala od 0 do 10).

## Szczegółowe omówienie tematu

### 1. Rola miar bezpieczeństwa w inżynierii systemów
W myśl zasady „nie możesz zarządzać czymś, czego nie potrafisz zmierzyć”, miary bezpieczeństwa są niezbędne do oceny stanu ochrony systemów komputerowych. Pozwalają one na:
- Identyfikację słabych punktów w infrastrukturze IT.
- Weryfikację skuteczności wdrożonych zabezpieczeń (np. firewalli, systemów EDR).
- Porównywanie poziomu bezpieczeństwa w czasie (analiza trendów).
- Uzasadnienie wydatków na cyberbezpieczeństwo (ROI) przed zarządem.
- Wykazanie zgodności (compliance) z normami prawnymi (np. RODO, ISO 27001, NIS2).

---

### 2. Klasyfikacja miar bezpieczeństwa

Miary bezpieczeństwa można podzielić na trzy główne kategorie:

#### A. Miary techniczne (systemowe)
Koncentrują się na parametrach technicznych infrastruktury i oprogramowania:
- **Gęstość i krytyczność podatności**: Liczba wykrytych luk bezpieczeństwa w systemie operacyjnym i aplikacjach, często ważona ich punktacją w skali **CVSS** (np. liczba luk o statusie *Critical* / CVSS >= 9.0).
- **Patch Latency (Opóźnienie aktualizacji)**: Średni czas (w dniach) pomiędzy wydaniem poprawki bezpieczeństwa przez producenta oprogramowania a jej faktycznym wdrożeniem na serwerach.
- **Wskaźnik pokrycia zabezpieczeniami**: Procent urządzeń w sieci posiadających aktywne i zaktualizowane oprogramowanie antywirusowe/EDR lub objętych monitoringiem logów (SIEM).
- **Dostępność usług (Availability)**: Procent czasu poprawnego działania systemu w skali roku (np. SLA na poziomie 99.9% oznacza dopuszczalny przestój ok. 8.76 godziny rocznie).

#### B. Miary operacyjne (procesowe)
Mierzą efektywność i sprawność działania zespołów odpowiedzialnych za bezpieczeństwo (np. Security Operations Center – SOC):
- **MTTD (Mean Time to Detect)**: Średni czas od momentu przełamania zabezpieczeń przez atakującego do chwili wykrycia tego faktu przez systemy monitorowania. Krótki MTTD ogranicza tzw. *dwell time* (czas przebywania włamywacza w sieci).
- **MTTR (Mean Time to Respond / Resolve)**: Średni czas potrzebny na powstrzymanie incydentu (np. zablokowanie konta, odizolowanie zainfekowanej maszyny od sieci) i przywrócenie normalnego działania.
- **False Positive Rate (Wskaźnik fałszywych alarmów)**: Stosunek liczby alertów błędnych (generowanych przez normalną aktywność użytkowników) do całkowitej liczby alertów wygenerowanych przez systemy detekcji (IDS/IPS/SIEM).

#### C. Miary ludzkie (behawioralne)
Mierzą świadomość użytkowników końcowych, którzy często są celem ataków socjotechnicznych:
- **Współczynnik podatności na phishing (Phishing Click Rate)**: Odsetek pracowników, którzy kliknęli w podejrzany link lub otworzyli załącznik podczas kontrolowanych, próbnych testów phishingowych.
- **Współczynnik raportowania incydentów**: Odsetek pracowników, którzy poprawnie rozpoznali podejrzaną wiadomość i zgłosili ją do działu bezpieczeństwa zamiast ją zignorować lub otworzyć.

---

### 3. Cechy skutecznych miar (Zasada SMART)
Właściwie zaprojektowane metryki bezpieczeństwa powinny być:
- **Obiektywne i ilościowe**: Oparte na faktach i liczbach, a nie na subiektywnej ocenie (np. "98% serwerów jest aktualnych" zamiast "serwery są bezpieczne").
- **Łatwe do pozyskania**: Proces zbierania danych powinien być w miarę możliwości zautomatyzowany, aby nie obciążać administratorów pracą manualną.
- **Zrozumiałe dla biznesu**: Powinny pozwalać na przełożenie ryzyka technicznego na ryzyko biznesowe i finansowe (np. czas przestoju systemu przeliczony na straty finansowe).

## Podsumowanie
Miary bezpieczeństwa systemu komputerowego to niezbędne narzędzie zarządcze. Pozwalają one na przejście od reaktywnego gaszenia pożarów do proaktywnego zarządzania ryzykiem. Skuteczna obrona opiera się na ciągłym monitorowaniu kluczowych wskaźników, takich jak czas wykrycia (MTTD), czas reakcji (MTTR) oraz stopień załatania podatności (Patch Latency).
