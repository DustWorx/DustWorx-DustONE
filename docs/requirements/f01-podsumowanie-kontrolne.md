# F01 — podsumowanie kontrolne ustaleń

Stan na: 2026-11-04. **Kontrola F01 zakończona; właściciel potwierdził zgodność całości i dalszą pracę. F01 zamknięty 2026-11-04.** Reguły map i konfiguracji są rozwijane odrębnie w F02. Podsumowanie nie zmienia wymagań; źródłem pozostaje [rejestr SYS](../01-zakres-systemu.md) i [ADR](../decisions/README.md).

## 1. Zakres silników i integracji

- Jeden cylinder, 2T albo 4T; **wyłącznie chłodzenie cieczą**, z pomiarem temperatury płynu (SYS-001/002/044/098).
- Jedna, jednakowo obsadzona PCB dla całego przyjętego zakresu, bez przeróbek PCB i wymiany komponentów między wariantami. Zastosowanie wybieramy konfiguracją; wiązka może być inna (SYS-003/015/045).
- Osprzęt i czujniki OEM zachowujemy w możliwie dużym stopniu, po potwierdzeniu interfejsów. Nowa wiązka i złącze ECU są dopuszczone.
- Instalacja nominalnie 12 V, akumulator AGM lub LiFePO4 na wspólnej PCB; zakresy napięć i profile wymagają późniejszej specyfikacji (SYS-013/092).
- Pierwszy motocykl: Beta 300 RR Racing 2015, gaźnik bez TPS. Pozostałe konfiguracje wymagają osobnego sprawdzenia; Beta nie ogranicza zakresu PCB.
- Przeznaczenie projektu: prototyp do sportu i testów poza drogami publicznymi.

| Klasa zastosowania | Zakres |
| --- | --- |
| 2T, gaźnik bez TPS | Obsługa bez wymaganego TPS. |
| 2T, gaźnik z TPS | Obsługa odczytu TPS. |
| 4T, gaźnik | W zakresie platformy. |
| 4T, wtrysk | Przepustnica mechaniczna na linkę. |
| 2T, TPI | Cel obsługi z warunkami smarowania i kwalifikacji poniżej. |
| 2T, TBI | W zakresie docelowej obsługi; zgodność osprzętu do potwierdzenia. |

## 2. Sterowanie silnikiem

| Funkcja | Ustalenie |
| --- | --- |
| Zapłon | **Jeden niezależny kanał**, obsługa CDI oraz indukcyjnego TCI/IDI; zgodność cewek i realizacja stopni mocy wymagają analizy/testów (SYS-067/068). |
| Wtrysk i pompa paliwa | Sterowanie dla przyjętych konfiguracji wtryskowych. Liczby kanałów, parametry i topologie wynikną z danych osprzętu (SYS-012/015). |
| Power valve 2T | Sterowanie elektronicznym zaworem wydechowym w wyposażonych konfiguracjach; typy napędów i sygnały później (SYS-034). |
| IAC 4T | Regulacja powietrza biegu jałowego z napędem krokowym dla potwierdzonych modeli. Konfiguracje bez IAC działają bez napędu (SYS-071). |
| Przepustnica | Poruszana mechanicznie linką; TPS odczytywany, jeżeli występuje (SYS-014/038). |
| Autonomia ECU | Silnik działa bez HMI, także od włączenia oraz po utracie CAN. Dane wymagane do jego sterowania i ochrony są dostępne ECU bez HMI (SYS-046/047). |

## 3. Pomiary i wejścia silnikowe

| Sygnał | Ustalenie |
| --- | --- |
| Wał korbowy | Obsługa VR i cyfrowego Halla na wspólnej PCB (SYS-069). |
| Faza cyklu 4T | Dodatkowe, odrębne wejście cyfrowego Halla; opcjonalne zależnie od konfiguracji, bez obsługi VR na tym wejściu (SYS-070). |
| TPS | Odczyt w wyposażonych konfiguracjach; gaźnik bez TPS pozostaje obsługiwany. |
| IAT | Temperatura dolotu z czujnika OEM lub dodatkowego, do kompensacji wtrysku (SYS-031). |
| Płyn chłodzący | Pomiar wartości temperatury i dane do HMI; konfigurowalne progi wentylatora (SYS-044). |
| Barometr | Ciśnienie atmosferyczne mierzone na PCB do kompensacji wtrysku (SYS-030). |
| Temperatura ECU | Osobny pomiar na PCB; odrębna wielkość od IAT (SYS-030/031). |
| MAP | Odczyt ciśnienia bezwzględnego dolotu z kompatybilnego czujnika OEM lub dodatkowego (SYS-096). |
| CCPS | Odczyt ciśnienia gazów w skrzyni korbowej 2T z kompatybilnego czujnika (SYS-097). |
| Ciśnienie paliwa | Pomiar wartości ciśnienia (SYS-029). |
| Ciśnienie oleju | Sygnał binarny: obecne / brak ciśnienia (SYS-029). |
| Napięcie akumulatora | Bieżący nadzór; przyjęte osobne profile AGM/LiFePO4 (SYS-084/092). |

