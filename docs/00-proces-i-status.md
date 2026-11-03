# DustONE — ścieżka projektu, status i odpowiedzialności

Stan na: 2026-11-03. Ocena głównej gałęzi, materiałów roboczych oraz uzgodnień właściciela do pytania 102. Ścieżka projektu i warunki postoju z PR #17/#18 są scalone. Dokument aktualizujemy przy istotnej odpowiedzi lub decyzji, wykonanej pracy, wyniku próby, zmianie zakresu i przeglądzie etapu; wraz z wymaganiami, ADR, interfejsami i weryfikacją.

## Aktualne miejsce w procesie

**Główny zakres funkcji jest opisany; trwa jego domykanie i opracowanie architektury systemu.** Równolegle potrzebujemy danych z inwentaryzacji Bety. Formalne zakończenie zakresu wymaga przeglądu opisanych niżej pakietów, a następnie bramki G0.

| Obszar | Stan potwierdzony dokumentacją |
| --- | --- |
| Wymagania systemowe | 94 wymagania SYS-001–094; pierwszy przydział do bloków i grup weryfikacji gotowy, kryteria i procedury do rozwinięcia. |
| Decyzje | 11 zapisów ADR-001–011; ostatni obejmuje strojenie na żywo i niezależne, kompletne zestawy map. |
| Zakres wariantów | Macierz 6 wariantów silnika; jest planem obsługi, nie potwierdzeniem zgodności modeli. |
| Pierwsza jednostka | Beta 300 RR Racing 2015; analiza dokumentów i zdjęć, bez raportów pomiarowych instalacji. |
| Architektura | Pierwszy diagram blokowy, funkcje sześciu wariantów i przydział zasobów gotowe jako wersje robocze. Modele, parametry i liczbowe bilanse pozostają otwarte. |
| Schematy, BOM, PCB i mechanika | W repozytorium brak projektu wykonawczego i zatwierdzonego kompletnego BOM ECU/HMI. |
| Kod i próby produktu | W repozytorium brak implementacji firmware/Windows i raportów prób DustONE. Istnieją plany, szablon procedury i przydział 94 wymagań do 13 grup weryfikacji. |

Podstawy: [wymagania](requirements/README.md), [decyzje](decisions/README.md), [macierz silników](architecture/macierz-wariantow-silnika.md), [I/O](interfaces/wstepna-lista-io.md) i [weryfikacja](verification/README.md). Liczba wymagań i pytań nie jest procentem wykonania produktu.

## Etapy i warunki zakończenia

Etapy częściowo prowadzimy równolegle. Wyjście z etapu wynika z gotowych rezultatów i przeglądu, a działanie produktu potwierdzają późniejsze dowody z prób.

