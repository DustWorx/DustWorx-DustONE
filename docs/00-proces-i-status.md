# DustONE — ścieżka projektu, status i odpowiedzialności

Stan na 2026-11-08. Ocena uwzględnia uzgodnienia właściciela do pytania 134 oraz reguły operacji na mapach, odzyskiwania danych, zawartości zestawów i map bazowych gaźnika oraz wtrysku (SYS-109–125). Ścieżka projektu i warunki postoju z PR #17/#18 są scalone. Dokument aktualizujemy przy istotnej odpowiedzi lub decyzji, wykonanej pracy, wyniku próby, zmianie zakresu i przeglądzie etapu; wraz z wymaganiami, ADR, interfejsami i weryfikacją.

Kontrola pełnego F01 została zakończona: właściciel potwierdził zgodność podsumowania i polecił dalszą pracę (2026-11-04). Źródło kontroli: [przyjęte podsumowanie F01](requirements/f01-podsumowanie-kontrolne.md). Potwierdzenie dotyczy F01. Późniejsza odpowiedź A na pytanie 108 określiła ostatnio wybrany prawidłowy zestaw po restarcie ECU (SYS-099).

## Aktualne miejsce w procesie

**Aktywny etap: 2 — zakres funkcjonalny. F01 zamknięty po kontroli właściciela 2026-11-04; aktywny pakiet: F02 — mapy, konfiguracja i strojenie ECU.** F03–F08 i etapy 3–12 oczekują w kolejce. Wcześniejsze wymagania, decyzje i materiały robocze pozostają zachowane; nie oznaczają formalnego rozpoczęcia ani zamknięcia dalszych etapów.

| Obszar | Stan potwierdzony dokumentacją |
| --- | --- |
| Wymagania systemowe | 125 wymagań SYS-001–125; pierwszy przydział do bloków i grup weryfikacji gotowy, kryteria i procedury do rozwinięcia. |
| Decyzje | 12 zapisów ADR-001–012; ostatni ogranicza platformę do silników chłodzonych cieczą. |
| Zakres wariantów | Macierz 6 wariantów silnika; jest planem obsługi, nie potwierdzeniem zgodności modeli. |
| Pierwsza jednostka | Beta 300 RR Racing 2015; analiza dokumentów i zdjęć, bez raportów pomiarowych instalacji. |
| Architektura | Pierwszy diagram blokowy, funkcje sześciu wariantów i przydział zasobów gotowe jako wersje robocze. Modele, parametry i liczbowe bilanse pozostają otwarte. |
| Schematy, BOM, PCB i mechanika | W repozytorium brak projektu wykonawczego i zatwierdzonego kompletnego BOM ECU/HMI. |
| Kod i próby produktu | W repozytorium brak implementacji firmware/Windows i raportów prób DustONE. Istnieją plany, szablon procedury i przydział 125 wymagań do 13 grup weryfikacji. |

Podstawy: [wymagania](requirements/README.md), [decyzje](decisions/README.md), [macierz silników](architecture/macierz-wariantow-silnika.md), [I/O](interfaces/wstepna-lista-io.md) i [weryfikacja](verification/README.md). Liczba wymagań i pytań nie jest procentem wykonania produktu.

## Etapy i warunki zakończenia

Ustalenie właściciela z 2026-11-04: **prowadzimy etapy i tematy kolejno, zamykając bieżący przed rozpoczęciem następnego**. Obowiązuje kolejność etapów 1–12, a w etapie 2: F01 → F02 → F03 → F04 → F05 → F06 → F07 → F08 → G0.

