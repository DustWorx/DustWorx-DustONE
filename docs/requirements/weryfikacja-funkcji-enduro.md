# Sprawdzanie funkcji w motocyklach enduro

Data: 2026-11-01. Zasada pracy przyjęta przez właściciela; poniższa analiza IAC nie jest decyzją o dodaniu funkcji do ECU.

## Podstawa pytania

Przed propozycją nowej funkcji silnika lub osprzętu przygotowujemy:

- konkretny model enduro, rocznik i wersję, do których odnosi się przykład;
- źródło producenta: instrukcję, schemat lub katalog, z numerem strony/pozycji;
- potwierdzony sposób realizacji i jawne braki danych;
- związek z zakresem DustONE, zachowaniem OEM oraz skutki dla I/O, komponentów, gabarytów i testów.

Rozróżniamy wyposażenie konkretnego modelu, docelową funkcję wskazaną przez właściciela oraz propozycję rozszerzenia. Materiały producentów uniwersalnych ECU i półprzewodników pomagają dobrać realizację; występowanie funkcji w danym enduro potwierdzamy w dokumentacji tego motocykla. Przykłady z innych kategorii pojazdów wymagają osobnego uzasadnienia. Znajomość wyposażenia nie stanowi jeszcze potwierdzenia zgodności elektrycznej.

## Przykład — regulacja biegu jałowego IAC

| Enduro / rocznik | Potwierdzone dane | Znaczenie dla projektu |
| --- | --- | --- |
| Beta RR 350/390/430/480 EFI, 2016 | Instrukcja, s. 33: bieg jałowy sterowany przez ECU; obok opisano linkę gazu. Schemat dla RR/Race 350–480 z lat 2016–2017: legenda, poz. 46 — silnik krokowy; poz. 47 — przepustnica. | Istnieje rzeczywisty przypadek enduro 4T uzasadniający rozważenie IAC z napędem krokowym przy zachowaniu osprzętu OEM. Parametry napędu i tor mocy wymagają analizy. |
| KTM 300 EXC Six Days, 2023, EU | Katalog przepustnicy 55590: poz. 5 — śruba biegu jałowego, poz. 6 — przycisk zimnego rozruchu. | Potwierdzona ręczna regulacja; nie przenosimy automatycznie rozwiązania Bety do każdego enduro lub każdej generacji wtrysku. Sam katalog nie jest specyfikacją całego sterowania silnikiem. |

Źródła:

- [Beta USA — instrukcja RR 4T EFI 2016, s. 33](https://betausa.com/content/SUPPORT_PDF%27s/2016%20RR%204%20stroke%20owners%20manual_0.pdf), wskazana w [indeksie producenta](https://betausa.com/off-road-support/).
- [Beta USA — schematy RR/Race 4T 2005–2024](https://betausa.com/content/WIRING%20DIAGRAM%204T%202%2024%20new.pdf), strony PDF 8–9: model 2015 350 / 2016–2017 350–480 oraz legenda poz. 46/47. To odniesienie do opublikowanego dokumentu, bez kopiowania oryginału do repozytorium.
- [KTM — katalog przepustnicy 300 EXC Six Days 2023, pozycje 5/6](https://sparepartsfinder.ktm.com/ComponentGroupTemplate/PrintComponentGroupTemplate/55590?culture=en&modelidentifier=1002337401&tenantId=1).

Pytanie 77 pozostaje otwarte. Właściciel poprosił o potwierdzenie zastosowania w enduro; nie zatwierdził ani nie wykluczył IAC. Ewentualny zakres musi odnosić się do potwierdzonych modeli i napędów. Przed wyborem elektroniki potrzebne są parametry uzwojeń/sterowania, kalibracja, wymagane zasoby, zachowanie przy usterce i plan prób. Nie przyjęto obsługi wszystkich zaworów IAC ani napędów krokowych.
