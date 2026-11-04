# Mapy i konfiguracja — operacje F02

Stan na: 2026-11-04. **F02 aktywny po zamknięciu F01; wcześniejsze ustalenia zachowane.** Wymagania źródłowe: SYS-003/007/028/047/094/095 w [rejestrze systemu](../01-zakres-systemu.md). Podstawa decyzji: [ADR-011](../decisions/adr-011-strojenie-na-zywo.md), odpowiedzi A na pytania 101–104.

## Zatwierdzona podstawa

- Dla jednej konfiguracji silnika ECU przechowuje maksymalnie trzy niezależne, kompletne zestawy uzgodnionych map. Zestawy mają własne wartości map, np. zapłonu i paliwa dla wtrysku.
- Aktywny zestaw można przełączać z HMI także podczas pracy silnika.
- Windows umożliwia zastosowanie zmian wybranych wartości map podczas pracy silnika.
- Po utracie połączenia z Windows ostatnio zastosowane wartości pozostają aktywne w bieżącej pracy ECU, bez automatycznego trwałego zapisu.
- Trwały zapis zmian wymaga wyraźnego polecenia użytkownika z Windows i zgaszonego silnika. ECU egzekwuje warunki; strojenie na żywo nie uruchamia automatycznego trwałego zapisu.
- ECU jest właścicielem danych i rozstrzyga wykonanie żądań. Odczyt i edycja w Windows oraz wybór w HMI muszą odzwierciedlać rzeczywiste dane ECU.

„Kompletny zestaw” oznacza komplet map uzgodnionych dla danej konfiguracji. Lista map, osie, wielkości tabel i podział między mapy a wspólne parametry silnika pozostają do specyfikacji. Obsługa paliwa dotyczy odpowiednich konfiguracji wtryskowych; nie dodajemy sterowania wtryskiem do wariantu gaźnikowego.

## Operacje i stan ustaleń

| Operacja | Co przyjęto | Co pozostaje do określenia |
| --- | --- | --- |
| Wybór zestawu z HMI | Dopuszczony także podczas pracy silnika. | Warunki, moment/spójność przełączenia, potwierdzenie i wybór po restarcie. |
| Edycja z Windows i zastosowanie zmian | Strojenie na żywo wybranych wartości jest w zakresie. | Lista pól, zakresy, walidacja, częstotliwość i moment zastosowania, edycja aktywnego/nieaktywnego zestawu. |
| Trwałe zapisanie zmian w ECU | Tylko przy zgaszonym silniku, na wyraźne polecenie użytkownika z Windows; warunki egzekwuje ECU (SYS-095). | Potwierdzanie zatrzymania silnika, warunki zasilania, spójność/przerwanie zapisu, reakcja na próbę rozruchu lub ruch wału w trakcie operacji. |
| Przesłanie pełnego zestawu i konfiguracji | Aplikacja konfiguruje i stroi ECU. | Warunki zastosowania całego zestawu, zgodność z silnikiem/FW i blokady krytycznej konfiguracji. |
| Utrata sesji Windows | ECU zachowuje ostatnio zastosowane wartości map w bieżącej pracy, bez automatycznego trwałego zapisu (SYS-094). | Detekcja utraty sesji, odczyt/uzgodnienie danych po ponownym połączeniu i ponowienie polecenia. |
| Restart / zanik zasilania | Trwałe przechowywanie zestawów pozostaje wymagane. | Dane wybierane po restarcie i zachowanie zmian nieutrwalonych. |

Testy wyjść po utracie sesji podlegają odrębnej regule SYS-091; zachowanie wartości map nie wydłuża ich limitów.

Status „otwarte” oznacza brak zatwierdzonej reguły danej operacji; nie uprawnia do dopuszczenia jej w każdym stanie pojazdu. Dobór pamięci, buforów, formatu danych i interfejsu wynika z tych reguł oraz bilansów, a ważne komponenty wybieramy wspólnie.

## Przewidywana weryfikacja

Rozwinięcie grup V02/V09 z [macierzy wymagań](../verification/macierz-wymagan.md):

1. Odrębne dane trzech zestawów; edycja jednego zachowuje wartości pozostałych.
2. Wybór zestawu, odczyt faktycznie aktywnych danych i dopuszczona zmiana podczas pracy.
3. Odrzucenie niezgodnych danych oraz sprawdzenie wpływu zmiany na czas sterowania.
4. Dopuszczenie trwałego zapisu na jawne polecenie przy zgaszonym silniku oraz odrzucenie żądania podczas pracy. Brak automatycznego trwałego zapisu zmian zastosowanych na żywo.
5. Utrata sesji po zastosowaniu zmian: wartości pozostają aktywne, a trwały zapis nie jest wykonywany automatycznie.
6. Powrót sesji, zanik zasilania i próba rozruchu podczas zapisu według rozstrzygniętych później reguł.

Kryteria liczbowe, połączenia, kroki i warunki przerwania powstaną przed wykonaniem prób. Brak implementacji i wyników produktu.
