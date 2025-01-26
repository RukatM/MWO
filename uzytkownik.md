1. Jako użytkownik, chcę szybko wybrać rodzaj biletu, aby zminimalizować czas
spędzony przy biletomacie.
2. Jako użytkownik, chcę mieć możliwość wyboru języka, aby móc korzystać z
biletomatu bez względu na znajomość języka lokalnego.
3. Jako użytkownik, chcę sprawdzić poprawność transakcji przed jej finalizacją,
aby uniknąć pomyłek.
4. Jako użytkownik, chcę otrzymać potwierdzenie zakupu (np. wydruk biletu lub
elektroniczny bilet), aby móc korzystać z transportu zgodnie z przepisami.
5. Jako użytkownik, chcę płacić za bilet kartą, gotówką lub telefonem, aby mieć
większą elastyczność w wyborze metody płatności.
6. Jako użytkownik, chcę otrzymać wyraźne instrukcje na ekranie, aby wiedzieć,
jak dokonać zakupu krok po kroku.
7. Jako użytkownik, chcę widzieć czas pozostały na decyzję (np. wyświetlany
licznik czasu), aby móc szybko podjąć działanie.

## DIAGRAMY PRZYPADKÓW UŻYCIA
### Otrzymanie instrukcji na ekranie

```mermaid
flowchart TD
    B["<br>Wyświetlenie instrukcji<br>"] --> C["Postępowanie według instrukcji"]
    B -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> n3["Anulowanie transakcji<br>"] & n4["Podstawowe instrukcje<br>"]
    n1["Użytkownik"] --> A["Rozpoczęcie interakcji<br>"]
    A --> B
    A -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> n3
    C --> n2["Wyświetlenie pomocy<br>"]
    C -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> n3
    n2 -. &lt;&lt;include&gt;&gt; .-> n3
    n5["Szczegółowa pomoc<br>"] -. "<span style=padding-left:>&lt;&lt;extend&gt;&gt;</span>" .-> n2

    C@{ shape: rect}
    n1@{ shape: text}
```

### Sprawdzenie poprawności transakcji

``` mermaid
flowchart TD
    n1["Użytkownik"] --> A["Wybór biletu i płatności"]
    B["Wyświetlenie podsumowania<br>"] --> C["Potwierdzenie lub cofnięcie"]
    B -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> E["Anulowanie transakcji"] & n2["Podsumowanie transakcji<br>"]
    C --> D["Kontynuacja lub anulowanie"]
    C -. &lt;&lt;include&gt;&gt; .-> E
    A --> B
    A -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> E
    D -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> E
    F["Ostrzeżenie o błędzie"] -. "<span style=padding-left:>&lt;&lt;extend&gt;&gt;</span>" .-> D

    n1@{ shape: text}
 ```
    
### Wybór języka

``` mermaid
flowchart TD
    n1["Użytkownik"] --> A["Rozpoczęcie interakcji"]
    A --> B["Wyświetlenie opcji języka"]
    A -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> n2["Domyślny język<br>"]
    B --> C["Wybór języka"]
    B -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> G["Anulowanie transakcji"]
    C --> E["Dostosowanie interfejsu <br>"]
    C -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> G
    A -. &lt;&lt;include&gt;&gt; .-> G
    F["Lista<br>popularnych języków<br>"] -. "<span style=padding-left:>&lt;&lt;extend&gt;&gt;</span>" .-> B
    E -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> G

    n1@{ shape: text}
```

### Płatność za bilet

```mermaid
flowchart TD
    A["Wybór metody płatności"] --> B["Weryfikacja metody płatności"]
    A -. &lt;&lt;include&gt;&gt; .-> E["Anulowanie transakcji"]
    B --> C["Realizacja płatności"]
    B -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> E
    B -. &lt;&lt;include&gt;&gt; .-> n2["Weryfikacja płatności"]
    C --> D["Potwierdzenie transakcji"]
    C -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> E
    F["Obsługa błędów płatności"] -. &lt;&lt;Extend&gt;&gt; .-> C
    n1["Użytkownik"] --> A
    D -. "<span style=padding-left:>&lt;&lt;include&gt;&gt;</span>" .-> E

    n1@{ shape: text}
```

