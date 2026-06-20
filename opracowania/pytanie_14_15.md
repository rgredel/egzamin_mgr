# Pytania 14-15: Zdefiniuj pojęcie "socjotechnika". W jaki sposób socjotechnika jest wykorzystywana w sieciach komputerowych?

## Kluczowe pojęcia
- **Socjotechnika (Inżynieria społeczna / ang. Social Engineering)**: Zbiór technik mających na celu manipulowanie ludźmi w celu skłonienia ich do wykonania określonych czynności (np. uruchomienia złośliwego oprogramowania) lub wyjawienia poufnych informacji (np. haseł, danych dostępowych).
- **Phishing**: Metoda ataku socjotechnicznego polegająca na wysyłaniu fałszywych wiadomości (e-mail, SMS) w celu wyłudzenia danych lub zainfekowania systemu.
- **Spear Phishing**: Spersonalizowany atak phishingowy wymierzony w konkretną osobę lub małą grupę osób na podstawie wcześniejszego rozpoznania (OSINT).
- **Baiting (Przynęta)**: Nakłonienie ofiary do wykonania czynności poprzez zaoferowanie jej obietnicy korzyści (np. darmowego oprogramowania lub pozostawienie zainfekowanego nośnika USB w miejscu publicznym).

## Szczegółowe omówienie tematu

### 1. Definicja socjotechniki (Inżynierii społecznej)
W kontekście bezpieczeństwa IT socjotechnika opiera się na założeniu, że **najsłabszym ogniwem każdego systemu bezpieczeństwa jest człowiek**. Atakujący zamiast szukać skomplikowanych podatności technicznych w oprogramowaniu (np. luk typu zero-day w zaporach sieciowych), manipuluje psychiką i emocjami użytkowników (strachem, ciekawością, chciwością, pośpiechem, szacunkiem do autorytetów), aby skłonić ich do samodzielnego otwarcia drzwi do systemu.

---

### 2. Wykorzystanie socjotechniki w sieciach komputerowych
Inżynieria społeczna w środowisku sieciowym przybiera różne formy komunikacji cyfrowej i metod infekcji:

#### A. Phishing i jego odmiany
Jest to najczęstszy wektor ataku w sieciach komputerowych.
- **Masowy Phishing**: Rozsyłanie milionów wiadomości e-mail/SMS (tzw. *Smishing*) podszywających się pod znane marki (np. DHL, Netflix, PGE) z informacją o konieczności dopłaty drobnej kwoty lub zweryfikowania konta. Link w wiadomości prowadzi do sfałszowanej bramki płatności lub panelu logowania.
- **Spear Phishing**: Atakujący bada cel przy użyciu białego wywiadu (OSINT) np. na portalach społecznościowych LinkedIn czy Facebook. Księgowa w firmie X otrzymuje maila od rzekomego klienta z zapytaniem o fakturę. Załącznik PDF (w rzeczywistości złośliwy plik `.exe` lub dokument z makrami) infekuje system i daje atakującemu dostęp do sieci firmowej.
- **Whaling (Polowanie na wieloryby)**: Odmiana spear phishingu wymierzona w kadrę zarządzającą wyższego szczebla (CEO, CFO).

#### B. BEC (Business Email Compromise) / CEO Fraud
Atak polegający na podszywaniu się pod dyrektora generalnego lub kontrahenta. Atakujący, często po uprzednim włamaniu na skrzynkę e-mail prezesa lub używając domeny łudząco podobnej (typosquatting), wysyła do działu finansowego pilne polecenie wykonania przelewu na nowe konto bankowe pod pretekstem "poufnej transakcji przejęcia firmy".

#### C. Pretexting i Vishing (Voice Phishing)
Atakujący dzwoni do ofiary (często fałszując numer telefonu nadawcy, tzw. *Caller ID Spoofing*) podając się za pracownika banku, policjanta lub dział IT (np. Microsoft Support). Przedstawia wymyśloną historię (pretekst) – np. wykrycie próby kradzieży środków z konta. Instruuje ofiarę, by zainstalowała oprogramowanie do zdalnego pulpitu (np. AnyDesk, TeamViewer), za pomocą którego przestępca przejmuje kontrolę nad jej komputerem i kontem bankowym.

#### D. Watering Hole Attack (Atak u żłopu)
Napastnik nie atakuje bezpośrednio wybranej firmy. Zamiast tego identyfikuje strony internetowe, z których pracownicy tej firmy często korzystają (np. lokalne forum branżowe, portal informacyjny, strona pobliskiej restauracji oferującej lunch). Atakujący włamuje się na tę witrynę i umieszcza na niej złośliwy kod, który infekuje komputery odwiedzających ją pracowników, wykorzystując podatności w ich przeglądarkach.

---

### 3. Psychologiczne mechanizmy wywierania wpływu (wg R. Cialdiniego)
Ataki socjotechniczne są skuteczne, ponieważ bazują na automatyzmach ludzkiego zachowania:
- **Autorytet**: Ludzie chętnie wykonują polecenia osób, które uznają za przełożonych lub przedstawicieli prawa (np. "Dyrektor IT", "Policja").
- **Reguła pilności (Niedostępności)**: Wywieranie presji czasu ("Twoje konto zostanie zablokowane za 15 minut"). W pośpiechu ludzie wyłączają racjonalne myślenie.
- **Sympatia i zaufanie**: Budowanie fałszywej więzi przez atakującego przed poproszeniem o przysługę.

---

### 4. Metody obrony przed socjotechniką
Ponieważ nie da się zainstalować antywirusa w ludzkim mózgu, obrona musi łączyć procedury organizacyjne z technologią:

1. **Szkolenia typu Security Awareness**: Systematyczne edukowanie pracowników i przeprowadzanie kontrolowanych, próbnych ataków phishingowych w celu wyrobienia nawyku ograniczonego zaufania.
2. **Techniczne uwierzytelnianie wieloskładnikowe (MFA)**: Wdrożenie kluczy sprzętowych (np. **YubiKey** w standardzie FIDO2/U2F). Są one odporne na phishing – nawet jeśli użytkownik poda hasło na fałszywej stronie, klucz sprzętowy nie wygeneruje tokenu dla fałszywej domeny.
3. **Zabezpieczenia poczty e-mail**: Konfiguracja mechanizmów autoryzacji poczty:
   - **SPF (Sender Policy Framework)**: Wskazuje, które serwery mogą wysyłać maile z danej domeny.
   - **DKIM (DomainKeys Identified Mail)**: Podpisuje maile kryptograficznie.
   - **DMARC (Domain-based Message Authentication, Reporting and Conformance)**: Określa, co serwer odbiorcy ma zrobić z mailem, który nie przeszedł testów SPF/DKIM.
4. **Zasada Zero Trust (Brak zaufania)**: Każda nietypowa prośba (np. zmiana numeru konta do faktury, prośba o podanie hasła) musi być zweryfikowana innym kanałem komunikacji (np. osobista rozmowa lub oddzwonienie na oficjalny numer).
