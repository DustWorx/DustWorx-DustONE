# F01 — przegląd sterowania i zamknięcie zakresu funkcji

Stan na: 2026-11-04. **Wynik przeglądu prowadzącego inżynierię; aktualnie F01 w kontroli właściciela przed F02.** Wcześniejsze zamknięcie zakresu przez asystenta nastąpiło po przeglądzie i zapisaniu przyjętych decyzji właściciela, w tym pytań 105–107. Wynik łączy [pomiary](f01-pomiary-silnika.md), [macierz funkcji i wariantów](../architecture/macierz-wariantow-silnika.md), wymagania i wyłączenia.

## Przyjęte sterowanie

| Funkcja | Przyjęty zakres | Podstawa |
| --- | --- | --- |
| Zapłon | Jeden niezależny kanał, CDI lub indukcyjny TCI/IDI według zgodnego osprzętu. | SYS-067/068, ADR-004. |
| Zasilanie paliwem | Gaźnik z/bez TPS i wtrysk w uzgodnionych wariantach, w tym cele TPI/TBI na wspólnej obsadzie PCB. | SYS-012/014/015. |
| Wtryskiwacze i pompa paliwa | Obsługa potrzebna dla uzgodnionych wariantów wtryskowych; liczby torów i parametry wynikną z osprzętu. | SYS-012/015, macierz wariantów. |
| Elektroniczny power valve 2T | Sterowanie napędem w wyposażonych konfiguracjach. | SYS-034. |
| Bieg jałowy IAC | Regulacja z napędem krokowym dla potwierdzonych enduro 4T. | SYS-071, ADR-006. |
| Przepustnica | Ruch mechaniczny linką; odczyt TPS zależnie od konfiguracji, z zachowaniem gaźnika bez TPS. | SYS-014/038. |
| Rozruch i gaszenie | Osobne START/STOP, odcięcia rozrusznika, wykrywanie przewrócenia i ponowny rozruch według przyjętych wymagań. | SYS-037/039/040/048/049. |

Przegląd nie ujawnił dalszej decyzji produktowej potrzebnej do samej listy funkcji F01. Reguły map są w F02; ochrona, wyjątki i reakcje na usterki w F03. Dane napędów, dekodery, algorytmy i numeryczne parametry sterowania należą do etapów 3–4, a komponenty i obwody do etapu 6.

## Zakres i wyłączenia

Jednocylindrowe silniki 2T/4T chłodzone cieczą (SYS-001/002/098); sześć klas zastosowania w macierzy wariantów. Zachowujemy przyjęte wyłączenia: dozownik oleju 2T, ride-by-wire, quickshifter, kontrola trakcji i zintegrowane tory lambda/EGT. Całkowity zakres funkcjonalny systemu pozostaje w etapie 2 do zamknięcia F02–F08 i G0.

TPI pozostaje celem zakresu z warunkami SYS-015/033: wykonalność konwersji smarowania mieszanką nie została potwierdzona. Sam demontaż pompy nie kwalifikuje motocykla. Nie deklarujemy zgodności konkretnych modeli na podstawie zamknięcia F01.

## Wynik przeglądu i przekazanie

| Kryterium F01 | Wynik / dalszy właściciel zadania |
| --- | --- |
| Lista pomiarów i sterowania | Przyjęta, powiązana z SYS; zakres MAP/CCPS i chłodzenia rozstrzygnięty. |
| Funkcje przypisane do wariantów | Macierz sześciu klas gotowa na poziomie funkcjonalnym; ograniczenie chłodzenia cieczą zapisane. |
| Wyłączenia i warunki | Zapisane w wymaganiach, ADR i powyżej. |
| Modele, sygnały i obciążenia | Etap 3: asystent przygotowuje analizę/modelowe dane OEM i procedury, właściciel dostarcza dane oraz wykonuje pomiary. |
| TPI i konwersja smarowania | Etap 3: asystent prowadzi ocenę wykonalności i plan walidacji; warunek przed deklaracją zgodności. |
| Liczby fizycznych kanałów, interfejsy, bilanse i strategie | Etap 4: asystent opracowuje na podstawie danych; istotne kompromisy konsultujemy. |
| Komponenty i obwody | Etap 6: ważne części wybieramy wspólnie, po spełnieniu warunków poprzednich etapów. |
| Weryfikacja produktu | Procedury etapu 5 i dowody z późniejszych prób; wymagania pozostają niezweryfikowane na produkcie. |

Nowa luka ujawniona w późniejszym etapie wymaga zapisu przyczyny i formalnego powrotu do zakresu zgodnie z procesem. **Bieżąca praca: [kontrola pełnego F01](f01-podsumowanie-kontrolne.md) na prośbę właściciela. F02 oczekuje do jej zakończenia.**