| Etap | Główny rezultat | Bieżący status | Warunek zakończenia / przejścia |
| --- | --- | --- | --- |
| 1. Organizacja | Repozytorium, struktura, zasady zmian i decyzji. | Baza gotowa; utrzymanie ciągłe. | Uzgodnienia i źródła mają miejsce w repozytorium, zmiany są wersjonowane. |
| 2. Zakres funkcjonalny | Funkcje, wyłączenia, warianty i reguły użytkowania ECU/HMI/Windows. | W trakcie domykania: F01/F02 w opracowaniu; 8 pakietów nadal otwartych. | G0: przyjęta baza zakresu, rozstrzygnięte decyzje produktowe i jawne otwarte parametry techniczne. |
| 3. Inwentaryzacja i dane | Osprzęt, sygnały, obciążenia, zasilanie i przestrzeń montażowa. | Częściowo: dokumenty i zdjęcia Bety; pomiary przed nami. | Dane wystarczają do projektowania odpowiedniego bloku; braki innych wariantów mają plan pozyskania. |
| 4. Architektura | Diagramy blokowe, I/O dla wariantów, zasoby, zasilanie, interfejsy i stany awaryjne. | Pierwszy diagram i funkcjonalny przydział zasobów gotowe do przeglądu; dane i bilanse otwarte. | G1: uzasadniony podział bloków, bilanse, granice interfejsów i zamknięte niewiadome wpływające na projektowane bloki. |
| 5. Plan weryfikacji | Powiązanie wymaganie → blok → metoda → kryterium → próba → dowód. | Pierwszy przydział 94 SYS do bloków i 13 grup gotowy; szczegółowe kryteria i procedury otwarte. | Wymagania mają przydzieloną metodę i etap; procedura wykonawcza jest gotowa przed daną próbą. |
| 6. Komponenty i schematy | Wspólny wybór ważnych części, obliczenia, biblioteki, schematy i BOM. | Projekt wykonawczy nie rozpoczęty. | Przyjęte części, zweryfikowane symbole/footprinty, obliczenia i przegląd schematów/ERC. |
| 7. Mechanika i instalacja | Obudowy, mocowania, uszczelnienia, złącza i nowa wiązka. | Wymagania wstępne; projekt wykonawczy przed nami. | Zgodność z miejscem montażu, dostępem, złączami, ciepłem i wymaganiami środowiskowymi. |
| 8. PCB w Fusion | Warstwy, rozmieszczenie, routing, zasilanie/masy i eksporty produkcyjne. | Nie rozpoczęto; CAD wykonuje właściciel przy wsparciu asystenta. | G2: przegląd schematu/BOM/bibliotek, ERC/DRC, mechaniki i planu uruchomienia; gotowy komplet do wykonania. |
| 9. Firmware i Windows | Sterowanie, CAN, HMI, mapy, diagnostyka, aktualizacja i narzędzia. | Zakres opisany; brak kodu w repozytorium. | Funkcje i interfejsy zaimplementowane oraz sprawdzone na właściwym poziomie. Rozwój może zaczynać się na symulatorach i stanowiskach. |
| 10. Prototypy i uruchomienie | PCB, montaż, kontrola wykonania i uruchamianie blokami. | Nie rozpoczęto. | G3: podstawowe zasilanie, komunikacja i I/O sprawdzone według procedur; gotowość do prób systemowych. |
| 11. Weryfikacja i walidacja | Testy bloków i systemu, stanowiska, motocykle oraz dobrane próby środowiskowe/EMC. | Plany części prób; brak wyników produktu. | Dowody dla przyjętego zakresu i konfiguracji, zarejestrowane niezgodności oraz ograniczenia. |
| 12. Korekty i wydanie prototypu | Poprawki, regresja, instrukcje i wersjonowany zakres działania. | Przed nami. | G4: przegląd wyników, potwierdzone konfiguracje, komplet wersji i jawne ograniczenia wydania. |

Projekt wspólnej PCB obejmuje docelowy uzgodniony zakres 2T/4T bez zmian obsady. Uruchamianie i firmware rozwijamy etapami od Bety; pozostałe warianty wymagają własnych analiz, stanowisk i prób.

## Co pozostało w funkcjonalności

Pozostaje **8 pakietów końcowego przeglądu F01–F08** oraz przegląd zamykający G0. Ich treść i wynik wymagany do zamknięcia opisuje [rejestr domknięcia zakresu](requirements/domkniecie-zakresu-funkcjonalnego.md). Pakiet może zawierać kilka decyzji; część jego funkcji jest już uzgodniona. Jest to roboczy plan domknięcia obecnego zakresu, aktualizowany przy ujawnieniu nowych luk.

Parametry wyliczane z osprzętu, charakterystyki czujników, wartości elementów, konkretne procesory i układy, formaty CAN oraz layout rozwijamy w odpowiednich etapach architektury i projektu wykonawczego. Ważne komponenty nadal wybieramy wspólnie.

## Bieżące prace i następny rezultat

