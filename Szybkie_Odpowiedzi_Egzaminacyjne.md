# Szybkie Odpowiedzi Egzaminacyjne - Cyberbezpieczeństwo (II stopień)

Zestawienie zwięzłych, bezpośrednich odpowiedzi na pytania egzaminacyjne, przygotowane z myślą o szybkiej powtórce i precyzyjnym odpowiadaniu na pytania wprost, bez zbędnych szczegółów.

---

### 1. Mechanizm wstrzykiwania zależności oraz rola i podstawowa funkcjonalność kontenera IoC.
* **Wstrzykiwanie zależności (DI - Dependency Injection)**: Wzorzec projektowy realizujący zasadę odwrócenia sterowania (IoC). Polega na dostarczaniu klasie gotowych obiektów (zależności) z zewnątrz (np. przez konstruktor, setter lub bezpośrednio w pole), zamiast samodzielnego ich tworzenia wewnątrz tej klasy za pomocą operatora `new`. Zapobiega to silnemu sprzężeniu komponentów i ułatwia testowanie.
* **Rola i funkcjonalność kontenera IoC**: Zewnętrzny framework/biblioteka odpowiedzialna za automatyzację zarządzania obiektami:
  1. *Zarządzanie cyklem życia*: Tworzenie, inicjalizacja i niszczenie komponentów.
  2. *Rozwiązywanie zależności*: Automatyczne wykrywanie i wstrzykiwanie wymaganych obiektów do innych klas.
  3. *Zarządzanie zasięgiem (Scope)*: Decydowanie o czasie życia i sposobie współdzielenia instancji (np. Singleton, Prototype/Transient, Request, Session).

### 2. Koncepcja rozwoju oprogramowania sterowanego testami (TDD).
* **TDD (Test-Driven Development)**: Metodyka tworzenia oprogramowania, w której testy jednostkowe są pisane **przed** napisaniem kodu produkcyjnego. Testy definiują wymagania i specyfikację projektową.
* **Cykl Red-Green-Refactor**:
  1. *RED (Czerwony)*: Napisanie testu jednostkowego dla nowej funkcjonalności. Test zostaje uruchomiony i musi zakończyć się niepowodzeniem, ponieważ kod produkcyjny jeszcze nie istnieje.
  2. *GREEN (Zielony)*: Napisanie minimalnej, najprostszej implementacji kodu produkcyjnego tak, aby test zakończył się sukcesem.
  3. *REFACTOR (Refaktoryzacja)*: Oczyszczenie, poprawa czytelności i optymalizacja kodu (zarówno produkcyjnego, jak i testów) bez zmiany jego zachowania zewnętrznego, przy stałej weryfikacji testami.

### 3. Wzorzec architektury Business Delegate, obszar zastosowań.
* **Business Delegate (Delegat biznesowy)**: Wzorzec projektowy warstwy prezentacji, który pośredniczy w komunikacji z usługami biznesowymi backendu. Jego celem jest ukrycie przed klientem szczegółów technicznych komunikacji sieciowej, lokalizacji usług oraz obsługi specyficznych wyjątków technicznych (np. JNDI lookups, wyjątki sieciowe RMI).
* **Składniki**: *Client* (warstwa prezentacji), *Business Delegate* (pośrednik), *Service Locator* (lokalizator/caching usług), *Business Service* (rzeczywista usługa).
* **Obszar zastosowań**:
  - Systemy rozproszone (np. wielowarstwowe aplikacje enterprise), gdzie klient i backend działają na różnych maszynach.
  - Integracja z zewnętrznymi API i serwisami w celu odizolowania od nich kodu prezentacji.
  - Centralizacja logiki odporności na awarie (np. mechanizmy retry, circuit breaker) przy połączeniach sieciowych.

### 4. Model dojrzałości usług sieciowych (usług RESTful) wg. Richardsona.
Model klasyfikujący poziom wdrożenia zasad architektury REST w usługach sieciowych na 4 poziomach:
* **Poziom 0: Swamp of POX (RPC)**: HTTP używane wyłącznie jako protokół transportowy. Istnieje jeden punkt końcowy (URI), wszystkie żądania przesyłane są zwykle metodą `POST`, a operacje i parametry są definiowane w ciele wiadomości (np. SOAP, XML-RPC).
* **Poziom 1: Resources (Zasoby)**: Wprowadza unikalne adresy URI dla każdego zasobu w systemie (np. `/users/12`), ale komunikacja nadal odbywa się najczęściej za pomocą jednej metody HTTP (np. `POST`).
* **Poziom 2: HTTP Verbs (Czasowniki HTTP)**: API w pełni wykorzystuje standardowe metody HTTP (GET do odczytu, POST do zapisu, PUT/PATCH do aktualizacji, DELETE do usuwania) oraz zwraca poprawne kody statusu odpowiedzi HTTP (np. 201 Created, 404 Not Found).
* **Poziom 3: Hypermedia Controls (HATEOAS)**: Najwyższy poziom. Serwer w odpowiedzi przesyła dane oraz dynamiczne hiperłącza informujące klienta o kolejnych dozwolonych operacjach na zasobie, zależnie od jego stanu i uprawnień użytkownika.

### 5. Omów doktrynę cyberbezpieczeństwa RP - przedstaw przyjęte definicje.
* **Doktryna Cyberbezpieczeństwa RP**: Strategiczny dokument określający cele, zasady i kierunki działań państwa w celu zapewnienia bezpieczeństwa RP w cyberprzestrzeni (suwerenność cyfrowa, ochrona infrastruktury krytycznej).
* **Kluczowe definicje**:
  - *Cyberbezpieczeństwo (wg ustawy o KSC)*: Odporność systemów informacyjnych na działania naruszające poufność, integralność, dostępność i autentyczność przetwarzanych danych lub powiązanych z nimi usług oferowanych przez te systemy.
  - *Krajowy System Cyberbezpieczeństwa (KSC)*: Struktura powołana ustawą z 2018 r. w celu ochrony usług kluczowych i cyfrowych. Składa się z operatorów usług kluczowych, dostawców usług cyfrowych oraz 3 zespołów CSIRT poziomu krajowego: **CSIRT GOV** (ABW - sektor rządowy i infrastruktura krytyczna), **CSIRT NASK** (NASK - sektor cywilny i obywatele), **CSIRT MON** (Wojska Obrony Cyberprzestrzeni - sektor wojskowy).
  - *Incydent*: Zdarzenie mające lub mogące mieć niekorzystny wpływ na cyberbezpieczeństwo. Klasyfikowane jako: *w podmiocie publicznym*, *istotny* (dotyczący usług kluczowych/cyfrowych) oraz *krytyczny* (zagrażający bezpieczeństwu państwa).

### 6. Zdefiniuj pojęcie złośliwego oprogramowania. Przedstaw taksonomię złośliwego oprogramowania. Scharakteryzuj trzy wybrane zagrożenia.
* **Złośliwe oprogramowanie (Malware)**: Dowolny kod lub program uruchamiany bez wiedzy i zgody użytkownika, stworzony w celu wyrządzenia szkód w systemie, naruszenia poufności, integralności lub dostępności danych.
* **Taksonomia**:
  - *Wg sposobu propagacji i uruchamiania*: **Wirusy** (wymagają nosiciela), **Robaki** (samodzielnie rozprzestrzeniają się przez sieć), **Trojany** (podszywają się pod legalne oprogramowanie).
  - *Wg szkodliwego działania (payload)*: **Ransomware** (szyfrowanie i okup), **Spyware/Keylogger** (szpiegowanie i kradzież danych), **Rootkit** (ukrywanie procesów w jadrze OS), **Botnet/Bot** (kontrola nad maszyną-zombie do ataków DDoS).
