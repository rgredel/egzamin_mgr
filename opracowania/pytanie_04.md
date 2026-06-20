# Pytanie 4: Model dojrzałości usług sieciowych (usług RESTful) wg. Richardsona.

## Kluczowe pojęcia
- **REST (Representational State Transfer)**: Styl architektoniczny systemów rozproszonych określający zbiór reguł komunikacji (bezstanowość, jednolity interfejs, architektura klient-serwer itp.).
- **Richardson Maturity Model (RMM)**: Model stworzony przez Leonarda Richardsona, dzielący stopień wdrożenia zasad REST w danej usłudze na cztery poziomy (0 do 3).
- **Zasób (Resource)**: Kluczowa abstrakcja w REST. Każdy element informacji (np. użytkownik, faktura, plik) reprezentowany przez unikalny identyfikator URI.
- **HATEOAS (Hypermedia As The Engine Of Application State)**: Warunek pełnej REST-owości, według którego interakcja z API odbywa się dynamicznie za pośrednictwem hiperłączy dostarczanych przez serwer w odpowiedziach.

## Szczegółowe omówienie tematu

Leonard Richardson zaproponował model klasyfikacji API sieciowych, aby ułatwić zrozumienie i prawidłowe wdrażanie zasad stylu architektonicznego REST. Model ten składa się z czterech kroków:

```
Poziom 3: Kontrola hipermediów (HATEOAS)
      ^
Poziom 2: Czasowniki HTTP (HTTP Verbs) i kody statusu
      ^
Poziom 1: Podział na zasoby (Resources / URI)
      ^
Poziom 0: Bagno POX (HTTP jako tunel komunikacyjny / RPC)
```

### Poziom 0: Swamp of POX (Bagno Plain Old XML)
Na tym poziomie HTTP jest traktowane wyłącznie jako protokół transportowy do przesyłania danych. Usługa nie korzysta z żadnych mechanizmów REST.
- **URI**: Istnieje tylko jeden punkt końcowy (np. `/api/service`).
- **Metody HTTP**: Zazwyczaj wszystkie zapytania wysyłane są metodą `POST`.
- **Logika**: To, co ma się wydarzyć, jest definiowane w ciele zapytania (np. SOAP lub XML-RPC).
- *Przykład*: Wywołanie operacji pobrania danych i zapisu danych odbywa się pod tym samym adresem `/service` przy użyciu metody `POST` z różną zawartością XML/JSON.

### Poziom 1: Resources (Zasoby)
Poziom pierwszy wprowadza podział monolitycznego punktu końcowego na pojedyncze zasoby, co jest pierwszym krokiem ku właściwej strukturze REST.
- **URI**: Każdy logiczny obiekt w systemie ma swój unikalny identyfikator URI (np. `/uzytkownicy`, `/uzytkownicy/15`, `/ksiazki/99`).
- **Metody HTTP**: Nadal najczęściej wykorzystuje się tylko jedną metodę (np. `POST` do wszystkich operacji).
- *Przykład*: Aby pobrać użytkownika o ID 15, wysyłamy `POST /uzytkownicy/15`, a żeby go usunąć, wysyłamy `POST /uzytkownicy/15/usun`.

### Poziom 2: HTTP Verbs (Czasowniki HTTP)
Na tym poziomie API w pełni wykorzystuje semantykę protokołu HTTP, czyli standardowe metody (czasowniki) oraz kody statusów odpowiedzi.
- **Metody HTTP**:
  - `GET`: Bezpieczne pobieranie zasobów (brak efektów ubocznych).
  - `POST`: Tworzenie nowych zasobów.
  - `PUT`: Nadpisywanie całych zasobów (operacja idempotentna).
  - `PATCH`: Częściowa aktualizacja zasobów.
  - `DELETE`: Usuwanie zasobów.
- **Kody odpowiedzi**: Zamiast zwracać zawsze kod `200 OK` z opisem błędu wewnątrz JSON-a, serwer zwraca natywne statusy HTTP:
  - `201 Created` dla pomyślnego utworzenia zasobu.
  - `400 Bad Request` w przypadku błędów walidacji.
  - `404 Not Found`, gdy dany zasób nie istnieje.
  - `401 Unauthorized` / `403 Forbidden` do kontroli uprawnień.

### Poziom 3: Hypermedia Controls (Kontrola Hipermediów - HATEOAS)
To najwyższy poziom dojrzałości, który czyni API prawdziwie "RESTful". Zapewnia on pełne uniezależnienie klienta od sztywnej struktury adresów URL serwera.
- **Mechanizm**: Serwer w odpowiedzi na zapytanie o zasób przesyła nie tylko dane tego zasobu, lecz również tablicę linków (hiperłączy) informujących o dopuszczalnych w tym momencie akcjach.
- **Zaleta**: Klient nie musi z góry znać schematu URI dla kolejnych kroków procesu. Jeśli użytkownik ma uprawnienia do edycji profilu, serwer zwróci w odpowiedzi link z relacją `rel="edit"`. Jeśli konto jest zablokowane, link ten nie zostanie wysłany.
- *Przykład*:
  ```json
  {
    "id": 12,
    "nazwisko": "Kowalski",
    "saldo": 150.00,
    "_links": {
      "self": { "href": "/klienci/12" },
      "wplata": { "href": "/klienci/12/wplaty" },
      "wyplata": { "href": "/klienci/12/wyplaty" }
    }
  }
  ```

## Podsumowanie
Większość komercyjnych usług sieciowych określanych jako REST API w rzeczywistości plasuje się na **Poziomie 2** modelu dojrzałości Richardsona. Wdrożenie **Poziomu 3 (HATEOAS)** jest rzadsze, ponieważ wymaga większego nakładu pracy przy tworzeniu i konsumowaniu API, jednak reprezentuje ono pełną, teoretyczną definicję stylu REST, zapewniając elastyczność i ewolucyjność API.
