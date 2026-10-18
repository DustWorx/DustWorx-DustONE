# Beta - czujnik temperatury B57301K0103A001

Data: 2026-10-18. Status: zidentyfikowany przez właściciela element istniejącego zestawu; kandydat do integracji prototypu, bez zatwierdzenia jako docelowego komponentu DustONE. Powiązania: SYS-043/044 w [zakresie systemu](../01-zakres-systemu.md).

## Ustalenia właściciela

Sterownik wentylatora jest własnym projektem właściciela. Wykorzystuje czujnik B57301K0103A001 i załącza wentylator automatycznie, bez ręcznego włącznika. Miejsce montażu czujnika, połączenia, schemat i parametry istniejącego sterownika nie zostały jeszcze przekazane.

## Dane producenta

Źródło: [TDK/EPCOS, K301-A001, dokument datowany January 2018, s. 2-4](https://product.tdk.com/system/files/dam/doc/product/sensor/ntc/ntc_assy/data_sheet/50/db/ntc/ntc_probe_ass_k301_a001.pdf), sprawdzono 2026-10-18.

| Parametr | Wartość dokumentowa |
| --- | --- |
| Typ | NTC, zespół pomiarowy K301-A001 |
| Rezystancja znamionowa | 3000 Ω przy 60°C; tolerancja ±2% |
| Rezystancja przy 25°C | 9959 Ω |
| Charakterystyka R/T | Nr 2908 |
| B25/100 | 3460 K ±1% |
| Maksymalna temperatura pracy | 110°C |
| Stała czasowa w wodzie | Około 5 s |
| Moc maksymalna przy 25°C | 375 mW; nie jest to docelowa moc pomiarowa |
| Obudowa / mocowanie | Niklowany mosiądz, G1/8 według ISO 228/1, uszczelnienie O-ring |

Producent opisuje sondę zanurzeniową do urządzeń wodnych; podaje również próby cykli temperatury metalowej głowicy w mieszaninie glikolu etylenowego i wody. [Strona produktu TDK](https://product.tdk.com/en/search/sensor/ntc/ntc_assy/info?part_no=B57301K0103A001) wskazuje brak kwalifikacji AEC-Q200. Zgodność z konkretnym płynem, ciśnieniem, montażem i warunkami enduro wymaga oceny zastosowania.

## Wnioski do projektu wejścia ECU

- Rodzaj sygnału pozwala rozpatrzyć rezystancyjny tor NTC. Dokładna charakterystyka musi być przypisana do numeru części; ogólne określenie „NTC 10 kΩ” jest niewystarczające do kalibracji.
- Wymagany zakres temperatur pomiaru i dopuszczalne warunki pracy silnika trzeba porównać z limitem 110°C tego zespołu. Tabela R/T obejmująca wyższe temperatury nie rozszerza dopuszczalnego zakresu pracy sondy.
- Do ustalenia: pobudzenie, rezystor odniesienia, tor ADC, filtracja, zabezpieczenia i wykrywanie przerwy/zwarcia. Sprawdzić budżet błędu, samonagrzewanie, tolerancje i opóźnienie całego pomiaru; ±2% rezystancji nie oznacza ±2°C.
- Po poznaniu schematu istniejącego sterownika określić docelowe połączenie czujnika z ECU i dalszą rolę obecnego modułu. Nie zatwierdzono współdzielenia jednego NTC przez dwa tory pomiarowe.
- Powiązać interpretację wskazania i progi wentylatora z miejscem pomiaru. Do czasu potwierdzenia montażu nie określono, czy czujnik mierzy płyn bezpośrednio.

Nie dobrano elementów wejścia ADC ani wartości progów. Obsługa tego czujnika w Becie nie ogranicza docelowej zgodności ECU do jednego typu NTC.