- W danym momencie aktywny jest jeden pakiet. Kolejny rozpoczynamy po spełnieniu kryteriów zakończenia i zapisaniu wyniku poprzedniego.
- Wpływ bieżącej decyzji na dalszy etap zapisujemy w odpowiednim dokumencie i kolejce; nie rozpoczynamy z tego powodu jego projektowania.
- Analiza źródeł potrzebna do określenia bieżącej funkcji należy do tego pakietu. Parametry, obliczenia i wykonanie rozwijamy na przypisanym późniejszym etapie.
- Zamknięcie zapisujemy z datą, rezultatem, podstawą decyzji i jawnymi danymi przekazanymi dalej. Nierozstrzygnięta decyzja o zakresie nie staje się zamknięta przez przeniesienie do kolejki.
- Gdy późniejsze ustalenie wymaga korekty zamkniętego wyniku, zapisujemy przyczynę i jawnie wracamy do tego miejsca, bez równoległego prowadzenia obu tematów.

Statusy: **aktywny**, **w kolejce**, **zamknięty**. Istniejący szkic oznaczamy osobno jako materiał wstępny; nie nadaje on statusu zamknięcia etapu. Zatwierdzenie wymagania i potwierdzenie działania produktu pozostają odrębnymi stanami.

| Etap | Główny rezultat | Bieżący status | Warunek zakończenia / przejścia |
| --- | --- | --- | --- |
| 1. Organizacja | Repozytorium, struktura, zasady zmian i decyzji. | Zamknięty: 2026-11-04. Dokumentację utrzymujemy. | Uzgodnienia i źródła mają miejsce w repozytorium, zmiany są wersjonowane. |
| 2. Zakres funkcjonalny | Funkcje, wyłączenia, warianty i reguły użytkowania ECU/HMI/Windows. | F01 zamknięty; aktywny F02. F03–F08 w kolejce. | G0: przyjęta baza zakresu, rozstrzygnięte decyzje produktowe i jawne otwarte parametry techniczne. |
| 3. Inwentaryzacja i dane | Osprzęt, sygnały, obciążenia, zasilanie i przestrzeń montażowa. | W kolejce po G0; istnieją dokumenty/zdjęcia i plan INV, bez wyników pomiarów. | Dane wystarczają do projektowania odpowiedniego bloku; braki innych wariantów mają plan pozyskania. |
| 4. Architektura | Diagramy blokowe, I/O dla wariantów, zasoby, zasilanie, interfejsy i stany awaryjne. | W kolejce po etapie 3; zachowane wstępne szkice diagramu i zasobów. | G1: uzasadniony podział bloków, bilanse, granice interfejsów i zamknięte niewiadome wpływające na projektowane bloki. |
| 5. Plan weryfikacji | Powiązanie wymaganie → blok → metoda → kryterium → próba → dowód. | W kolejce po etapie 4; zachowane szablon i wstępny przydział wymagań. | Wymagania mają przydzieloną metodę i etap; procedura wykonawcza jest gotowa przed daną próbą. |
| 6. Komponenty i schematy | Wspólny wybór ważnych części, obliczenia, biblioteki, schematy i BOM. | W kolejce; brak projektu wykonawczego. | Przyjęte części, zweryfikowane symbole/footprinty, obliczenia i przegląd schematów/ERC. |
| 7. Mechanika i instalacja | Obudowy, mocowania, uszczelnienia, złącza i nowa wiązka. | W kolejce; zapisane wstępne potrzeby. | Zgodność z miejscem montażu, dostępem, złączami, ciepłem i wymaganiami środowiskowymi. |
| 8. PCB w Fusion | Warstwy, rozmieszczenie, routing, zasilanie/masy i eksporty produkcyjne. | W kolejce; CAD wykona właściciel przy wsparciu asystenta. | G2: przegląd schematu/BOM/bibliotek, ERC/DRC, mechaniki i planu uruchomienia; gotowy komplet do wykonania. |
| 9. Firmware i Windows | Sterowanie, CAN, HMI, mapy, diagnostyka, aktualizacja i narzędzia. | W kolejce; brak kodu w repozytorium. | Funkcje i interfejsy zaimplementowane oraz sprawdzone na właściwym poziomie. |
| 10. Prototypy i uruchomienie | PCB, montaż, kontrola wykonania i uruchamianie blokami. | W kolejce; nie rozpoczęto. | G3: podstawowe zasilanie, komunikacja i I/O sprawdzone według procedur; gotowość do prób systemowych. |
| 11. Weryfikacja i walidacja | Testy bloków i systemu, stanowiska, motocykle oraz dobrane próby środowiskowe/EMC. | W kolejce; brak wyników produktu. | Dowody dla przyjętego zakresu i konfiguracji, zarejestrowane niezgodności oraz ograniczenia. |
| 12. Korekty i wydanie prototypu | Poprawki, regresja, instrukcje i wersjonowany zakres działania. | W kolejce; nie rozpoczęto. | G4: przegląd wyników, potwierdzone konfiguracje, komplet wersji i jawne ograniczenia wydania. |

