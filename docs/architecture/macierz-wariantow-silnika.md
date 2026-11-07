# Macierz wariantów silnika — dane do architektury

Stan na: 2026-11-07. Część funkcjonalna stanowi wynik zamkniętego F01. Zakres obejmuje wyłącznie silniki chłodzone cieczą (SYS-098). Przydział zasobów i bilanse są materiałem wstępnym na etap 4 w kolejce; tabela nie jest listą zatwierdzonych zgodności. Podstawa: [wymagania systemu](../01-zakres-systemu.md). Wspólna, jednakowo obsadzona PCB ma pokrywać uzgodnione warianty; zmienia się konfiguracja i dopuszczalna wiązka.

| Wariant | Podstawa / jednostka referencyjna | Dane decydujące o sprzęcie |
| --- | --- | --- |
| 2T, gaźnik bez TPS | W zakresie; właściciel potwierdził brak TPS w swojej Becie Racing 2015 | Synchronizacja, zapłon, zasilanie, pozostałe czujniki i akcesoria do sprawdzenia. [Analiza instrukcji](../interfaces/beta-2015-analiza-dokumentacji.md) nie potwierdza jeszcze zgodności złączy egzemplarza. |
| 2T, gaźnik z TPS | W zakresie; model referencyjny do wyboru | Jak wyżej oraz interfejs TPS i strategia jego wykorzystania. |
| 4T, gaźnik | W zakresie ogólnej obsługi 4T/gaźnika; model do wyboru | Synchronizacja fazy cyklu i zapłon, wyposażenie czujnikowe i zakres obrotów. |
| 4T, wtrysk, przepustnica na linkę | W zakresie; model do wyboru | Synchronizacja, wtryskiwacze, pompa, zapłon i komplet czujników strategii sterowania; IAC z napędem krokowym w wyposażonych modelach według SYS-071. |
| 2T, TPI, przepustnica na linkę | Cel interfejsów; model/rocznik i zgodność konwersji niepotwierdzone | Wtryskiwacze i pompa, ciśnienia/czujniki, zapłon, synchronizacja; osobno wykonalność smarowania mieszanką. |
| 2T, TBI, przepustnica na linkę | Cel interfejsów; model/rocznik do wyboru | Wtryskiwacze, pompa, czujniki, zapłon i synchronizacja; napęd power valve dla jednostek z takim wyposażeniem. |

Warianty 2T podlegają SYS-032/033 i [ADR-001](../decisions/adr-001-smarowanie-2t-mieszanka.md). Macierz nie potwierdza konwersji TPI przez sam demontaż dozownika. Ride-by-wire oraz kontrola trakcji (SYS-072) pozostają poza zakresem.

## Dane potrzebne przed zamknięciem architektury

- Wybrać konkretne modele/roczniki i dokumenty referencyjne reprezentujące powyższe warianty. Beta nie jest jedyną podstawą do określenia wspólnego sprzętu.
- Wejście wału obsługuje VR oraz Hall z wyjściem cyfrowym według SYS-069. Dodatkowe wejście fazy 4T obsługuje tylko Hall z wyjściem cyfrowym; czujnik jest opcjonalny w konfiguracjach niewykorzystujących tego sygnału (SYS-070, [ADR-005](../decisions/adr-005-interfejsy-synchronizacji.md)). Ustalić parametry i modele czujników, maksymalne obroty, układy znaczników, odniesienie do GMP oraz zasady synchronizacji i utraty sygnałów.
- Obsługa CDI oraz zapłonu indukcyjnego TCI/IDI jest wymagana według SYS-067 i [ADR-004](../decisions/adr-004-zaplon-cdi-indukcyjny.md). Liczba niezależnych kanałów zapłonu: jeden według SYS-068. Zidentyfikować cewki/moduły referencyjne, parametry i granicę między ECU i ewentualnym zewnętrznym stopniem mocy. Nazwa wariantu silnika nie rozstrzyga interfejsu elektrycznego; zgodność wymaga analizy i testów.
- Ustalić liczbę, typy i równoczesne działanie wtryskiwaczy; parametry pompy i power valve. Nie sumować automatycznie kanałów alternatywnych wariantów.
- Dla IAC z napędem krokowym potwierdzić modele i parametry oraz zgodność według SYS-071 i [ADR-006](../decisions/adr-006-iac-naped-krokowy.md). Ocenić zasoby, kalibrację i pozycjonowanie, czas gotowości do rozruchu oraz wpływ na zarządzanie energią.
- Ustalić wymagane czujniki i ich zakresy, zasilanie, dokładność, zabezpieczenia oraz diagnostykę, w tym opcjonalny czujnik rezerwy paliwa według SYS-073. Jego rodzaj i interfejs trzeba potwierdzić; stan rezerwy nie określa typu wejścia sprzętowego. Szczegółowe braki: [lista I/O](../interfaces/wstepna-lista-io.md).
- Zamknąć zakres zasilania, warunki rozruchu i równoczesne obciążenia; oddzielnie ocenić kopniak przy osłabionym akumulatorze dla gaźnika i wtrysku.

