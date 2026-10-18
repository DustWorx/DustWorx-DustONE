# Beta 300 RR Racing 2015 — plan inwentaryzacji

Data: 2026-10-18. Status: plan wstępny; nie wykonano pomiarów. Cel: dane do [listy I/O](../interfaces/wstepna-lista-io.md), zasilania i integracji, a nie potwierdzenie zgodności gotowego ECU.

## Dostępne wyposażenie

Właściciel potwierdził następujące wyposażenie:

| Przyrząd / sonda | Dostępność według właściciela | Stan danych |
| --- | --- | --- |
| Multimetr | Dostępny | Model, zakresy i parametry do określenia. |
| Rigol DHO804 | Dostępny | Seria DHO800 ma nieizolowane wejścia ze wspólną masą, powiązaną z masami interfejsów; uwzględnić instrukcję i cały układ połączeń [1]. |
| Rigol PVP3150 | 4 szt., przełączane ×1/×10 | Instrukcja podaje: ×1 — 20 MHz, 150 V RMS CAT II; ×10 — 150 MHz, 300 V RMS CAT II. Obowiązuje obniżanie dopuszczalnego napięcia wraz z częstotliwością [2]. |
| P4100 | 3 szt., według właściciela ×100, 2 kV, 100 MHz | Producent i instrukcja nieznane; warunki napięcia znamionowego, pasmo, kompensacja i ograniczenia impulsowe niezweryfikowane. |

Nie potwierdzono dostępności sondy różnicowej/izolowanej ani prądowej. Samo tłumienie ×100 i oznaczenie 2 kV nie potwierdzają izolacji ani przydatności do konkretnego punktu zapłonu.

## Kolejność prac

Właściciel potwierdził 2026-10-18, że sterownik wentylatora wykonał samodzielnie i zastosował czujnik [B57301K0103A001](../interfaces/beta-czujnik-temperatury-b57301k0103a001.md). Sterowanie obecnie automatyczne, bez ręcznego włącznika. W INV-01 zebrać schemat modułu, oznaczenia wentylatora, miejsce montażu czujnika i połączenia. Następnie ocenić wykorzystanie NTC do pomiaru temperatury płynu, zabezpieczenia i prądy roboczy/rozruchowy wentylatora (INV-06). Dokumentacja czujnika jest rozpoznana; nie przeprowadzono weryfikacji montażu ani pomiarów.

| Etap | Zakres | Wynik |
| --- | --- | --- |
| INV-01 | Oznaczenia motocykla, gaźnika, modułu zapłonowego, cewki, regulatora, akumulatora i dostępnych czujników; fotografie złączy, liczba styków i przebieg wiązki. | Karta osprzętu: oznaczenie, lokalizacja, złącze, źródło identyfikacji i status potwierdzenia. |
| INV-02 | Zebranie instrukcji rocznika/modelu i schematu, sprawdzenie zgodności z wyposażeniem egzemplarza. | Lista dokumentów z rewizją i stronami; mapa obwodów, bez zgadywania pinów według koloru przewodu. |
| INV-03 | Oględziny i pomiary nieaktywnej instalacji według potwierdzonego schematu; ustalenie połączeń mas i styków przełączników. | Mapa połączeń i stanów. Ciągłość/rezystancję badać wyłącznie w odpowiednio odłączonych, pozbawionych zasilania obwodach. |
| INV-04 | Po identyfikacji punktów i przyrządów: plan pomiaru napięcia akumulatora, zasilania odbiorników i spadków podczas rozruchu. | Przebiegi z warunkami, minimum napięcia i czasem spadku; identyfikacja obwodów AC/DC. |
| INV-05 | Po ustaleniu toru pomiarowego: charakterystyka sygnału synchronizacji podczas kopania/rozruchu i pracy silnika. | Amplituda, polaryzacja, kształt i odstępy impulsów, odniesienie pomiaru i warunki. |
| INV-06 | Po identyfikacji odbiorników: charakterystyki obciążeń świateł, klaksonu, wentylatora i toru sterowania rozrusznikiem, o ile są dostępne. | Prądy robocze, rozruchowe, czas pracy i równoczesność; podstawa do doboru SmartFET-ów i złączy. |
| INV-07 | Pomiar dostępnej przestrzeni, prowadzenia wiązki, mocowań i otoczenia cieplnego. | Obrys instalacyjny ECU i HMI z miejscem na złącza, przewody i dostęp montażowy. |

