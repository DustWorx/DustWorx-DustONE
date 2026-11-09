# ADR-005 — interfejsy synchronizacji silnika

Data decyzji 2026-11-01. Uzupełnienie 2026-11-09. Zatwierdzono zakres wejść wału i fazy 4T oraz reakcje na utratę synchronizacji podczas pracy i rozruchu elektrycznego. Parametry i realizacja są otwarte.

## Problem i opcje

Zachowywane czujniki OEM mogą mieć różne interfejsy. Rozważano obsługę indukcyjnych czujników VR i czujników Halla z wyjściem cyfrowym albo jednego rodzaju, z dopuszczeniem wymiany niezgodnego czujnika.

## Decyzja i podstawa zatwierdzenia

W odpowiedzi na pytanie 75 z 2026-11-01 właściciel wybrał obsługę obu rodzajów czujników położenia wału na wspólnej PCB. Wymaganie: [SYS-069](../01-zakres-systemu.md). Zgodność konkretnych czujników OEM wymaga potwierdzenia parametrów oraz analizy i prób.

W odpowiedzi na pytanie 76 z 2026-11-01 właściciel wybrał dodatkowe, opcjonalne wejście fazy 4T tylko dla czujnika Halla z wyjściem cyfrowym. Rozważano wejście VR/Hall, wejście wyłącznie Hall lub brak dodatkowego wejścia. Wymaganie: SYS-070. Czujnik fazy jest opcjonalny w konfiguracjach niewykorzystujących tego sygnału; obsługa VR na wejściu fazy pozostaje poza zakresem.

W odpowiedzi **A na pytanie 167** (2026-11-09) właściciel zatwierdził odcięcie po potwierdzonej utracie synchronizacji wału podczas pracy. Powrót sygnału przed zatrzymaniem utrzymuje odcięcie. Zapłon i wtrysk mogą wznowić się w nowej świadomej próbie rozruchu po zatrzymaniu i ponownej wiarygodnej synchronizacji, przy spełnieniu pozostałych warunków (SYS-157). [Macierz F03 i plan próby](../requirements/f03-ochrona-i-usterki.md).

W odpowiedzi **A na pytanie 168** (2026-11-09) właściciel zatwierdził wyłączenie rozrusznika po potwierdzonej utracie wcześniej uzyskanej synchronizacji przed rozpoznaniem pracy silnika. Nowa próba elektryczna wymaga zatrzymania oraz zwolnienia i ponownego naciśnięcia START. Zapłon i wtrysk w nowej próbie wymagają wiarygodnej synchronizacji (SYS-158). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md).

## Konsekwencje i otwarte dane

- Uwzględnić odpowiednie tory wejściowe i ewentualne zasilanie czujnika, zabezpieczenia, filtrację oraz zasoby czasowe procesora. Liczba pinów i topologia nie zostały wybrane.
- Ustalić modele referencyjne, zakresy i polaryzację sygnałów, interfejsy mas, zasilanie, progi i opóźnienia. Dla VR uwzględnić zakres amplitud od kopania/rozruchu do maksymalnych obrotów; dla Halla także rodzaj wyjścia i wymagane podciąganie.
- Zakresy wejść są odrębne: wał VR/Hall (SYS-069), faza 4T tylko Hall z wyjściem cyfrowym (SYS-070). Układy znaczników, ich odniesienie do GMP, obsługiwane dekodery oraz kryteria wykrycia utraty i odzyskania synchronizacji pozostają do określenia. Rozruch kopniakiem i utrata fazy są w F03. Nie przyjęto automatycznego rozpoznawania rodzaju czujnika.
- Układy wejściowe i ważne elementy wybieramy wspólnie z właścicielem po analizie i porównaniu.

## Proponowana weryfikacja

Dla obu rodzajów przygotować próby stanowiskowe z reprezentatywnymi sygnałami, a następnie rzeczywistymi czujnikami. Potwierdzić poprawną detekcję impulsów oraz określić dopuszczalne opóźnienie i jitter w wymaganym zakresie obrotów, sygnałów i zasilania. Uwzględnić rozruch kopniakiem, zakłócenia, utratę sygnału i ustalone uszkodzenia. Kryteria liczbowe, wyposażenie i procedury powstaną po charakterystyce interfejsów; prób nie wykonano. Wynik dla jednego czujnika nie potwierdza zgodności wszystkich czujników danego rodzaju.

Dla wejścia fazy przygotować próby z sygnałem Halla równolegle z sygnałem wału: potwierdzić rozpoznawanie fazy pełnego cyklu 4T oraz pracę konfiguracji niewykorzystującej czujnika fazy przy jego braku. Brak opcjonalnego czujnika sprawdzać oddzielnie od utraty/uszkodzenia sygnału czujnika zadeklarowanego w konfiguracji jako używany; reakcje ustalić przed próbami. Dobór wspólnych lub odrębnych torów zasilania i progów dla obu wejść wynika z analizy czujników.

Przykłady dokumentacji interfejsów: [Analog Devices — VR](https://www.analog.com/media/en/technical-documentation/data-sheets/MAX9924-MAX9927.pdf), [Bosch Motorsport — Hall z wyjściem cyfrowym](https://www.bosch-motorsport.com/products/sensors/speed/speed-sensor-hall-effect-mini-ha-p-sealed/). Są to źródła techniczne, nie wybór komponentów DustONE.

Podstawa techniczna rozpoznawania fazy pełnego cyklu przez dodatkowy sygnał: [Haltech — Trigger, Home Signal](https://support.haltech.com/portal/en/kb/articles/trigger-elite). Nie przyjmujemy ustawień ani ograniczeń tego ECU jako specyfikacji DustONE.
