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

Firmware przygotowuje właściciel z Codexem zgodnie z ustalonym sposobem współpracy. Praca inżynierska obejmuje wymagania, przydział zasobów, interfejsy, kryteria i testy potrzebne również do firmware oraz aplikacji Windows.

## Odpowiedzialność za testy

Asystent przygotowuje plan, powiązanie testów z wymaganiami, stanowiska, wyposażenie, procedury, oczekiwane wyniki i kryteria przerwania. Właściciel wykonuje próby fizyczne i przekazuje dane. Asystent analizuje wyniki, wskazuje niezgodności, proponuje poprawki oraz określa potrzebną regresję. [Zasady weryfikacji i szablon procedury](verification/README.md) są miejscem źródłowym dla tego procesu.

Każde wymaganie musi mieć właściwą metodę i dowód potwierdzenia. Funkcje i parametry działania obejmujemy próbami rzeczywistego ECU/HMI/aplikacji; obliczenia i przeglądy uzupełniają weryfikację konstrukcji. Status uzgodnionego wymagania jest odrębny od statusu zweryfikowanego wykonania.

## Warunki przechodzenia dalej

- Blok można projektować po ustaleniu potrzebnych mu parametrów i interfejsów; pozostałe obszary mogą nadal być doprecyzowywane.
- Przed zleceniem PCB potrzebne są przeglądy schematu, symboli/footprintów i BOM, kontrola ERC/DRC oraz mechaniki i plan uruchomienia. Otwarte kwestie wpływające na wspólną PCB 2T/4T muszą zostać rozstrzygnięte przed jej wydaniem.
- Wymaganie uznajemy za zweryfikowane po wykonaniu przyjętej metody, uzyskaniu wyniku i zapisaniu dowodu dla konkretnej rewizji. Nieuzupełnione kryteria lub niewykonana próba pozostawiają je niezweryfikowane.
- Wydanie prototypu zawiera potwierdzony zakres i jawne ograniczenia. Beta jest pierwszą konfiguracją testową; 4T oraz docelowe TPI/TBI wymagają odrębnych stanowisk i jednostek referencyjnych.

Najbliższe większe rezultaty: uszczegółowiona architektura blokowa, bilans I/O i zasilania, parametry zachowywanego osprzętu oraz macierz weryfikacji rozwijana razem ze specyfikacjami bloków.
