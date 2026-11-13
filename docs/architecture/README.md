# Architektura

Miejsce na architekturę całego systemu, ECU, HMI i aplikacji Windows: podział odpowiedzialności, diagramy blokowe, przepływy danych i zachowanie przy awariach.

**Etap 4 oczekuje w kolejce.** Materiały robocze obejmują wstępną [architekturę blokową](blokowa-systemu.md), funkcjonalny przydział zasobów i jednoczesności w [macierzy wariantów](macierz-wariantow-silnika.md) oraz [przydział SYS do bloków i grup weryfikacji](../verification/macierz-wymagan.md). Modele referencyjne poza Betą, parametry, liczbowe bilanse i G1 pozostają otwarte; procesory i układy wybierzemy wspólnie po ustaleniu danych bloku.

Zatwierdzona podstawa: [ADR-002 — samodzielność ECU](../decisions/adr-002-samodzielnosc-ecu.md). ECU pozostaje właścicielem danych i działa bez HMI; HMI odczytuje dane i wysyła żądania. Nieobecność HMI ani utrata CAN ECU–HMI nie wyłącza silnika. Przyciski obsługi HMI pozostają w HMI; START ma osobne wejście ECU, a STOP niezależny obwód gaszenia (SYS-016/037/048). Uzgodnione reakcje akcesoriów na utratę HMI lub CAN określają SYS-050–053. Zachowanie klaksonu i wyjść konfigurowalnych jest w [kolejce F04](../requirements/domkniecie-zakresu-funkcjonalnego.md). Szczegóły protokołu pozostają do projektu.

Wybudzanie i czuwanie: [ADR-003 — obsługa bez osobnego włącznika](../decisions/adr-003-wybudzanie-bez-wlacznika.md). START, kopniak, przyciski HMI i podłączenie komputera wybudzają ECU oraz HMI. Gotowość ECU do rozruchu ma priorytet i nie zależy od uruchomienia HMI. Podłączenie komputera blokuje usypianie obu urządzeń (SYS-054–057). Obrót przedniego koła wybudza oba urządzenia, a ECU nalicza drogę niezależnie od gotowości HMI (SYS-079/080). Bez PC, przy zgaszonym silniku i zakończonych zadaniach system zasypia po konfigurowalnym czasie bezczynności; przyciski odnawiają odliczanie (SYS-059). Tory sprzętowe, sekwencje, parametry czasu i budżet prądu czuwania wymagają projektu.

Praca wentylatora po zgaszeniu silnika: funkcja konfigurowalna, z limitem czasu i odcięciem przy niskim napięciu; obsługa wstrzymuje uśpienie ECU (SYS-060). Te same ograniczenia obowiązują ręczne wymuszenie i są egzekwowane w ECU (SYS-061), co wymaga nadzoru napięcia akumulatora. HMI pozostaje aktywne do polecenia ECU. Zastosowanie w danym układzie chłodzenia i parametry wymagają doprecyzowania.

Usypianie koordynuje ECU: [normalna sekwencja ECU–HMI](usypianie-ecu-hmi.md), SYS-062/063. HMI potwierdza przyjęcie polecenia ramką CAN, kończy nadawanie i zasypia; następnie zasypia ECU. Wyjście zasilania HMI pozostaje włączone podczas normalnego snu obu urządzeń (SYS-066). Zasilanie wychodzi z ECU i jest przez nie kontrolowane; odłączenie jest ostateczną ścieżką awaryjną lub wynika ze zdefiniowanych ograniczeń HMI (SYS-064–066). Wybudzanie przyciskami po odłączeniu pozostaje wymagane; topologia i parametry są do projektu.

Analizy architektoniczne:

- [Brak potwierdzenia uśpienia HMI](brak-potwierdzenia-uspienia-hmi.md): porównanie alternatyw i uzasadnienie wyboru kontroli zasilania z ECU; zachowanie wybudzania przyciskami jest wymagane, topologia i parametry pozostają do projektu.
- [Zasilanie podczas serwisu — 12 V czy z komputera](zasilanie-serwisowe-porownanie.md): wybrano wariant A — wymagane zasilanie 12 V, kabel PC do komunikacji i wybudzenia (SYS-058). Parametry toru zasilania pozostają do projektu.
- [Macierz wariantów silnika](macierz-wariantow-silnika.md): zakres gaźnika/wtrysku i 2T/4T oraz dane potrzebne do wspólnej PCB; modele poza Betą pozostają do wyboru.
- [Wyjścia akcesoriów — porównanie realizacji](wyjscia-akcesoriow-porownanie.md): preferowany kierunek to SmartFET-y na PCB ECU; podział i parametry kanałów oraz wykonalność pełnej integracji pozostają do analizy.
- [Chronione liczniki motogodzin i ODO](chronione-liczniki.md): zatwierdzone reguły dostępu, inicjalizacji i przenoszenia liczników, wpływ na sprzęt i firmware oraz plan prób. Mechanizmy ochrony i szczegóły procedury są do projektu.
- [Oszczędzanie energii po zgaszeniu silnika](oszczedzanie-energii.md): przejście na pozycyjne, nadzór akumulatora, wyłączenie zbędnych odbiorników, rekomendacje i plan prób (SYS-083/084).
- [Akumulatory AGM i LiFePO4 — porównanie zakresu](akumulatory-agm-lifepo4-porownanie.md): po porównaniu właściciel wybrał oba typy na wspólnej PCB, z osobnymi profilami i testami zgodności (SYS-092, ADR-010); parametry i dobór toru pozostają otwarte.
- [Budżet energii podczas postoju](budzet-energii-postoju.md): minimum 4 tygodnie bez doładowania z rezerwą na rozruch według ustalonych warunków (SYS-093). Limit poboru prądu i procedury prób są do opracowania.
- [ADR-011 — strojenie na żywo](../decisions/adr-011-strojenie-na-zywo.md): Windows może stosować zmiany wybranych wartości map podczas pracy silnika; zapis i utrata sesji mają przyjęte reguły. [Zamknięty zakres F02](../requirements/f02-przeglad-zakresu.md) przekazuje realizację do etapu 4.