* **Charakterystyka trzech zagrożeń**:
  1. *Ransomware*: Szyfruje pliki na dysku silnymi algorytmami kryptograficznymi (np. AES+RSA), usuwa oryginały i żąda opłaty (okupu) w kryptowalutach za klucz deszyfrujący. Często stosuje szantaż wycieku skradzionych wcześniej danych.
  2. *Spyware (Keylogger)*: Niewykrywalnie monitoruje aktywność użytkownika, rejestruje uderzenia w klawisze, zrzuty ekranu oraz hasła i wysyła je na serwer C2 (Command & Control) napastnika.
  3. *RAT (Remote Access Trojan)*: Trojan dający atakującemu pełny zdalny dostęp administracyjny do zainfekowanego urządzenia (nawiązuje połączenie zwrotne - reverse shell - do serwera C2).

### 7. Przedstaw ideę ataków typu DoS i krótko scharakteryzuj ich rodzaje.
* **Idea DoS (Denial of Service)**: Atak mający na celu uniemożliwienie uprawnionym użytkownikom dostępu do systemu lub usługi poprzez celowe przeciążenie pasma sieciowego, wyczerpanie zasobów serwera (CPU, RAM) lub wywołanie awarii oprogramowania. Gdy atak jest prowadzony z wielu rozproszonych urządzeń (botnetu), nazywa się go **DDoS**.
* **Rodzaje**:
  1. *Wolumetryczne*: Zasypywanie celu ogromną ilością danych w celu całkowitego zatkania łącza (np. *UDP Flood*, *DNS/NTP Amplification* wykorzystujący fałszowanie IP ofiary i zwielokrotnione odpowiedzi z publicznych serwerów).
  2. *Na protokoły*: Wyczerpywanie tabel stanów urządzeń sieciowych (np. *SYN Flood* – zalewanie pakietami SYN z fałszywych IP, co blokuje pamięć serwera na oczekiwanie na potwierdzenia ACK, które nigdy nie nadejdą).
  3. *Na warstwę aplikacji*: Celowanie w konkretne zasoby aplikacji serwera (np. *Slowloris* – otwieranie setek połączeń HTTP i powolne wysyłanie nagłówków, co szybko blokuje całą pulę dostępnych wątków serwera).

### 8. Wymień i omów siedem zasad RODO.
1. **Zgodność z prawem, rzetelność i przejrzystość**: Przetwarzanie must opierać się na jasnej podstawie prawnej (np. zgoda, umowa), być uczciwe i jasno opisane w politykach prywatności.
2. **Ograniczenie celu**: Dane można zbierać wyłącznie w konkretnych, wyraźnych i prawnie uzasadnionych celach i nie wolno ich przetwarzać niezgodnie z nimi.
3. **Minimalizacja danych**: Zbierane dane muszą być adekwatne i ograniczone wyłącznie do tego, co niezbędne do realizacji celów.
4. **Prawidłowość**: Dane muszą być poprawne i aktualne. Błędne informacje należy niezwłocznie sprostować lub usunąć.
5. **Ograniczenie przechowywania**: Dane mogą być przechowywane w formie umożliwiającej identyfikację tylko przez czas niezbędny do celów ich przetwarzania.
6. **Integralność i poufność (Bezpieczeństwo)**: Obowiązek wdrożenia technicznych i organizacyjnych zabezpieczeń chroniących dane przed wyciekiem, zniszczeniem lub nieuprawnionym dostępem (np. szyfrowanie).
7. **Rozliczalność**: Administrator (ADO) jest odpowiedzialny za przestrzeganie wszystkich powyższych zasad oraz must być w stanie to udowodnić przed organem nadzorczym (UODO).

### 9. Zdefiniuj pojęcie podatności aplikacji internetowej na ataki, podaj przykłady luk i uzasadnij dlaczego aplikacje internetowe są podatne na ataki.
* **Podatność (Vulnerability)**: Słabość lub błąd w kodzie, projekcie, konfiguracji lub administracji aplikacji webowej, który może zostać wykorzystany przez atakującego do naruszenia poufności, integralności lub dostępności systemu.
* **Przykłady luk**: *SQL Injection (SQLi)*, *Cross-Site Scripting (XSS)*, *Insecure Direct Object Reference (IDOR)*, *Security Misconfiguration* (np. domyślne hasła).
* **Dlaczego aplikacje są podatne**:
  1. *Publiczna dostępność*: Porty 80 i 443 są otwarte dla każdego, co umożliwia ciągłe próby ataków z dowolnego miejsca na ziemi.
  2. *Brak kontroli nad klientem*: Użytkownik ma pełną kontrolę nad przeglądarką i może dowolnie manipulować żądaniami HTTP przed wysłaniem ich na serwer.
  3. *Złożoność i zależności*: Współczesne aplikacje bazują na tysiącach zewnętrznych bibliotek (npm, NuGet), co zwiększa ryzyko wprowadzenia podatnej zależności.
  4. *Presja biznesowa*: Wymaganie szybkiego wdrożenia funkcjonalności (time-to-market) często spycha bezpieczeństwo na dalszy plan.

### 10. Zdefiniuj pojęcie exploit i payload w kontekście ataków na aplikacje internetowe, podaj przykłady narzędzi do tworzenia exploitów oraz wykrywania podatności w aplikacjach internetowych.
* **Exploit**: Kod, program lub sekwencja danych wykorzystująca konkretny błąd (podatność) w oprogramowaniu w celu przejęcia kontroli nad programem lub wywołania jego nieoczekiwanego zachowania (to "klucz" do luki).
* **Payload (Ładunek)**: Złośliwy kod (np. shellcode) dostarczany i uruchamiany na maszynie ofiary dzięki temu, że exploit przełamał zabezpieczenia (np. kod otwierający połączenie zwrotne - *Reverse Shell*).
* **Narzędzia**:
  - *Do tworzenia exploitów / ataków*: **Metasploit Framework** (platforma z bazą gotowych exploitów i ładunków), języki programowania (np. skrypty w Pythonie).
  - *Do wykrywania podatności*: **Burp Suite** / **OWASP ZAP** (narzędzia typu intercepting proxy służące do analizy i modyfikacji ruchu HTTP), **Nessus** (skaner podatności sieciowych i konfiguracji), **SonarQube** (narzędzie do statycznej analizy kodu źródłowego - SAST).

### 11. Zdefiniuj atak Cross-Site Scripting na aplikację internetową, podaj typy ataków XSS oraz przykłady kontekstów ataków i metod obrony przed nimi.
* **XSS (Cross-Site Scripting)**: Podatność polegająca na wstrzyknięciu złośliwego kodu JavaScript na stronę internetową, który wykonuje się w przeglądarce innego użytkownika.
* **Typy XSS**:
  1. *Stored XSS (Trwały)*: Złośliwy skrypt jest zapisywany w bazie danych serwera (np. w komentarzu) i uruchamiany u każdego, kto wyświetli daną stronę.
  2. *Reflected XSS (Odbity)*: Skrypt jest przekazywany w parametrach żądania (np. w URL) i odsyłany przez serwer w odpowiedzi. Wymaga kliknięcia złośliwego linku przez ofiarę.
  3. *DOM-based XSS*: Skrypt wykonuje się w całości po stronie przeglądarki na skutek niebezpiecznej modyfikacji drzewa DOM przez skrypty klienta.
* **Przykłady kontekstów**: *HTML Body* (wstrzyknięcie tagu `<script>`), *Attribute* (zamknięcie atrybutu tagu cudzysłowem i dodanie zdarzenia JS, np. `value="x" onfocus="alert(1)"`).
* **Metody obrony**:
  1. *Kodowanie znaków wyjściowych (Output Encoding / Escaping)*: Konwersja znaków specjalnych na encje (np. `<` na `&lt;`).
  2. *Sanitacja HTML*: Odfiltrowanie niebezpiecznych tagów za pomocą sprawdzonych bibliotek (np. *DOMPurify*).
  3. *Flaga HttpOnly*: Zabezpieczenie ciasteczek sesyjnych przed odczytem przez JavaScript.
  4. *Content Security Policy (CSP)*: Nagłówek HTTP określający zaufane źródła skryptów.

