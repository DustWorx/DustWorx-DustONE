# Macierz wariantów silnika — dane do architektury

Data: 2026-10-18. Status: roboczy podział zakresu, nie lista zatwierdzonych zgodności. Podstawa: [wymagania systemu](../01-zakres-systemu.md). Wspólna, jednakowo obsadzona PCB ma pokrywać uzgodnione warianty; zmienia się konfiguracja i dopuszczalna wiązka.

| Wariant | Podstawa / jednostka referencyjna | Dane decydujące o sprzęcie |
| --- | --- | --- |
| 2T, gaźnik bez TPS | W zakresie; właściciel potwierdził brak TPS w swojej Becie Racing 2015 | Synchronizacja, zapłon, zasilanie, pozostałe czujniki i akcesoria do sprawdzenia. [Analiza instrukcji](../interfaces/beta-2015-analiza-dokumentacji.md) nie potwierdza jeszcze zgodności złączy egzemplarza. |
| 2T, gaźnik z TPS | W zakresie; model referencyjny do wyboru | Jak wyżej oraz interfejs TPS i strategia jego wykorzystania. |
| 4T, gaźnik | W zakresie ogólnej obsługi 4T/gaźnika; model do wyboru | Synchronizacja fazy cyklu i zapłon, wyposażenie czujnikowe i zakres obrotów. |
| 4T, wtrysk, przepustnica na linkę | W zakresie; model do wyboru | Synchronizacja, wtryskiwacze, pompa, zapłon i komplet czujników strategii sterowania; IAC z napędem krokowym w wyposażonych modelach według SYS-071. |
| 2T, TPI, przepustnica na linkę | Cel interfejsów; model/rocznik i zgodność konwersji niepotwierdzone | Wtryskiwacze i pompa, ciśnienia/czujniki, zapłon, synchronizacja; osobno wykonalność smarowania mieszanką. |
| 2T, TBI, przepustnica na linkę | Cel interfejsów; model/rocznik do wyboru | Wtryskiwacze, pompa, czujniki, zapłon i synchronizacja; napęd power valve dla jednostek z takim wyposażeniem. |

Warianty 2T podlegają SYS-032/033 i [ADR-001](../decisions/adr-001-smarowanie-2t-mieszanka.md). Macierz nie potwierdza konwersji TPI przez sam demontaż dozownika. Ride-by-wire pozostaje poza zakresem.

## Dane potrzebne przed zamknięciem architektury

- Wybrać konkretne modele/roczniki i dokumenty referencyjne reprezentujące powyższe warianty. Beta nie jest jedyną podstawą do określenia wspólnego sprzętu.
- Wejście wału obsługuje VR oraz Hall z wyjściem cyfrowym według SYS-069. Dodatkowe wejście fazy 4T obsługuje tylko Hall z wyjściem cyfrowym; czujnik jest opcjonalny w konfiguracjach niewykorzystujących tego sygnału (SYS-070, [ADR-005](../decisions/adr-005-interfejsy-synchronizacji.md)). Ustalić parametry i modele czujników, maksymalne obroty, układy znaczników, odniesienie do GMP oraz zasady synchronizacji i utraty sygnałów.
- Obsługa CDI oraz zapłonu indukcyjnego TCI/IDI jest wymagana według SYS-067 i [ADR-004](../decisions/adr-004-zaplon-cdi-indukcyjny.md). Liczba niezależnych kanałów zapłonu: jeden według SYS-068. Zidentyfikować cewki/moduły referencyjne, parametry i granicę między ECU i ewentualnym zewnętrznym stopniem mocy. Nazwa wariantu silnika nie rozstrzyga interfejsu elektrycznego; zgodność wymaga analizy i testów.
- Ustalić liczbę, typy i równoczesne działanie wtryskiwaczy; parametry pompy i power valve. Nie sumować automatycznie kanałów alternatywnych wariantów.
- Dla IAC z napędem krokowym potwierdzić modele i parametry oraz zgodność według SYS-071 i [ADR-006](../decisions/adr-006-iac-naped-krokowy.md). Ocenić zasoby, kalibrację i pozycjonowanie, czas gotowości do rozruchu oraz wpływ na zarządzanie energią.
- Ustalić wymagane czujniki i ich zakresy, zasilanie, dokładność, zabezpieczenia oraz diagnostykę. Szczegółowe braki: [lista I/O](../interfaces/wstepna-lista-io.md).
- Zamknąć zakres zasilania, warunki rozruchu i równoczesne obciążenia; oddzielnie ocenić kopniak przy osłabionym akumulatorze dla gaźnika i wtrysku.

## Weryfikacja

Beta: pierwsza integracja wariantu zgodnego z zinwentaryzowanym osprzętem. Pozostałe interfejsy: najpierw analiza dokumentacji i próby stanowiskowe; testy na jednostkach reprezentatywnych w późniejszym etapie. Symulacja elektryczna nie zastępuje walidacji sterowania silnikiem ani smarowania. Jeden niezależny kanał zapłonu jest wymagany według SYS-068. Liczby pozostałych kanałów i lista komponentów zostaną określone po zebraniu powyższych danych.