MAP i CCPS nie są obowiązkowe do podłączenia w konfiguracjach, które nie wymagają danego pomiaru. Lista funkcji nie przesądza liczby fizycznych pinów ani możliwości współdzielenia torów.

## 4. Rozruch, STOP i przewrócenie

- START jest przewodowym wejściem ECU, niezależnym od HMI/CAN. Rozrusznik działa podczas przytrzymywania; puszczenie kończy sterowanie (SYS-048).
- ECU odłącza rozrusznik po potwierdzeniu pracy silnika lub przekroczeniu maksymalnego czasu kręcenia. Kolejna próba wymaga puszczenia i ponownego naciśnięcia START (SYS-049).
- STOP ma osobny obwód gaszenia niezależny od HMI/CAN. Szczegółowa realizacja elektryczna i reakcje na uszkodzenie przewodów pozostają do projektu (SYS-037).
- Przyciski obsługi HMI i przełączniki akcesoriów pozostają podłączone do HMI; żądania trafiają do ECU przez CAN (SYS-016).
- Potwierdzone przewrócenie powoduje wyłączenie silnika. Po postawieniu i spełnieniu warunków możliwy jest świadomy ponowny rozruch START/kopniakiem, bez wyłączania zasilania (SYS-039/040).
- Opcjonalne sprzęgło i czujnik poszczególnych biegów służą do danych/wskazań, bez zależnych od nich blokad rozrusznika (SYS-041).
- Cel rozruchu kopniakiem z osłabionym akumulatorem zakłada podłączony akumulator z energią dla ECU i niezbędnego osprzętu. Granice napięć i próby pozostają do określenia.

## 5. Smarowanie 2T i wyłączenia

**2T pracuje na mieszance paliwowo-olejowej w zbiorniku.** ECU nie steruje dozownikiem oleju; montaż w motocyklu z dozownikiem wymaga jego sprzętowego usunięcia i odpowiedniego przystosowania układu paliwowego/smarowania (SYS-032/033).

**Konwersja TPI nie ma jeszcze potwierdzonej wykonalności dla konkretnego modelu. Sam demontaż pompy nie potwierdza poprawnego smarowania.** Obsługa TPI jest celem zakresu, z warunkiem oceny i walidacji przed deklaracją zgodności.

Poza zakresem pozostają: chłodzenie powietrzem, ride-by-wire, dwa niezależne kanały zapłonu, quickshifter, kontrola trakcji, dozownik oleju 2T, wejście stopki bocznej oraz zintegrowane tory pomiarowe lambda/EGT. Zewnętrzne pomiary podczas strojenia pozostają przyjętym kierunkiem.

## 6. Przekazanie do dalszych pakietów i etapów

- F02: szczegółowa zawartość map i operacje konfiguracji/edycji. Ustalenia 101–104 są zachowane; aktualne reguły F02, w tym późniejsze odpowiedzi, mają źródło w [specyfikacji map](../interfaces/mapy-i-konfiguracja.md).
- F03/F04: pełne reakcje na usterki, wyjątki rozruchu, ochrona oraz reguły akcesoriów. Przyjęte już funkcje i reguły pozostają w wymaganiach.
- Etapy 3–4: modele referencyjne, parametry czujników/cewek/napędów, liczby i jednoczesność kanałów, dekodery, algorytmy, prądy, energia, czasy i bilanse.
- Etap 6: wspólny wybór ważnych komponentów i obwodów. MCU, czujniki na PCB i drivery nie zostały wybrane przez zamknięcie zakresu funkcji.
- Testy: asystent przygotowuje właściwe procedury i kryteria, właściciel wykonuje próby. Brak wyników produktu; wymagania pozostają niezweryfikowane na wykonanym ECU.

Właściciel potwierdził zgodność całego F01 i polecił kontynuację w rozmowie 2026-11-04. Kontrolę zakończono bez zmiany wymagań; F02 jest aktywny zgodnie z kolejnością procesu. Dalsze decyzje F02 są zapisywane w jego specyfikacji.