### 12. Zdefiniuj atak SQL Injection, podaj typy ataków SQL Injection na aplikacje internetowe, ich skutki i metody obrony przed nimi.
* **SQL Injection (SQLi)**: Podatność polegająca na wstrzyknięciu złośliwego kodu SQL do parametrów zapytania wysyłanego do bazy danych, co zmienia pierwotną strukturę i logikę zapytania. Powstaje przy dynamicznym łączeniu (konkatenacji) stringów zamiast parametryzacji.
* **Typy ataków**:
  1. *In-band SQLi (Klasyczny)*: Wyniki lub błędy bazy są zwracane bezpośrednio na stronie. Obejmuje: **Union-based** (łączenie wyników za pomocą `UNION SELECT`) i **Error-based** (wywoływanie błędów bazy ujawniających dane).
  2. *Blind SQLi (Ślepy)*: Brak błędów i wyników na ekranie. Atakujący wnioskuje o danych poprzez zapytania logiczne prawda/fałsz: **Boolean-based** (zmiana zachowania strony przy prawdzie/fałszu) lub **Time-based** (zmuszanie bazy do opóźnienia odpowiedzi, np. `SLEEP(5)`).
  3. *Out-of-band SQLi*: Baza danych przesyła informacje poza kanałem (np. wykonując zapytanie DNS do serwera atakującego).
* **Skutki**: Kradzież baz danych (poufność), modyfikacja danych/uprawnień (integralność), usuwanie danych (dostępność), a nawet zdalne wykonanie poleceń w OS serwera (RCE).
* **Metody obrony**:
  1. *Zapytania parametryzowane (Prepared Statements)*: Baza kompiluje strukturę zapytania osobno, a dane traktuje wyłącznie jako literały tekstowe/liczbowe.
  2. *Stosowanie ORM* (np. Hibernate, Entity Framework).
  3. *Zasada minimalnych uprawnień* dla konta bazy danych.

### 13. Scharakteryzuj trzy techniki ataków stosowanych w sieciach komputerowych.
1. **ARP Spoofing (Zatruwanie ARP)**: Wysyłanie fałszywych odpowiedzi ARP w sieci lokalnej (LAN), co pozwala powiązać adres IP bramy domyślnej lub ofiary z adresem MAC karty sieciowej atakującego. Umożliwia przechwytywanie, podsłuchiwanie (MitM) i modyfikację ruchu ofiary. *Obrona*: Funkcja Dynamic ARP Inspection (DAI) na przełącznikach.
2. **DNS Spoofing (Zatruwanie DNS Cache)**: Wprowadzenie fałszywych wpisów IP dla domen (np. `bank.pl ➔ fałszywe IP`) do pamięci podręcznej lokalnego serwera DNS. Skutkuje to przekierowaniem użytkowników na fałszywe strony phishingowe. *Obrona*: Wdrożenie podpisów cyfrowych **DNSSEC** oraz szyfrowania DNS (DoH, DoT).
3. **IP Spoofing (Fałszowanie adresu IP)**: Tworzenie pakietów sieciowych ze sfałszowanym adresem IP nadawcy w nagłówku. Używane do omijania zapór (autoryzacji IP) oraz w atakach DDoS typu Reflection/Amplification (gdzie serwery odsyłają masowo duże odpowiedzi do ofiary, pod którą podszył się atakujący). *Obrona*: Filtrowanie ruchu na routerach brzegowych (standard BCP 38 / uRPF).

### 14-15. Zdefiniuj pojęcie "socjotechnika". W jaki sposób socjotechnika jest wykorzystywana w sieciach komputerowych?
* **Socjotechnika (Inżynieria społeczna)**: Zbiór technik manipulacji psychologicznej, które wykorzystują ludzkie słabości i emocje (strach, pośpiech, ciekawość, zaufanie do autorytetu) w celu skłonienia ofiary do wykonania określonych akcji (np. zrobienia przelewu, otwarcia załącznika) lub wyjawienia poufnych informacji (haseł).
* **Wykorzystanie w sieciach**:
  - *Phishing i Spear Phishing*: Masowe lub celowane wiadomości e-mail/SMS podszywające się pod zaufane firmy (banki, kurierów) ze złośliwymi załącznikami (makra w Office) lub linkami do fałszywych paneli logowania.
  - *BEC (Business Email Compromise)*: Podszywanie się pod prezesa (CEO Fraud) lub kontrahenta w celu wyłudzenia przelewu finansowego.
  - *Vishing*: Rozmowy telefoniczne z Caller ID Spoofing (np. podszywanie się pod bank lub IT) w celu przejęcia komputera przez zdalny pulpit (AnyDesk).
  - *Watering Hole Attack*: Zainfekowanie portalu branżowego, z którego często korzystają pracownicy atakowanej firmy, w celu zarażenia ich przeglądarek.
* **Obrona**: Szkolenia pracowników (Security Awareness), wdrażanie sprzętowych kluczy bezpieczeństwa U2F/FIDO2, autoryzacja poczty (SPF, DKIM, DMARC), zasada Zero Trust i weryfikacja operacji finansowych drugim kanałem.

### 16. Zdefiniuj pojęcia: Phishing, Spam, Trojan.
* **Phishing**: Metoda ataku socjotechnicznego polegająca na wysyłaniu wiadomości (e-mail, SMS) podszywających się pod wiarygodne instytucje w celu wyłudzenia poufnych danych (haseł, numerów kart płatniczych) za pomocą sfałszowanych stron internetowych.
* **Spam**: Masowo wysyłana, niezamówiona korespondencja elektroniczna. Choć w większości jest to reklama, stanowi główny nośnik przesyłania wiadomości phishingowych oraz złośliwego oprogramowania.
* **Trojan (Koń trojański)**: Rodzaj złośliwego oprogramowania (malware), które maskuje swoje szkodliwe działanie pod postacią pożytecznej aplikacji (np. darmowej gry, kodeka). Nie potrafi samodzielnie się replikować – wymaga pobrania i ręcznego uruchomienia przez użytkownika. Po uruchomieniu instaluje złośliwy ładunek (np. RAT, backdoor).

### 17. Omów mechanizmy zabezpieczeń stosowane w sieciach bezprzewodowych Wi-Fi.
Bezpieczeństwo Wi-Fi realizuje się przez uwierzytelnianie i szyfrowanie transmisji radiowej:
* **WEP**: Przestarzały, całkowicie złamany standard szyfrowania (RC4). Krótki wektor inicjujący (IV) pozwala na łatwe odzyskanie klucza sieci w minutę.
* **WPA**: Standard przejściowy wprowadzający TKIP (dynamiczną zmianę kluczy na bazie RC4), obecnie wycofany.
* **WPA2**: Standard powszechny, wprowadzający silne szyfrowanie **AES-CCMP**.
  - *WPA2-PSK (Personal)*: Uwierzytelnianie jednym hasłem współdzielonym. Podatny na offline-owe ataki słownikowe na przechwycony proces logowania (4-way handshake) oraz podatność KRACK.
  - *WPA2-Enterprise*: Uwierzytelnianie 802.1X przez serwer RADIUS – każdy użytkownik loguje się własnym kontem/certyfikatem, a klucze szyfrujące sesji są generowane dynamicznie.
* **WPA3**: Najnowszy i bezpieczny standard. Zastępuje hasło współdzielone protokołem **SAE (Simultaneous Authentication of Equals / Dragonfly)**, co uniemożliwia offline-owe łamanie haseł brute-force. Wprowadza *Forward Secrecy* oraz *OWE* (szyfrowanie w sieciach otwartych).
* *Antywzorce*: Ukrywanie SSID oraz filtrowanie adresów MAC nie stanowią zabezpieczenia (dane te krążą w powietrzu jawnym tekstem). Funkcja **WPS** (PIN) jest podatna na brute-force i musi być wyłączona.

