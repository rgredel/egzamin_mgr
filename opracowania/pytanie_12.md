# Pytanie 12: Zdefiniuj atak SQL Injection, podaj typy ataków SQL Injection na aplikacje internetowe, ich skutki i metody obrony przed nimi.

## Kluczowe pojęcia
- **SQL Injection (SQLi / Wstrzykiwanie kodu SQL)**: Podatność polegająca na wstrzyknięciu złośliwego kodu SQL do parametrów zapytania wysyłanego przez aplikację do bazy danych, co pozwala na zmianę logiki pierwotnego zapytania i wykonanie nieautoryzowanych instrukcji.
- **Zapytanie parametryzowane (Prepared Statements)**: Technika bezpiecznego budowania zapytań SQL, w której struktura zapytania jest definiowana oddzielnie od danych wejściowych, co uniemożliwia interpretację danych jako kodu.
- **Fuzzing**: Metoda testowania polegająca na wysyłaniu do aplikacji losowych, nieoczekiwanych lub zniekształconych danych wejściowych w celu wykrycia błędów i luk.

## Szczegółowe omówienie tematu

### 1. Definicja i mechanizm działania SQL Injection
Do wstrzykiwania kodu SQL dochodzi, gdy programista buduje zapytanie SQL dynamicznie poprzez konkatenację (łączenie) ciągów tekstowych z danymi pochodzącymi od użytkownika. Przeglądarka lub aplikacja kliencka wysyła te dane, a baza danych interpretuje je jako instrukcje sterujące, a nie jako zwykłe wartości (literały).

*Przykład podatnego kodu (Java/JDBC)*:
```java
String query = "SELECT * FROM users WHERE login = '" + request.getParameter("user") + "'";
```
Jeśli użytkownik wpisze login: `admin' OR '1'='1`, zapytanie przetworzone przez bazę danych przyjmie postać:
```sql
SELECT * FROM users WHERE login = 'admin' OR '1'='1'
```
Ponieważ warunek `'1'='1'` jest zawsze prawdziwy, baza danych zwróci rekordy wszystkich użytkowników (lub pierwszego z nich, czyli zazwyczaj administratora), omijając proces weryfikacji hasła.

---

### 2. Typy ataków SQL Injection

Ataki SQLi klasyfikuje się na podstawie metody, w jaki sposób atakujący wyciąga dane z bazy:

#### A. In-band SQLi (Klasyczny / W kanale komunikacji):
Najprostsza i najszybsza forma ataku, w której wyniki zapytania oraz ewentualne błędy są zwracane bezpośrednio w odpowiedzi aplikacji (np. na wyświetlanej stronie).
- **Union-based SQLi**: Wykorzystuje operator `UNION` do połączenia wyników oryginalnego zapytania z wynikami zapytania wstrzykniętego przez atakującego. Pozwala to na wyciągnięcie zawartości dowolnej tabeli w bazie danych (np. `UNION SELECT username, password FROM admin_users`).
- **Error-based SQLi**: Wywoływanie błędów bazy danych (np. dzielenie przez zero, konwersja typów) w taki sposób, aby treść błędu wyświetlana na stronie zawierała poszukiwane dane (np. wersję serwera bazy danych czy nazwę bieżącej bazy).

#### B. Blind SQLi (Ślepy / Inferencyjny):
Aplikacja nie wyświetla wyników zapytania SQL ani komunikatów o błędach. Atakujący musi wnioskować o danych poprzez zadawanie bazie danych pytań typu prawda/fałsz.
- **Boolean-based Blind SQLi**: Atakujący modyfikuje zapytanie tak, aby zwracało prawdę (np. `AND 1=1`) lub fałsz (`AND 1=2`). Jeśli aplikacja reaguje subtelną zmianą wyglądu strony (np. brakiem jakiegoś elementu), atakujący może odczytywać dane znak po znaku (np. "Czy pierwsza litera hasła administratora to 'A'?").
- **Time-based Blind SQLi**: Używany, gdy aplikacja zachowuje się identycznie niezależnie od wyniku zapytania. Atakujący zmusza bazę danych do opóźnienia odpowiedzi (np. `AND IF(1=1, SLEEP(5), 0)`). Jeśli serwer odpowie po 5 sekundach, oznacza to, że postawiony warunek był prawdziwy.

#### C. Out-of-band SQLi (Poza kanałem komunikacji):
Stosowany, gdy serwer bazy danych jest odizolowany, a zapytania ślepe są zbyt powolne. Atakujący zmusza bazę danych do wysłania żądania sieciowego (np. zapytania DNS o domenę `kradzione-dane.atakujacy.com`) za pomocą wbudowanych funkcji bazy danych.

---

### 3. Skutki ataku SQLi
Udana eksploatacja SQLi może doprowadzić do:
- **Naruszenia poufności**: Kradzież baz danych, w tym haseł, danych osobowych (RODO) i tajemnic handlowych.
- **Naruszenia integralności**: Modyfikacja danych w bazie (np. zmiana salda konta, uprawnień użytkownika) lub usuwanie danych (`DROP TABLE`).
- **Naruszenia dostępności**: Zablokowanie bazy danych.
- **Remote Code Execution (RCE)**: W niektórych konfiguracjach (np. `xp_cmdshell` w MS SQL) atakujący może za pośrednictwem bazy danych uruchamiać polecenia w systemie operacyjnym serwera, co prowadzi do pełnego przejęcia komputera.

---

### 4. Metody obrony przed SQLi
Obrona przed SQLi jest relatywnie prosta, o ile zasady są konsekwentnie stosowane w całym projekcie:

1. **Używanie zapytań parametryzowanych (Prepared Statements)**:
   Dane wejściowe od użytkownika są przesyłane do bazy danych osobno jako parametry, a nie jako część instrukcji SQL. Baza najpierw kompiluje zapytanie, a parametry traktuje wyłącznie jako wartości tekstowe/liczbowe, przez co znaki takie jak `'` tracą swoje znaczenie sterujące.
   *Przykład bezpiecznego kodu (Java)*:
   ```java
   String query = "SELECT * FROM users WHERE login = ?";
   PreparedStatement stmt = connection.prepareStatement(query);
   stmt.setString(1, request.getParameter("user"));
   ```

2. **Stosowanie ORM (Object-Relational Mapping)**:
   Korzystanie z frameworków takich jak Hibernate, JPA czy Entity Framework chroni przed SQLi, ponieważ pod spodem automatycznie generują one zapytania parametryzowane. (Należy jednak unikać ręcznej konkatenacji stringów w zapytaniach typu HQL/JPQL).

3. **Zasada minimalnych uprawnień (Least Privilege)**:
   Konto bazy danych używane przez aplikację powinno mieć uprawnienia ograniczone tylko do niezbędnych tabel i operacji (np. brak praw do modyfikacji struktury bazy - `DROP`, `ALTER`).

4. **Walidacja danych wejściowych**:
   Wprowadzenie białej listy dopuszczalnych znaków oraz weryfikacja typów danych (np. upewnienie się, że parametr `id` zawiera wyłącznie cyfry przed wykonaniem zapytania).