## Weryfikacja

Beta: pierwsza integracja wariantu zgodnego z zinwentaryzowanym osprzętem. Pozostałe interfejsy: najpierw analiza dokumentacji i próby stanowiskowe; testy na jednostkach reprezentatywnych w późniejszym etapie. Symulacja elektryczna nie zastępuje walidacji sterowania silnikiem ani smarowania. Jeden niezależny kanał zapłonu jest wymagany według SYS-068. Liczby pozostałych kanałów i lista komponentów zostaną określone po zebraniu powyższych danych.

## Funkcje silnika według wariantu

Oznaczenia: **R** — funkcja wymagana w tym wariancie; **W** — obsługa, jeżeli wybrany osprzęt jej wymaga; **O** — opcjonalny sygnał, praca bez niego dopuszczalna; **D** — potrzeba/interfejs do ustalenia z dokumentacji i strategii; **—** — poza funkcją danego wariantu. Tabela jest przydziałem funkcji, bez deklaracji wyposażenia konkretnego motocykla.

| Funkcja | 2T gaźnik bez TPS | 2T gaźnik z TPS | 4T gaźnik | 4T wtrysk | 2T TPI | 2T TBI |
| --- | --- | --- | --- | --- | --- | --- |
| Wał: VR lub cyfrowy Hall, według czujnika | R | R | R | R | R | R |
| Dodatkowa faza 4T: cyfrowy Hall | — | — | O | O | — | — |
| Jeden kanał zapłonu; CDI lub TCI/IDI według osprzętu | R | R | R | R | R | R |
| Odczyt TPS | — | R | W | W | W | W |
| Sterowanie wtryskiwaczami | — | — | — | R | R | R |
| Sterowanie pompą układu wtryskowego | — | — | — | R | R | R |
| IAT do kompensacji wtrysku | — | — | — | R | R | R |
| Barometr na PCB do kompensacji wtrysku | — | — | — | R | R | R |
| MAP z czujnika zewnętrznego, zgodnie z konfiguracją | W | W | W | W | W | W |
| Ciśnienie skrzyni korbowej 2T — CCPS, zgodnie z konfiguracją | W | W | — | — | W | W |
| Pomiar temperatury płynu w silniku chłodzonym cieczą | R | R | R | R | R | R |
| Elektroniczny power valve, jeżeli występuje | W | W | — | — | W | W |
| IAC z napędem krokowym według SYS-071 | — | — | — | W | — | — |
| Tor wartości ciśnienia paliwa | — | — | — | W | W | W |
| Binarne ciśnienie oleju, zgodnie z wyposażeniem | W | W | W | W | W | W |

F01: [MAP](../interfaces/cisnienie-dolotu-map.md) przyjęto w SYS-096, odpowiedź A na pytanie 105. Użycie zależy od konfiguracji; nie wybrano czujnika, parametrów ani liczby fizycznych kanałów. [CCPS](../interfaces/cisnienie-skrzyni-korbowej.md) przyjęto w SYS-097. Zakres ograniczono do chłodzenia cieczą z pomiarem temperatury płynu (SYS-044/098), odpowiedź B na pytanie 107; [przegląd pomiarów](../requirements/f01-pomiary-silnika.md).

