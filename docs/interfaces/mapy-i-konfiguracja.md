# Mapy i konfiguracja — operacje F02

Stan na: 2026-11-04. **F02 aktywny po zakończeniu kontroli F01 przez właściciela; wcześniejsze ustalenia zachowane.** Pytanie 108 rozstrzygnięte: ostatnio wybrany prawidłowy zestaw po restarcie. Pytanie 109 rozstrzygnięte: po prawidłowym śnie/wybudzeniu odrzucamy edycję roboczą i wczytujemy trwale zapisane wartości. Pytanie 110 rozstrzygnięte: robocza edycja aktywnego i nieaktywnych zestawów podczas pracy, bez przełączania wskutek edycji. Bieżący temat: warunki zmiany krytycznej konfiguracji silnika. Wymagania źródłowe: SYS-003/007/028/047/094/095/099/100/101 w [rejestrze systemu](../01-zakres-systemu.md). Podstawa decyzji: [ADR-011](../decisions/adr-011-strojenie-na-zywo.md), odpowiedzi A na pytania 101–104 i 108–110.

## Zatwierdzona podstawa

- Dla jednej konfiguracji silnika ECU przechowuje maksymalnie trzy niezależne, kompletne zestawy uzgodnionych map. Zestawy mają własne wartości map, np. zapłonu i paliwa dla wtrysku.
- Aktywny zestaw można przełączać z HMI także podczas pracy silnika.
- Po ponownym uruchomieniu ECU aktywuje ostatnio wybrany prawidłowy zestaw spośród trwale zapisanych, również bez HMI. ECU zapamiętuje wybór (SYS-099).
- Windows umożliwia przesyłanie roboczych zmian wybranych wartości map aktywnego i nieaktywnych zestawów podczas pracy silnika. Edycja nie przełącza zestawu; zmiany nieaktywnego zestawu wpływają na silnik dopiero po jego świadomym wybraniu (SYS-101).
- Po utracie połączenia z Windows ostatnio zastosowane wartości pozostają aktywne w bieżącej pracy ECU, bez automatycznego trwałego zapisu.
- Trwały zapis zmian wymaga wyraźnego polecenia użytkownika z Windows i zgaszonego silnika. ECU egzekwuje warunki; strojenie na żywo nie uruchamia automatycznego trwałego zapisu.
- Po prawidłowym śnie i wybudzeniu, także bez restartu, ECU odrzuca niezapisane zmiany i korzysta z trwale zapisanych wartości wybranego zestawu. Nie wykonuje automatycznego trwałego zapisu (SYS-100).
- ECU jest właścicielem danych i rozstrzyga wykonanie żądań. Odczyt i edycja w Windows oraz wybór w HMI muszą odzwierciedlać rzeczywiste dane ECU.

„Kompletny zestaw” oznacza komplet map uzgodnionych dla danej konfiguracji. Lista map, osie, wielkości tabel i podział między mapy a wspólne parametry silnika pozostają do specyfikacji. Obsługa paliwa dotyczy odpowiednich konfiguracji wtryskowych; nie dodajemy sterowania wtryskiem do wariantu gaźnikowego.

## Operacje i stan ustaleń

| Operacja | Co przyjęto | Co pozostaje do określenia |
| --- | --- | --- |
| Wybór zestawu z HMI | Dopuszczony także podczas pracy silnika; po restarcie wybierany jest ostatnio wybrany prawidłowy zestaw (SYS-099). | Warunki i moment/spójność przełączenia, potwierdzenie, mechanizm zapamiętywania wyboru i walidacja. |
| Edycja z Windows i zastosowanie zmian | Dopuszczona robocza edycja wybranych wartości aktywnego i nieaktywnych zestawów podczas pracy. Sama edycja nie przełącza zestawu; zmiany nieaktywnego zestawu wpływają na silnik dopiero po jego świadomym wybraniu (SYS-101). | Lista pól, zakresy, walidacja, częstotliwość i spójny moment zastosowania danych. |
| Trwałe zapisanie zmian w ECU | Tylko przy zgaszonym silniku, na wyraźne polecenie użytkownika z Windows; warunki egzekwuje ECU (SYS-095). | Potwierdzanie zatrzymania silnika, warunki zasilania, spójność/przerwanie zapisu, reakcja na próbę rozruchu lub ruch wału w trakcie operacji. |
| Przesłanie pełnego zestawu i konfiguracji | Aplikacja konfiguruje i stroi ECU. | Warunki zastosowania całego zestawu, zgodność z silnikiem/FW i blokady krytycznej konfiguracji. |
| Utrata sesji Windows | ECU zachowuje ostatnio zastosowane wartości map w bieżącej pracy, bez automatycznego trwałego zapisu (SYS-094). | Detekcja utraty sesji, odczyt/uzgodnienie danych po ponownym połączeniu i ponowienie polecenia. |
| Restart / zanik zasilania | Ostatnio wybrany prawidłowy zestaw z danych trwale zapisanych, bez oczekiwania na HMI (SYS-099). | Mechanizm i spójność pamiętania wyboru, walidacja i reakcja na niepoprawne dane. |
| Zwykły sen i wybudzenie | Niezapisana edycja jest odrzucana; po wybudzeniu używane są trwale zapisane wartości. Brak automatycznego trwałego zapisu (SYS-100). | Dokładny moment odrzucenia/wczytania danych, gotowość do rozruchu, obsługa sekwencji snu przerwanej nową aktywnością. |

