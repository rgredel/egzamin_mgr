# Pytanie 17: Omów mechanizmy zabezpieczeń stosowane w sieciach bezprzewodowych Wi-Fi.

## Kluczowe pojęcia
- **WEP (Wired Equivalent Privacy)**: Pierwszy, przestarzały i całkowicie złamany standard szyfrowania Wi-Fi.
- **WPA2 (Wi-Fi Protected Access 2)**: Szeroko stosowany standard bezpieczeństwa, wprowadzający silne szyfrowanie AES-CCMP.
- **WPA3**: Najnowsza generacja zabezpieczeń Wi-Fi, zastępująca podatny mechanizm PSK protokołem SAE (Simultaneous Authentication of Equals).
- **TKIP (Temporal Key Integrity Protocol)**: Protokół szyfrowania oparty na RC4, wprowadzony jako tymczasowa łata na WEP, obecnie uznawany za niebezpieczny.
- **RADIUS**: Serwer uwierzytelniania stosowany w sieciach korporacyjnych (Enterprise) do weryfikacji tożsamości użytkowników.

## Szczegółowe omówienie tematu

Ponieważ fale radiowe sieci Wi-Fi rozchodzą się w przestrzeni publicznej, fizyczna ochrona medium transmisyjnego jest niemożliwa. Bezpieczeństwo Wi-Fi opiera się w całości na mechanizmach kryptograficznych realizujących dwa cele: **uwierzytelnianie** (kto może się połączyć) oraz **szyfrowanie** (ochrona przed podsłuchem).

---

### 1. Protokoły zabezpieczeń Wi-Fi i ich ewolucja

#### WEP (Wired Equivalent Privacy) - *Standard wycofany i niebezpieczny*
- **Szyfrowanie**: Wykorzystuje algorytm strumieniowy RC4. Klucz szyfrujący jest łączony z 24-bitowym Wektorem Inicjującym (IV).
- **Podatności**: Ze względu na krótki wektor IV, w sieci o dużym natężeniu ruchu te same wektory szybko się powtarzają. Atakujący, przechwytując odpowiednią liczbę ramek (za pomocą np. `aircrack-ng`), może matematycznie odtworzyć klucz główny sieci w czasie krótszym niż minuta.

#### WPA (Wi-Fi Protected Access) - *Standard przejściowy*
- **Szyfrowanie**: Wprowadził protokół **TKIP** (Temporal Key Integrity Protocol), który dynamicznie generował nowy klucz dla każdego pakietu danych, co eliminowało problem powtarzalności IV z WEP. Pod spodem jednak nadal działał algorytm RC4. Obecnie WPA-TKIP jest uznawany za przestarzały i podatny na ataki.

#### WPA2 (Wi-Fi Protected Access 2) - *Standard powszechny*
- **Szyfrowanie**: Zastąpił TKIP bezpiecznym protokołem **CCMP** opartym na zaawansowanym algorytmie szyfrowania symetrycznego **AES** (Advanced Encryption Standard).
- **Warianty**:
  - **WPA2-PSK (Personal)**: Autoryzacja za pomocą jednego, wspólnego hasła (Pre-Shared Key).
    *Słabość*: Podatność na offline-owe ataki słownikowe. Atakujący podsłuchuje proces logowania klienta do stacji bazowej (tzw. *4-way handshake*). Następnie na własnym komputerze próbuje dopasować hasło ze słownika do przechwyconego hashu. Dodatkowo w 2017 r. ujawniono podatność **KRACK** (Key Reinstallation Attack) w samym protokole nawiązywania połączenia.
  - **WPA2-Enterprise**: Używany w korporacjach. Wykorzystuje standard **IEEE 802.1X**. Użytkownicy logują się indywidualnie (login/hasło, certyfikat cyfrowy) przez zewnętrzny serwer **RADIUS**, który generuje unikalne klucze szyfrujące dla każdej sesji.

#### WPA3 - *Najnowszy i zalecany standard*
- **Dragonfly Handshake (SAE)**: Klucz współdzielony został zastąpiony protokołem **SAE (Simultaneous Authentication of Equals)**. Protokół ten uniemożliwia przeprowadzanie offline-owych ataków słownikowych (brute-force) na przechwycony ruch. Nawet jeśli hasło jest słabe, atakujący nie może go złamać bez interakcji online z punktem dostępowym (AP), co pozwala na łatwe zablokowanie takich prób.
- **Forward Secrecy (Poufność przekazywania)**: Nawet jeśli hasło do sieci zostanie złamane w przyszłości, nie pozwoli to na odszyfrowanie ruchu sieciowego zarejestrowanego wcześniej.
- **OWE (Opportunistic Wireless Encryption)**: Szyfrowanie ruchu w sieciach otwartych (bezhasłowych, np. w hotelach). Chroni użytkowników przed podsłuchiwaniem ich transmisji przez inne osoby w tej samej sieci.

---

### 2. Pomocnicze i przestarzałe mechanizmy (antywzorce)
W przeszłości stosowano metody, które dziś nie są uznawane za rzeczywiste zabezpieczenia:
- **Ukrywanie SSID**: Wyłączenie rozgłaszania nazwy sieci w ramkach typu Beacon. Jest to nieskuteczne, ponieważ nazwa sieci (SSID) jest przesyłana jawnym tekstem w ramkach żądania asocjacji (Association Requests), gdy legalne urządzenia próbują się połączyć.
- **Filtrowanie adresów MAC**: Blokowanie urządzeń o nieznanych adresach fizycznych MAC. Adresy te są przesyłane otwartym tekstem w nagłówkach ramek 802.11. Atakujący może łatwo odczytać dozwolony adres MAC i podrobić go na swoim urządzeniu (tzw. *MAC Spoofing*).
- **WPS (Wi-Fi Protected Setup)**: Standard ułatwiający łączenie urządzeń (np. za pomocą 8-cyfrowego kodu PIN). Posiada krytyczną lukę projektową (podatność na atak brute-force za pomocą narzędzia *Reaver*), umożliwiającą odzyskanie hasła sieci w kilka godzin. **Powinien być bezwzględnie wyłączony**.

## Podsumowanie
W celu zapewnienia bezpieczeństwa sieci Wi-Fi należy bezwzględnie wyłączyć obsługę protokołów WEP, WPA oraz WPS. Rekomendowaną konfiguracją jest stosowanie **WPA3-SAE** dla sieci domowych oraz **WPA3-Enterprise** (z uwierzytelnianiem 802.1X i serwerem RADIUS) w środowiskach biznesowych.