Projekt wspólnej PCB obejmuje docelowy uzgodniony zakres 2T/4T bez zmian obsady. Uruchamianie i firmware rozwijamy etapami od Bety; pozostałe warianty wymagają własnych analiz, stanowisk i prób.

## Co pozostało w funkcjonalności

**F01 zamknięty; pozostaje 7 pakietów F02–F08** oraz przegląd zamykający G0. Ich treść i wynik wymagany do zamknięcia opisuje [rejestr domknięcia zakresu](requirements/domkniecie-zakresu-funkcjonalnego.md). Pakiet może zawierać kilka decyzji; część jego funkcji jest już uzgodniona. Jest to roboczy plan domknięcia obecnego zakresu, aktualizowany przy ujawnieniu nowych luk.

Parametry wyliczane z osprzętu, charakterystyki czujników, wartości elementów, konkretne procesory i układy, formaty CAN oraz layout rozwijamy w odpowiednich etapach architektury i projektu wykonawczego. Ważne komponenty nadal wybieramy wspólnie.

## Bieżąca praca i kolejka

| Zadanie | Status | Materiał / warunek podjęcia |
| --- | --- | --- |
| W04 — Zakres funkcjonalny: F01 | Zamknięty po kontroli właściciela: 2026-11-04. | [Pomiary](requirements/f01-pomiary-silnika.md), [przegląd sterowania i wynik zamknięcia](requirements/f01-sterowanie-silnikiem.md); dane techniczne przekazane do kolejki etapów 3–6. |
| F02 — Mapy, konfiguracja i strojenie ECU | Aktywny po zamknięciu F01. | Ustalenia 101–104 i 108–134 przyjęte; rozwijamy [tabelę operacji i warunków](interfaces/mapy-i-konfiguracja.md). Edycja aktywnego i nieaktywnych zestawów podczas pracy przyjęta (SYS-101). Wariant A po porównaniu do pytania 111 przyjęty: transfer/wdrożenie krytycznej konfiguracji tylko po zgaszeniu, z blokadami przez całą operację (SYS-102). Po utracie Windows przed wdrożeniem niepełny transfer jest anulowany, a blokady zwalniane przy poprawnej dotychczasowej konfiguracji; rozruch wymaga nowej próby (SYS-103). SYS-104 przyjęty: przy komplecie danych, przyjętym poleceniu i prawidłowym zasilaniu ECU kończy samodzielnie; blokady zwalnia po powodzeniu, a rozruch wymaga nowej świadomej próby. SYS-105 przyjęty: po błędzie automatyczny powrót do poprzedniej potwierdzonej poprawnej konfiguracji i zwolnienie blokad; bez poprawnych danych blokady i dostęp serwisowy pozostają. SYS-106 przyjęty: po powrocie zasilania tylko kompletna poprawna konfiguracja i nowa świadoma próba bez Windows; bez poprawnych danych blokady i dostęp serwisowy. SYS-107 przyjęty: pełny zestaw map tylko przy zgaszonym silniku, na żywo dopuszczone wybrane wartości. SYS-108 przyjęty: zapis wybranego kompletnego zestawu, aktywnego lub nieaktywnego, oraz wszystkich skonfigurowanych jednym poleceniem. SYS-109 ustala wybór jednej kompletnej wersji map po zaniku zasilania podczas zapisu wszystkich. SYS-110 ustala blokadę rozruchu i odrzucanie poleceń kierowcy do potwierdzenia poprawnych danych. SYS-111 określa powrót do poprzednich map i flagę błędnej sumy po nieudanym zapisie. SYS-112 określa kasowanie flagi po kolejnym zweryfikowanym trwałym zapisie map. SYS-113 ustala samodzielne dokończenie przyjętego zapisu z kompletem danych po utracie Windows. SYS-114 określa anulowanie niepełnego transferu po utracie Windows i zachowanie dotychczasowych map. SYS-115 określa odczyt stanu map, flagi błędu sumy i statusu operacji po ponownym połączeniu Windows. SYS-116 określa zastosowanie całej poprawnej grupy zmian lub odrzucenie całego polecenia z przyczyną. SYS-117 ustala przywrócenie roboczych wartości wybranego zestawu z trwałego zapisu przy zgaszonym silniku. SYS-118 ustala mapy w przełączanych zestawach i pojedyncze nastawy wspólne dla konfiguracji. SYS-119 ustala mapę położenia zaworu wydechowego w każdym zestawie wyposażonych konfiguracji 2T. SYS-120 ustala krzywą zapłonu od obrotów bez TPS oraz mapę od obrotów i położenia przepustnicy z TPS w konfiguracji gaźnikowej. SYS-121 ustala zweryfikowaną krzywą awaryjną od obrotów i zgłoszenie usterki TPS w gaźniku. SYS-122 ustala jedną wspólną krzywą awaryjną dla zestawów danej konfiguracji. SYS-123 ustala powrót do mapy zapłonu z TPS przy następnym rozruchu z wiarygodnym sygnałem. SYS-124 ustala dopuszczenie rozruchu gaźnika z usterką TPS na krzywej zweryfikowanej do rozruchu. SYS-125 ustala osie bazowej mapy dawki paliwa we wtrysku 2T i 4T. Konfiguracja wybiera TPS lub MAP jako źródło obciążenia. Bieżący temat to wspólny lub osobny wybór źródła obciążenia dla map zapłonu i paliwa we wtrysku. |
| W05 — Inwentaryzacja Bety | W kolejce, etap 3. | Zachowany [plan INV](verification/beta-2015-plan-inwentaryzacji.md); brak wyników pomiarowych. |
| W01/W02 — Architektura i zasoby | W kolejce, etap 4. | Zachowane [diagram](architecture/blokowa-systemu.md) i [macierz wariantów](architecture/macierz-wariantow-silnika.md); bez zamkniętych bilansów. |
| W03 — Weryfikacja wymagań | W kolejce, etap 5. | Zachowany [przydział 125 SYS do grup](verification/macierz-wymagan.md); kryteria, procedury i dowody do rozwinięcia. |
| W06 — Bilanse i wybór komponentów | W kolejce, etapy 4 i 6. | Wymagane wejściowe parametry; ważne komponenty wybierzemy wspólnie. |

