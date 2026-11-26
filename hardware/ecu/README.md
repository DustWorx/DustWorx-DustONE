# Sprzęt ECU

Miejsce na edytowalne schematy i PCB, BOM oraz kontrolowane eksporty produkcyjne ECU.

Wymaganie bazowe: jedna platforma sprzętowa dla jednocylindrowych silników 2T i 4T chłodzonych cieczą (SYS-098); wymagany jest pomiar temperatury płynu według SYS-044. Parametry i interfejsy obsługiwanych układów zapłonu, paliwa, czujników i obciążeń oraz granice warunków zasilania wymagają szczegółowej specyfikacji.

Narzędzie EDA: **Autodesk Fusion Electronics**, płatna subskrypcja właściciela projektu. Komponenty nie zostały jeszcze wybrane.

Wymagania i otwarte decyzje: [zakres systemu](../../docs/01-zakres-systemu.md). Definicje interfejsów rozwijamy w `docs/interfaces/`.

SYS-167 jest wejściem do projektu torów zapłonu i wtrysku. Sprawny przewodowy STOP musi wymusić odcięcie także przy zawieszonym głównym firmware. Projekt ma uwzględnić zapłon CDI i TCI/IDI, tory wtrysku oraz warunki wznowienia według SYS-162. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-167).

SYS-168 rozszerza wymaganie odcięcia przez STOP na tor wykonawczy rozrusznika. Odłączenie działa przy zawieszonym głównym firmware i przytrzymanym START. Wymaganie uwzględnić przy projektowaniu toru rozrusznika. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-168).

SYS-169 wymaga odcięcia zapłonu, wtrysku i toru rozrusznika przez niezależny nadzór przy zawieszeniu głównego firmware. Odcięcie działa również przy nieskutecznym resecie. Nadzór inicjuje reset jako odrębne działanie. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-169).

Tory wykonawcze muszą umożliwić utrzymanie odcięcia po skutecznym resecie zgodnie z SYS-170 dla zapłonu i wtrysku oraz z SYS-171 dla rozrusznika. [Próba zapłonu i wtrysku](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-170), [próba rozrusznika](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-171).

Wybór nadzoru i MCU musi uwzględniać możliwość potwierdzenia przyczyny resetu po uruchomieniu ECU według SYS-172. Dostępność dodatkowych danych zdarzenia zależy od projektu nadzoru i pamięci. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-172).

Nadzór musi ograniczać automatyczne próby uruchomienia i utrzymywać odcięcie po osiągnięciu limitu zgodnie z SYS-173, także przy niezakończonym uruchomieniu głównego firmware. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-173).

Nadzór i tor uruchamiania ECU muszą umożliwić wyzwolenie odzyskiwania po limicie standardowych prób również przy niezakończonym uruchomieniu głównego firmware (SYS-174). [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-174).

Tor obsługi przewodowej musi umożliwić naprawę z Windows po niepowodzeniu samodzielnego odzyskiwania przy nieuruchomionym głównym firmware (SYS-175). [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-175).

Projekt pamięci i uruchamiania ECU ma umożliwiać odtworzenie stanu oczekiwania na naprawę po zaniku zasilania oraz odcięcie od chwili jego powrotu (SYS-177). [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-177).

Projekt pamięci i uruchamiania ma umożliwić odtworzenie wykorzystania limitu samodzielnych prób po zaniku zasilania, w tym jednokrotne zaliczenie przerwanej próby według SYS-178. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-178).

Projekt pamięci, nadzoru i uruchamiania ma umożliwić odtworzenie liczby zakończonych standardowych prób po zaniku zasilania oraz ponowienie przerwanej próby w tym samym miejscu limitu (SYS-179). [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-179).

Projekt nadzoru i uruchamiania ma umożliwić potwierdzenie okresu stabilnej pracy i rozliczenie ponownego zawieszenia w bieżącej serii według SYS-180. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-180).

Tory zapłonu i wtrysku mają utrzymywać odcięcie od powrotu zasilania do dopuszczenia sterowania po przerwaniu pracy silnika lub rozruchu kopniakiem według SYS-181 i SYS-183. [Próba podczas pracy](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-181), [próba kopniakiem](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-183).

Tor rozrusznika ma pozostawać wyłączony od chwili powrotu zasilania po przerwanym rozruchu do nowej dopuszczonej próby według SYS-182. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-182).

Dobór MCU, pamięci i zasilania musi uwzględnić [chronione motogodziny i ODO](../../docs/architecture/chronione-liczniki.md), SYS-074–076: trwałość zapisu, utratę zasilania, ochronę dostępu i mechanizmy uruchamiania/aktualizacji. Konkretne mechanizmy i ważne komponenty wybieramy wspólnie z właścicielem po ustaleniu granic ochrony.