Faza 4T jest opcjonalna w konfiguracjach niewykorzystujących tego sygnału; dopuszczone strategie bez fazy muszą być określone i sprawdzone. Symbol W/D nie potwierdza danego typu osprzętu w enduro. Każdy taki przypadek wymaga źródła model/rocznik przed przyjęciem parametrów sprzętu. MAP i CCPS są przyjętymi możliwościami według SYS-096/097; nie wybrano liczby kanałów ani fizycznego podziału torów.

Wspólne dla platformy pozostają także funkcje motocykla: START/STOP, dwa hamulce, koło i ODO, wykrywanie przewrócenia, napięcie akumulatora, temperatura ECU, opcjonalne sprzęgło/biegi/rezerwa, CAN, HMI i serwis. Ich zakres określa [lista I/O](../interfaces/wstepna-lista-io.md). Obecność funkcji na PCB nie oznacza obowiązku podłączenia każdego opcjonalnego czujnika.

## Pierwszy przydział zasobów sprzętowych

| Funkcja / grupa | Co jest już ustalone | Czego jeszcze nie wolno zamknąć |
| --- | --- | --- |
| Synchronizacja wału | Jeden funkcjonalny tor wału dla alternatywnych VR/Hall. | Liczba pinów i elementów kondycjonujących, częstotliwości/granice czasu, progi i dekodery. |
| Faza 4T | Dodatkowe, odrębne wejście cyfrowego Halla; nie współdzieli funkcji wału. | Parametry elektryczne, zasilanie i strategia użycia. |
| Zapłon | Jeden niezależnie wyzwalany kanał; wybrany tryb CDI albo TCI/IDI. | Liczba fizycznych torów mocy/wyprowadzeń, integracja, zasilanie i zabezpieczenia. |
| Wtrysk | Obsługa uzgodnionych wariantów wtryskowych. | Liczba kanałów, rodzaj drivera, prąd, czasy i równoczesność; nie wynika z liczby cylindrów. |
| Pompa paliwa | Sterowanie w wariantach wtryskowych. | Wyjście mocy lub sterujące, prąd rozruchowy i po zatrzymaniu/zwarciu. |
| Power valve i IAC | Obie funkcje mają być obsługiwane na tej samej obsadzie PCB. | Typ/zasoby driverów, liczba linii i możliwość ich współdzielenia. |
| Hamulce | Dwa rozróżniane wejścia przewodowe ECU. | Typy wejść i sygnałów, obwód lampy, diagnostyka i filtry. |
| Ruch koła | Tor ECU zdolny do detekcji w śnie i naliczania drogi także bez pracy silnika/HMI. | Interfejs czujnika, pobór i zachowanie pierwszych impulsów. |
| Pomiary | Zestaw funkcji z listy I/O, w tym barometr i temperatura ECU na PCB. | Liczba ADC/pinów/zasilaczy czujników, rozdzielczość i błędy torów. |
| Akcesoria i HMI | Zdefiniowane funkcje oraz sterowany tor zasilania HMI. | Liczba wyjść, prądy, podział high-side/low-side, ciepło i granice awaryjne. |
| CAN i PC | CAN ECU–HMI oraz jeden przewodowy punkt standardowej obsługi obu urządzeń. | Liczba kontrolerów/transceiverów/interfejsów, przepustowość i lokalizacja mostka. |
| Mapy, dane i zegar | Maks. trzy niezależne, kompletne zestawy uzgodnionych map (SYS-028), strojenie na żywo SYS-094, robocza edycja aktywnego i nieaktywnych zestawów bez przełączenia SYS-101, transfer/wdrożenie krytycznej konfiguracji po zgaszeniu z blokadami SYS-102, anulowanie nieukończonego transferu i nowa próba rozruchu SYS-103, samodzielne dokończenie wdrożenia mimo utraty Windows SYS-104, potwierdzony powrót do poprzedniej konfiguracji po błędzie lub blokady i dostęp serwisowy SYS-105, odtworzenie poprawnej konfiguracji po zaniku zasilania SYS-106, pełny zestaw map przyjmowany i roboczo zastępowany tylko po zgaszeniu SYS-107, trwały zapis wybranego zestawu lub wszystkich skonfigurowanych SYS-108, odzyskanie jednej kompletnej grupy map po zaniku zasilania SYS-109, blokada rozruchu podczas pełnej podmiany i zapisu map SYS-110, powrót do zapisanych map i flaga błędu sumy SYS-111, kasowanie flagi po zweryfikowanym zapisie SYS-112, dokończenie przyjętego zapisu po utracie Windows SYS-113, anulowanie niepełnego transferu map SYS-114, odczyt stanu map i statusu operacji po ponownym połączeniu SYS-115, spójne zastosowanie całej poprawnej grupy zmian SYS-116, robocze przywrócenie wybranego zestawu z zapisu SYS-117, pojedyncze nastawy wspólne dla zestawów SYS-118, mapa położenia zadanego zaworu wydechowego w zestawach wyposażonego 2T SYS-119, odtworzenie ostatniego prawidłowego wyboru po restarcie SYS-099, odrzucenie roboczej edycji po prawidłowym śnie SYS-100, DTC i chronione liczniki. | Wielkości pamięci, organizacja dostępu i zapisów, zasoby czasowe oraz mechanizmy ochrony. |

