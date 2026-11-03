# ADR-011 — strojenie map podczas pracy silnika

Data: 2026-11-03. Status: **zatwierdzony zakres funkcji; realizacja otwarta**.

## Problem i opcje

Aplikacja Windows ma umożliwiać strojenie map. Należało rozstrzygnąć, czy zmienione wartości mogą być stosowane podczas pracy silnika, czy dopiero po jego zatrzymaniu. Przełączanie maksymalnie trzech gotowych zestawów z HMI jest już wymagane przez SYS-028.

## Decyzja i podstawa

Windows umożliwia zmianę wybranych wartości map podczas pracy silnika. Dopuszczalny zakres i zabezpieczenia określimy w projekcie. ECU pozostaje wykonawcą i właścicielem aktywnych danych.

Źródło: odpowiedź właściciela **A na pytanie 101** w rozmowie projektowej: „Tak — wybrane wartości map można zmieniać podczas pracy silnika; dopuszczalny zakres i zabezpieczenia określimy w projekcie”.

Powiązanie: SYS-007, SYS-028, SYS-047 oraz nowe SYS-094.

## Skutki i sprawy otwarte

- Architektura ECU, protokołu i Windows ma uwzględnić przyjmowanie, sprawdzanie i stosowanie zmian bez zakłócenia sterowania silnikiem.
- W pakiecie F02 określimy dozwolone pola, zakresy zmian, spójny moment ich zastosowania, potwierdzenie rzeczywistego stanu, zachowanie po utracie sesji/zasilania i zmianie aktywnego zestawu.
- Sposób i warunki trwałego zapisu, przywracanie poprzednich danych i wybór danych po restarcie pozostają otwarte. Zgoda na strojenie na żywo nie zatwierdza zapisu pamięci nieulotnej przy pracującym silniku.
- Rozmiar i organizacja danych, potrzebna pamięć, przepustowość oraz granice czasowe wymagają obliczeń przed wyborem MCU i protokołu.

## Weryfikacja

Plan obejmie zmianę dozwolonej wartości podczas pracy, potwierdzenie danych aktywnych, odrzucenie danych niedopuszczonych i wpływ na czas sterowania. Oddzielnie sprawdzimy utratę sesji, przełączenie zestawu i zanik zasilania według przyjętych później reguł. Najpierw stanowisko/symulator, następnie właściwa konfiguracja silnika; procedury i kryteria wykonawcze powstaną po określeniu tych reguł. Brak implementacji i wyników prób.
