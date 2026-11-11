# Macierz wymagań, bloków i weryfikacji

Stan na 2026-11-11. **Materiał wstępny dla etapu 5 w kolejce — przydział 168 wymagań do 13 grup.** Treść wymagań ma jedno miejsce źródłowe w [rejestrze SYS](../01-zakres-systemu.md), a ID bloków w [architekturze](../architecture/blokowa-systemu.md).

Wszystkie wymagania pozostają **niezweryfikowane na produkcie**. Poniższe powiązanie nie jest kompletem procedur ani potwierdzeniem kompletności funkcji. Dla każdej próby rozwijamy: wariant/model i konfigurację, rewizje HW/FW/aplikacji, metodę, mierzalne kryteria, wyposażenie/połączenia, kroki, warunki przerwania oraz dowód wyniku. Wymaganie może mieć kilka bloków i prób.

## Grupy do rozwinięcia w procedury

| Grupa | Zakres | Metoda i etap | Kierunek kryterium akceptacji | Otwarte dane przed wykonaniem |
| --- | --- | --- | --- | --- |
| V01 | Synchronizacja | Analiza, generator/symulator i stanowisko; później silnik. | Sygnały wału VR/Hall i dodatkowej fazy Hall rozpoznawane zgodnie z przyjętymi dekoderami; granice i utrata synchronizacji. Dla SYS-157 sprawdzamy odcięcie i utrzymanie go po powrocie sygnału przed zatrzymaniem. Dla SYS-159 sprawdzamy utrzymanie odcięcia po powrocie sygnału w przerwanej próbie kopniakiem. | Modele, zakres prędkości/amplitud, dokładność i czasy reakcji. |
| V02 | Sterowanie silnikiem i mapy | Analiza osprzętu, testy bloków/stanowiska i właściwy silnik. | Zapłon/wtrysk/napędy działają zgodnie z konfiguracją; pełne zestawy mają niezależne wartości. Robocza edycja aktywnego i nieaktywnych zestawów nie przełącza zestawu; zmiany nieaktywnego wpływają na silnik dopiero po jego świadomym wybraniu. Zgodność zestawu, przełączanie i strojenie na żywo nie zakłócają wymaganej pracy. Poprawna grupa zmian wartości obowiązuje jako jedna aktualizacja (SYS-116). ECU używa map aktywnego zestawu i pojedynczych nastaw wspólnych (SYS-118). W wyposażonym 2T z zestawem przełącza mapę położenia zadanego zaworu wydechowego (SYS-119). W wariantach gaźnikowych ECU dobiera bazowy kąt zapłonu z krzywej obrotowej albo mapy obrotów i TPS według konfiguracji (SYS-120). Po usterce używanego TPS w gaźniku ECU stosuje zweryfikowaną krzywą awaryjną od obrotów w ustalonych granicach (SYS-121). Krzywa awaryjna jest wspólna dla wszystkich zestawów danej konfiguracji (SYS-122). Po odzyskaniu TPS powrót do zwykłej mapy zapłonu następuje przy kolejnym rozruchu z wiarygodnym sygnałem (SYS-123). Dla profilu z jednym pomiarem obciążenia sprawdzamy dwie osie i wspólne źródło w mapach paliwa i zapłonu (SYS-125 i SYS-126). W profilach wymagających TPS i pomiaru ciśnienia sprawdzamy udział obu w sterowaniu nominalnym według ich ról (SYS-127). Przy pojedynczej usterce i spełnionych warunkach sprawdzamy zgłoszenie i pracę na zweryfikowanej kalibracji właściwej dla tej utraty (SYS-128). Po odzyskaniu sygnału sprawdzamy pozostanie na kalibracji awaryjnej do zatrzymania i dobór sterowania przy następnym rozruchu (SYS-130). Po usterce pomiaru obciążenia sprawdzamy automatyczny wybór „Standard” do pracy nominalnej i sterowanie na właściwej kalibracji w pracy awaryjnej (SYS-136). Dla SYS-028 sprawdzamy zmianę zestawu z HMI i użycie jego map w nominalnej pracy silnika na postoju i podczas kontrolowanej jazdy. Dla SYS-149 sprawdzamy wybór na postoju przy zgaszonym silniku i wykonanie nadal ważnego żądania przyjętego podczas jazdy. Dla SYS-164 sprawdzamy kontynuację pracy nominalnej na wybranym zestawie po potwierdzeniu przerwy w STOP. Dla SYS-166 sprawdzamy dalszą pracę na wybranym zestawie po potwierdzeniu zwarcia STOP do masy. | Cewki, wtryskiwacze/napędy, strategie, tolerancje czasowe, reguły map i walidacja smarowania 2T. |
| V03 | Pomiary i wejścia | Analiza błędów, wzorce/symulatory i rzeczywiste czujniki. | Prawidłowe wartości/stany oraz rozróżnianie braku wyposażenia i usterek według konfiguracji. Dla SYS-163 sprawdzamy rozróżnienie zwolnionego i naciśniętego STOP oraz przerwy w obwodzie. Dla SYS-165 sprawdzamy rozpoznanie zwarcia przewodu STOP do masy jako stanu odrębnego od naciśnięcia sprawnego przycisku, jego zwolnienia i przerwy w obwodzie. | Charakterystyki, dokładności, zakresy, progi i diagnostyka wejść. |
| V04 | START, STOP i przewrócenie | Stanowisko, następnie kontrolowane próby właściwego motocykla. | START podczas przytrzymania, odcięcia i ponowienie, STOP bez HMI/CAN, zatrzymanie po przewróceniu i świadomy ponowny rozruch; blokada rozruchu podczas całej operacji krytycznej konfiguracji; po anulowaniu niepełnego transferu zgodnie z SYS-103 blokady operacji są zwalniane, a rozruch wymaga nowej świadomej próby; SYS-104 dopuszcza zwolnienie po samodzielnie dokończonym i potwierdzonym wdrożeniu mimo utraty Windows; SYS-105 wymaga po błędzie potwierdzonego powrotu do poprzedniej konfiguracji albo utrzymania blokad przy braku poprawnych danych; po zaniku zasilania SYS-106 wymaga sprawdzenia konfiguracji przed zwolnieniem blokad i nowej świadomej próby rozruchu. Podczas operacji na mapach SYS-110 wymaga blokady rozruchu, potwierdzenia poprawnych danych i nowej próby po jej zwolnieniu. Rozruch gaźnika z usterką TPS wymaga krzywej awaryjnej zweryfikowanej do rozruchu oraz spełnienia pozostałych warunków (SYS-124). We wtrysku sprawdzamy kontrolowane zatrzymanie przy pojedynczej usterce wymaganego pomiaru i braku właściwej zweryfikowanej kalibracji awaryjnej (SYS-129). Rozruch wtrysku z pojedynczą usterką wymaga kalibracji zweryfikowanej do rozruchu dla tej usterki oraz spełnienia pozostałych warunków (SYS-131). Przy utracie obu pomiarów sprawdzamy kontrolowane zatrzymanie, blokadę rozruchu i warunki nowej próby po odzyskaniu jednego pomiaru (SYS-132). Dla utraty jedynego pomiaru sprawdzamy domyślne zatrzymanie i blokadę oraz dowody dopuszczenia wyjątku dla danego silnika (SYS-133). Odrębnie sprawdzamy dowody i próbę rozruchu dla wyjątku oraz blokadę przy dopuszczeniu tylko dalszej pracy (SYS-134). Dla SYS-139 sprawdzamy blokadę rozruchu mimo dostępnego innego zestawu oraz nową próbę po odzyskaniu poprawnego „Standard”. Dla SYS-140 sprawdzamy dopuszczenie rozruchu na „Standard” po odrzuceniu zapisanego zestawu kierowcy przy spełnionych pozostałych warunkach. Dla SYS-141 sprawdzamy blokadę przy dostępności wyłącznie trzeciego poprawnego zestawu oraz nową próbę po odzyskaniu „Standard” albo zestawu kierowcy. Dla SYS-157 sprawdzamy dopuszczenie sterowania w nowej próbie po zatrzymaniu i ponownej synchronizacji. Dla SYS-158 sprawdzamy odcięcie rozrusznika w przerwanej próbie oraz wymaganie nowego START po zatrzymaniu. Dla SYS-159 sprawdzamy nową próbę kopniakiem po zatrzymaniu i ponownej synchronizacji. Dla SYS-160 sprawdzamy blokadę rozrusznika przy START naciśniętym podczas STOP oraz wymóg nowego START po zwolnieniu STOP. Dla SYS-161 sprawdzamy wyłączenie rozrusznika po naciśnięciu STOP w trakcie kręcenia oraz nową próbę po ponownym naciśnięciu START. Dla SYS-162 sprawdzamy utrzymanie odcięcia po zwolnieniu STOP podczas obrotu oraz wznowienie po zatrzymaniu i nowej świadomej próbie. Dla SYS-164 sprawdzamy dopuszczenie nowej próby przy utrzymującej się przerwie w STOP i spełnionych pozostałych warunkach. Dla SYS-166 sprawdzamy dopuszczenie nowej próby rozruchu przy utrzymującym się zwarciu STOP do masy i spełnionych pozostałych warunkach. Dla SYS-167 sprawdzamy odcięcie zapłonu i wtrysku po naciśnięciu STOP przy zawieszonym głównym firmware oraz warunki wznowienia według SYS-162. Dla SYS-168 sprawdzamy odłączenie rozrusznika przez STOP przy zawieszonym głównym firmware i wciśniętym START oraz wymóg nowej próby według SYS-161. | Warunki/czasy, kryterium pracy silnika i przewrócenia, tor STOP, połączenia stanowiska. |
| V05 | Akcesoria i ochrona energii | Symulacja stanów, stanowisko obciążeń i integracja. | Światła, hamulce, kierunkowskazy, klakson, wentylator i wyjścia realizują przyjęte stany, priorytety i odcięcia. | Prądy, temperatury, progi/czasy, brakujące stany po usterkach/resecie i lista dodatkowych odbiorników. |
| V06 | Zasilanie, wybudzanie i sen | Bilans, pomiary całego zestawu i próby konfiguracji akumulator/regulator/temperatura. | Wymagane wybudzenia, sen, sterowanie zasilaniem HMI, blokada snu z PC i rezerwa na rozruch po 28 dniach; po przerwaniu zmiany konfiguracji zasilaniem odtworzenie tylko kompletnych poprawnych danych i stan blokad według SYS-106. Po przerwaniu zapisu wszystkich map ECU odzyskuje jedną poprawną wersję grupy według SYS-109. Po zaniku zasilania sprawdzamy odtworzenie wymuszonego wyboru „Standard” przy spełnionych warunkach pracy nominalnej (SYS-138). Dla SYS-142 sprawdzamy odtworzenie zastępczego wyboru „Standard” po odzyskaniu zestawu kierowcy i cyklu zasilania. Dla SYS-150 sprawdzamy zakończenie ważności oczekującej zmiany przy restarcie i odtworzenie wcześniej zastosowanego zestawu. Dla SYS-155 sprawdzamy dokończenie trwale przyjętego resetu po powrocie zasilania bez połączenia z Windows. | Domeny/napięcia, prądy, czasy, modele i stan baterii, kryteria rozruchu oraz kompletne warunki prób. |
| V07 | CAN, role i autonomia | Stanowisko ECU–HMI, wymuszanie usterek komunikacji i integracja. | ECU działa bez HMI; realizuje rzeczywiste stany/odmowy i uzgodnione reakcje po utracie łączności; poprawna sekwencja snu. Podczas pracy awaryjnej sprawdzamy odmowę zmiany zestawu przez ECU i wyświetlenie jej przyczyny w HMI (SYS-135). Dla SYS-137 sprawdzamy także odmowę zmiany zestawu po usterce zatrzymującej silnik. Dla SYS-143 sprawdzamy przyjęcie żądania podczas jazdy, status oczekiwania w HMI i aktualizację aktywnego zestawu po przełączeniu. Dla SYS-144 sprawdzamy wygaśnięcie i informację w HMI o konieczności ponowienia wyboru. Dla SYS-145 sprawdzamy zastąpienie oczekującego żądania, wskazanie aktualnego wyboru i limit od przyjęcia nowego żądania. Dla SYS-146 sprawdzamy anulowanie oczekującej zmiany przez wybór aktywnego zestawu i potwierdzenie w HMI. Dla SYS-147 sprawdzamy anulowanie przy usterce wymuszającej „Standard” i wymaganie nowego wyboru po powrocie do pracy nominalnej. Dla SYS-148 sprawdzamy wykonanie bez HMI przed upływem pierwotnego limitu, wygaśnięcie po jego upływie i odczyt rzeczywistego stanu po odzyskaniu łączności. Dla SYS-151 sprawdzamy dalsze oczekiwanie i wygaśnięcie w pierwotnym terminie po ponownym wyborze tego samego zestawu. | Protokół, częstotliwości i czasy, kryteria utraty/powrotu, odzyskiwanie magistrali. |
| V08 | HMI i edytowalne ekrany | Przegląd scenariuszy oraz rzeczywiste HMI z konfiguracjami ekranów. | Obsługa przyciskami, odczyt danych/ostrzeżeń, szablony i układy użytkownika zgodnie z zakresem. | Ekrany/menu, priorytety, limity zasobów, czytelność i czasy. |
| V09 | Windows i operacje serwisowe | Testy aplikacji/protokołu, potem ECU–HMI–Windows. | Jeden punkt obsługi obu urządzeń, konfiguracja/strojenie, narzędzia I/O/CAN i dopuszczanie poleceń w ustalonych stanach; pełny zestaw map przyjmowany i roboczo zastępowany tylko przy zgaszonym silniku; trwały zapis wybranego zestawu lub wszystkich skonfigurowanych tylko na jawne polecenie przy zgaszonym silniku, z zachowaniem pozostałych danych przy zapisie pojedynczego; po utracie Windows wartości zastosowane na żywo pozostają aktywne bez automatycznego utrwalania. Po błędzie sumy trwałego zapisu map ECU przywraca dane z poprzedniego zapisu i udostępnia flagę wyniku (SYS-111). Flaga kasuje się dopiero po zweryfikowanym trwałym zapisie map (SYS-112). Przyjęty zapis z kompletem danych ECU kończy i weryfikuje po utracie Windows przy prawidłowym zasilaniu (SYS-113). Nieukończony transfer do roboczej podmiany ECU anuluje po utracie Windows i zachowuje dotychczasowe mapy (SYS-114). Po ponownym połączeniu działające ECU udostępnia stan map, flagę błędu sumy i status operacji rozpoczętej przed rozłączeniem (SYS-115). Przy błędzie w grupie zmian ECU odrzuca całe polecenie i podaje przyczynę (SYS-116). Przy zgaszonym silniku ECU na polecenie przywraca wybrany zestaw do pamięci roboczej z poprawnego zapisu (SYS-117). Dla SYS-152 sprawdzamy stan pierwszej konfiguracji i dostęp z Windows po potwierdzonym resecie, z blokadą rozruchu i zachowanymi licznikami. Dla SYS-155 sprawdzamy samodzielne ukończenie resetu po utracie sesji Windows. Dla SYS-156 sprawdzamy odczyt nieaktywnego projektu po restarcie oraz aktywację po dodaniu zgodnego „Standard” i wyraźnym poleceniu. | Przypadki użycia, interfejs, uprawnienia, parametry map, krytyczna konfiguracja, detekcja przerwanego transferu i potwierdzanie samodzielnie dokończonego wdrożenia po utracie sesji, detekcja/powrót sesji, powrót po błędzie konfiguracji, dostęp serwisowy bez poprawnych danych i stany końcowe. |
| V10 | DTC, czas i trwałość | Wymuszanie usterek, cykle pracy/zaniki zasilania, odczyt i eksport. | DTC/freeze frame, pierwsze/ostatnie wystąpienie, licznik, ważność czasu, wygaszanie i ręczne kasowanie według SYS-019–025. Dla SYS-154 sprawdzamy potwierdzenie obejmujące historię, eksport przed kasowaniem, usunięcie historii w potwierdzonym resecie i jej zachowanie po anulowaniu. Dla SYS-164 sprawdzamy zgłoszenie DTC i zapis zamrożonej ramki po potwierdzeniu przerwy w STOP. Dla SYS-166 sprawdzamy DTC właściwy dla zwarcia STOP do masy i zapis zamrożonej ramki. | Katalog, kryteria detekcji, pełna pamięć, tolerancja utraty danych, sposób i dokładność czasu. |
| V11 | Motogodziny, ODO i dostęp | Wzorce czasu/impulsów, cykle snu/zasilania, próby ról i migracji. | Naliczanie we właściwych warunkach, ODO bez HMI/pracy silnika, trwałość i odrzucenie niedozwolonej korekty; rejestr operacji uprawnionych. Dla SYS-153 sprawdzamy zmianę wyłącznie z uprawnieniem producenta, zapis operacji i odmowę zmiany z innymi uprawnieniami. | Dokładność, kalibracja koła, zapis po zaniku, model zagrożeń i autoryzacja. |
| V12 | Firmware, aktualizacja i odzyskiwanie | Przegląd mechanizmów, testy wersji/uprawnień i przerwanych aktualizacji. | Zatwierdzony firmware ECU w trybie użytkowym, zachowany dostęp twórców, aktualizacja obu urządzeń i ochrona danych. | Polityka HMI/starszych wersji, tryby, drogi odzyskiwania, zachowanie po przerwaniu. |
| V13 | Zakres konstrukcji i instalacja | Inspekcja schematów/BOM/PCB/konfiguracji oraz pomiary i próby kompletnego urządzenia. | Ta sama obsada PCB dla zakresu; właściwa wiązka i montaż, kompaktowość, obudowy/złącza i uzgodnione warunki wodne; jawne wyłączenia funkcji. Dla SYS-167 sprawdzamy realizację toru odcięcia niezależnego od wykonywania głównego firmware. Dla SYS-168 sprawdzamy realizację odłączenia toru rozrusznika przez STOP niezależnie od wykonywania głównego firmware. | Gabaryty, środowisko, parametry prób i kwalifikowane konfiguracje. Inspekcja wyłączenia funkcji jest odrębna od testów funkcji użytkowych. |