| Zadanie | Status | Dowód / kolejny wynik |
| --- | --- | --- |
| W01 — Architektura blokowa | Pierwsza wersja robocza gotowa. | [Diagram i bloki](architecture/blokowa-systemu.md); G1 pozostaje otwarta. |
| W02 — Funkcje i zasoby wariantów | Pierwsza macierz gotowa; bilans liczbowy w przygotowaniu danych. | [Macierz](architecture/macierz-wariantow-silnika.md); uzupełnić modele, parametry i jednoczesność kanałów. |
| W03 — Powiązanie wymagań i weryfikacji | Pierwszy przydział gotowy. | [94 SYS → blok → 13 grup](verification/macierz-wymagan.md); kryteria/procedury i dowody przed nami. |
| W04 — Domknięcie F01/F02 | W opracowaniu; strojenie na żywo i maks. trzy pełne, niezależne zestawy przyjęte w SYS-094/028. | Modele referencyjne oraz lista map i reguły edycji/utrwalania; [specyfikacja F02](interfaces/mapy-i-konfiguracja.md). |
| W05 — Inwentaryzacja Bety | Plan jest; brak wyników pomiarowych. | Uzupełnić dane według [planu INV](verification/beta-2015-plan-inwentaryzacji.md) i przygotować właściwe procedury pomiarowe. |
| W06 — Bilanse przed wyborem komponentów | Dane wejściowe niekompletne. | Prądy/ciepło, czasy, pamięć, interfejsy i budżet snu; dopiero potem porównanie kandydatów. |

**Kolejny rezultat: uzupełnione dane osprzętu i reguły map, potrzebne do liczbowego bilansu I/O, czasu, pamięci i zasilania.** Asystent przygotowuje analizy modeli/OEM i propozycje; właściciel rozstrzyga decyzje produktowe oraz dostarcza dane/pomiary Bety. Równolegle rozwijamy mierzalne kryteria i procedury właściwych prób.

Nie zamykamy etapu samym utworzeniem dokumentu. Po uzyskaniu danych dla bloku porównamy MCU, zasilanie, transceivery, drivery i inne ważne komponenty do wspólnego wyboru. Firmware/CAN/Windows mogą być rozwijane równolegle po określeniu interfejsów. Próba 28-dniowa może trwać równolegle z innymi pracami po uzyskaniu stabilnego snu i gotowych kryteriów.

## Warunki przechodzenia dalej

| Bramka | Co musi być gotowe |
| --- | --- |
| G0 — baza funkcjonalna | Przeglądy F01–F08 zakończone decyzją lub jawnym wyłączeniem; spójny rejestr wymagań; pozostałe niewiadome mają właściciela zadania i etap rozstrzygnięcia. |
| G1 — architektura do projektowania | I/O i zasoby dla wariantów, bilanse zasilania i ciepła, interfejsy oraz ocena istotnych niewykonalności; dane wystarczające dla projektowanego bloku. |
| G2 — wykonanie PCB | Przyjęte schematy/BOM/biblioteki, ważne części wybrane wspólnie, przegląd PCB, ERC/DRC i mechaniki oraz plan uruchomienia z punktami pomiarowymi. |
| G3 — próby systemowe | Kontrolowane uruchomienie zasilania i bloków, gotowe stanowiska/procedury, znane limity oraz zapisane wyniki dopuszczające kolejne próby. |
| G4 — wydanie prototypu | Potwierdzony zakres działania dla właściwych rewizji i konfiguracji, regresja, dokumentacja oraz lista ograniczeń i prac pozostałych. |

Projekt pojedynczego bloku może ruszyć po uzyskaniu jego danych wejściowych. Zamrożenie PCB wymaga rozstrzygnięcia kwestii wpływających na wspólny sprzęt. Status uzgodnionego wymagania i status zweryfikowanego produktu prowadzimy oddzielnie.

## Najważniejsze niewiadome do następnego etapu

| Temat | Działanie i miejsce rozstrzygnięcia |
| --- | --- |
| TPI i smarowanie mieszanką | Ocena wykonalności dla konkretnych jednostek zgodnie z macierzą wariantów; warunek przed deklaracją zgodności. |
| Wspólny sprzęt i kompaktowość | Parametry CDI/TCI, czujników i napędów, jednoczesność I/O, prądy oraz ciepło — etapy 3–6. |
| Wybudzanie i rezerwa energii | Powiązać kopniak/koło/HMI, normalne zasilanie HMI w śnie oraz 4 tygodnie postoju przy −10°C…+40°C dla minimum 3 Ah AGM / 2 Ah LiFePO4 — bilans i próby. |
| Pokrycie poza Betą | Zaplanować reprezentatywne stanowiska i jednostki 4T/TPI/TBI; wyniki Bety potwierdzają jej konfigurację. |