## DIAGRAMY SEKWENCJI

### DIAGRAM SEKWENCJI DLA PRZYPADKU UŻYCIA SPRAWDZENIE POPRAWNOŚCI TRANSAKCJI
### SCENARIUSZ GŁÓWNY
- **AKTOR**: Użytkownik
- **OBIEKTY**: Interfejs biletomatu, Serwer, BazaDanych
- **KOLEJNOŚĆ KOMUNIKATÓW**:
  1. Użytkownik wybiera bilet i sposób płatności.
  2. Interfejs biletomatu wyświetla podsumowanie transakcji.
  3. Użytkownik potwierdza transakcję.
  4. Interfejs biletomatu przesyła dane transakcji do serwera.
  5. Serwer sprawdza poprawność transakcji w bazie danych.
  6. Serwer potwierdza poprawność transakcji.
  7. Interfejs biletomatu wyświetla komunikat o zakończeniu transakcji.

---

### SCENARIUSZ ALTERNATYWNY 1: (Cofnięcie transakcji)
- **KOLEJNOŚĆ KOMUNIKATÓW**:
  1. Użytkownik cofa transakcję.
  2. Interfejs biletomatu anuluje obecne dane transakcji.
  3. Interfejs biletomatu wyświetla ekran wyboru biletu i sposobu płatności.

---

### SCENARIUSZ ALTERNATYWNY 2: (Rezygnacja)
- **KOLEJNOŚĆ KOMUNIKATÓW**:
  1. Użytkownik anuluje transakcję.
  2. Interfejs biletomatu przekazuje żądanie anulowania do serwera.
  3. Serwer potwierdza anulowanie interakcji.
  4. Interfejs biletomatu wyświetla informację o anulowaniu.

---

### SCENARIUSZ ALTERNATYWNY 3: (Błąd)
1. Serwer wykrywa błąd poprawności transakcji
2. Serwer przesyła komunikat o błędzie do interfejsu biletomatu.
3. Interfejs biletomatu wyświetla użytkownikowi ostrzeżenie o błędzie.

### WIZUALIZACJA DIAGRAMU SEKWENCJI
```mermaid
sequenceDiagram
    actor Użytkownik
    participant InterfejsBiletomatu
    participant Serwer
    participant BazaDanych

    Użytkownik ->> InterfejsBiletomatu: Wybór biletu i sposobu płatności
    InterfejsBiletomatu ->> Użytkownik: Wyświetlenie podsumowania transakcji
    
    alt Potwierdzenie transakcji
        Użytkownik ->> InterfejsBiletomatu: Potwierdzenie transakcji
        InterfejsBiletomatu ->> Serwer: Przesłanie danych transakcji
        Serwer ->> BazaDanych: Sprawdzenie poprawności transakcji
        alt Błąd poprawności transakcji
            BazaDanych -->> Serwer: Wykryto błąd
            Serwer ->> InterfejsBiletomatu: Komunikat o błędzie
            InterfejsBiletomatu ->> Użytkownik: Wyświetlenie ostrzeżenia o błędzie
        else Transakcja poprawna
            BazaDanych -->> Serwer: Potwierdzenie poprawności
            Serwer -->> InterfejsBiletomatu: Potwierdzenie poprawności
            InterfejsBiletomatu ->> Użytkownik: Wyświetlenie komunikatu o zakończeniu transakcji
        end
    else Cofnięcie transakcji
        Użytkownik ->> InterfejsBiletomatu: Cofnięcie transakcji
        InterfejsBiletomatu ->> InterfejsBiletomatu: Anulowanie obecnych danych transakcji
        InterfejsBiletomatu ->> Użytkownik: Wyświetlenie ekranu wyboru biletu i sposobu płatności
    end

    alt Rezygnacja
        Użytkownik ->> InterfejsBiletomatu: Anulowanie transakcji
        InterfejsBiletomatu ->> Serwer: Przekazanie żądania anulowania
        Serwer -->> InterfejsBiletomatu: Potwierdzenie anulowania
        InterfejsBiletomatu ->> Użytkownik: Wyświetlenie informacji o anulowaniu
    end

```

