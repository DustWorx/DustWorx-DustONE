# Wyjścia akcesoriów — porównanie realizacji

Data: 2026-10-18. Status: preferencja właściciela — SmartFET-y na PCB ECU; dobór elementów, podział kanałów i wykonalność pełnej integracji pozostają do analizy.

Zakres: światła, wentylator, klakson i pozostałe akcesoria według SYS-004. Tor dużego prądu rozrusznika wymaga osobnej analizy. Wyjścia zapłonu, wtrysku i zaworu wydechowego nie są przedmiotem tego porównania.

## Porównanie

Wariant zintegrowany zakłada elektroniczne klucze mocy na PCB ECU. Wariant mieszany dopuszcza część takich wyjść oraz zewnętrzne przekaźniki lub moduły mocy dla wybranych odbiorników. Przekaźniki w tym porównaniu są zewnętrzne; nie proponowano ich montażu na PCB ECU. Poniższe wnioski są oceną projektową, a nie wynikiem pomiarów DustONE.

| Kryterium | Wyjścia mocy na PCB ECU | Wybrane stopnie mocy poza ECU |
| --- | --- | --- |
| Gabaryty | Mniej zewnętrznych elementów, lecz PCB, złącza i odprowadzanie ciepła muszą obsłużyć prądy odbiorników. | Możliwe odciążenie gabarytów samego ECU; potrzebne dodatkowe miejsce na stopnie mocy, gniazda i wiązkę. |
| Nagrzewanie | Straty przełączników i torów prądowych występują w ECU, blisko elektroniki pomiarowej. | Część strat występuje poza ECU; przekaźniki mają również pobór energii cewki i straty na stykach. |
| Diagnostyka | Odpowiednio dobrane inteligentne klucze mogą mierzyć prąd i sygnalizować wybrane usterki obciążenia [1]. | Zwykły przekaźnik bez dodatkowego pomiaru nie potwierdza działania odbiornika. Zewnętrzny inteligentny moduł może zapewniać diagnostykę, jeśli ma odpowiedni interfejs zwrotny. |
| Naprawa | Uszkodzenie stopnia na PCB może wymagać naprawy lub wymiany ECU. | Przekaźnik w gnieździe można wymienić osobno [2]; dostępność części i dostęp serwisowy trzeba zapewnić w projekcie. |
| Instalacja | Mniej osobnych stopni wykonawczych; trasy dużych prądów przechodzą przez złącza ECU. | Dodatkowe połączenia; stopień mocy można umieścić przy odbiorniku, jeśli pozwala na to miejsce i środowisko. |
| Ochrona i trwałość | Wymagane obliczenia cieplne, koordynacja zabezpieczeń i reakcje na awarie. Klucz półprzewodnikowy nie gwarantuje odłączenia przy każdym uszkodzeniu. | Wymagane zabezpieczenia przewodów, dobór styków do obciążenia i tłumienie przepięć cewki; producent opisuje ryzyko sklejania styków [3]. |

W obu wariantach należy zaprojektować ochronę zasilania i wiązki, stany po restarcie/utracie komunikacji oraz odporność na wodę. Elektroniczne zabezpieczenie kanału nie oznacza automatycznie rezygnacji z bezpiecznika zasilania. Bez liczby kanałów i parametrów obciążeń nie rozstrzygamy kosztu, końcowych wymiarów ani niezawodności całej instalacji.

## Preferowany kierunek i dalsza analiza

Po porównaniu właściciel zaproponował zastąpienie przekaźników SmartFET-ami w celu ograniczenia miejsca. Przyjmujemy SmartFET-y na PCB ECU jako preferowany kierunek dalszej analizy wyjść akcesoriów. Nie jest to jeszcze potwierdzenie możliwości zasilania wszystkich odbiorników bezpośrednio z ECU ani zatwierdzenie wariantu mieszanego. Nie wybrano komponentów i parametrów kanałów.

Inteligentny klucz mocy łączy tranzystor z funkcjami sterowania, ochrony i diagnostyki; zakres zależy od układu [1]. Dla odbiorników zasilanych przełączanym plusem rozpatrzymy klucze high-side. Interfejs należy dopasować do sposobu podłączenia obciążenia OEM. Miejsce na PCB musi obejmować także miedź odprowadzającą ciepło, tory prądowe, otoczenie układu i złącza. Straty przewodzenia oceniamy z P = I² × R; uwzględniamy rezystancję w temperaturze pracy i równoczesne obciążenie kanałów. Sam mały rozmiar obudowy układu nie potwierdza docelowych gabarytów ECU.

Przed zatwierdzeniem podziału kanałów zebrać: prądy robocze i rozruchowe, czas jednoczesnej pracy, rodzaj obciążenia, wymagania sterowania i diagnostyki, przekroje/trasy przewodów, parametry złączy oraz warunki chłodzenia szczelnej obudowy. Porównywać przestrzeń zajętą przez kompletny układ zgodnie z SYS-035.

## Podstawy techniczne

1. [Texas Instruments — TPS1HB08-Q1](https://www.ti.com/product/TPS1HB08-Q1): przykład klucza z pomiarem prądu, ograniczaniem prądu, ochroną termiczną i diagnostyką wybranych usterek. Jest to przykład funkcji, a nie wybór części do DustONE.
2. [TE Connectivity — przekaźniki wtykowe automotive](https://www.te.com/en/products/relays-and-contactors/electromechanical-relays/automotive-relays/plug-in-automotive-relays.html): wymienne przekaźniki i gniazda, m.in. do wentylatorów i pomp.
3. [TE Connectivity — Relay Coil Suppression with DC Relays](https://www.te.com/en/products/relays-and-contactors/electromechanical-relays/intersection/relay-coil-suppression-dc-relays.html): wpływ tłumienia cewki i obciążenia na rozłączanie oraz trwałość styków.