## Zakres prowadzenia inżynierii

Asystent prowadzący inżynierię odpowiada za przygotowanie i uzasadnienie wymagań, architektury, interfejsów, obliczeń, doboru komponentów, schematów, bibliotek i footprintów, opracowanie i przeglądy rozmieszczenia elementów oraz prowadzenia połączeń PCB, integrację mechaniczną i dokumentację wykonawczą. Decyzje podejmujemy z właścicielem projektu i zapisujemy ich podstawę.

Dobór elementów obejmuje potrzebne parametry, wartości i tolerancje, zapasy, obudowę, symbol/footprint, numer producenta i powiązanie z BOM. Głębokość analizy dopasowujemy do roli elementu; kluczowe układy wymagają porównania i weryfikacji dokumentacji producenta. Schemat i PCB obejmują też zasilanie, zabezpieczenia, masy, prądy, ciepło, prowadzenie sygnałów, montaż i wykonalność produkcji.

### Wspólny dobór ważnych komponentów

Ustalenie właściciela: wybór każdego ważnego komponentu konsultujemy i podejmujemy wspólnie przed przyjęciem go do projektu. Obejmuje to procesory ECU/HMI, czujniki na PCB (w tym akcelerometr/IMU i czujnik ciśnienia atmosferycznego), transceivery, układy zasilania, sterowniki wyjść, pamięci i inne elementy istotne dla funkcji, interfejsów, dokładności, gabarytów lub niezawodności. Zasada obejmuje także elementy pasywne, jeśli ich wybór ma takie znaczenie, oraz istotne zmiany wcześniej przyjętych części.

Asystent przygotowuje wymagania dla elementu, weryfikuje dokumentację i przedstawia zwykle 2–3 odpowiednich kandydatów: konkretne numery producenta, parametry, obudowy, interfejsy, pobór mocy, ograniczenia, dostępność i orientacyjny koszt z datą sprawdzenia. Porównanie zawiera rekomendację z uzasadnieniem i skutki dla pozostałych bloków, firmware oraz PCB. Jeżeli brak sensownych alternatyw, przedstawia przyczynę. Właściciel może zaproponować własny komponent do oceny.

Wybór omawiamy z właścicielem; propozycje pozostają propozycjami do czasu jego potwierdzenia. Przyjętą część, uzasadnienie i źródło decyzji zapisujemy przy danym bloku/BOM, a decyzje architektoniczne także w ADR. Asystent następnie opracowuje potrzebne obwody, wartości elementów towarzyszących, połączenia, wymagania dla bibliotek i layoutu oraz kryteria weryfikacji. Projekt w Autodesk Fusion wykonuje właściciel, otrzymując od asystenta informacje, dane i wymagania potrzebne do jego realizacji oraz przeglądy wyników.

Firmware przygotowuje właściciel z Codexem zgodnie z ustalonym sposobem współpracy. Praca inżynierska obejmuje wymagania, przydział zasobów, interfejsy, kryteria i testy potrzebne również do firmware oraz aplikacji Windows.

## Współpraca przy schematach i PCB

Ustalenie właściciela: projekt CAD wykonuje w Autodesk Fusion Electronics, korzystając z przygotowanych przez asystenta rozwiązań. Asystent dostarcza schematy bloków z wartościami i połączeniami, uzasadnienie doboru elementów, propozycje rozmieszczenia komponentów oraz liczby i funkcji warstw. Określa zasady prowadzenia sygnałów, zasilania i mas, wymagane odstępy, szerokości i przelotki oraz potrzebne kontrole elektryczne, cieplne i produkcyjne. Parametry ustalamy z obliczeń, danych producentów i warunków wykonania PCB.

Pracujemy blokami: dane wejściowe → rozwiązanie i obliczenia → odwzorowanie w Fusion → przegląd schematu, bibliotek i PCB → korekty. Archiwizujemy pliki edytowalne oraz powiązane eksporty dla konkretnej rewizji. Zrzuty ekranu pomagają w przeglądzie, ale nie zastępują kontroli połączeń, reguł i footprintów.