Zapamiętanie identyfikatora zestawu jest odrębne od trwałego zapisu jego edytowanych wartości. Z SYS-095/099 wynika odtworzenie po restarcie trwale zapisanych danych, bez automatycznego odtwarzania nieutrwalonej edycji. Zwykły sen/wybudzenie ma przyjętą regułę SYS-100: nie wymagamy zachowania roboczych edycji map przez sen. Tryby pamięci i MCU pozostają do późniejszego wyboru. W bieżącej pracy po utracie Windows wartości pozostają aktywne według SYS-094; samo zgaszenie silnika lub żądanie snu nie zastępuje zakończonej sekwencji snu i wybudzenia.

Testy wyjść po utracie sesji podlegają odrębnej regule SYS-091; zachowanie wartości map nie wydłuża ich limitów.

Status „otwarte” oznacza brak zatwierdzonej reguły danej operacji; nie uprawnia do dopuszczenia jej w każdym stanie pojazdu. Dobór pamięci, buforów, formatu danych i interfejsu wynika z tych reguł oraz bilansów, a ważne komponenty wybieramy wspólnie.

## Przewidywana weryfikacja

Rozwinięcie grup V02/V09 z [macierzy wymagań](../verification/macierz-wymagan.md):

1. Odrębne dane trzech zestawów; podczas pracy silnika edycja wybranych wartości aktywnego oraz nieaktywnych zestawów zachowuje wartości pozostałych zestawów i nie zmienia aktywnego wyboru. Zmiany nieaktywnego zestawu nie wpływają na bieżące sterowanie.
2. Świadomy wybór wcześniej edytowanego nieaktywnego zestawu podczas pracy: sterowanie korzysta z jego zmienionych wartości; odczyt potwierdza faktycznie aktywny zestaw i dane. Robocza edycja nie powoduje automatycznego trwałego zapisu.
3. Odrzucenie niezgodnych danych oraz sprawdzenie wpływu zmiany na czas sterowania.
4. Dopuszczenie trwałego zapisu na jawne polecenie przy zgaszonym silniku oraz odrzucenie żądania podczas pracy. Brak automatycznego trwałego zapisu zmian zastosowanych na żywo.
5. Utrata sesji po zastosowaniu zmian: wartości pozostają aktywne, a trwały zapis nie jest wykonywany automatycznie.
6. Wybór różnych zapisanych zestawów i restart ECU z HMI oraz bez HMI: odtworzenie ostatniego prawidłowego wyboru i zapisanych wartości. Niezapisana edycja nie staje się trwałym zapisem wskutek restartu.
7. Robocza edycja, odłączenie PC, prawidłowy sen i wybudzenie bez restartu: odrzucenie edycji, użycie trwale zapisanych wartości wybranego zestawu, brak automatycznego utrwalania. Samo rozłączenie Windows nadal zachowuje zastosowane wartości w bieżącej pracy.
8. Przerwana sekwencja snu, powrót sesji, uszkodzone dane wyboru i próba rozruchu podczas zapisu według rozstrzygniętych później reguł.

Kryteria liczbowe, połączenia, kroki i warunki przerwania powstaną przed wykonaniem prób. Brak implementacji i wyników produktu.
