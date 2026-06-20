# Pytanie 6: Zdefiniuj pojęcie złośliwego oprogramowania. Przedstaw taksonomię złośliwego oprogramowania. Scharakteryzuj trzy wybrane zagrożenia.

## Kluczowe pojęcia
- **Malware (Złośliwe oprogramowanie)**: Oprogramowanie stworzone w celu wyrządzenia szkody użytkownikowi, systemowi komputerowemu lub sieci, działające bez wiedzy i zgody ofiary (skrót od *malicious software*).
- **Taksonomia malware**: Klasyfikacja złośliwego kodu oparta na metodach infekcji, replikacji oraz szkodliwym działaniu (payload).
- **Wirus komputerowy**: Złośliwy kod wymagający programu-nosiciela do uruchomienia i replikacji.
- **Robak (Worm)**: Samodzielny złośliwy program rozprzestrzeniający się automatycznie przez sieć komputerową bez konieczności interakcji użytkownika.
- **Trojan (Koń trojański)**: Szkodliwe oprogramowanie maskujące się pod postacią legalnej i przydatnej aplikacji.

## Szczegółowe omówienie tematu

### 1. Definicja złośliwego oprogramowania (Malware)
Złośliwym oprogramowaniem nazywamy każdy program, skrypt lub instrukcję, która celowo narusza bezpieczeństwo systemu komputerowego. Działania te mogą obejmować:
- Naruszenie poufności (kradzież haseł, szpiegowanie).
- Naruszenie integralności (modyfikacja plików, manipulacja danymi).
- Naruszenie dostępności (szyfrowanie danych, niszczenie systemu operacyjnego).

### 2. Taksonomia złośliwego oprogramowania
Tradycyjna taksonomia dzieli złośliwe oprogramowanie na kategorie według mechanizmu replikacji i propagacji oraz według celu ich działania:

#### A. Podział ze względu na sposób rozprzestrzeniania się i uruchamiania:
- **Wirusy (Viruses)**: Infekują inne pliki wykonywalne (np. `.exe`, `.dll`) lub sektory rozruchowe dysków. Wykonują się wtedy, gdy użytkownik uruchomi zainfekowany plik.
- **Robaki (Worms)**: Wykorzystują luki w protokołach sieciowych (np. SMB, RDP) do samodzielnego kopiowania się z jednego komputera na drugi w sieci. Nie potrzebują pliku-nosiciela.
- **Trojany (Trojans)**: Nie rozprzestrzeniają się same. Wymagają, aby użytkownik został oszukany (np. pobrał rzekomy instalator gry, a w rzeczywistości zainstalował złośliwy program).

#### B. Podział ze względu na szkodliwe działanie (Payload):
- **Ransomware**: Szyfruje dane użytkownika i blokuje ekran, żądając okupu (ransom) za klucz deszyfrujący.
- **Spyware (Oprogramowanie szpiegujące)**: Monitoruje aktywność użytkownika, historię przeglądania oraz zbiera dane wrażliwe. Specjalną odmianą są **Keyloggery** rejestrujące uderzenia w klawisze.
- **Rootkity**: Narzędzia zaprojektowane w celu ukrycia procesów, plików i połączeń sieciowych malware przed oprogramowaniem antywirusowym poprzez głęboką modyfikację jądra systemu operacyjnego (OS kernel).
- **Botnet i Boty**: Programy włączające zainfekowane komputery do sieci maszyn-zombie sterowanych przez jeden serwer C2 (Command & Control), wykorzystywanych m.in. do masowych ataków DDoS.
- **Adware**: Programy natrętnie wyświetlające niechciane reklamy w systemie lub przeglądarce.

---

### 3. Charakterystyka trzech wybranych zagrożeń

#### Zagrożenie 1: Ransomware (np. WannaCry, LockBit)
- **Charakterystyka**: Po przedostaniu się do systemu (często przez załącznik phishingowy lub lukę w sieci), ransomware uruchamia proces szyfrowania plików użytkownika za pomocą silnych algorytmów kryptograficznych (np. AES-256 dla plików i RSA-2048 do zaszyfrowania klucza AES). Po zakończeniu szyfrowania oryginalne pliki są usuwane, a użytkownik widzi komunikat z żądaniem okupu w kryptowalutach (np. Bitcoin, Monero). Nowoczesne grupy stosują **podwójny szantaż (double extortion)** – przed zaszyfrowaniem dane są eksfiltrowane, a w razie odmowy zapłaty grozi się ich publikacją w darknecie.
- **Metody obrony**: Regularne tworzenie kopii zapasowych w architekturze 3-2-1 (3 kopie, 2 różne nośniki, 1 kopia offline/w chmurze), aktualizowanie systemów operacyjnych w celu łatana luk podatności (np. MS17-010 dla WannaCry).

#### Zagrożenie 2: Spyware / Keylogger (np. Agent Tesla, Pegasus)
- **Charakterystyka**: Keyloggery i oprogramowanie szpiegujące działają w tle, starając się pozostać niezauważonymi. Przechwytują dane wprowadzane z klawiatury (loginy, hasła, numery kart kredytowych), robią zrzuty ekranu, a Pegasus potrafi dodatkowo podsłuchiwać rozmowy telefoniczne i aktywować kamerę. Przechwycone informacje są okresowo wysyłane na serwer kontrolowany przez atakującego.
- **Metody obrony**: Używanie uwierzytelniania dwuskładnikowego (2FA/MFA), systemy antywirusowe klasy EDR (Endpoint Detection and Response) z analizą behawioralną (wykrywanie podejrzanych operacji zapisu i czytania z pamięci procesów).

#### Zagrożenie 3: RAT (Remote Access Trojan - Trojan Zdalnego Dostępu, np. Gh0st RAT, njRAT)
- **Charakterystyka**: RAT to trojan, który po instalacji otwiera ukryty port i nawiązuje połączenie zwrotne (reverse shell) do serwera C2 atakującego. Daje to cyberprzestępcy pełną kontrolę administracyjną nad zainfekowanym komputerem. Atakujący może modyfikować rejestr, pobierać i uruchamiać inne złośliwe pliki, kraść pliki lokalne czy użyć komputera ofiary jako punktu przesiadkowego (pivot) do dalszego ataku w sieci lokalnej.
- **Metody obrony**: Filtrowanie ruchu wychodzącego na zaporach sieciowych (Firewall egress filtering), wykrywanie anomalii sieciowych (np. niespodziewane połączenia na nietypowe porty zewnętrzne), zasada minimalnych uprawnień dla użytkowników systemu.

## Podsumowanie
Współczesna taksonomia malware staje się coraz bardziej płynna, ponieważ złośliwe programy są modułowe – jedno zagrożenie może być jednocześnie trojanem (dropperem), pobierać robaka do propagacji w sieci lokalnej, instalować spyware w celu kradzieży danych, a na końcu zaszyfrować dysk jako ransomware. Skuteczna ochrona wymaga kompleksowego podejścia (Defense in Depth) na poziomie sieci, punktów końcowych oraz edukacji użytkowników.