Próby dobieramy do wymagania; pełna grupa nie jest automatycznie obowiązkowa dla każdego przypisanego wiersza. Pierwsze stanowisko obejmie Betę, a pozostałe warianty wymagają własnych danych i prób zgodnie z [macierzą silników](../architecture/macierz-wariantow-silnika.md). SYM/stanowisko nie zastępuje walidacji na wymaganym silniku. Zasady i wzór procedury: [weryfikacja](README.md).

## Przydział SYS → blok → grupa

| Wymaganie | Bloki realizujące / współpracujące | Grupy weryfikacji |
| --- | --- | --- |
| SYS-001 | ECU-CTRL, ECU-IN, ECU-OUT | V01, V02 |
| SYS-002 | ECU-CTRL, ECU-IN, ECU-OUT, SYS-INST | V01, V02, V03, V13 |
| SYS-003 | ECU-CTRL, WIN-APP | V09 |
| SYS-004 | ECU-CTRL, ECU-OUT | V04, V05 |
| SYS-005 | ECU-COM, HMI-COM | V07 |
| SYS-006 | WIN-APP | V09 |
| SYS-007 | ECU-CTRL, ECU-DATA, WIN-APP | V09 |
| SYS-008 | HMI-UI, WIN-APP | V08, V09 |
| SYS-009 | ECU-COM, HMI-COM, WIN-APP | V09, V10 |
| SYS-010 | ECU-COM, HMI-COM, WIN-APP | V12 |
| SYS-011 | ECU-COM, ECU-IN, ECU-OUT, WIN-APP | V09 |
| SYS-012 | ECU-CTRL, ECU-OUT | V02 |
| SYS-013 | ECU-PWR | V06 |
| SYS-014 | ECU-IN, ECU-CTRL | V02, V03 |
| SYS-015 | ECU-IN, ECU-OUT, ECU-CTRL, SYS-INST | V02, V03, V13 |
| SYS-016 | HMI-UI, HMI-COM, ECU-COM, ECU-CTRL | V05, V07 |
| SYS-017 | HMI-UI | V08 |
| SYS-018 | ECU-IN, ECU-DATA, HMI-UI | V08, V11 |
| SYS-019 | ECU-CTRL, ECU-DATA | V10 |
| SYS-020 | ECU-DATA, WIN-APP | V10 |
| SYS-021 | ECU-DATA | V10 |
| SYS-022 | ECU-DATA | V10 |
| SYS-023 | ECU-CTRL, ECU-COM, HMI-UI | V08, V10 |
| SYS-024 | ECU-DATA | V10 |
| SYS-025 | ECU-DATA, ECU-COM, WIN-APP | V10 |
| SYS-026 | ECU-COM, WIN-APP | V09 |
| SYS-027 | ECU-COM, HMI-COM, WIN-APP | V09, V12 |
| SYS-028 | ECU-CTRL, ECU-DATA, HMI-UI | V02, V09 |
| SYS-029 | ECU-IN | V03 |
| SYS-030 | ECU-IN, SYS-INST | V03, V13 |
| SYS-031 | ECU-IN | V03 |
| SYS-032 | ECU-CTRL, ECU-OUT, SYS-INST | V13 |
| SYS-033 | SYS-INST, ECU-CTRL, ECU-OUT | V02, V13 |
| SYS-034 | ECU-IN, ECU-OUT, ECU-CTRL | V02 |
| SYS-035 | SYS-INST | V13 |
| SYS-036 | SYS-INST | V13 |
| SYS-037 | ECU-CTRL, ECU-OUT | V04 |
| SYS-038 | ECU-IN, ECU-CTRL, SYS-INST | V02, V13 |
| SYS-039 | ECU-IN, ECU-CTRL, ECU-OUT | V04 |
| SYS-040 | ECU-IN, ECU-CTRL, ECU-OUT | V04 |
| SYS-041 | ECU-IN, ECU-CTRL | V03 |
| SYS-042 | ECU-IN, ECU-CTRL | V13 |
| SYS-043 | ECU-IN, ECU-CTRL, ECU-OUT | V05 |
| SYS-044 | ECU-IN, ECU-CTRL, HMI-UI | V03, V05 |
| SYS-045 | SYS-INST | V13 |
| SYS-046 | ECU-CTRL, ECU-IN, ECU-OUT | V07 |
| SYS-047 | ECU-CTRL, ECU-DATA, ECU-COM | V07 |
| SYS-048 | ECU-IN, ECU-WAKE, ECU-CTRL, ECU-OUT | V04, V06 |
| SYS-049 | ECU-IN, ECU-CTRL, ECU-OUT | V04 |
| SYS-050 | ECU-CTRL, ECU-OUT, ECU-COM | V05, V07 |
| SYS-051 | ECU-IN, ECU-CTRL, ECU-OUT | V05, V07 |
| SYS-052 | ECU-CTRL, ECU-OUT, ECU-COM | V05, V07 |
| SYS-053 | ECU-CTRL, ECU-OUT, ECU-COM | V05, V07 |
| SYS-054 | ECU-PWR, ECU-WAKE, ECU-CTRL, HMI-PWR | V04, V06 |
| SYS-055 | ECU-WAKE, HMI-PWR, HMI-UI | V06 |
| SYS-056 | ECU-COM, ECU-WAKE, HMI-PWR | V06, V09 |
| SYS-057 | ECU-COM, ECU-WAKE, ECU-CTRL, HMI-PWR | V06, V09 |
| SYS-058 | ECU-PWR, HMI-PWR | V06, V09 |
| SYS-059 | ECU-WAKE, ECU-CTRL, HMI-PWR | V06 |
| SYS-060 | ECU-IN, ECU-CTRL, ECU-OUT, ECU-WAKE | V05, V06 |
| SYS-061 | ECU-IN, ECU-CTRL, ECU-OUT | V05, V06 |
| SYS-062 | ECU-WAKE, ECU-CTRL, HMI-PWR, HMI-COM | V06, V07 |
| SYS-063 | ECU-COM, HMI-COM, ECU-WAKE | V06, V07 |
| SYS-064 | ECU-PWR, ECU-WAKE, HMI-PWR | V06 |
| SYS-065 | ECU-PWR, ECU-WAKE, ECU-COM, ECU-DATA, HMI-PWR | V06, V07, V10 |
| SYS-066 | ECU-PWR, ECU-WAKE, HMI-PWR | V06 |
| SYS-067 | ECU-CTRL, ECU-OUT | V02 |
| SYS-068 | ECU-CTRL, ECU-OUT, SYS-INST | V02, V13 |
| SYS-069 | ECU-IN | V01 |
| SYS-070 | ECU-IN | V01 |
| SYS-071 | ECU-IN, ECU-CTRL, ECU-OUT | V02 |
| SYS-072 | ECU-CTRL | V13 |
| SYS-073 | ECU-IN, HMI-UI | V03, V08 |
| SYS-074 | ECU-CTRL, ECU-DATA, HMI-UI, WIN-APP | V11 |
| SYS-075 | ECU-IN, ECU-DATA, HMI-UI, WIN-APP | V11 |
| SYS-076 | ECU-CTRL, ECU-DATA, ECU-COM, WIN-APP | V11, V12 |
| SYS-077 | ECU-DATA, ECU-COM, WIN-APP | V11 |
| SYS-078 | ECU-CTRL, ECU-COM, WIN-APP | V12 |
| SYS-079 | ECU-IN, ECU-WAKE, ECU-DATA | V06, V11 |
| SYS-080 | ECU-WAKE, HMI-PWR, ECU-DATA | V06, V11 |
| SYS-081 | ECU-CTRL, ECU-OUT | V05, V06 |
| SYS-082 | ECU-CTRL, ECU-OUT | V05, V07 |
| SYS-083 | ECU-CTRL, ECU-OUT | V05 |
| SYS-084 | ECU-IN, ECU-CTRL, ECU-OUT | V05, V06 |
| SYS-085 | ECU-CTRL, ECU-OUT, ECU-COM | V05, V09 |
| SYS-086 | HMI-UI, ECU-CTRL, ECU-COM | V05, V08 |
| SYS-087 | ECU-IN, ECU-CTRL, ECU-OUT | V05, V06 |
| SYS-088 | ECU-CTRL, ECU-OUT | V05 |
| SYS-089 | ECU-IN, ECU-CTRL, ECU-OUT | V05 |
| SYS-090 | ECU-IN, ECU-CTRL, ECU-OUT, ECU-COM, WIN-APP | V05, V09 |
| SYS-091 | ECU-CTRL, ECU-OUT, ECU-COM, WIN-APP | V05, V09 |
| SYS-092 | ECU-PWR, ECU-IN, ECU-CTRL | V06 |
| SYS-093 | ECU-PWR, ECU-WAKE, HMI-PWR | V04, V06 |
| SYS-094 | ECU-CTRL, ECU-DATA, ECU-COM, WIN-APP | V02, V09 |
| SYS-095 | ECU-CTRL, ECU-DATA, ECU-COM, WIN-APP | V09 |
| SYS-096 | ECU-IN, ECU-CTRL | V03 |
| SYS-097 | ECU-IN, ECU-CTRL | V03 |
| SYS-098 | SYS-INST, ECU-IN, ECU-CTRL | V03, V13 |
| SYS-099 | ECU-CTRL, ECU-DATA | V07, V09 |
| SYS-100 | ECU-CTRL, ECU-DATA, ECU-WAKE | V06, V09 |
| SYS-101 | ECU-CTRL, ECU-DATA, ECU-COM, WIN-APP | V02, V09 |
| SYS-102 | ECU-CTRL, ECU-IN, ECU-OUT, ECU-DATA, ECU-COM, WIN-APP | V02, V04, V09 |
| SYS-103 | ECU-CTRL, ECU-IN, ECU-OUT, ECU-DATA, ECU-COM, WIN-APP | V04, V09 |
| SYS-104 | ECU-CTRL, ECU-IN, ECU-OUT, ECU-DATA, ECU-COM, WIN-APP | V04, V09 |
| SYS-105 | ECU-CTRL, ECU-IN, ECU-OUT, ECU-DATA, ECU-COM, WIN-APP | V04, V09 |
| SYS-106 | ECU-PWR, ECU-CTRL, ECU-IN, ECU-OUT, ECU-DATA, ECU-COM, WIN-APP | V04, V06, V09 |
| SYS-107 | ECU-CTRL, ECU-IN, ECU-DATA, ECU-COM, WIN-APP | V02, V09 |
| SYS-108 | ECU-CTRL, ECU-IN, ECU-DATA, ECU-COM, WIN-APP | V02, V09 |
| SYS-109 | ECU-PWR, ECU-CTRL, ECU-DATA | V02, V06, V09 |
| SYS-110 | ECU-IN, ECU-CTRL, ECU-OUT, ECU-DATA, ECU-COM, WIN-APP | V04, V09 |
| SYS-111 | ECU-CTRL, ECU-DATA, ECU-COM, WIN-APP | V02, V04, V09 |
| SYS-112 | ECU-CTRL, ECU-DATA, ECU-COM, WIN-APP | V09 |
| SYS-113 | ECU-CTRL, ECU-DATA, ECU-COM, WIN-APP | V09 |
| SYS-114 | ECU-CTRL, ECU-DATA, ECU-COM, WIN-APP | V09 |
| SYS-115 | ECU-CTRL, ECU-DATA, ECU-COM, WIN-APP | V09 |
| SYS-116 | ECU-CTRL, ECU-DATA, ECU-COM, WIN-APP | V02, V09 |
| SYS-117 | ECU-CTRL, ECU-DATA, ECU-IN, ECU-OUT, ECU-COM, WIN-APP | V04, V09 |
| SYS-118 | ECU-CTRL, ECU-DATA, HMI-UI, WIN-APP | V02, V09 |
| SYS-119 | ECU-CTRL, ECU-DATA, ECU-OUT, HMI-UI, WIN-APP | V02, V09 |
| SYS-120 | ECU-IN, ECU-CTRL, ECU-DATA, ECU-OUT, WIN-APP | V02, V09 |
| SYS-121 | ECU-IN, ECU-CTRL, ECU-DATA, ECU-OUT, ECU-COM | V02, V10 |
| SYS-122 | ECU-CTRL, ECU-DATA, WIN-APP | V02, V09 |
| SYS-123 | ECU-IN, ECU-CTRL, ECU-DATA, ECU-OUT | V02 |
| SYS-124 | ECU-IN, ECU-CTRL, ECU-DATA, ECU-OUT, ECU-COM | V02, V04, V10 |
| SYS-125 | ECU-IN, ECU-CTRL, ECU-DATA, WIN-APP | V02, V09 |
| SYS-126 | ECU-IN, ECU-CTRL, ECU-DATA, WIN-APP | V02, V09 |
| SYS-127 | ECU-IN, ECU-CTRL, ECU-DATA, WIN-APP | V02, V03, V09 |
| SYS-128 | ECU-IN, ECU-CTRL, ECU-DATA, ECU-OUT, ECU-COM | V02, V10 |
| SYS-129 | ECU-IN, ECU-CTRL, ECU-DATA, ECU-OUT, ECU-COM | V02, V04, V10 |
| SYS-130 | ECU-IN, ECU-CTRL, ECU-DATA, ECU-OUT | V02, V04 |
| SYS-131 | ECU-IN, ECU-CTRL, ECU-DATA, ECU-OUT, ECU-COM | V02, V04, V10 |
| SYS-132 | ECU-IN, ECU-CTRL, ECU-DATA, ECU-OUT | V02, V04 |
| SYS-133 | ECU-IN, ECU-CTRL, ECU-DATA, ECU-OUT | V02, V04 |
| SYS-134 | ECU-IN, ECU-CTRL, ECU-DATA, ECU-OUT | V02, V04 |
| SYS-135 | ECU-CTRL, ECU-DATA, ECU-COM, HMI-COM, HMI-UI | V02, V07, V08 |
| SYS-136 | ECU-IN, ECU-CTRL, ECU-DATA, ECU-OUT | V02, V04 |
| SYS-137 | ECU-CTRL, ECU-DATA, ECU-COM, HMI-COM, HMI-UI | V02, V04, V07, V08 |
| SYS-138 | ECU-CTRL, ECU-DATA | V02, V06, V07, V09 |
| SYS-139 | ECU-CTRL, ECU-DATA, ECU-OUT, ECU-COM | V02, V04, V09, V10 |
| SYS-140 | ECU-CTRL, ECU-DATA, ECU-OUT, ECU-COM | V02, V04, V09, V10 |
| SYS-141 | ECU-CTRL, ECU-DATA, ECU-OUT, ECU-COM | V02, V04, V09, V10 |
| SYS-142 | ECU-CTRL, ECU-DATA | V02, V06, V07, V09 |
| SYS-143 | ECU-CTRL, ECU-DATA, ECU-COM, HMI-COM, HMI-UI | V02, V07, V08 |
| SYS-144 | ECU-CTRL, ECU-DATA, ECU-COM, HMI-COM, HMI-UI | V02, V07, V08 |
| SYS-145 | ECU-CTRL, ECU-DATA, ECU-COM, HMI-COM, HMI-UI | V02, V07, V08 |
| SYS-146 | ECU-CTRL, ECU-DATA, ECU-COM, HMI-COM, HMI-UI | V02, V07, V08 |
| SYS-147 | ECU-CTRL, ECU-DATA, ECU-COM, HMI-COM, HMI-UI | V02, V04, V07, V08 |
| SYS-148 | ECU-CTRL, ECU-DATA, ECU-COM, HMI-COM, HMI-UI | V02, V07, V08 |
| SYS-149 | ECU-CTRL, ECU-IN, ECU-DATA, ECU-COM, HMI-COM, HMI-UI | V02, V04, V07, V08 |
| SYS-150 | ECU-CTRL, ECU-DATA, ECU-COM, HMI-COM, HMI-UI | V02, V06, V07, V08 |
| SYS-151 | ECU-CTRL, ECU-COM, HMI-COM, HMI-UI | V02, V07, V08 |
| SYS-152 | ECU-CTRL, ECU-IN, ECU-OUT, ECU-DATA, ECU-COM, WIN-APP | V04, V06, V09, V11 |
| SYS-153 | ECU-DATA, ECU-COM | V11 |
| SYS-154 | ECU-DATA, ECU-COM, WIN-APP | V09, V10 |
| SYS-155 | ECU-PWR, ECU-CTRL, ECU-OUT, ECU-DATA, ECU-COM, WIN-APP | V04, V06, V09 |
| SYS-156 | ECU-CTRL, ECU-OUT, ECU-DATA, ECU-COM, WIN-APP | V04, V06, V09 |
| SYS-157 | ECU-IN, ECU-CTRL, ECU-OUT | V01, V02, V04 |
| SYS-158 | ECU-IN, ECU-CTRL, ECU-OUT | V01, V04 |
| SYS-159 | ECU-IN, ECU-CTRL, ECU-OUT | V01, V02, V04 |
| SYS-160 | ECU-IN, ECU-CTRL, ECU-OUT | V04 |
| SYS-161 | ECU-IN, ECU-CTRL, ECU-OUT | V04 |
| SYS-162 | ECU-IN, ECU-CTRL, ECU-OUT | V04 |
| SYS-163 | ECU-IN, ECU-CTRL | V03, V04 |
| SYS-164 | ECU-IN, ECU-CTRL, ECU-OUT, ECU-DATA | V02, V04, V10 |
| SYS-165 | ECU-IN, ECU-CTRL | V03 |
| SYS-166 | ECU-IN, ECU-CTRL, ECU-OUT, ECU-DATA | V02, V04, V10 |
| SYS-167 | ECU-IN, ECU-CTRL, ECU-OUT | V04, V13 |
| SYS-168 | ECU-IN, ECU-CTRL, ECU-OUT | V04, V13 |

## Sposób utrzymania

- Nowe lub zmienione SYS otrzymuje przydział bloków i weryfikacji w tej samej zmianie dokumentacji.
- Rozwijana procedura otrzyma własny trwały ID i odsyłacz z odpowiedniego wymagania; ID grupy V nie jest numerem gotowej procedury.
- Wyniki zapisujemy dla konkretnych rewizji i konfiguracji. Test przeprowadzony na Becie nie zamyka automatycznie wiersza dla 4T/TPI/TBI.
- Zamknięcie wymagania następuje dopiero po ocenie wymaganych dowodów i ograniczeń. Do tego czasu zachowujemy status niezweryfikowany.

Najbliżej: uzupełnić dane osprzętu, reguły map i stany awaryjne; następnie dopisać mierzalne kryteria i procedury dla projektowanych bloków. [Plan INV Bety](beta-2015-plan-inwentaryzacji.md) dotyczy pozyskania danych wejściowych, nie jest próbą gotowego DustONE.
