# Szablon procedury testowej i zapisu wyniku

Status: szablon do wypełnienia dla konkretnej próby. Procedura jest gotowa do wykonania po określeniu połączeń, warunków, limitów i kryteriów akceptacji. Zasady: [weryfikacja](README.md).

## Identyfikacja

| Pole | Wartość do uzupełnienia |
| --- | --- |
| ID i tytuł próby | TST-… |
| Rewizja procedury i status | Projekt / gotowa do wykonania / wykonana. |
| Wymagania | Powiązane SYS-… oraz kryteria szczegółowe. |
| Cel, metoda i etap | Co potwierdzamy; test/pomiar, analiza lub inspekcja; etap projektu. |
| Badany wariant | Silnik/stanowisko, ECU/HMI/aplikacja, wyposażenie i konfiguracja. |
| Rewizje | PCB/BOM, firmware, bootloadery, aplikacja, mapy i inne istotne dane. |
| Przygotował / wykonał / data | Autor procedury, wykonawca i data próby. |

## Stanowisko i przygotowanie

- Wymagane przyrządy i osprzęt, ich zakresy, dokładności i istotne ustawienia.
- Schemat połączeń z potwierdzonymi punktami, odniesieniami pomiarowymi i trybami pracy.
- Warunki zasilania, obciążenia, sygnały wejściowe i stan początkowy.
- Limity oraz warunki natychmiastowego przerwania; sposób zakończenia próby i przywrócenia stanu.

## Przebieg

| Krok | Czynność / wymuszenie | Oczekiwany wynik i tolerancja | Wynik rzeczywisty / dowód |
| --- | --- | --- | --- |
| 1 | Uzupełnić dla konkretnego stanowiska. | Mierzalne kryterium, jednostki i dopuszczalne granice. | Pomiar, plik lub obserwacja. |

Dodać przypadki graniczne i uszkodzenia wymagane przez cel próby oraz warunki ich wprowadzania. Nierozstrzygnięte parametry oznaczyć jawnie; do wykonania potrzebne są kompletne wartości kryteriów i limitów.

## Ocena i zapis

- Wynik: zaliczony / niezaliczony / niewykonany; wskazać osobno ocenę każdego powiązanego wymagania.
- Dowody: pliki pomiarowe, przebiegi, logi, zdjęcia/inspekcja lub obliczenia, z jednostkami i ustawieniami.
- Odchylenia, niezgodności, przyczyny przerwania i ograniczenia próby.
- Wniosek, wymagane zmiany oraz zakres ponownej weryfikacji i regresji.

Procedura lub szablon bez wykonania i dowodów nie stanowi potwierdzenia wymagania.
