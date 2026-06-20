# Pytanie 2: Koncepcja rozwoju oprogramowania sterowanego testami (TDD).

## Kluczowe pojęcia
- **TDD (Test-Driven Development - Rozwój sterowany testami)**: Metodyka tworzenia oprogramowania polegająca na pisaniu testów przed napisaniem właściwego kodu implementacji.
- **Cykl Red-Green-Refactor**: Trzyetapowy, fundamentalny cykl pracy w TDD: napisz test, który nie przechodzi (Red), napisz minimalny kod, aby test przeszedł (Green), popraw jakość kodu bez zmiany jego zachowania (Refactor).
- **Test jednostkowy (Unit Test)**: Test sprawdzający poprawność działania małego, odizolowanego fragmentu kodu (np. pojedynczej metody) z mockowaniem zewnętrznych zależności.
- **Regresja**: Sytuacja, w której zmiana w kodzie powoduje błąd w innej, dotychczas poprawnie działającej części systemu.

## Szczegółowe omówienie tematu

### 1. Przebieg cyklu Red-Green-Refactor
Praca w TDD odbywa się w mikro-krokach:
1. **RED (Czerwony)**: Programista projektuje interfejs nowej metody/funkcji i pisze dla niej test jednostkowy. Test zostaje uruchomiony i musi zakończyć się niepowodzeniem (ponieważ implementacja jeszcze nie istnieje lub jest pusta). Krok ten gwarantuje, że test jest poprawny i nie przechodzi bez powodu.
2. **GREEN (Zielony)**: Pisana jest minimalna konieczna implementacja kodu produkcyjnego tak, aby uruchomiony test przeszedł na zielono. Dopuszczalne są tu uproszczenia (np. zwracanie zahardkodowanej wartości), o ile test kończy się sukcesem.
3. **REFACTOR (Refaktoryzacja)**: Kod produkcyjny oraz kod testu są czyszczone. Usuwa się powtórzenia (zasada DRY), poprawia czytelność zmiennych, dzieli zbyt duże metody, bez zmiany funkcjonalności zewnętrznej. Każda zmiana jest natychmiast weryfikowana ponownym uruchomieniem testów.

### 2. Korzyści wynikające z TDD
- **Wymuszenie modularności**: Aby klasę dało się łatwo przetestować w izolacji, musi być ona luźno powiązana z innymi (loose coupling). TDD naturalnie promuje wstrzykiwanie zależności i stosowanie interfejsów.
- **Mniejsza liczba defektów**: Stałe testowanie sprawia, że błędy są wykrywane niemal natychmiast po ich wprowadzeniu.
- **Dokumentacja techniczna**: Testy są najbardziej precyzyjną formą dokumentacji – pokazują konkretne przypadki użycia, wejścia i oczekiwane wyjścia.
- **Odwaga w zmianach**: Posiadanie bogatego zestawu testów daje programistom pewność, że refaktoryzacja nie popsuje istniejących mechanizmów.

### 3. Bariery i ograniczenia TDD
- **Czas i koszty początkowe**: Czas programisty potrzebny na dostarczenie pierwszej wersji kodu jest większy niż w przypadku pominięcia testów (choć w długiej perspektywie TDD skraca czas fazy stabilizacji i debugowania).
- **Próg wejścia**: Wymaga dyscypliny i doświadczenia w projektowaniu testowalnego kodu. Złe testy (np. zbyt mocno powiązane z wewnętrzną implementacją klasy zamiast z jej kontraktem) utrudniają refaktoryzację.

## Podsumowanie
TDD to metodyka projektowa, w której testy pełnią rolę wymagań projektowych i specyfikacji. Zapewnia ona tworzenie oprogramowania o wysokiej jakości technicznej, ułatwiając ciągłą integrację i elastyczność w modyfikacji kodu.
