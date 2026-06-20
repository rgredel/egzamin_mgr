# Pytanie 19: Omów jedno z narzędzi modelowania zagrożeń systemów komputerowych.

## Kluczowe pojęcia
- **Modelowanie zagrożeń (Threat Modeling)**: Systematyczny proces identyfikacji, oceny i mitygowania ryzyk bezpieczeństwa na etapie projektowania architektury systemu IT (podejście *Secure by Design*).
- **STRIDE**: Metodologia klasyfikacji zagrożeń opracowana przez Microsoft (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege).
- **DFD (Data Flow Diagram / Diagram Przepływu Danych)**: Graficzny model systemu przedstawiający procesy, magazyny danych, elementy zewnętrzne i przepływy informacji przez granice zaufania.
- **Granica zaufania (Trust Boundary)**: Umowna linia oddzielająca obszary systemu o różnych poziomach uprawnień i zaufania (np. sieć publiczna a sieć prywatna).

## Szczegółowe omówienie tematu

Jednym z najbardziej znanych i najszerzej stosowanych narzędzi do modelowania zagrożeń jest **Microsoft Threat Modeling Tool (TMT)**. Jest to bezpłatne narzędzie stworzone w celu wsparcia bezpiecznego cyklu wytwarzania oprogramowania (SDL - Security Development Lifecycle).

---

### 1. Idea działania Microsoft Threat Modeling Tool (TMT)
Narzędzie opiera się na koncepcji, że najtaniej i najskuteczniej poprawia się błędy bezpieczeństwa na etapie **projektowania architektury**, zanim powstanie kod źródłowy. TMT pozwala na graficzne zamodelowanie systemu, a następnie automatycznie (na podstawie wbudowanego silnika reguł) generuje listę potencjalnych zagrożeń, które architekt lub inżynier bezpieczeństwa musi przeanalizować.

---

### 2. Główne elementy modelowania w TMT
Podczas tworzenia modelu w narzędziu użytkownik rysuje diagram DFD, korzystając z następujących komponentów (szablonów):
- **External Interactor (Podmiot zewnętrzny)**: Elementy poza bezpośrednią kontrolą systemu (np. użytkownik, przeglądarka internetowa, zewnętrzne API).
- **Process (Proces)**: Dowolny kod wykonujący operacje (np. aplikacja webowa, mikrousługa, zadanie w tle).
- **Data Store (Magazyn danych)**: Miejsce, w którym dane są zapisywane (np. baza danych SQL, plik konfiguracyjny, pamięć cache).
- **Data Flow (Przepływ danych)**: Kanał komunikacji między elementami (np. zapytanie HTTPS, połączenie TCP, potok systemowy).
- **Trust Boundary (Granica zaufania)**: Zaznaczana czerwoną przerywaną linią. Rozgranicza strefy o różnym poziomie zaufania. Przejście danych przez granicę zaufania (np. od użytkownika z Internetu do bazy danych w sieci lokalnej) to miejsce, w którym najczęściej dochodzi do ataków.

---

### 3. Automatyczna analiza zagrożeń (Metodologia STRIDE)
Gdy diagram DFD jest gotowy, użytkownik przełącza narzędzie w tryb analizy (*Analysis View*). TMT automatycznie generuje zagrożenia dopasowane do narysowanej architektury, klasyfikując je według modelu **STRIDE**:

| Litera | Zagrożenie (ang.) | Tłumaczenie / Opis | Przykład generowany przez TMT |
| :--- | :--- | :--- | :--- |
| **S** | **Spoofing** | Podszywanie się pod kogoś/coś | Brak uwierzytelniania użytkownika przesyłającego dane. |
| **T** | **Tampering** | Manipulacja danymi | Dane przesyłane przez granicę zaufania jawnym tekstem (możliwość modyfikacji). |
| **R** | **Repudiation** | Zaprzeczalność czynu | Brak logowania zdarzeń (użytkownik może zaprzeczyć, że wykonał akcję). |
| **I** | **Information Disclosure** | Ujawnienie informacji (wyciek) | Baza danych zapisuje poufne informacje bez szyfrowania. |
| **D** | **Denial of Service** | Odmowa usługi (przeciążenie) | Brak limitów zapytań (rate limiting) na serwerze WWW. |
| **E** | **Elevation of Privilege** | Eskalacja uprawnień | Brak autoryzacji (użytkownik może wywołać funkcje admina). |

---

### 4. Cykl zarządzania zagrożeniami w TMT
Dla każdego wygenerowanego przez narzędzie zagrożenia, zespół projektowy musi określić jego status oraz opisać sposób mitygacji:
1. **Mitigated (Rozwiązane)**: Wskazanie konkretnego zabezpieczenia technicznego (np. „Połączenie zabezpieczone TLS 1.3, hasła hashowane za pomocą bcrypt”).
2. **Accepted (Zaakceptowane)**: Świadome ryzyko biznesowe (np. „Serwer nie ma rate-limitera, ponieważ działa wyłącznie w zamkniętej sieci testowej”).
3. **Needs Investigation**: Wymaga dalszej analizy.

Narzędzie umożliwia wygenerowanie kompletnego raportu (w formacie HTML), który służy jako dokumentacja bezpieczeństwa dla audytorów oraz wytyczne dla programistów wdrażających system.

## Podsumowanie
Microsoft Threat Modeling Tool to potężne, ustrukturyzowane narzędzie, które przekłada architekturę logiczną systemu na konkretne zagrożenia bezpieczeństwa przy użyciu metodologii STRIDE. Pomaga ono deweloperom i architektom myśleć jak atakujący, co pozwala na eliminację luk bezpieczeństwa na najwcześniejszym etapie SDLC.
