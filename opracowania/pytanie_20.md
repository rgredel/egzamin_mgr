# Pytanie 20: Omów model FAIR pozwalający na szacowanie ryzyka zagrożenia bezpieczeństwa systemu komputerowego.

## Kluczowe pojęcia
- **FAIR (Factor Analysis of Information Risk - Analiza Czynnikowa Ryzyka Informacyjnego)**: Międzynarodowy standard i jedyny powszechnie akceptowany model ilościowej analizy ryzyka operacyjnego i cyberbezpieczeństwa.
- **Ilościowa analiza ryzyka**: Szacowanie ryzyka w konkretnych wartościach liczbowych i finansowych (np. roczna oczekiwana strata w PLN), w przeciwieństwie do analizy jakościowej (np. ryzyko „wysokie”, „czerwone”).
- **Loss Event Frequency (Częstotliwość zdarzeń powodujących stratę)**: Prawdopodobieństwo lub liczba przypadków wystąpienia udanego ataku w określonym przedziale czasu (np. raz na rok).
- **Loss Magnitude (Wielkość straty)**: Całkowity wymiar finansowy szkód (kosztów) wywołanych przez pojedynczy incydent.

## Szczegółowe omówienie tematu

### 1. Czym jest model FAIR?
Tradycyjne metody oceny ryzyka IT (np. na podstawie ISO 27005 lub NIST SP 800-30) często opierają się na subiektywnych macierzach ryzyka (np. Prawdopodobieństwo 1-5 x Skutki 1-5 = Poziom Ryzyka). Prowadzi to do ocen typu „ryzyko średnio-wysokie”, które są trudne do zinterpretowania przez zarząd firmy podejmujący decyzje finansowe.

**Model FAIR** rozwiązuje ten problem poprzez zdefiniowanie ryzyka jako **prawdopodobieństwa wystąpienia i wielkości przyszłej straty finansowej**. FAIR rozkłada ryzyko na czynniki składowe, tworząc matematyczne drzewo zależności, i pozwala wyliczyć ryzyko w walucie (np. PLN, USD).

---

### 2. Struktura czynników ryzyka w modelu FAIR
Model FAIR dzieli ryzyko na dwie główne gałęzie: **Częstotliwość zdarzeń powodujących stratę (Loss Event Frequency)** oraz **Wielkość straty (Loss Magnitude)**.

```
                          [ RYZYKO (RISK) ]
                                  |
            +---------------------+---------------------+
            |                                           |
[ Loss Event Frequency (LEF) ]             [ Loss Magnitude (LM) ]
            |                                           |
     +------+------+                             +------+------+
     |             |                             |             |
  [ TEF ]    [ Podatność ]                    [ Straty ]    [ Straty ]
            (Vulnerability)                 [ Pierwotne ] [ Wtórne ]
```

#### A. Loss Event Frequency (LEF) – Częstotliwość strat
Określa, jak często w danym okresie dojdzie do pomyślnego ataku skutkującego stratą. Zależy od:
- **TEF (Threat Event Frequency - Częstotliwość zdarzeń zagrożeń)**: Jak często profilowany napastnik (Threat Agent) podejmie próbę ataku na nasz zasób. Zależy to od częstotliwości kontaktu (*Contact*) oraz siły działania (*Force*).
- **Vulnerability (Podatność)**: Prawdopodobieństwo, że próba ataku zakończy się sukcesem. Wynika bezpośrednio z porównania zdolności/siły napastnika (**Threat Capability**) z poziomem wdrożonych przez nas zabezpieczeń (**Control Strength**).

#### B. Loss Magnitude (LM) – Wielkość straty
Określa finansowe konsekwencje jednego incydentu. FAIR rozróżnia dwa rodzaje strat:
- **Primary Loss (Straty pierwotne)**: Bezpośrednie koszty poniesione przez samą organizację w celu usunięcia awarii (np. koszt pracy programistów naprawiających system, utracone przychody w czasie przestoju sklepu internetowego).
- **Secondary Loss (Straty wtórne)**: Koszty wynikające z reakcji otoczenia zewnętrznego na incydent (np. kary administracyjne od UODO za wyciek danych osobowych, odszkodowania dla klientów, koszty PR mające na celu ratowanie wizerunku, utrata klientów na rzecz konkurencji).

---

### 3. Zastosowanie statystyki (Metoda Monte Carlo)
W modelu FAIR rzadko podaje się dane wejściowe jako pojedyncze, sztywne wartości (np. "dokładnie 12 ataków rocznie"), ponieważ cyberbezpieczeństwo jest pełne niepewności. Zamiast tego analitycy wprowadzają zakresy danych: **wartość minimalną, maksymalną oraz najbardziej prawdopodobną** (tworząc rozkład prawdopodobieństwa PERT lub trójkątny).

Następnie silnik FAIR wykorzystuje **symulację Monte Carlo**, która wykonuje tysiące (np. 10 000) losowań scenariuszy w celu wygenerowania krzywej rozkładu prawdopodobieństwa rocznych strat. Wynik pozwala określić:
- Średnią (oczekiwaną) wartość strat rocznych (ALE - Annual Loss Expectancy).
- Najgorszy możliwy scenariusz (np. z prawdopodobieństwem 5%).

## Podsumowanie
Model FAIR to potężne narzędzie łączące techniczną inżynierię bezpieczeństwa z zarządzaniem biznesowym. Pozwala on na precyzyjne uzasadnienie budżetów bezpieczeństwa. Zamiast argumentować: „musimy kupić ten system, bo bez niego ryzyko jest wysokie”, oficer bezpieczeństwa (CISO) korzystający z FAIR może powiedzieć: „wydanie 50 000 PLN na to zabezpieczenie zmniejszy naszą roczną oczekiwaną stratę z tytułu wycieku danych z 400 000 PLN do 120 000 PLN, co daje oszczędność 280 000 PLN rocznie”.