Dobór MCU i interfejsów programowania musi również uwzględnić [SYS-078 i ADR-008](../../docs/decisions/adr-008-dostep-do-firmware-ecu.md): w trybie użytkowym tylko firmware zatwierdzony przez producenta oraz zachowany dostęp rozwojowy twórców. Sposób autoryzacji i przejścia między trybami wymaga projektu; nie wybrano układów, algorytmów ani nieodwracalnych blokad.

Tor przedniego koła musi umożliwiać wykrywanie obrotów podczas snu i wybudzanie ECU do naliczania ODO także przy zgaszonym silniku (SYS-075/079, [I/O](../../docs/interfaces/wstepna-lista-io.md)). Czujnik, interfejs i elementy dobierzemy wspólnie; uwzględnić pobór w śnie i obsługę początku ruchu.

SYS-092 wymaga obsługi AGM i motocyklowych LiFePO4 na wspólnej PCB bez zmiany obsady. Zakres wejścia, ochrona, pomiar i budżet czuwania wymagają obliczeń oraz prób dla uzgodnionych konfiguracji; komponenty wybieramy wspólnie. [ADR-010 i plan weryfikacji](../../docs/decisions/adr-010-akumulatory-agm-lifepo4.md).

Budżet poboru ECU, zasilanego z niego HMI i torów czuwania musi wynikać z celu minimum 4 tygodni postoju bez doładowania z rezerwą na rozruch przy otoczeniu od −10°C do +40°C podczas postoju i późniejszego uruchomienia (SYS-093). Dla tego celu przyjęto pojemności znamionowe od 3 Ah AGM i 2 Ah LiFePO4 (C10). Limit prądu i szczegóły pomiaru wyliczymy dla zgodnych modeli oraz kryteriów rozruchu; zakres pracy elektroniki podczas jazdy ustalimy osobno: [analiza i plan prób](../../docs/architecture/budzet-energii-postoju.md).

Do późniejszego projektu: SYS-096 wymaga możliwości odczytu MAP z kompatybilnego czujnika OEM lub dodatkowego na wspólnej PCB. Konfiguracje niewymagające MAP pracują bez czujnika; model, parametry toru i komponenty dobierzemy we właściwych etapach. [Karta MAP](../../docs/interfaces/cisnienie-dolotu-map.md).

Do późniejszego projektu: SYS-097 wymaga możliwości odczytu ciśnienia gazów w skrzyni korbowej 2T (CCPS) z kompatybilnego czujnika. Model, parametry i podział zasobów z MAP określimy w etapach projektowych; [karta CCPS](../../docs/interfaces/cisnienie-skrzyni-korbowej.md).

Przy projekcie zasilania, pomiarów i torów wykonawczych uwzględnić próby autotestu dostępne przed rozruchem według SYS-203, w tym próbę wentylatora. Tory rozrusznika, zapłonu i wtrysku pozostają bez sterowania rozruchowego do zakończenia tych prób. Czasy gotowości i warunki zasilania wymagają bilansu i pomiarów, także przy wybudzeniu kopniakiem. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-203).

Tor przewodowego START ma umożliwiać wybudzenie i odczyt aktualnego przytrzymania po zakończeniu autotestu według SYS-204. Uwzględnić ciągłość obserwacji stanu i zwolnienie przycisku podczas wybudzania. Interfejs oraz filtrację dobierzemy w projekcie. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-204).

Do późniejszego projektu: SYS-208 przewiduje ocenę temperatury ECU jako pomocniczych danych do oszacowania IAT przy usterce. Przy doborze pomiaru temperatury na PCB, ewentualnego kanału w barometrze oraz rozmieszczeniu komponentów uwzględnić samonagrzewanie, wpływ stopni mocy i obudowy, montaż oraz opóźnienie cieplne. Błąd modelu porównać z referencyjnym IAT przed dopuszczeniem strategii. Podstawowy IAT pozostaje zewnętrzny według SYS-031; ważne komponenty wybieramy wspólnie. [Plan oceny i prób pracy/rozruchu](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-208).

