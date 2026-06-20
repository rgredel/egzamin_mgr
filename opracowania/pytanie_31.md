# Pytanie 31: Tajność doskonała. Twierdzenie Shannona.

## Kluczowe pojęcia
- **Tajność doskonała (Perfect Secrecy)**: Właściwość kryptosystemu gwarantująca, że posiadanie szyfrogramu nie daje żadnej dodatkowej wiedzy na temat tekstu jawnego.
- **Claude Shannon**: Amerykański matematyk i inżynier, uznawany za ojca teorii informacji, który w 1949 r. opisał matematyczne podstawy kryptografii.
- **Klucz jednorazowy (One-Time Pad - OTP)**: Klasyczny szyfr binarny, który jako jedyny udowodniony matematycznie zapewnia tajność doskonałą.
- **Prawdopodobieństwo warunkowe**: Prawdopodobieństwo zajścia zdarzenia pod warunkiem zajścia innego zdarzenia.

## Szczegółowe omówienie tematu

### 1. Definicja tajności doskonałej
Szyfr zapewnia tajność doskonałą (zwaną też bezpieczeństwem informacyjnym), jeśli przechwycenie szyfrogramu ($C$) przez przeciwnika w żaden sposób nie przybliża go do poznania tekstu jawnego ($M$). 

Z perspektywy teorii prawdopodobieństwa oznacza to, że a posteriori (po zapoznaniu się z szyfrogramem) prawdopodobieństwo, że tekst jawny ma określoną wartość, jest identyczne jak prawdopodobieństwo a priori (przed zobaczeniem szyfrogramu):
$$P(M = m \mid C = c) = P(M = m)$$
dla każdego komunikatu $m$ i każdego szyfrogramu $c$.

W praktyce: niezależnie od tego, jak dużą mocą obliczeniową dysponuje kryptoanalityk, nie jest on w stanie odszyfrować wiadomości, ponieważ przy próbie ataku brute-force (przetestowania wszystkich kluczy) otrzyma **wszystkie możliwe sensowne teksty jawne** o danej długości, nie mając żadnej metody na wskazanie, który z nich jest prawdziwy.

---

### 2. Twierdzenie Shannona
Claude Shannon sformułował fundamentalne twierdzenie, które precyzuje warunki konieczne i dostateczne do zaistnienia tajności doskonałej w systemach o skończonej liczbie komunikatów.

**Treść twierdzenia**:
Załóżmy, że mamy kryptosystem, w którym przestrzeń tekstów jawnych $\mathcal{M}$, przestrzeń kluczy $\mathcal{K}$ oraz przestrzeń szyfrogramów $\mathcal{C}$ mają taki sam rozmiar ($|\mathcal{M}| = |\mathcal{K}| = |\mathcal{C}|$). Kryptosystem ten zapewnia tajność doskonałą wtedy i tylko wtedy, gdy spełnione są dwa warunki:
1. Każdy klucz $k \in \mathcal{K}$ jest wybierany z jednakowym prawdopodobieństwem (rozkład jednostajny):
   $$P(K = k) = \frac{1}{|\mathcal{K}|}$$
2. Dla każdej wiadomości $m \in \mathcal{M}$ i każdego szyfrogramu $c \in \mathcal{C}$ istnieje dokładnie jeden klucz $k \in \mathcal{K}$ taki, że:
   $$E_k(m) = c$$

#### Kluczowy wniosek (Ograniczenie Shannona):
Z twierdzenia Shannona wynika bezpośrednio, że aby kryptosystem był doskonale bezpieczny, rozmiar przestrzeni kluczy musi być co najmniej tak duży jak rozmiar przestrzeni wiadomości:
$$|\mathcal{K}| \ge |\mathcal{M}|$$
Oznacza to, że **klucz szyfrujący musi być co najmniej tak długi jak szyfrowana wiadomość**. Jest to powód, dla którego tajność doskonała jest skrajnie trudna do zastosowania w codziennej komunikacji.

---

### 3. Szyfr z kluczem jednorazowym (One-Time Pad) jako realizacja tajności doskonałej
Szyfr z kluczem jednorazowym (OTP, szyfr Vernama) działa na bitach reprezentujących tekst jawny ($M$) oraz klucz ($K$):
- **Szyfrowanie**:
  $$C = M \oplus K$$ (operacja XOR bit po bicie).
- **Odszyfrowanie**:
  $$M = C \oplus K$$

#### Dlaczego OTP jest doskonale bezpieczny w myśl twierdzenia Shannona?
1. Klucz $K$ musi składać się z bitów wygenerowanych w sposób **prawdziwie losowy** (rozkład jednostajny).
2. Długość klucza $K$ jest **równa** długości wiadomości $M$.
3. Klucz jest używany **tylko jeden raz** (stąd nazwa *One-Time*). Jeśli klucz zostanie użyty dwukrotnie, to z dwóch szyfrogramów:
   $$C_1 = M_1 \oplus K \quad \text{i} \quad C_2 = M_2 \oplus K$$
   kryptoanalityk może wyliczyć:
   $$C_1 \oplus C_2 = M_1 \oplus M_2$$
   co całkowicie eliminuje losowy klucz i pozwala na łatwe odczytanie obu wiadomości metodami statystycznymi.

## Podsumowanie
Tajność doskonała to najwyższy możliwy poziom bezpieczeństwa kryptograficznego. Chroni ona dane niezależnie od mocy obliczeniowej przeciwnika (jest odporna nawet na komputery kwantowe). Zgodnie z twierdzeniem Shannona wymaga to jednak klucza o długości równej długości wiadomości, który musi być przesłany bezpiecznym kanałem i użyty tylko raz. Z tego powodu współczesna kryptografia użytkowa (np. HTTPS, AES, RSA) opiera się na **bezpieczeństwie obliczeniowym** – szyfry te można teoretycznie złamać, ale wymagałoby to miliardów lat obliczeń na współczesnych komputerach.