**Najbliższy rezultat: tabela operacji i warunków F02**, rozwijająca przyjęte zestawy i strojenie na żywo. F01 ma zapisany wynik zamknięcia na poziomie funkcji, bez deklaracji zgodności modeli ani gotowości sprzętu. Konkrety osprzętu, w tym wykonalność konwersji TPI, mają właścicieli i etapy w [przekazaniu F01](requirements/f01-sterowanie-silnikiem.md). Parametry elektryczne, bilanse i procedury wykonawcze pozostają w kolejce właściwych etapów.

## Warunki przechodzenia dalej

| Bramka | Co musi być gotowe |
| --- | --- |
| G0 — baza funkcjonalna | Przeglądy F01–F08 zakończone decyzją lub jawnym wyłączeniem; spójny rejestr wymagań; pozostałe niewiadome mają właściciela zadania i etap rozstrzygnięcia. |
| G1 — architektura do projektowania | I/O i zasoby dla wariantów, bilanse zasilania i ciepła, interfejsy oraz ocena istotnych niewykonalności; dane wystarczające dla projektowanego bloku. |
| G2 — wykonanie PCB | Przyjęte schematy/BOM/biblioteki, ważne części wybrane wspólnie, przegląd PCB, ERC/DRC i mechaniki oraz plan uruchomienia z punktami pomiarowymi. |
| G3 — próby systemowe | Kontrolowane uruchomienie zasilania i bloków, gotowe stanowiska/procedury, znane limity oraz zapisane wyniki dopuszczające kolejne próby. |
| G4 — wydanie prototypu | Potwierdzony zakres działania dla właściwych rewizji i konfiguracji, regresja, dokumentacja oraz lista ograniczeń i prac pozostałych. |