Do późniejszego projektu: SYS-241/242 wymagają trzech niezależnie sterowanych dodatkowych kanałów mocy do oświetlenia i zasilania zewnętrznych akcesoriów. Prądy pojedyncze/równoczesne, topologię, zabezpieczenia i pinout ustalimy w architekturze, a ważne komponenty wybierzemy wspólnie. [Zakres i plan próby F04](../../docs/requirements/f04-akcesoria-i-io.md#trzy-dodatkowe-kanały-mocy).

Przy projektowaniu inicjalizacji i sterowania dodatkowymi torami mocy uwzględnić stan wyłączony po odzyskaniu gotowości ECU po nieplanowanym restarcie lub powrocie zasilania według SYS-244. Przebieg inicjalizacji i zachowanie wyjść określimy z architekturą i danymi układów. [Plan próby F04](../../docs/requirements/f04-akcesoria-i-io.md#plan-próby-sys-244).

SYS-245 wymaga wyłączenia dodatkowych torów przed prawidłowym snem i pozostawienia ich wyłączonych po zwykłym wybudzeniu do nowego polecenia. Zachowanie sterowania w stanach niskiego poboru uwzględnić w projekcie domen i interfejsów wyjść. [Plan próby F04](../../docs/requirements/f04-akcesoria-i-io.md#plan-próby-sys-245).

SYS-246 wymaga ON/OFF i opcjonalnego PWM mocy zgodnych lamp na każdym z trzech dodatkowych kanałów; GPS i ładowarki pracują w trybie ON/OFF. W kolejce etapów 3–6 ustalić dane odbiorników, częstotliwość i zakres regulacji, zasoby sterowania, zgodność diagnostyki z PWM oraz prądy, straty cieplne i wpływ zakłóceń. Ważne układy wybierzemy wspólnie. [Ustalenie i plan próby F04](../../docs/requirements/f04-akcesoria-i-io.md#onoff-i-opcjonalny-pwm-mocy).

SYS-247 wymaga po odcięciu dodatkowego kanału braku samoczynnych ponowień i możliwości ograniczonej próby ze sprawdzeniem obwodu na nowe świadome polecenie. Dobór stopnia mocy i nadzoru musi uwzględnić jego wewnętrzną ochronę oraz PWM; progi, energia próby i warunki termiczne wymagają danych i projektu. Nie wybrano komponentu. [Plan próby F04](../../docs/requirements/f04-akcesoria-i-io.md#plan-próby-sys-247).

SYS-248 wymaga odnowienia prawa do próby po pełnym cyklu snu lub pełnym zaniku i powrocie zasilania oraz zachowania blokady przy zwykłym resecie programu. Do architektury: kryteria zaniku/resetu, domeny zasilania i możliwości utrzymania stanu; czas ostygnięcia i ograniczenia energii pozostają nadrzędne. Odnowienie nie załącza kanału. Ważne układy i pamięć wybierzemy wspólnie. [Plan próby F04](../../docs/requirements/f04-akcesoria-i-io.md#plan-próby-sys-248).

SYS-249 wymaga, przy sprawnych pozostałych obwodach i prawidłowych warunkach wspólnych, odcięcia tylko lokalnie uszkodzonego dodatkowego kanału. Do architektury i doboru: wspólne ścieżki zasilania, ograniczenie zwarcia, sprzężenia cieplne i wpływ na sąsiednie kanały. Niezależne zwykłe sterowanie nie potwierdza izolacji usterki; wynik wymaga bilansu i prób. Wspólne zagrożenia mogą wymagać szerszej reakcji. Ważne układy wybierzemy wspólnie. [Plan próby F04](../../docs/requirements/f04-akcesoria-i-io.md#plan-próby-sys-249).

SYS-250 określa OFF podstawowych pozycyjnych, mijania i drogowych po odzyskaniu gotowości po nieplanowanym restarcie przy zgaszonym silniku. Inicjalizację torów, zachowanie wyjść i współdziałanie z automatyką pozycyjnych oraz bezpośrednimi wejściami światła hamowania uwzględnić w architekturze i projekcie. [Plan próby F04](../../docs/requirements/f04-akcesoria-i-io.md#plan-próby-sys-250).

SYS-253 rozszerza wymaganie ograniczonej świadomej próby i blokady po niepowodzeniu na kanały podstawowego oświetlenia, kierunkowskazów i klaksonu. Dobór torów ma uwzględnić ich wewnętrzną ochronę, prądy załączania, energię próby, termikę i współdziałanie z limitem ECU. Liczba kanałów i ważne układy wymagają wspólnego projektu; inicjowanie próby światła hamowania z jego bezpośrednich wejść określa przyjęte SYS-254. [Plan próby](../../docs/requirements/f04-akcesoria-i-io.md#plan-próby-sys-253).

SYS-254 wymaga oceny bezpośrednich wejść obu hamulców i ograniczonej próby toru bez udziału HMI przy dostępnym limicie. Parametry wejść, filtracja, pomiar i kryteria próby do architektury oraz doboru; ważne elementy wybierzemy wspólnie. [Plan próby F04](../../docs/requirements/f04-akcesoria-i-io.md#plan-próby-sys-254).

SYS-255: każdy zewnętrzny port ma uzgodnione zastosowanie; bez dodatkowej rezerwy zewnętrznej do nieokreślonych urządzeń. Zachować przyjęte funkcje i dostęp obsługi/programowania/debugowania według ról. Wewnętrzne zasoby, magistrale i punkty testowe ocenić w architekturze; pinout i ważne układy dobierzemy wspólnie. [Plan weryfikacji F04](../../docs/requirements/f04-akcesoria-i-io.md#plan-próby-sys-255).