To wejście do bilansu, nie liczbowy bilans MCU ani pinout. Najpierw uzupełniamy parametry i jednoczesność, następnie porównujemy procesory i układy z właścicielem.

## Jednoczesność i obciążenia do policzenia

| Scenariusz | Co uwzględnić równocześnie |
| --- | --- |
| Rozruch elektryczny | Spadek napięcia przy rozruszniku, ECU i wymagane czujniki, zapłon, a dla wtrysku pompa/wtryskiwacze; gotowość power valve/IAC według osprzętu. HMI nie warunkuje rozruchu. |
| Kopniak z osłabionym akumulatorem | Detekcja i czas gotowości ECU, energia zapłonu i ewentualnego układu wtrysku, zachowanie przy kolejnych ruchach kopniaka. |
| Jazda / strojenie na żywo | Maksymalne zdarzenia silnikowe, pomiary, napędy, aktualnie wymagane akcesoria, CAN/HMI, przyjęcie zmian map i diagnostyka. Policzalne granice wymagają modeli i zakresów pracy. |
| Silnik zatrzymany, system aktywny | Wentylator po zgaszeniu, stany świateł/wyjść, HMI i zapis danych; limity czasu/napięcia i przejście do snu. |
| Sen przez 28 dni | Pełny pobór ECU/HMI przy normalnie włączonym zasilaniu HMI, czujnik koła i wszystkie tory wybudzania, pamięć/czas i pozostała instalacja. Podstawa: [budżet postoju](budzet-energii-postoju.md). |
| Obsługa Windows / aktualizacja | Oba urządzenia wybudzone, komunikacja i pamięć, wymagane zasilanie warsztatowe/akumulator; osobno dopuszczone testy obciążeń. |
| Usterka / odzyskiwanie | Dopuszczone stany wyjść, ograniczenia przeciążenia i temperatury, zanik CAN/HMI/PC, częściowe zasilanie oraz restart. |

Warianty silnika są alternatywnymi konfiguracjami jednego ECU: nie sumujemy ich automatycznie. Współdzielenie zasobów wolno przyjąć dopiero po wykazaniu zgodności wszystkich dopuszczonych trybów, w tym rozruchu, serwisu i resetu, oraz właściwego stanu nieużywanych wyjść.

Stan: F01 zamknięty w zakresie funkcji; [wynik przeglądu i przekazanie danych](../requirements/f01-sterowanie-silnikiem.md). Modele poza Betą, parametry, prądy/liczby fizycznych kanałów, algorytmy i bilanse pozostają na etapy 3–4. G1 pozostaje otwarta; zgodności modeli jeszcze nie potwierdzono.