### 18. Omów miary bezpieczeństwa systemu komputerowego.
Miary bezpieczeństwa służą do ilościowej oceny stopnia ochrony i efektywności obrony systemów:
* **Miary techniczne (systemowe)**:
  - *Krytyczność podatności*: Mierzona standardem **CVSS** (Common Vulnerability Scoring System, oceniającym luki w skali od 0 do 10).
  - *Patch Latency*: Średni czas od wydania poprawki bezpieczeństwa przez producenta do jej wdrożenia na urządzeniach.
  - *Dostępność usług*: Procent czasu poprawnego działania systemu w roku (np. SLA 99.9%).
  - *Pokrycie systemów*: Procent maszyn posiadających aktualnego agenta EDR/SIEM.
* **Miary operacyjne (procesowe)**:
  - **MTTD (Mean Time to Detect)**: Średni czas od momentu przełamania zabezpieczeń do wykrycia incydentu przez monitorowanie.
  - **MTTR (Mean Time to Respond/Resolve)**: Średni czas potrzebny na zablokowanie zagrożenia (odizolowanie maszyny) i usunięcie skutków awarii.
  - *Współczynnik False Positive*: Odsetek fałszywych alertów generowanych przez systemy bezpieczeństwa.
* **Miary ludzkie (behawioralne)**:
  - *Click Rate*: Procent pracowników klikających w złośliwe linki w próbnych testach phishingowych.
  - *Współczynnik raportowania*: Procent pracowników poprawnie zgłaszających podejrzenia.

### 19. Omów jedno z narzędzi modelowania zagrożeń systemów komputerowych.
* **Microsoft Threat Modeling Tool (TMT)**: Bezpłatne narzędzie desktopowe wspierające proces projektowania architektury zgodnie z zasadą *Secure by Design*.
* **Sposób działania**:
  Projektant rysuje diagram przepływu danych (**DFD**), używając predefiniowanych komponentów: procesów (aplikacji), magazynów danych (baz danych), interaktorów zewnętrznych (użytkowników) i przepływów danych. Granice między obszarami o różnych poziomach uprawnień zaznacza się tzw. **granicami zaufania (Trust Boundaries)**.
* **Analiza**:
  Po przełączeniu w tryb analizy, TMT automatycznie generuje listę potencjalnych zagrożeń, dopasowanych do narysowanej architektury, klasyfikując je według modelu **STRIDE**:
  - **S**poofing (Podszywanie się pod użytkownika/usługę)
  - **T**ampering (Manipulacja danymi w locie)
  - **R**epudiation (Zaprzeczalność wykonania operacji)
  - **I**nformation Disclosure (Wyciek danych / nieuprawniony odczyt)
  - **D**enial of Service (Odmowa usługi / przeciążenie)
  - **E**levation of Privilege (Eskalacja uprawnień / wykonanie kodu admina)
* Zespół projektowy musi przypisać każdemu zagrożeniu status (np. Mitigated, Accepted) wraz z opisem zabezpieczenia.

### 20. Omów model FAIR pozwalający na szacowanie ryzyka zagrożenia bezpieczeństwa systemu komputerowego.
* **Model FAIR (Factor Analysis of Information Risk)**: Międzynarodowy standard służący do **ilościowej (finansowej)** analizy ryzyka cyberbezpieczeństwa. Pozwala przełożyć zagrożenia techniczne na wymierne straty finansowe wyrażone w konkretnej kwocie (np. roczna oczekiwana strata finansowa w PLN).
* **Struktura modelu**: Rozbija ryzyko na dwa podstawowe czynniki:
  1. **Loss Event Frequency (LEF - Częstotliwość Zdarzeń Stratogennych)**: Prawdopodobieństwo zaistnienia udanego ataku w czasie. Zależy od *Threat Event Frequency (TEF)* (częstość prób ataku) oraz *Vulnerability (V)* (podatność systemu na sukces ataku).
  2. **Loss Magnitude (LM - Wielkość Straty)**: Szacowany koszt pojedynczego incydentu. Składa się ze *straty pierwotnej* (koszty bezpośrednie: przestój, odzyskanie danych) oraz *straty wtórnej* (koszty wynikające z reakcji otoczenia: kary RODO, utrata wizerunku, procesy).
* Analiza FAIR wykorzystuje symulacje **Monte Carlo** w celu wygenerowania rozkładów prawdopodobieństwa strat, co ułatwia kadrze zarządzającej podejmowanie decyzji o budżetach bezpieczeństwa (analiza ROI).

### 21. Omów rolę bibliotek ataków na systemy komputerowe w procesie zapewniania ich bezpieczeństwa.
* **Biblioteki ataków**: Ustrukturyzowane, ogólnodostępne bazy wiedzy opisujące taktyki, techniki i procedury (TTP) stosowane przez rzeczywistych napastników. Najważniejszym standardem jest **MITRE ATT&CK** (oraz CAPEC i OWASP).
* **Rola w procesie zapewniania bezpieczeństwa**:
  1. *Weryfikacja ochrony (Gap Analysis)*: Pozwalają zmapować posiadane zabezpieczenia i sprawdzić, na które techniki ataku system jest ślepy.
  2. *Tworzenie reguł detekcji*: Służą jako wytyczne dla inżynierów bezpieczeństwa do pisania reguł korelacji w systemach SIEM/EDR na podstawie zachowań atakujących.
  3. *Projektowanie testów penetracyjnych (Red Teaming)*: Pozwalają na symulowanie działań konkretnych grup APT (np. APT28) przy użyciu dokładnie ich technik.
  4. *Standaryzacja komunikacji*: Wprowadzają jednolitą nomenklaturę w raportach o incydentach, co ułatwia współpracę między zespołami obrony a zarządem.

### 22. Omów znane Ci metodyki realizacji przedsięwzięcia projektowego. Porównaj wybrane metodyki: tradycyjną i zwinną.
* **Metodyka tradycyjna (kaskadowa / Waterfall)**: Projekt realizowany jest liniowo i sekwencyjnie w sztywnych fazach (Analiza ➔ Projektowanie ➔ Implementacja ➔ Testy ➔ Wdrożenie). Każda faza musi się zakończyć przed rozpoczęciem kolejnej.
* **Metodyka zwinna (Agile, np. Scrum, Kanban)**: Projekt realizowany jest iteracyjnie i przyrostowo w krótkich cyklach (sprintach, np. 2-tygodniowych). Po każdym cyklu dostarczany jest działający, przetestowany fragment oprogramowania (Increment), a wymagania mogą ewoluować.
* **Porównanie**:
  - *Wymagania*: W Waterfall zdefiniowane szczegółowo na początku; w Agile ogólne na początku, doprecyzowywane w trakcie.
  - *Zmiany*: W Waterfall bardzo trudne i kosztowne (Change Request); w Agile zmiany są naturalną częścią procesu.
  - *Udział klienta*: W Waterfall na początku (wymagania) i na końcu (odbiór); w Agile klient współpracuje na bieżąco i odbiera przyrosty po każdej iteracji.
  - *Ryzyko*: W Waterfall wysokie ryzyko niedopasowania produktu (luki wychodzą pod koniec); w Agile ryzyko jest minimalizowane przez ciągłą weryfikację.
* *Zastosowanie*: Waterfall – systemy o krytycznym znaczeniu bezpieczeństwa i stałych wymaganiach (np. lotnictwo, wojsko); Agile – innowacyjne produkty (np. aplikacje mobilne, SaaS, e-commerce).

### 23. Wskaż rodzaje projektów informatycznych. Wymień oraz scharakteryzuj metody estymacji kosztu wybranego przedsięwzięcia projektowego.
* **Rodzaje projektów IT**:
  - *Wytwórcze*: Budowa nowego oprogramowania od podstaw.
  - *Wdrożeniowe*: Instalacja i konfiguracja gotowych systemów (np. ERP SAP, Salesforce) u klienta.
  - *Migracyjne/Integracyjne*: Przenoszenie danych (np. do chmury) lub łączenie systemów.
  - *Infrastrukturalne*: Budowa sieci lub modernizacja serwerowni.
