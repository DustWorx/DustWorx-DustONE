# Architektura

Miejsce na architekturę całego systemu, ECU, HMI i aplikacji Windows: podział odpowiedzialności, diagramy blokowe, przepływy danych i zachowanie przy awariach.

Stan: architektura docelowa do opracowania po określeniu silników referencyjnych, zasilania oraz listy wejść i wyjść. Procesory i interfejsy sprzętowe nie zostały jeszcze wybrane; narzędzie EDA określono w zakresie systemu.

Zatwierdzona podstawa: [ADR-002 — samodzielność ECU](../decisions/adr-002-samodzielnosc-ecu.md). ECU pozostaje właścicielem danych i działa bez HMI; HMI odczytuje dane i wysyła żądania. Nieobecność HMI ani utrata CAN ECU–HMI nie wyłącza silnika. Przyciski obsługi HMI pozostają w HMI; START ma osobne wejście ECU, a STOP niezależny obwód gaszenia (SYS-016/037/048). Szczegóły reakcji akcesoriów i protokołu pozostają otwarte (SYS-046/047).

Wybudzanie i czuwanie: [ADR-003 — obsługa bez osobnego włącznika](../decisions/adr-003-wybudzanie-bez-wlacznika.md). START, kopniak, przyciski HMI i podłączenie komputera wybudzają ECU oraz HMI. Gotowość ECU do rozruchu ma priorytet i nie zależy od uruchomienia HMI. Podłączenie komputera blokuje usypianie obu urządzeń (SYS-054–057). Tory sprzętowe, sekwencja zasilania, czasy, budżet prądu czuwania i warunki zasypiania wymagają projektu.

Analizy architektoniczne:

- [Zasilanie podczas serwisu — 12 V czy z komputera](zasilanie-serwisowe-porownanie.md): wybrano wariant A — wymagane zasilanie 12 V, kabel PC do komunikacji i wybudzenia (SYS-058). Parametry toru zasilania pozostają do projektu.
- [Macierz wariantów silnika](macierz-wariantow-silnika.md): zakres gaźnika/wtrysku i 2T/4T oraz dane potrzebne do wspólnej PCB; modele poza Betą pozostają do wyboru.
- [Wyjścia akcesoriów — porównanie realizacji](wyjscia-akcesoriow-porownanie.md): preferowany kierunek to SmartFET-y na PCB ECU; podział i parametry kanałów oraz wykonalność pełnej integracji pozostają do analizy.
