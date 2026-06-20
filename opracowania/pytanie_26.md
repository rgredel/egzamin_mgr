# Pytanie 26: Charakterystyka systemów rozproszonych - zalety i wady.

## Kluczowe pojęcia
- **System rozproszony**: Zbiór autonomicznych komputerów (węzłów) połączonych siecią, które komunikują się i koordynują swoje działania poprzez przesyłanie komunikatów, sprawiając wrażenie jednego, spójnego systemu dla użytkownika.
- **Skalowalność horyzontalna (w poziomie)**: Zwiększanie wydajności systemu poprzez dodawanie kolejnych komputerów do klastra.
- **Tolerancja na awarie (Fault Tolerance)**: Zdolność systemu do poprawnego działania nawet w przypadku uszkodzenia niektórych jego elementów.
- **Twierdzenie CAP**: Twierdzenie mówiące, że w rozproszonym magazynie danych można jednocześnie zapewnić tylko dwie z trzech cech: Spójność (Consistency), Dostępność (Availability) i Tolerancję na podział sieci (Partition Tolerance).

## Szczegółowe omówienie tematu

### 1. Charakterystyka systemów rozproszonych
Systemy rozproszone charakteryzują się brakiem wspólnej pamięci fizycznej (każdy węzeł ma własny procesor i pamięć RAM) oraz brakiem globalnego zegara systemowego (węzły muszą synchronizować czas za pomocą protokołów sieciowych, np. NTP, lub zegarów logicznych Lamporta). Kluczowe cechy to:
- **Współbieżność**: Wiele procesów działa w tym samym czasie na różnych maszynach.
- **Brak centralnego zegara**: Zdarzenia są porządkowane logicznie, a nie na podstawie bezwzględnego czasu fizycznego.
- **Niezależne awarie**: Awaria jednego komputera nie oznacza awarii całego systemu.

---

### 2. Zalety systemów rozproszonych

- **Skalowalność (Scalability)**:
  Możliwość niemal nieograniczonego skalowania w poziomie. Zamiast kupować jeden bardzo drogi superkomputer (skalowanie pionowe), można łączyć setki lub tysiące tanich, standardowych serwerów w klaster.
- **Wysoka dostępność (High Availability) i niezawodność**:
  Dzięki replikacji danych i nadmiarowości (redundancji) awaria jednego lub kilku serwerów nie przerywa działania aplikacji. Brak pojedynczego punktu awarii (SPOF - Single Point of Failure).
- **Efektywność kosztowa (Cost Effectiveness)**:
  Stosunek wydajności do ceny dla klastra złożonego ze zwykłych komputerów (commodity hardware) jest zazwyczaj znacznie korzystniejszy niż dla maszyn typu Mainframe.
- **Wydajność i lokalizacja geograficzna**:
  Zasoby mogą być rozproszone geograficznie (np. sieci CDN, takie jak Cloudflare). Serwery znajdujące się fizycznie najbliżej użytkownika obsługują jego zapytania, co minimalizuje opóźnienia sieciowe (latency).
- **Podział ról i elastyczność**:
  Różne węzły mogą realizować różne zadania (np. baza danych, serwer plików, serwer aplikacyjny) i działać na różnych systemach operacyjnych (heterogeniczność).

---

### 3. Wady i wyzwania systemów rozproszonych

- **Wysoka złożoność programistyczna**:
  Programowanie systemów rozproszonych jest znacznie trudniejsze. Deweloper musi obsłużyć problemy takie jak: utrata pakietów, opóźnienia sieciowe, brak odpowiedzi z innych węzłów, wyścigi o zasoby oraz transakcje rozproszone (np. protokół dwufazowego zatwierdzania - 2PC).
- **Problem spójności danych (Twierdzenie CAP)**:
  W przypadku wystąpienia awarii sieci i jej podziału na odizolowane segmenty (Partition), architekt musi wybrać:
    - *Spójność (C)*: Blokujemy zapis do czasu przywrócenia łączności, aby dane wszędzie były identyczne (kosztem utraty dostępności).
    - *Dostępność (A)*: Zezwalamy na zapis na dowolnym węźle, ale dane w różnych częściach sieci będą się różnić (brak spójności).
  Wiele systemów wybiera model **spójności ostatecznej (Eventual Consistency)**, gdzie dane stają się spójne po pewnym czasie.
- **Bezpieczeństwo**:
  Komunikacja sieciowa między węzłami zwiększa powierzchnię ataku. Konieczne jest wdrażanie zaawansowanego szyfrowania transmisji (np. mTLS) oraz uwierzytelniania każdego węzła.
- **Trudność w diagnostyce i monitorowaniu**:
  Tradycyjne logowanie nie sprawdza się, gdy zapytanie użytkownika przechodzi przez 20 mikrousług na różnych serwerach. Wymaga to wdrożenia skomplikowanych systemów rozproszonego śledzenia (Distributed Tracing, np. Zipkin, Jaeger) oraz centralizacji logów (np. stos ELK).
- **Synchronizacja i porządkowanie zdarzeń**:
  Z powodu braku globalnego zegara fizycznego określenie, która operacja zapisu w bazie danych wydarzyła się pierwsza, wymaga stosowania skomplikowanych algorytmów synchronizacji (np. algorytm Paxos, Raft lub zegary wektorowe).

## Podsumowanie
Systemy rozproszone to fundament nowoczesnego IT, na którym opierają się największe platformy na świecie (Netflix, Google, Facebook). Zapewniają one niezrównaną skalowalność i odporność na awarie, jednak ceną za te korzyści jest drastyczny wzrost złożoności kodu, konieczność radzenia sobie z problemem spójności danych oraz trudniejsze administrowanie infrastrukturą.