Etapy INV-04–06 wymagają osobnych instrukcji z konkretnymi punktami, zakresem i sposobem podłączenia po otrzymaniu danych z INV-01–03 oraz modeli przyrządów. Ten dokument nie jest instrukcją podłączenia sond do zapłonu. Prądów rozruchowych odbiorników nie uznajemy za zmierzone samym oscyloskopem; może być potrzebna sonda prądowa lub odpowiednio zaprojektowany tor pomiarowy.

## Warunki opracowania pomiarów przebiegów

Sprawdzić wspólne masy kanałów, uziemienie, połączenia USB/ładowarek i limity przyrządu oraz sond. Uziemienie wykonać zgodnie z instrukcją DHO800; zasilanie USB-C nie oznacza izolacji wejść [1]. Nie łączyć zacisków masy sond z punktami o różnych potencjałach. Zwykła sonda nie jest automatycznie odpowiednia do wyjścia CDI, uzwojenia wzbudzającego ani wtórnego obwodu zapłonu. Właściwe połączenia i osprzęt określimy dla rozpoznanego układu. Zasada ogólna: [Tektronix — pomiary pływające i ochrona operatora](https://www.tek.com/en/datasheet/floating-measurements-selection-guide).

1. [Rigol — DHO800 Quick Guide, rozdział 1.1](https://www.rigol.com/dam/global/downloads/brochures/en/quick-guide/oscilloscopes/DHO800_QuickGuide_EN.pdf): nieizolowane wejścia i masy interfejsów; instrukcja jest podstawą połączeń przyrządu.
2. [Rigol — PVP3150 User Guide, strony 2–3](https://www.rigol.com/dam/global/downloads/brochures/en/user-manual/probes/PVP3150UserGuide_CNEN.pdf): parametry w zależności od tłumienia i wykres obniżania dopuszczalnego napięcia z częstotliwością. Parametry sondy nie są parametrami całego toru oscyloskop–sonda.

## Dokumentacja źródłowa i zapis wyników

Właściciel przekazał 2026-10-18 instrukcję użytkownika RR 250-300 2T i suplement Racing. Przeanalizowano dane techniczne, legendy i schematy; [wyniki, identyfikacja kopii i lista punktów do przygotowania pomiarów](../interfaces/beta-2015-analiza-dokumentacji.md) są osobnym opracowaniem. Suplement w treści ma oznaczenie MY14 mimo nazwy pliku wskazującej 2015. Właściciel potwierdził brak TPS w swoim gaźniku. Zgodność dokumentacji z rzeczywistymi złączami i osprzętem pozostaje do sprawdzenia; INV-02 nie jest jeszcze zamknięty.

[Indeks Beta Motorcycles Australia](https://www.betamotor.com.au/support/off-road/) wymienia instrukcję serwisową 2015 250/300 RR/RACING 2T, instrukcję użytkownika 2015 RR 2T i suplement Race 2T. Podczas sprawdzenia 2026-10-18 odsyłacze przekierowywały do logowania SharePoint. Analizę oparto na lokalnych plikach właściciela wskazanych w opracowaniu, nie na niedostępnych plikach z indeksu. Nie przenosimy danych innego rocznika na egzemplarz właściciela bez potwierdzenia.

Dla każdego pomiaru zapisać: obiekt i oznaczenia styków, warunki, przyrząd/sondę, odniesienie masy, tłumienie, ustawienia rejestracji, jednostki, wynik i plik źródłowy. Odróżniać dane producenta, deklarację właściciela, pomiar i hipotezę. Kryteria oceny ustalimy przed daną próbą; nie ma jeszcze wyników ani potwierdzonych parametrów elektrycznych.