* **Metody estymacji kosztów i pracochłonności**:
  1. *Metoda Delficka (ekspercka)*: Grupa anonimowych ekspertów niezależnie szacuje koszt. Koordynator zbiera wyniki i organizuje kolejne rundy ocen, aż eksperci dojdą do wspólnego konsensusu. Zapobiega to dominacji liderów.
  2. *Model COCOMO (algorytmiczna)*: Szacowanie pracochłonności (w osobo-miesiącach) na podstawie wzorów matematycznych wykorzystujących liczbę tysięcy linii kodu (KLOC) lub punkty funkcyjne, korygowanych współczynnikami środowiskowymi (doświadczenie zespołu, presja czasu).
  3. *Oddolna (Bottom-Up)*: Hierarchiczny podział prac (WBS) na najmniejsze zadania, wycena każdego z nich osobno przez wykonawców i zsumowanie kosztów w górę. Najdokładniejsza, ale najbardziej pracochłonna.
  4. *PERT (Trójpunktowa)*: Szacowanie czasu/kosztu ze wzoru: $E = \frac{O + 4M + P}{6}$ (gdzie $O$ - optymistyczny, $M$ - prawdopodobny, $P$ - pesymistyczny), co uwzględnia czynniki ryzyka.

### 24. Wskaż fazy realizacji projektu informatycznego wytwórczego i wdrożeniowego. Wymień i omów metody śledzenia postępu projektu w czasie.
* **Fazy projektu wytwórczego (SDLC)**: Analiza wymagań ➔ Projektowanie architektury ➔ Implementacja (pisanie kodu) ➔ Testowanie (QA) ➔ Wdrożenie (Deployment) i utrzymanie.
* **Fazy projektu wdrożeniowego**: Przygotowanie projektu ➔ Analiza przedwdrożeniowa (Blueprinting / analiza Fit-Gap) ➔ Konfiguracja i dostosowanie (Realization) ➔ Przygotowanie końcowe (migracja danych, szkolenia) ➔ Start produkcyjny i wsparcie (Go-Live & Hypercare).
* **Metody śledzenia postępu**:
  1. **EVM (Earned Value Management)**: Analiza ilościowa poruszająca trzy wskaźniki: PV (wartość planowana), AC (koszt rzeczywisty) i EV (wartość prac rzeczywiście wykonanych). Pozwala wyliczyć wskaźniki odchylenia kosztów (CV) i harmonogramu (SV) oraz indeksy wydajności CPI i SPI.
  2. **Wykres Gantta i Kamienie Milowe**: Prezentacja graficzna zadań na osi czasu z uwzględnieniem zależności między nimi. Kamienie milowe (zdarzenia o zerowym czasie trwania) reprezentują kluczowe momenty kontrolne odbioru etapów.
  3. **Wykresy Spalania (Burn-down / Burn-up)**: Stosowane w Scrumie. Burn-down pokazuje ilość pracy pozostałej do wykonania w sprincie względem czasu. Burn-up pokazuje pracę ukończoną na tle całkowitego zakresu (pozwala śledzić przyrost zakresu – *scope creep*).

### 25. Omów sposoby tworzenia struktury zadań w projekcie. Co to jest ścieżka krytyczna? Podaj co najmniej dwie metody wyznaczania ścieżki krytycznej w projekcie informatycznym.
* **Struktura podziału pracy (WBS)**: Hierarchiczna dekompozycja całego zakresu projektu na mniejsze zadania. Tworzona na dwa sposoby:
  - *Zorientowana na produkty (Deliverable-oriented)*: Podział według elementów dostarczanych klientowi (np. Baza danych, Moduł płatności).
  - *Zorientowane na fazy (Phase-oriented)*: Podział oparty na etapach cyklu życia (np. Analiza, Projektowanie, Testy).
  *Zasady WBS*: Zasada 100% (suma zadań musi dawać 100% zakresu) oraz reguła 8/80 (pakiety robocze powinny trwać od 8 do 80 godzin).
* **Ścieżka krytyczna**: Najdłuższa sekwencja zależnych od siebie zadań od rozpoczęcia do zakończenia projektu. Określa minimalny czas trwania całego projektu. Zadania na tej ścieżce mają **zerowy luz czasowy** ($Luz = 0$) – opóźnienie dowolnego z nich opóźnia termin oddania całego projektu.
* **Metody wyznaczania**:
  1. **Metoda CPM (Critical Path Method)**: Deterministyczny algorytm polegający na przejściu sieci w przód (Forward Pass – obliczanie najwcześniejszych startów ES i zakończeń EF) oraz w tył (Backward Pass – obliczanie najpóźniejszych startów LS i zakończeń LF). Zadania, dla których luz $LF - EF = 0$, tworzą ścieżkę krytyczną.
  2. **Metoda PERT**: Podejście probabilistyczne, w którym czas trwania każdego zadania wyliczany jest jako średnia ważona trzech szacunków: $t_e = \frac{o+4m+p}{6}$ (optymistyczny, prawdopodobny, pesymistyczny). Następnie na podstawie tych czasów ścieżka krytyczna jest wyznaczana algorytmem CPM.

### 26. Charakterystyka systemów rozproszonych - zalety i wady.
* **System rozproszony**: Zbiór autonomicznych maszyn (węzłów) połączonych siecią i komunikujących się poprzez przesyłanie komunikatów, który dla użytkownika zachowuje się jak jeden spójny system. Brak wspólnej pamięci fizycznej i wspólnego zegara fizycznego.
* **Zalety**:
  - *Skalowalność horyzontalna*: Możliwość zwiększania mocy poprzez dodawanie kolejnych tanich serwerów do klastra.
  - *Tolerancja na awarie*: Awaria jednego węzła nie wyłącza całego systemu (brak pojedynczego punktu awarii - SPOF).
  - *Efektywność kosztowa*: Zbudowanie klastra z tańszych maszyn (commodity hardware) jest tańsze niż zakup jednego superkomputera.
  - *Niskie opóźnienia*: Dane mogą być bliżej użytkownika geograficznie (np. CDN).
* **Wady i wyzwania**:
  - *Złożoność oprogramowania*: Trudna synchronizacja, transakcje rozproszone, obsługa utraty pakietów w sieci.
  - *Problem spójności (Twierdzenie CAP)*: W przypadku podziału sieci (Partition) trzeba wybrać między pełną Spójnością (Consistency) a Dostępnością (Availability).
  - *Trudniejsze monitorowanie*: Konieczność wdrożenia rozproszonego śledzenia (Distributed Tracing) i centralizacji logów.
  - *Bezpieczeństwo*: Transmisja danych przez sieć zwiększa powierzchnię ataku (wymagany np. mTLS).

### 27. Modele programowania równoległego.
Abstrakcja określająca sposób komunikacji i dostępu wątków/procesów do pamięci:
1. **Model z pamięcią współdzieloną (Shared Memory)**: Wszystkie procesy/wątki współdzielą tę samą przestrzeń adresową RAM (np. OpenMP, Pthreads). Komunikacja jest bezpośrednia, ale istnieje wysokie ryzyko wyścigów (race conditions), co wymaga synchronizacji (blokad, muteksów).
2. **Model z pamięcią rozproszoną (Message Passing)**: Węzły mają niezależne pamięci (np. MPI). Komunikacja odbywa się przez jawne wysyłanie i odbieranie pakietów przez sieć. Brak wyścigów w pamięci współdzielonej, wysoka skalowalność, ale narzut sieciowy.
3. **Model hybrydowy**: Połączenie pamięci współdzielonej wewnątrz węzła (OpenMP) oraz przesyłania komunikatów między węzłami (MPI).
4. **Model równoległości danych (Data-Parallel / SIMD)**: Wykonywanie tych samych operacji matematycznych jednocześnie na dużych zbiorach danych. Podstawa obliczeń na kartach graficznych (CUDA, OpenCL).
5. **Model aktorów**: Niezależne obiekty (aktorzy) nie współdzielą stanu i komunikują się wyłącznie za pomocą asynchronicznych wiadomości, co eliminuje blokady i wyścigi (np. Erlang, biblioteka Akka).
6. **MapReduce**: Podział danych na części, równoległe przetworzenie (Map) i agregacja wyników (Reduce) w klastrze rozproszonym (np. Hadoop, Spark).

