# Pytanie 27: Modele programowania równoległego.

## Kluczowe pojęcia
- **Przetwarzanie równoległe (Parallel Processing)**: Równoczesne wykonywanie wielu obliczeń przez różne rdzenie procesora lub różne komputery w klastrze w celu skrócenia czasu wykonania zadania.
- **Pamięć współdzielona (Shared Memory)**: Architektura, w której wszystkie procesory/wątki mają dostęp do tej samej fizycznej przestrzeni adresowej pamięci operacyjnej.
- **Pamięć rozproszona (Distributed Memory)**: Architektura klastrowa, w której każdy węzeł ma własną fizyczną pamięć, a komunikacja zachodzi przez sieć.
- **MPI (Message Passing Interface)**: Standard przesyłania komunikatów w systemach z pamięcią rozproszoną.
- **OpenMP**: Standard programowania wielowątkowego dla systemów z pamięcią współdzieloną.

## Szczegółowe omówienie tematu

Model programowania równoległego to abstrakcja określająca, w jaki sposób procesory lub wątki współpracują, komunikują się oraz jak uzyskują dostęp do pamięci. Wybór modelu zależy od architektury sprzętowej komputera lub klastra.

---

### 1. Klasyfikacja modeli ze względu na zarządzanie pamięcią

#### A. Model z pamięcią współdzieloną (Shared Memory Model)
W tym modelu wszystkie wątki lub procesy działają na tej samej przestrzeni adresowej RAM.
- **Komunikacja**: Odbywa się bezpośrednio. Zmiana wartości zmiennej przez jeden wątek jest natychmiast widoczna dla innych wątków.
- **Zalety**: Prosta wymiana danych, nie ma potrzeby jawnego pakowania i wysyłania komunikatów przez sieć.
- **Wyzwania**: Ryzyko **wyścigów (race conditions)**, kiedy dwa wątki próbują jednocześnie zapisać dane w tym samym miejscu w pamięci. Wymaga stosowania mechanizmów synchronizacji (blokad, muteksów, semaforów, sekcji krytycznych).
- **Implementacje**:
  - **OpenMP**: Standard oparty na dyrektywach kompilatora dla języków C/C++ i Fortran, ułatwiający zrównoleglanie pętli (np. `#pragma omp parallel for`).
  - **Wątki systemowe / biblioteczne**: Np. Pthreads (POSIX), `std::thread` w C++, wątki w Javie.

#### B. Model z pamięcią rozproszoną (Distributed Memory / Message Passing Model)
Stosowany w klastrach komputerowych (np. superkomputerach). Każdy procesor (węzeł) ma swoją prywatną pamięć i nie może bezpośrednio odczytać ani zapisać pamięci innego węzła.
- **Komunikacja**: Musi być jawnie zaprogramowana za pomocą przesyłania komunikatów (Message Passing) przez sieć (Ethernet, InfiniBand).
- **Zalety**: Doskonała skalowalność (możliwość łączenia tysięcy maszyn). Brak problemu wyścigów w pamięci współdzielonej (stan jest odizolowany).
- **Wyzwania**: Narzut sieciowy na przesyłanie komunikatów, trudniejsza implementacja (programista musi ręcznie zarządzać wysyłaniem i odbieraniem danych).
- **Implementacje**:
  - **MPI (Message Passing Interface)**: Standard definiujący funkcje do przesyłania danych punkt-do-punktu (`MPI_Send`, `MPI_Recv`) oraz operacje grupowe (np. `MPI_Bcast` – rozgłaszanie danych, `MPI_Reduce` – agregacja wyników).

#### C. Model hybrydowy (Hybrid Model)
Łączy oba powyższe podejścia. Stosowany w klastrach, w których każdy węzeł ma procesor wielordzeniowy. Wewnątrz jednego węzła stosuje się pamięć współdzieloną (np. OpenMP), a komunikacja między węzłami odbywa się poprzez sieć z użyciem MPI (tzw. podejście **MPI + OpenMP**).

---

### 2. Inne modele programowania równoległego

#### A. Model równoległości danych (Data-Parallel Model / SIMD)
Te same operacje matematyczne wykonywane są jednocześnie na różnych elementach dużego zbioru danych. Jest to fundament obliczeń na kartach graficznych (GPGPU).
- **Mechanizm**: Karta graficzna uruchamia tysiące bardzo prostych wątków, z których każdy wykonuje tę samą instrukcję dla innej komórki macierzy.
- **Narzędzia**: **CUDA** (architektura własnościowa firmy NVIDIA) oraz **OpenCL** (standard otwarty).

#### B. Model aktorów (Actor Model)
Model, w którym podstawową jednostką obliczeniową jest samodzielny obiekt zwany „aktorem”. Aktorzy nie współdzielą stanu. Każdy aktor ma skrzynkę pocztową i przetwarza przychodzące wiadomości asynchronicznie. W odpowiedzi na wiadomość aktor może zmodyfikować swój stan, utworzyć nowych aktorów lub wysłać kolejne wiadomości.
- **Zalety**: Całkowity brak blokad (lock-free) i wyścigów w kodzie aplikacji.
- **Narzędzia**: Język Erlang (używany np. w systemach telekomunikacyjnych), biblioteka Akka dla języków Java/Scala.

#### C. Model MapReduce
Wprowadzony przez Google model do przetwarzania wielkich zbiorów danych (Big Data) w klastrach rozproszonych.
- **Faza Map**: Podział dużego problemu na małe części i równoległe przetworzenie ich przez węzły robotnicze do postaci par klucz-wartość.
- **Faza Reduce**: Agregacja pośrednich wyników przez węzły redukujące na podstawie klucza.
- **Narzędzia**: Apache Hadoop, Apache Spark.

## Wizualizacja

Oto schemat blokowy / diagram ułatwiający zrozumienie zagadnienia:

```mermaid
graph TD
    subgraph Pamięć Współdzielona (np. OpenMP)
        P1["Procesor 1"] & P2["Procesor 2"] & P3["Procesor 3"] --> SharedMem[("Wspólna Pamięć RAM")]
    end
    subgraph Przesyłanie Wiadomości (np. MPI)
        NodeA["Węzeł A: Procesor 1 + RAM A"] <-->|Komunikacja sieciowa (MPI Send/Recv)| NodeB["Węzeł B: Procesor 2 + RAM B"]
    end
```

## Podsumowanie
Współczesne programowanie równoległe opiera się na dopasowaniu modelu programowania do architektury sprzętowej. Do obliczeń na komputerach wielordzeniowych stosuje się pamięć współdzieloną (OpenMP/wątki), w klastrach rozproszonych standardem jest przekazywanie komunikatów (MPI), w obliczeniach naukowych i sztucznej inteligencji dominuje równoległość danych na kartach GPU (CUDA), natomiast w systemach wysoko-dostępnych i mikrousługach popularność zyskuje model aktorów.