Bezpośrednia obsługa Fusion przez asystenta pozostaje opcjonalnym sposobem pracy. W sesji z 2026-10-25 narzędzie Windows wykryło zainstalowany Fusion, bez uruchomionego okna; brak dedykowanego narzędzia Fusion w tej sesji. Obsługa edytora schematów i PCB nie została jeszcze sprawdzona w praktyce. Przed wykorzystaniem jej do projektu należy przeprowadzić próbę na małym obwodzie, obejmującą zapis, ponowne otwarcie i kontrolę wyniku.

## Podstawa pytań i kontrola kompletności

Pytania wynikają z celów właściciela i wcześniejszych odpowiedzi, scenariuszy użycia i stanów urządzeń, macierzy wariantów silnika, dokumentacji zachowywanego osprzętu oraz analizy zależności i możliwych uszkodzeń. Dokumenty referencyjne dostarczają danych; potwierdzenie zgodności danego osprzętu wymaga analizy i pomiarów.

Ustalenie właściciela z 2026-11-01: przed pytaniem o nową funkcję silnika lub osprzętu sprawdzamy jej występowanie w motocyklach enduro odpowiadających celowi DustONE. Przedstawiamy konkretny model, rocznik, źródło producenta i potwierdzony sposób realizacji oraz znaczenie dla wspólnej PCB. Funkcje wynikające bezpośrednio z celów właściciela oznaczamy jako takie. [Zasada weryfikacji i przykład IAC](requirements/weryfikacja-funkcji-enduro.md) określa sposób dokumentowania podstaw pytania. Brak potwierdzenia pozostaje jawną luką; sam opis funkcji w uniwersalnym ECU nie potwierdza wyposażenia enduro.

Najpierw określamy decyzje wpływające na sprzęt i wspólną PCB. Szczegóły niezależne od sprzętu można rozwijać później. Pytania pojedyncze z propozycjami służą ustalaniu preferencji, zakresu, brakujących informacji oraz wspólnemu wyborowi ważnych komponentów po przedstawieniu porównania. Obliczenia i propozycje rozwiązań technicznych przygotowuje asystent z uzasadnieniem; właściciel aktywnie uczestniczy w doborze części według powyższej zasady.

Kompletność sprawdzamy według [mapy obszarów i otwartych tematów](requirements/pokrycie-funkcjonalne.md), a nie liczby zadanych pytań. Dla każdego obszaru przeglądamy normalną pracę, rozruch/wyłączenie, granice, brak opcjonalnego wyposażenia, usterki oraz serwis i aktualizację, odpowiednio do jego roli. Zapisujemy wymagania przyjęte, wyłączenia i kwestie otwarte. Każda istotna decyzja otrzymuje źródło; wymagania łączymy dalej z blokiem realizującym i weryfikacją.

Przed zamknięciem architektury, wydaniem PCB i rozpoczęciem prób wykonujemy odpowiedni przegląd pokrycia. Późniejsza zmiana wymaga oceny wpływu na pozostałe urządzenia, I/O, zasoby, dokumentację i testy. Pełny przegląd kompletności oraz szczegółowa macierz realizacji i weryfikacji pozostają do opracowania; sama mapa obszarów ich nie zastępuje.

## Odpowiedzialność za testy

Asystent przygotowuje plan, powiązanie testów z wymaganiami, stanowiska, wyposażenie, procedury, oczekiwane wyniki i kryteria przerwania. Właściciel wykonuje próby fizyczne i przekazuje dane. Asystent analizuje wyniki, wskazuje niezgodności, proponuje poprawki oraz określa potrzebną regresję. [Zasady weryfikacji i szablon procedury](verification/README.md) są miejscem źródłowym dla tego procesu.

Każde wymaganie musi mieć właściwą metodę i dowód potwierdzenia. Funkcje i parametry działania obejmujemy próbami rzeczywistego ECU/HMI/aplikacji; obliczenia i przeglądy uzupełniają weryfikację konstrukcji. Status uzgodnionego wymagania jest odrębny od statusu zweryfikowanego wykonania.