### 28. Miary efektywności obliczeń równoległych.
* **Przyspieszenie (Speedup - $S_p$)**: $S_p = \frac{T_1}{T_p}$ – stosunek czasu wykonania algorytmu sekwencyjnego na jednym rdzeniu ($T_1$) do czasu wersji równoległej na $p$ rdzeniach ($T_p$). Może być liniowe ($S_p = p$), podliniowe (najczęstsze – z powodu narzutów sieci) lub superliniowe ($S_p > p$, np. dzięki lepszemu wykorzystaniu pamięci Cache).
* **Efektywność (Efficiency - $E_p$)**: $E_p = \frac{S_p}{p}$ – stopień wykorzystania procesorów (wartość od 0 do 1). Współczynnik 0.8 oznacza, że przez 80% czasu rdzenie wykonywały obliczenia użyteczne, a przez 20% czekały lub komunikowały się.
* **Prawo Amdahla (Silne skalowanie)**: Określa granice przyspieszenia przy **stałym rozmiarze zadania**. Przy ułamku kodu sekwencyjnego $s$, maksymalne teoretyczne przyspieszenie przy nieskończonej liczbie procesorów wynosi $S_{limit} = \frac{1}{s}$.
* **Prawo Gustafsona (Słabe skalowanie)**: Określa przyspieszenie, gdy **rozmiar zadania rośnie proporcjonalnie do liczby procesorów** ($S_p = p - s(p-1)$). Pokazuje, że zrównoleglanie pozwala na rozwiązywanie dokładniejszych problemów w tym samym czasie.
* *Narzuty (Overhead)*: Strata czasu na komunikację sieciową, synchronizację oraz bezczynność rdzeni (brak load balancingu).

### 29. Środowiska programowania równoległego.
* **OpenMP**: Standard dla systemów z pamięcią współdzieloną (wielordzeniowe CPU). Programista dodaje do kodu C/C++ dyrektywy kompilatora (np. `#pragma omp parallel for`), a kompilator automatycznie dzieli iteracje pętli na wątki (model Fork-Join).
* **MPI (Message Passing Interface)**: Standard komunikacyjny dla klastrów rozproszonych. Definiuje funkcje do przesyłania danych punkt-do-punktu (`MPI_Send`, `MPI_Recv`) oraz operacje grupowe (np. `MPI_Bcast` – rozgłaszanie, `MPI_Reduce` – agregacja wyników na jednym węźle).
* **CUDA**: Stworzona przez firmę NVIDIA platforma do obliczeń ogólnego przeznaczenia na kartach graficznych (GPGPU). Umożliwia pisanie kodu wykonywanego przez tysiące bardzo lekkich wątków GPU.
* **OpenCL**: Otwarty, przenośny standard do obliczeń na systemach heterogenicznych (różne procesory CPU, układy GPU różnych producentów, FPGA, DSP).

### 30. Szyfry podstawieniowe (proste i wieloalfabetowe).
Polegają na zastępowaniu znaków tekstu jawnego innymi znakami zgodnie z kluczem:
* **Jednoalfabetowe (proste)**: Każda litera tekstu jawnego jest zawsze zastępowana przez dokładnie jeden, stały znak szyfru (np. *Szyfr Cezara* przesuwający alfabet o 3 pozycje).
  - *Podatność*: Całkowicie niebezpieczne. Szyfrogram zachowuje strukturę statystyczną języka i można go łatwo złamać za pomocą **analizy częstotliwościowej** występowania liter.
