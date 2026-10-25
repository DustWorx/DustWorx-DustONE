# DustONE — proces, odpowiedzialności i status

Stan na: 2026-10-25. Podstawa: uzgodnienia właściciela i zawartość repozytorium. Postęp oceniamy po gotowych rezultatach i dowodach weryfikacji. Etapy częściowo prowadzimy równolegle, a testy przygotowujemy przed odpowiadającymi im próbami.

## Aktualne miejsce w procesie

Projekt jest na etapie wymagań, inwentaryzacji i wstępnej architektury funkcjonalnej. [Rejestr wymagań](requirements/README.md) obejmuje uzgodnione funkcje oraz otwarte parametry. W repozytorium są analizy i plany; nie ma jeszcze schematów wykonawczych, PCB, kompletnego BOM ani implementacji ECU/HMI i Windows. Nie udokumentowano pomiarów ani prób produktu.

| Etap | Główny rezultat | Aktualny status |
| --- | --- | --- |
| 1. Organizacja projektu | Repozytorium, struktura, zasady zmian i decyzji. | Gotowa baza; dokumentację rozwijamy wraz z projektem. |
| 2. Zakres i wymagania systemowe | Funkcje ECU/HMI/Windows, warianty silników, ograniczenia i zachowanie systemu. | W trakcie; rejestr istnieje, część parametrów i decyzji pozostaje otwarta. |
| 3. Inwentaryzacja i pomiary referencyjne | Interfejsy zachowywanych czujników i osprzętu do nowej wiązki, warunki zasilania, obciążenia i miejsce montażu. | W trakcie; dokumenty i zdjęcia Bety opracowane, pomiary przed nami. Pozostałe jednostki referencyjne do określenia. |
| 4. Architektura i specyfikacje szczegółowe | Diagramy blokowe, I/O, zasoby procesorów, bilans mocy, sygnały i protokoły. | Wstępne założenia; część zasad pracy i zasilania uzgodniona, pełny projekt otwarty. |
| 5. Plan weryfikacji | Macierz wymaganie–metoda–procedura–wynik, kryteria akceptacji i etap wykonania. | Propozycje prób i plan inwentaryzacji istnieją; pełna macierz i gotowe procedury do opracowania. |
| 6. Komponenty i schematy | Dobór elementów, obliczenia, biblioteki, schematy ECU/HMI, przeglądy i BOM. | Projekt wykonawczy nie rozpoczęty; przykłady układów w analizach nie są zatwierdzonym BOM. |
| 7. Mechanika i instalacja | Obudowy, mocowania, uszczelnienia, złącza, wiązka i zgodność z dostępną przestrzenią. | Wymagania wstępne; modele i rozwiązania wykonawcze przed nami. |
| 8. Projekt PCB | Stack-up, placement, routing, zasilanie/masy, odprowadzanie ciepła, DRC i przygotowanie do produkcji. | Nie rozpoczęto; praca w Autodesk Fusion Electronics. |
| 9. Implementacja firmware i Windows | Kod, bootloadery, komunikacja, mapy, diagnostyka, HMI i narzędzia Windows. | Zakres opisany; w repozytorium brak implementacji. Prace mogą przebiegać równolegle z projektowaniem sprzętu. |
| 10. Wykonanie i uruchomienie prototypów | Pliki produkcyjne, montaż, kontrola wykonania i uruchamianie blokami. | Nie rozpoczęto. |
| 11. Weryfikacja i walidacja systemu | Pomiary, testy funkcjonalne/integracyjne, próby na stanowiskach i motocyklach oraz potrzebne próby środowiskowe/EMC. | Propozycje części prób; brak raportów z wykonania. Testy bloków zaczynają się wcześniej, zgodnie z ich gotowością. |
| 12. Korekty i wydanie prototypu | Poprawki, regresja, potwierdzony zakres działania, instrukcje i wykaz ograniczeń. | Przed nami; kolejne rewizje wynikną z analizy i prób. |

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

Najpierw określamy decyzje wpływające na sprzęt i wspólną PCB. Szczegóły niezależne od sprzętu można rozwijać później. Pytania pojedyncze z propozycjami służą ustalaniu preferencji, zakresu, brakujących informacji oraz wspólnemu wyborowi ważnych komponentów po przedstawieniu porównania. Obliczenia i propozycje rozwiązań technicznych przygotowuje asystent z uzasadnieniem; właściciel aktywnie uczestniczy w doborze części według powyższej zasady.

Kompletność sprawdzamy według [mapy obszarów i otwartych tematów](requirements/pokrycie-funkcjonalne.md), a nie liczby zadanych pytań. Dla każdego obszaru przeglądamy normalną pracę, rozruch/wyłączenie, granice, brak opcjonalnego wyposażenia, usterki oraz serwis i aktualizację, odpowiednio do jego roli. Zapisujemy wymagania przyjęte, wyłączenia i kwestie otwarte. Każda istotna decyzja otrzymuje źródło; wymagania łączymy dalej z blokiem realizującym i weryfikacją.

Przed zamknięciem architektury, wydaniem PCB i rozpoczęciem prób wykonujemy odpowiedni przegląd pokrycia. Późniejsza zmiana wymaga oceny wpływu na pozostałe urządzenia, I/O, zasoby, dokumentację i testy. Pełny przegląd kompletności oraz szczegółowa macierz realizacji i weryfikacji pozostają do opracowania; sama mapa obszarów ich nie zastępuje.

## Odpowiedzialność za testy

Asystent przygotowuje plan, powiązanie testów z wymaganiami, stanowiska, wyposażenie, procedury, oczekiwane wyniki i kryteria przerwania. Właściciel wykonuje próby fizyczne i przekazuje dane. Asystent analizuje wyniki, wskazuje niezgodności, proponuje poprawki oraz określa potrzebną regresję. [Zasady weryfikacji i szablon procedury](verification/README.md) są miejscem źródłowym dla tego procesu.

Każde wymaganie musi mieć właściwą metodę i dowód potwierdzenia. Funkcje i parametry działania obejmujemy próbami rzeczywistego ECU/HMI/aplikacji; obliczenia i przeglądy uzupełniają weryfikację konstrukcji. Status uzgodnionego wymagania jest odrębny od statusu zweryfikowanego wykonania.

## Warunki przechodzenia dalej

- Blok można projektować po ustaleniu potrzebnych mu parametrów i interfejsów; pozostałe obszary mogą nadal być doprecyzowywane.
- Przed zleceniem PCB potrzebne są przeglądy schematu, symboli/footprintów i BOM, kontrola ERC/DRC oraz mechaniki i plan uruchomienia. Otwarte kwestie wpływające na wspólną PCB 2T/4T muszą zostać rozstrzygnięte przed jej wydaniem.
- Wymaganie uznajemy za zweryfikowane po wykonaniu przyjętej metody, uzyskaniu wyniku i zapisaniu dowodu dla konkretnej rewizji. Nieuzupełnione kryteria lub niewykonana próba pozostawiają je niezweryfikowane.
- Wydanie prototypu zawiera potwierdzony zakres i jawne ograniczenia. Beta jest pierwszą konfiguracją testową; 4T oraz docelowe TPI/TBI wymagają odrębnych stanowisk i jednostek referencyjnych.

Najbliższe większe rezultaty: uszczegółowiona architektura blokowa, bilans I/O i zasilania, parametry zachowywanego osprzętu oraz macierz weryfikacji rozwijana razem ze specyfikacjami bloków.
