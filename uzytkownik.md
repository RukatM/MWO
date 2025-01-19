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
### Sprawdzenie poprawności transakcji

``` mermaid
flowchart TD
    n1["Użytkownik"] --> A["Wybór biletu i metody płatności"]
    A -- &lt;&lt;include&gt;&gt; --> B["Wyświetlenie podsumowania transakcji"]
    B --> C["Potwierdzenie lub cofnięcie"]
    C --> D["Kontynuacja lub anulowanie"]
    C -- &lt;&lt;include&gt;&gt; --> E["Anulowanie transakcji"]
    D -- &lt;&lt;extend&gt;&gt; --> F["Ostrzeżenie o błędnym wyborze"]
    
    n1@{ shape: text}
 ```
    
### Wybór języka

``` mermaid
flowchart TD
    n1["Użytkownik"] --> A["Uruchomienie biletomatu"]
    A --> B["Wyświetlenie opcji języka"]
    B --> C["Wybór języka"]
    C -- &lt;&lt;include&gt;&gt; --> D["Ustawienie domyślnego języka"]
    C --> E["Dostosowanie interfejsu"]
    B -- &lt;&lt;extend&gt;&gt; --> F["Wyświetlenie listy popularnych języków"]
    A -- &lt;&lt;include&gt;&gt; --> G["Anulowanie transakcji"]

    n1@{ shape: text}
```

### Płatność za bilet

```mermaid
flowchart TD
    A["Wybór metody płatności"] -- &lt;&lt;include&gt;&gt; --> B["Weryfikacja metody płatności"] & E["Anulowanie transakcji"]
    B --> C["Realizacja płatności"]
    C --> D["Potwierdzenie transakcji"]
    F["Obsługa błędów płatności"] -- &lt;&lt;Extend&gt;&gt; --> C
    n1["Użytkownik"] --> A

    n1@{ shape: text}
```