* **Wieloalfabetowe**: Ta sama litera tekstu jawnego może być zastępowana różnymi znakami w szyfrogramie, w zależności od jej pozycji w tekście (zmiana alfabetu jest sterowana kluczem).
  - *Szyfr Vigenère'a*: Wykorzystuje słowo-klucz powtarzane nad tekstem jawnym. Przesunięcie litery tekstu określane jest przez literę klucza za pomocą Kwadratu Vigenère'a.
  - *Podatność*: Jeśli klucz jest krótszy niż tekst, szyfr można złamać poprzez wyznaczenie długości klucza (metoda Kasiski'ego lub indeks koincydencji) i wykonanie analizy częstotliwościowej dla podgrup.
  - *Rozwinięcie*: Szyfr z **kluczem jednorazowym (One-Time Pad - OTP)**. Szyfr wieloalfabetowy o długości klucza równej długości wiadomości, użyty tylko raz, który jako jedyny gwarantuje tajność doskonałą.

### 31. Tajność doskonała. Twierdzenie Shannona.
* **Tajność doskonała (Perfect Secrecy)**: Właściwość kryptosystemu oznaczająca, że posiadanie szyfrogramu nie daje kryptoanalitykowi żadnej dodatkowej wiedzy na temat tekstu jawnego (prawdopodobieństwo a posteriori jest równe prawdopodobieństwu a priori: $P(M=m \mid C=c) = P(M=m)$). Atak brute-force wygeneruje wszystkie możliwe sensowne teksty o danej długości, bez szans na wskazanie prawdziwego.
* **Twierdzenie Shannona**: Kryptosystem o równej liczbie tekstów jawnych, kluczy i szyfrogramów zapewnia tajność doskonałą wtedy i tylko wtedy, gdy:
  1. Każdy klucz jest wybierany z rozkładem jednostajnym ($P(K=k) = 1/|K|$).
  2. Dla każdej pary wiadomość-szyfrogram istnieje dokładnie jeden klucz przekształcający tę wiadomość w ten szyfrogram.
* **Konsekwencja (Ograniczenie Shannona)**: Aby system był doskonale bezpieczny, przestrzeń kluczy must być co najmniej tak duża jak przestrzeń wiadomości ($|K| \ge |M|$), czyli **klucz must być co najmniej tak długi jak sama wiadomość**.
* **Realizacja**: Szyfr z kluczem jednorazowym (OTP), w którym bity wiadomości i klucza są sumowane modulo 2 ($C = M \oplus K$), pod warunkiem prawdziwie losowego klucza o długości równej wiadomości, użytego tylko raz.

### 32. Problem pakowania plecaka. Szyfry plecakowe.
* **Problem pakowania plecaka (Suma podzbioru)**: Mając dany zbiór wag $W = \{w_1, \dots, w_n\}$ oraz sumę docelową $S$, należy znaleźć ciąg binarny $X = \{x_1, \dots, x_n\}$ taki, że $\sum x_i \cdot w_i = S$. Dla losowych wag jest to problem **NP-zupełny** (trudny). Dla ciągu **superrosnącego** (gdzie każda kolejna liczba jest większa niż suma wszystkich poprzednich) problem jest **łatwy** i rozwiązuje się go liniowo algorytmem zachłannym.
* **Szyfr plecakowy (Merkle-Hellmana)**: Pierwszy asymetryczny kryptosystem, wykorzystujący "zapadnię" opartą na plecaku:
  - *Klucz prywatny*: Ciąg superrosnący $A$ (łatwy plecak) oraz sekretny mnożnik $W$ i moduł $M$.
  - *Klucz publiczny*: Ciąg $B$, gdzie $b_i = (a_i \cdot W) \pmod{M}$. Ciąg ten traci superrosnącość i wygląda na losowy (trudny plecak).
  - *Szyfrowanie*: Suma elementów klucza publicznego $B$ odpowiadających bitom 1 w wiadomości.
  - *Odszyfrowanie*: Odbiorca eliminuje maskowanie, mnożąc szyfrogram przez odwrotność modularną $W^{-1} \pmod{M}$, co sprowadza problem do łatwego plecaka z ciągiem superrosnącym $A$, który rozwiązuje zachłannie.
* **Dlaczego nie są stosowane**: Szyfr został całkowicie złamany w 1982 r. przez Adi Shamira przy użyciu **algorytmu LLL** (redukcji baz krat), który pozwala na wyliczenie klucza prywatnego ($W$ i $M$) z klucza publicznego $B$ w czasie wielomianowym.

### 33. Algorytmy asymetryczne. Szyfr RSA.
* **Kryptografia asymetryczna (z kluczem publicznym)**: Szyfrowanie odbywa się kluczem publicznym (dostępnym dla każdego), a deszyfrowanie powiązanym matematycznie kluczem prywatnym (tajnym). Rozwiązuje problem dystrybucji kluczy.
* **Algorytm RSA**:
  - *Generowanie kluczy*:
    1. Wybór dwóch dużych liczb pierwszych $p$ i $q$.
    2. Obliczenie modułu $n = p \cdot q$ oraz wartości funkcji Eulera $\phi(n) = (p-1)(q-1)$.
    3. Wybór wykładnika publicznego $e$ względnie pierwszego z $\phi(n)$ (zwykle $e = 65537$).
    4. Obliczenie wykładnika prywatnego $d$ jako odwrotności modularnej $e \pmod{\phi(n)}$ ($d \cdot e \equiv 1 \pmod{\phi(n)}$).
    - Klucz publiczny: $(e, n)$; klucz prywatny: $(d, n)$.
  - *Szyfrowanie*: $C = M^e \pmod{n}$
  - *Deszyfrowanie*: $M = C^d \pmod{n}$
  - *Podpis cyfrowy*: Podpisywanie: $S = H(M)^d \pmod{n}$; Weryfikacja: sprawdzenie, czy $S^e \pmod{n} = H(M)$ (gdzie $H$ to funkcja skrótu).
* **Bezpieczeństwo**: Opiera się na trudności faktoryzacji (rozkładu modułu $n$ na czynniki pierwsze $p$ i $q$). Współczesne minimum bezpieczeństwa to klucz **2048-bitowy**. Szyfrowanie wymaga stosowania dopełnienia **OAEP** w celu unikania ataków deterministycznych. RSA jest podatne na komputery kwantowe (algorytm Shora).

### 34. Opisz trzy zagrożenia dotyczące aplikacji mobilnych według projektu OWASP.
1. **Insecure Data Storage (Niezabezpieczone przechowywanie danych)**: Przechowywanie przez aplikację poufnych danych (haseł, tokenów JWT, danych osobowych) w plikach konfiguracyjnych XML/plist, bazach SQLite lub logach w postaci otwartego tekstu. W przypadku zgubienia urządzenia lub infekcji malware (szczególnie na telefonach z root/jailbreak), dane te mogą zostać zrzucone. *Obrona*: używanie Android Keystore, iOS Keychain oraz szyfrowania baz danych przez SQLCipher.
2. **Insecure Communication (Niezabezpieczona komunikacja)**: Komunikacja aplikacji z serwerem przez nieszyfrowany protokół HTTP, przestarzałe wersje TLS lub brak weryfikacji certyfikatu serwera (akceptacja certyfikatów self-signed). Umożliwia to podsłuch i manipulację ruchem (ataki MitM) w publicznych sieciach Wi-Fi. *Obrona*: wymuszenie HTTPS oraz wdrożenie **SSL Pinning** (zapisanie sumy kontrolnej klucza publicznego serwera bezpośrednio w kodzie aplikacji).
3. **Reverse Engineering (Inżynieria wsteczna)**: Łatwość dekompilacji paczki instalacyjnej aplikacji (APK/IPA) do czytelnego kodu źródłowego przy użyciu darmowych narzędzi (np. JADX). Pozwala to na wyciągnięcie zahardkodowanych kluczy API, analizę logiki biznesowej pod kątem podatności lub zmodyfikowanie aplikacji i wdrożenie jej ze złośliwym kodem. *Obrona*: stosowanie obfuskacji kodu (ProGuard/R8) i mechanizmów detekcji środowiska (detekcja roota/debuggera, RASP).

### 35. W jaki sposób systemy mobilne (Android, iOS) zabezpieczają dane przed dostępem nieautoryzowanych aplikacji?
1. **Piaskownica aplikacji (Sandboxing)**: Podstawowa izolacja procesów i plików. W systemie Android każda aplikacja otrzymuje unikalny identyfikator użytkownika Linux (**UID**), co na poziomie jądra blokuje innym procesom dostęp do jej katalogu plików. W systemie iOS piaskownica jest wymuszana przez profil bezpieczeństwa jądra Darwin/XNU, odcinając aplikację od kontenerów innych aplikacji.
2. **Szyfrowanie pamięci (FBE - File-Based Encryption)**: Dane są szyfrowane na poziomie plików kluczami zintegrowanymi ze sprzętem (Secure Enclave / TEE) oraz kodem blokady ekranu. Dane w klasie CE (Credential Encrypted / Complete Protection) są fizycznie niemożliwe do odszyfrowania, gdy ekran urządzenia pozostaje zablokowany.
3. **Sprzętowe kontenery kluczy**: Systemy udostępniają API **iOS Keychain** oraz **Android Keystore**, które generują i przechowują klucze kryptograficzne w sprzętowym, odizolowanym module bezpieczeństwa (Secure Enclave / TEE). Klucze te nigdy nie są widoczne w pamięci RAM systemu w postaci jawnej.
4. **Blokowanie bezpośredniej komunikacji IPC**: Bezpośredni dostęp do pamięci innych procesów jest zabroniony. Wymiana danych odbywa się wyłącznie przez ściśle kontrolowane interfejsy systemowe (Intents w Androidzie, URL Schemes w iOS).

### 36. W jaki sposób systemy mobilne zabezpieczają użytkownika przed dostępem aplikacji do funkcji takich jak kamera, wykonywanie/ odbieranie połączeń, bluetooth, położenie?
1. **Uprawnienia dynamiczne (Runtime Permissions)**: Aplikacja must zadeklarować chęć użycia sensora w pliku konfiguracyjnym, ale dostęp jest przyznawany dopiero po wyraźnej, jednostkowej akceptacji użytkownika w systemowym oknie dialogowym w trakcie działania aplikacji (np. "zezwól tylko tym razem", "tylko podczas korzystania z aplikacji").
2. **Wskaźniki prywatności (Privacy Indicators)**: Systemowe ikony/kropki na pasku stanu (zielona dla kamery, pomarańczowa dla mikrofonu) informujące użytkownika na bieżąco, że aplikacja właśnie korzysta z danego sensora.
3. **Blokada sensorów w tle**: System automatycznie odcina aplikacjom działającym w tle (zminimalizowanym) dostęp do kamery i mikrofonu. Dostęp do lokalizacji w tle wymaga przejścia przez osobny, restrykcyjny proces autoryzacji w ustawieniach systemu.
4. **Ograniczenia logiczne**:
  - Skanowanie otoczenia za pomocą Bluetooth lub Wi-Fi jest traktowane przez systemy jako zbieranie lokalizacji i wymaga włączenia usług GPS oraz zgody na lokalizację.
  - Nawiązywanie połączeń i wysyłanie SMS-ów jest przekazywane do dialera systemowego, w którym użytkownik must osobiście zatwierdzić operację, co zapobiega potajemnemu wysyłaniu SMS-ów premium.

### 37. W jaki sposób programista powinien chronić wrażliwe dane użytkowników aplikacji mobilnych?
Programista powinien stosować zasadę **obrony w głąb (Defense in Depth)**:
1. *Bezpieczny zapis*: Hasła i tokeny sesyjne należy przechowywać wyłącznie w **Keychain** (iOS) lub przy użyciu biblioteki **EncryptedSharedPreferences** (Android). Lokalne bazy danych muszą być szyfrowane za pomocą **SQLCipher**.
2. *Bezpieczna sieć*: Wymuszenie protokołu HTTPS (blokada cleartext traffic w konfiguracji aplikacji) oraz wdrożenie **SSL Pinning** w celu ochrony przed przechwyceniem ruchu przez podstawiony certyfikat (ataki MitM).
3. *Maskowanie ekranu w tle*: Podmiana widoku na pusty ekran w metodach cyklu życia (np. `onPause()`), aby system operacyjny podczas minimalizowania aplikacji nie zapisał wrażliwych danych na zrzucie ekranu w menedżerze zadań.
4. *Ochrona kodu*: Obfuskacja kodu (R8/ProGuard), bezwzględny zakaz zapisywania sekretów i kluczy API bezpośrednio w kodzie (wszystkie operacje autoryzacji powinny przechodzić przez serwer backendowy).
5. *Zabezpieczenia RASP*: Wdrożenie bibliotek wykrywających obecność root/jailbreak, podłączenie debugera lub działanie na emulatorze i blokowanie uruchomienia aplikacji w takim środowisku.

### 38. Wyjaśnij na czym polega strategia budowania pozycji firmy na rynkach krajowych i zagranicznych w oparciu o fuzje, przejęcia, alianse strategiczne.
Jest to strategia **wzrostu zewnętrznego**, pozwalająca na szybką ekspansję bez konieczności powolnego budowania zasobów od zera:
* **Fuzje i Przejęcia (M&A - Mergers & Acquisitions)**:
  - *Fuzja*: Dobrowolne połączenie dwóch firm o podobnej skali w jeden nowy podmiot.
  - *Przejęcie*: Wykupienie pakietu kontrolnego udziałów/akcji przedsiębiorstwa przez drugą firmę.
  - *Zastosowanie*: Pozwala na natychmiastowe pozyskanie bazy klientów, udziałów w nowym rynku, marki oraz sieci dystrybucji na rynku zagranicznym. Prowadzi do **efektu synergii** (operacyjnej lub finansowej) – redukcji kosztów i wzrostu przychodów (efekt $2+2=5$).
* **Alianse strategiczne**:
  - Partnerska współpraca (np. wymiana technologii, porozumienia dystrybucyjne lub spółki typu **Joint Venture**) niezależnych podmiotów.
  - *Zastosowanie*: Wejście na trudne, zamknięte lub prawnie ograniczone rynki zagraniczne przy pomocy zasobów i wiedzy lokalnego partnera (dzielenie się ryzykiem i kosztami bez konieczności pełnej integracji kapitałowej).

### 39. Wymień i opisz podstawowe metody wykorzystywane w analizie strategicznej makrootoczenia, otoczenia branżowego firmy.
Metody te służą do badania wpływu czynników zewnętrznych na organizację:
* **Analiza Makrootoczenia (Otoczenie dalsze)**:
  - **Analiza PEST / PESTEL**: Identyfikacja szans i zagrożeń z otoczenia dalszego podzielonych na 6 kategorii:
    - **P**olityczne (stabilność władzy, cła),
    - **E**konomiczne (inflacja, PKB, stopy procentowe),
    - **S**połeczne (demografia, styl życia),
    - **T**echnologiczne (nowe patenty, cyfryzacja),
    - **E**kologiczne (ochrona środowiska, emisje CO2),
    - **L**egalne (prawo pracy, podatki).
* **Analiza Otoczenia Branżowego (Otoczenie bliższe/konkurencyjne)**:
  - **Model 5 Sił Portera**: Służy do badania atrakcyjności i rentowności sektora przez analizę 5 czynników:
    1. *Rywalizacja wewnątrz sektora* (liczba konkurentów, agresywność walki).
    2. *Groźba nowych wejść* (wysokość barier wejścia, wymagany kapitał).
    3. *Groźba pojawienia się substytutów* (alternatywne rozwiązania zaspokajające tę samą potrzebę).
    4. *Siła przetargowa dostawców* (stopień uzależnienia od kluczowych dostawców).
    5. *Siła przetargowa nabywców* (zdolność klientów do negocjowania niskich cen).

### 40. Przedstaw zestaw celów i mierników dla wybranej strategii (wzrostu/ stabilizacji/redukcji).
Wybrana strategia: **Strategia wzrostu** (ekspansja rynkowa i wzrost skali działania).
Mierniki podzielone są zgodnie z perspektywami Zrównoważonej Karty Wyników (BSC):
1. **Perspektywa finansowa**:
   - *Cel*: Zwiększenie powtarzalnego zysku ze sprzedaży. ➔ *Miernik*: **ARR (Annual Recurring Revenue)** (Cel: wzrost o 30% r/r).
   - *Cel*: Efektywność pozyskiwania klientów. ➔ *Miernik*: **Wskaźnik LTV : CAC** (stosunek wartości klienta do kosztu jego pozyskania, Cel: > 3:1).
2. **Perspektywa klienta**:
   - *Cel*: Zdobywanie udziału w rynku. ➔ *Miernik*: **Udział w rynku (Market Share)** (Cel: wzrost z 8% do 12%).
   - *Cel*: Zatrzymanie klientów. ➔ *Miernik*: **Churn Rate** (procent rezygnacji, Cel: < 1% miesięcznie).
3. **Perspektywa procesów wewnętrznych**:
   - *Cel*: Szybkie dostarczanie innowacji. ➔ *Miernik*: **Time-to-Market (TTM)** (czas od pomysłu do wdrożenia, Cel: skrócenie do 21 dni).
   - *Cel*: Niezawodność infrastruktury. ➔ *Miernik*: **SLA (Dostępność systemów)** (Cel: 99.9%).
4. **Perspektywa rozwoju i nauki**:
   - *Cel*: Skalowanie bazy użytkowników. ➔ *Miernik*: **MAU (Monthly Active Users)** (Cel: osiągnięcie 100 000 MAU).

### 41. Wyjaśnij pojęcie model biznesu, scharakteryzuj składowe modelu biznesu.
* **Model biznesu**: Koncepcyjne przedstawienie architektury operacyjno-finansowej przedsiębiorstwa, wyjaśniające podstawową logikę ekonomiczną: w jaki sposób firma tworzy wartość dla klientów, dostarcza ją na rynek oraz przechwytuje tę wartość w postaci generowanych zysków.
* **Składowe (według szablonu Business Model Canvas - 9 powiązanych bloków)**:
  1. *Segmenty klientów (Customer Segments)*: Grupy odbiorców, do których kierowana jest oferta.
  2. *Propozycja wartości (Value Proposition)*: Unikalny pakiet produktów/usług rozwiązujący problem klienta (serce modelu).
  3. *Kanały dotarcia (Channels)*: Punkty styku wykorzystywane do dostarczania propozycji wartości (sklep, dystrybutorzy).
  4. *Relacje z klientami (Customer Relationships)*: Charakter interakcji z odbiorcami (np. dedykowany opiekun, samoobsługa).
  5. *Strumienie przychodów (Revenue Streams)*: Sposób generowania gotówki (np. subskrypcja, jednorazowa sprzedaż, reklama).
  6. *Kluczowe zasoby (Key Resources)*: Środki niezbędne do działania modelu (fizyczne, intelektualne, ludzkie, finansowe).
  7. *Kluczowe działania (Key Activities)*: Najważniejsze procesy i czynności operacyjne (np. produkcja, programowanie).
  8. *Kluczowi partnerzy (Key Partnerships)*: Zewnętrzna sieć dostawców i kooperantów optymalizująca koszty i ryzyko.
  9. *Struktura kosztów (Cost Structure)*: Wszystkie koszty stałe i zmienne ponoszone w celu uruchomienia i utrzymania modelu.
