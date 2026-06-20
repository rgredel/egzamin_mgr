# Pytanie 37: W jaki sposób programista powinien chronić wrażliwe dane użytkowników aplikacji mobilnych?

## Kluczowe pojęcia
- **Obrona w głąb (Defense in Depth)**: Strategia bezpieczeństwa polegająca na stosowaniu wielu niezależnych mechanizmów zabezpieczających, tak aby przełamanie jednego nie powodowało kompromitacji całego systemu.
- **Jetpack Security (EncryptedSharedPreferences)**: Biblioteka w systemie Android służąca do automatycznego szyfrowania kluczy i wartości w plikach konfiguracyjnych przy użyciu algorytmu AES-256.
- **SSL Pinning**: Technika kryptograficzna zapobiegająca atakom Man-in-the-Middle poprzez weryfikację poprawności klucza publicznego certyfikatu serwera bezpośrednio w kodzie aplikacji.
- **RASP (Runtime Application Self-Protection)**: Mechanizmy pozwalające aplikacji na wykrywanie zagrożeń w czasie rzeczywistym (np. wykrycie roota, debuggera) i odpowiednie reagowanie (np. zamknięcie aplikacji).

## Szczegółowe omówienie tematu

Programista aplikacji mobilnej musi zakładać, że fizyczne urządzenie, na którym uruchamiany jest jego program, może być środowiskiem wrogim (np. zgubiony telefon, obecność złośliwego oprogramowania, uprawnienia roota/jailbreaka). Bezpieczeństwo danych użytkownika leży po stronie kodu aplikacji i powinno obejmować kilka obszarów.

---

### 1. Bezpieczne przechowywanie danych lokalnych (Data at Rest)
Programista nie może zapisywać danych wrażliwych (haseł, tokenów sesyjnych, danych osobowych) otwartym tekstem na partycjach pamięci.
- **Wykorzystanie systemowych magazynów**:
  - **Android**: Stosowanie biblioteki **EncryptedSharedPreferences** z pakietu *Android Jetpack Security*. Szyfruje ona automatycznie klucze i wartości algorytmem AES-256 w trybie GCM, przechowując klucz deszyfrujący w sprzętowo odizolowanym **Android Keystore**.
  - **iOS**: Zapisywanie haseł i tokenów wyłącznie w **Keychain** z ustawieniem klasy dostępności (np. `kSecAttrAccessibleAfterFirstUnlockThisDeviceOnly` – dane są niedostępne, gdy ekran telefonu jest zablokowany).
- **Szyfrowanie baz danych**: W przypadku zapisu dużych ilości danych strukturalnych należy wdrożyć bazę SQLite zaszyfrowaną przy użyciu biblioteki **SQLCipher**.
- **Maskowanie ekranu w tle (Backgrounding Protection)**:
  Podczas minimalizowania aplikacji system operacyjny robi jej zrzut ekranu w celu wyświetlenia go w menedżerze zadań. Programista powinien zaimplementować mechanizm podmieniający widok na pusty ekran (lub logo firmy) w metodzie cyklu życia aplikacji (np. `onPause()` w Androidzie lub `applicationWillResignActive()` w iOS), aby zapobiec wyciekowi danych (np. stanu konta) na zrzutach ekranu.
- **Zabezpieczenie przed zapamiętywaniem (Autofill i Cache)**:
  Wyłączenie autouzupełniania i autokorekty dla wrażliwych pól tekstowych (np. PESEL, numer karty) oraz blokowanie zapisu odpowiedzi API w cache przeglądarki/klienta HTTP.

---

### 2. Bezpieczna komunikacja sieciowa (Data in Transit)
- **Wymuszenie szyfrowania**: Całkowite zablokowanie ruchu nieszyfrowanego (HTTP) w konfiguracji aplikacji (parametr `cleartextTrafficPermitted="false"` w Androidzie oraz restrykcje `App Transport Security - ATS` w iOS).
- **SSL Pinning**: Zaimplementowanie powiązania certyfikatu (np. przy użyciu biblioteki OkHttp CertificatePinner w Androidzie). Zapobiega to przechwyceniu ruchu HTTPS przez napastnika, który zainstalował na urządzeniu własny, zaufany certyfikat CA (częsty scenariusz przy podsłuchu przez oprogramowanie szpiegujące).

---

### 3. Ochrona przed analizą kodu i modyfikacją (Inżynieria wsteczna)
Ponieważ paczka aplikacji (APK/IPA) jest publicznie dostępna, kod źródłowy musi być chroniony.
- **Zaciemnianie kodu (Obfuskacja)**: Konfiguracja narzędzi takich jak **R8/ProGuard** (Android) w celu skrócenia i zaciemnienia nazw metod, zmiennych i klas, co drastycznie utrudnia analizę kodu po dekompilacji.
- **Zakaz przechowywania sekretów w kodzie (Hardcoding)**: Programista **nigdy** nie powinien umieszczać kluczy prywatnych ani kluczy API (np. do bramek płatniczych, baz danych) bezpośrednio w kodzie źródłowym. Dostęp do zewnętrznych usług powinien być realizowany przez serwer pośredniczący (backend), który autoryzuje zapytania od aplikacji mobilnej.
- **Mechanizmy RASP (Runtime Application Self-Protection)**:
  Implementacja testów bezpieczeństwa środowiska uruchomieniowego:
    - *Wykrywanie Root/Jailbreak*: Aplikacja powinna wykryć obecność plików takich jak `su` czy aplikacji takich jak *Magisk*/*Cydia* i zablokować dostęp do funkcji wrażliwych.
    - *Anti-debugging / Anti-emulator*: Blokowanie możliwości podłączenia debugera (np. za pomocą JDWP) lub działania w środowisku emulowanym.
    - *Weryfikacja podpisu (Tamper Detection)*: Sprawdzanie w czasie działania, czy podpis cyfrowy aplikacji nie uległ zmianie (co wskazywałoby na modyfikację kodu i ponowne spakowanie aplikacji przez hakera).

---

### 4. Bezpieczne uwierzytelnianie i autoryzacja
- **Uwierzytelnianie biometryczne**: Integracja z systemowym interfejsem biometrii (BiometricPrompt / FaceID). Weryfikacja biometryczna powinna być zintegrowana kryptograficznie – np. poprawny odczyt odcisku palca odblokowuje dostęp do klucza w Keystore/Keychain, którym szyfrowany jest token sesji.
- **Zarządzanie tokenami**: Stosowanie tokenów dostępowych (np. OAuth 2.0 / JWT) o krótkim czasie ważności, wymuszanie ponownego logowania przy próbie wykonania operacji krytycznych (np. zmiana hasła, przelew).

## Podsumowanie
Bezpieczeństwo aplikacji mobilnej zależy od świadomości programisty. Stosując zasadę **obrony w głąb**, należy zabezpieczyć dane lokalne przy użyciu sprzętowo chronionych kluczy (Keystore/Keychain) i szyfrowania (EncryptedSharedPreferences, SQLCipher), wymusić bezpieczną komunikację sieciową (HTTPS, SSL Pinning) oraz zabezpieczyć sam plik binarny przed dekompilacją i uruchomieniem w niezaufanym środowisku (obfuskacja, RASP).