Projekt wykonawczy bloków rozpoczynamy w etapie 6 po zakończeniu wcześniejszych etapów i uzyskaniu danych wejściowych. Zamrożenie PCB wymaga rozstrzygnięcia kwestii wpływających na wspólny sprzęt. Status uzgodnionego wymagania i status zweryfikowanego produktu prowadzimy oddzielnie.

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

Przed pytaniem wskazujemy aktywny pakiet i cel. Przechodzimy do następnego pakietu dopiero po zapisanym zamknięciu poprzedniego; wpływ na późniejsze tematy odkładamy do ich kolejki. Najpierw określamy decyzje wpływające na sprzęt i wspólną PCB. Szczegóły niezależne od sprzętu można rozwijać później. Pytania pojedyncze z propozycjami służą ustalaniu preferencji, zakresu, brakujących informacji oraz wspólnemu wyborowi ważnych komponentów po przedstawieniu porównania. Obliczenia i propozycje rozwiązań technicznych przygotowuje asystent z uzasadnieniem; właściciel aktywnie uczestniczy w doborze części według powyższej zasady.

Kompletność sprawdzamy według [mapy obszarów i otwartych tematów](requirements/pokrycie-funkcjonalne.md), a nie liczby zadanych pytań. Dla każdego obszaru przeglądamy normalną pracę, rozruch/wyłączenie, granice, brak opcjonalnego wyposażenia, usterki oraz serwis i aktualizację, odpowiednio do jego roli. Zapisujemy wymagania przyjęte, wyłączenia i kwestie otwarte. Każda istotna decyzja otrzymuje źródło; wymagania łączymy dalej z blokiem realizującym i weryfikacją.

Przed zamknięciem architektury, wydaniem PCB i rozpoczęciem prób wykonujemy odpowiedni przegląd pokrycia. Późniejsza zmiana wymaga oceny wpływu na pozostałe urządzenia, I/O, zasoby, dokumentację i testy. Pełny przegląd kompletności oraz szczegółowa macierz realizacji i weryfikacji pozostają do opracowania; sama mapa obszarów ich nie zastępuje.

## Odpowiedzialność za testy

Asystent przygotowuje plan, powiązanie testów z wymaganiami, stanowiska, wyposażenie, procedury, oczekiwane wyniki i kryteria przerwania. Właściciel wykonuje próby fizyczne i przekazuje dane. Asystent analizuje wyniki, wskazuje niezgodności, proponuje poprawki oraz określa potrzebną regresję. [Zasady weryfikacji i szablon procedury](verification/README.md) są miejscem źródłowym dla tego procesu.

Każde wymaganie musi mieć właściwą metodę i dowód potwierdzenia. Funkcje i parametry działania obejmujemy próbami rzeczywistego ECU/HMI/aplikacji; obliczenia i przeglądy uzupełniają weryfikację konstrukcji. Status uzgodnionego wymagania jest odrębny od statusu zweryfikowanego wykonania.
