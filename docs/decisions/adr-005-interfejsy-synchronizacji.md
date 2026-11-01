# ADR-005 — interfejsy synchronizacji silnika

Data: 2026-11-01. Status: zatwierdzony zakres czujników wału; parametry i realizacja otwarte.

## Problem i opcje

Zachowywane czujniki OEM mogą mieć różne interfejsy. Rozważano obsługę indukcyjnych czujników VR i czujników Halla z wyjściem cyfrowym albo jednego rodzaju, z dopuszczeniem wymiany niezgodnego czujnika.

## Decyzja i podstawa zatwierdzenia

W odpowiedzi na pytanie 75 z 2026-11-01 właściciel wybrał obsługę obu rodzajów czujników położenia wału na wspólnej PCB. Wymaganie: [SYS-069](../01-zakres-systemu.md). Zgodność konkretnych czujników OEM wymaga potwierdzenia parametrów oraz analizy i prób.

## Konsekwencje i otwarte dane

- Uwzględnić odpowiednie tory wejściowe i ewentualne zasilanie czujnika, zabezpieczenia, filtrację oraz zasoby czasowe procesora. Liczba pinów i topologia nie zostały wybrane.
- Ustalić modele referencyjne, zakresy i polaryzację sygnałów, interfejsy mas, zasilanie, progi i opóźnienia. Dla VR uwzględnić zakres amplitud od kopania/rozruchu do maksymalnych obrotów; dla Halla także rodzaj wyjścia i wymagane podciąganie.
- Decyzja dotyczy rodzajów czujnika wału. Układy znaczników, ich odniesienie do GMP i obsługiwane dekodery oraz dodatkowe wejście fazy 4T pozostają otwarte. Nie przyjęto automatycznego rozpoznawania rodzaju czujnika.
- Układy wejściowe i ważne elementy wybieramy wspólnie z właścicielem po analizie i porównaniu.

## Proponowana weryfikacja

Dla obu rodzajów przygotować próby stanowiskowe z reprezentatywnymi sygnałami, a następnie rzeczywistymi czujnikami. Potwierdzić poprawną detekcję impulsów oraz określić dopuszczalne opóźnienie i jitter w wymaganym zakresie obrotów, sygnałów i zasilania. Uwzględnić rozruch kopniakiem, zakłócenia, utratę sygnału i ustalone uszkodzenia. Kryteria liczbowe, wyposażenie i procedury powstaną po charakterystyce interfejsów; prób nie wykonano. Wynik dla jednego czujnika nie potwierdza zgodności wszystkich czujników danego rodzaju.

Przykłady dokumentacji interfejsów: [Analog Devices — VR](https://www.analog.com/media/en/technical-documentation/data-sheets/MAX9924-MAX9927.pdf), [Bosch Motorsport — Hall z wyjściem cyfrowym](https://www.bosch-motorsport.com/products/sensors/speed/speed-sensor-hall-effect-mini-ha-p-sealed/). Są to źródła techniczne, nie wybór komponentów DustONE.
