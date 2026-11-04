# F01 — przegląd pomiarów silnika

Stan na: 2026-11-04, po odpowiedzi B na pytanie 107. **Zakres pomiarów F01 zamknięty.** Uzgodnienie funkcji jest odrębne od późniejszego doboru czujników i potwierdzenia działania produktu.

## Przyjęte funkcje

| Funkcja | Podstawa | Status zakresu / dalsza praca |
| --- | --- | --- |
| Wał VR lub cyfrowy Hall | SYS-069 | Przyjęte; czujniki i dekodery w etapach 3–4. |
| Dodatkowa faza 4T, cyfrowy Hall | SYS-070 | Przyjęte, opcjonalne zależnie od konfiguracji. |
| TPS oraz wariant gaźnika bez TPS | SYS-014/038 | Przyjęte; parametry i wykorzystanie według konfiguracji. |
| Temperatura dolotu IAT | SYS-031 | Przyjęte; temperatura ECU jest osobnym pomiarem. |
| Temperatura płynu chłodzącego | SYS-044 | Wymagane; platformę ograniczono do chłodzenia cieczą (SYS-098). |
| Ciśnienie atmosferyczne i temperatura ECU na PCB | SYS-030 | Przyjęte; ważne sensory wybierzemy wspólnie później. |
| MAP | SYS-096 | Zakres funkcji zamknięty po pytaniu 105. |
| Ciśnienie gazów w skrzyni korbowej 2T, CCPS | SYS-097 | Zakres funkcji zamknięty po pytaniu 106. |
| Wartość ciśnienia paliwa i binarne ciśnienie oleju | SYS-029 | Przyjęte; interfejsy według osprzętu. |
| Napięcie akumulatora | SYS-084/092 | Przyjęty nadzór i profile; wartości parametrów później. |

Pozostałe uzgodnione sygnały motocykla — m.in. koło, hamulce, sprzęgło, biegi, rezerwa i wykrywanie przewrócenia — zachowują swoje wymagania. Ich pozostałe reguły są przypisane do odpowiednich pakietów, bez rozpoczynania ich teraz. Zintegrowane tory lambda i EGT pozostają poza przyjętym zakresem.

## Rozstrzygnięcie zakresu chłodzenia

Właściciel odpowiedzią B na pytanie 107 wybrał wyłącznie silniki chłodzone cieczą i pomiar temperatury płynu (SYS-044/098, [ADR-012](../decisions/adr-012-zakres-chlodzenia-ciecza.md)).

Potwierdzony przykład: **Honda XR400R MY2000**, jednocylindrowy 4T chłodzony powietrzem. [Dane producenta](https://global.honda/jp/news/2000/c000117d.html), tabela „2000 PRODUCTION RACE MACHINES — MAIN SPECIFICATIONS 2”, kolumna XR400R. Źródło potwierdza sposób chłodzenia; nie potwierdza fabrycznego czujnika temperatury głowicy.

Przykład Hondy pozostaje podstawą rozważanego wariantu, wyłączonego z zakresu decyzją właściciela. Dla przyjętych silników chłodzonych cieczą pozostają do późniejszego określenia czujniki, charakterystyki, zakres, dokładność i tor pomiarowy. Dobór ważnych elementów będzie wspólny.

Przegląd funkcji pomiarowych zamknięto po zapisaniu MAP, CCPS i sposobu chłodzenia. [Przegląd sterowania i wynik zamknięcia F01](f01-sterowanie-silnikiem.md) zbiera pozostały zakres oraz dane przekazane dalej. Zamknięcie zakresu nie jest potwierdzeniem parametrów ani wyników produktu.
