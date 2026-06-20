# Pytanie 34: Opisz trzy zagrożenia dotyczące aplikacji mobilnych według projektu OWASP.

## Kluczowe pojęcia
- **OWASP Mobile Top 10**: Cykliczne zestawienie najpoważniejszych zagrożeń bezpieczeństwa dla aplikacji mobilnych (Android, iOS) opracowane przez organizację OWASP.
- **SSL Pinning**: Mechanizm zabezpieczający komunikację sieciową przed atakami MitM poprzez powiązanie aplikacji mobilnej z konkretnym certyfikatem serwera.
- **Obfuskacja (Zaciemnianie kodu)**: Przekształcenie kodu źródłowego do postaci nieczytelnej dla człowieka w celu utrudnienia inżynierii wstecznej (dekompilacji).
- **EDR / RASP**: Technologie ochrony aplikacji w czasie rzeczywistym (Runtime Application Self-Protection) przed modyfikacjami i uruchamianiem na urządzeniach z root/jailbreak.

## Szczegółowe omówienie tematu

Projekt OWASP tworzy dedykowaną listę zagrożeń specyficznych dla urządzeń mobilnych, uwzględniając fakt, że aplikacja mobilna działa w środowisku klienta (fizyczne urządzenie użytkownika), co daje atakującemu znacznie większe możliwości ingerencji w jej kod i dane lokalne. Poniżej przedstawiono charakterystykę trzech głównych zagrożeń według OWASP.

---

### Zagrożenie 1: Insecure Data Storage (Niezabezpieczone przechowywanie danych)
- **Charakterystyka**:
  Aplikacja mobilna przechowuje poufne informacje (np. hasła, tokeny uwierzytelniające JWT, dane osobowe, numery kart płatniczych, klucze szyfrujące) bezpośrednio w pamięci flash urządzenia bez odpowiedniego szyfrowania. Dane te są często zapisywane w plikach konfiguracyjnych (np. `SharedPreferences` w Androidzie, pliki `.plist` w iOS), lokalnych bazach danych SQLite lub w logach systemowych aplikacji (logcat).
- **Zagrożenie**:
  W przypadku fizycznej kradzieży lub zgubienia telefonu, osoba nieuprawniona może zrzucić pamięć urządzenia. Jeśli telefon ma odblokowane uprawnienia administratora (Root na Androidzie / Jailbreak na iOS), złośliwe oprogramowanie zainstalowane w systemie może uzyskać dostęp do prywatnego katalogu aplikacji i skraść te dane.
- **Metody obrony**:
  - Przechowywanie danych uwierzytelniających wyłącznie w bezpiecznych, sprzętowo izolowanych kontenerach systemowych: **Android Keystore System** oraz **iOS Keychain**.
  - Szyfrowanie lokalnych baz danych SQLite za pomocą biblioteki **SQLCipher**.
  - Bezwzględny zakaz logowania danych wrażliwych w konsoli deweloperskiej.

---

### Zagrożenie 2: Insecure Communication (Niezabezpieczona komunikacja)
- **Charakterystyka**:
  Aplikacja mobilna komunikuje się z serwerem (API backendowym) za pomocą nieszyfrowanego protokołu HTTP, używa przestarzałych wersji protokołu TLS (np. TLS 1.0, 1.1) lub nie weryfikuje poprawności certyfikatu SSL/TLS wystawionego przez serwer (np. akceptuje certyfikaty podpisane samodzielnie - self-signed).
- **Zagrożenie**:
  Podatność na ataki typu **Man-in-the-Middle (MitM)**. Gdy użytkownik łączy się z publiczną, niezabezpieczoną siecią Wi-Fi (np. w kawiarni), atakujący może przechwycić cały ruch sieciowy, w tym tokeny sesyjne i hasła, lub wstrzyknąć fałszywe dane do aplikacji.
- **Metody obrony**:
  - Wymuszenie komunikacji wyłącznie przez bezpieczny protokół **HTTPS** (wspierający TLS 1.2/1.3) przy użyciu mechanizmów systemowych (np. Network Security Configuration w Androidzie).
  - Wdrożenie **SSL/Certificate Pinning** – zapisanie w kodzie aplikacji sumy kontrolnej klucza publicznego certyfikatu serwera. Dzięki temu aplikacja odrzuci połączenie z serwerem, jeśli certyfikat zostanie podmieniony (nawet jeśli system operacyjny uzna fałszywy certyfikat za zaufany).

---

### Zagrożenie 3: Reverse Engineering (Inżynieria wsteczna)
- **Charakterystyka**:
  Brak odpowiednich zabezpieczeń binarnych aplikacji. Paczkę instalacyjną aplikacji (plik `.apk` na Androidzie lub `.ipa` na iOS) można łatwo pobrać ze sklepu i dekompilować do niemal oryginalnego kodu źródłowego przy użyciu bezpłatnych narzędzi (np. *Jadx*, *Apktool*, *Hopper*).
- **Zagrożenie**:
  Atakujący analizuje kod źródłowy aplikacji w celu:
    - Odszukania ukrytych kluczy API, haseł do baz danych lub kluczy kryptograficznych zahardkodowanych w kodzie.
    - Zrozumienia logiki biznesowej i znalezienia luk w API backendowym.
    - Modyfikacji kodu binarnego (np. usunięcia weryfikacji licencji lub reklam), ponownego podpisania aplikacji i opublikowania jej zainfekowanej wersji w nieoficjalnych sklepach.
- **Metody obrony**:
  - Stosowanie narzędzi do **obfuskacji (zaciemniania)** kodu (np. *ProGuard*, *R8* w Androidzie) – zmieniają one nazwy klas i funkcji na losowe ciągi znaków, utrudniając analizę.
  - Implementacja mechanizmów anty-dekompilacji i detekcji modyfikacji kodu (Root/Jailbreak detection) – aplikacja powinna odmówić uruchomienia, jeśli wykryje, że działa na zmodyfikowanym urządzeniu lub jej podpis cyfrowy został zmieniony.
