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

## DIAGRAM PRZYPADKÓW UŻYCIA
```mermaid
flowchart TD
    n1["Użytkownik"] --> A["Uruchomienie biletomatu<br>"]
    A -- &lt;&lt;include&gt;&gt; --> B["Wyświetlenie podstawowych instrukcji"] & G["Wyświetlenie opcji języka"] & H["Wybór biletu i metody płatności"] & R["Anulowanie transakcji"]
    G --> I["Wybór języka"]
    I -- &lt;&lt;include&gt;&gt; --> J["Ustawienie domyślnego języka"]
    I --> K["Dostosowanie interfejsu"]
    L["Wyświetlenie listy popularnych języków"] -- &lt;&lt;extend&gt;&gt; --> G
    B --> M["Postępowanie według instrukcji"]
    N["Szczegółowa pomoc"] -- &lt;&lt;extend&gt;&gt; --> B
    H -- &lt;&lt;include&gt;&gt; --> O["Wyświetlenie podsumowania transakcji"] & T["Weryfikacja metody płatności"]
    O --> P["Potwierdzenie lub cofnięcie"]
    P --> Q["Kontynuacja lub anulowanie"]
    %% P -- &lt;&lt;include&gt;&gt; --> R["Anulowanie transakcji"]
    S["Ostrzeżenie o błędnym wyborze"] -- &lt;&lt;extend&gt;&gt; --> Q
    T --> U["Realizacja płatności"]
    U --> V["Potwierdzenie transakcji"]
    W["Obsługa błędów płatności"] -- &lt;&lt;extend&gt;&gt; --> U

    n1@{ shape: text}
```

