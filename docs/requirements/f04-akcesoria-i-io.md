# F04 — akcesoria i dodatkowe I/O

Stan na 2026-11-25. **F04 aktywny po zamknięciu F03 w pytaniu 243.** Aktualny temat: dodatkowe wyjścia mocy. Zasady klaksonu SYS-236–240 są już przyjęte i zachowane poniżej. Źródłem wymagań jest [rejestr SYS](../01-zakres-systemu.md); kolejność i warunki zamknięcia określa [proces](../00-proces-i-status.md).

## Zakres i kolejność

| Temat | Stan |
| --- | --- |
| Klakson po utracie HMI/CAN | Przyjęty SYS-236, odpowiedź A na pytanie 244. |
| Klakson po odzyskaniu łączności | Przyjęty SYS-237, odpowiedź A na pytanie 245: zwolnienie i nowe naciśnięcie. |
| Klakson po restarcie ECU | Przyjęty SYS-238, odpowiedź A na pytanie 246: zwolnienie i nowe naciśnięcie. |
| Klakson przy zwykłym wybudzeniu ze snu | Przyjęty SYS-239, odpowiedź B na pytanie 247: pierwsze naciśnięcie wybudza; sygnał wymaga zwolnienia i nowego naciśnięcia. |
| Autotest klaksonu | Przyjęty SYS-240, odpowiedź A na pytanie 248: bez samoczynnego dźwięku; próba dźwiękowa na świadome polecenie użytkownika. |
| Pozostałe stany akcesoriów | W kolejce w F04: start/restart ECU, powrót łączności i brakujące reguły wyjść. Zachowujemy przyjęte SYS-050–053 oraz SYS-081–091. |
| Dodatkowe wyjścia mocy | Przyjęte zastosowania SYS-241, odpowiedź B na pytanie 249: oświetlenie i zewnętrzne akcesoria. Przyjęte 3 niezależne kanały SYS-242, odpowiedź B na pytanie 250; po utracie HMI/CAN każdy zachowuje swój stan według SYS-243 (A na pytanie 251). Stany po restarcie są otwarte w pytaniu 252. |
| Sygnałowe I/O i komunikacja | Osobny przegląd po wyjściach mocy; wymagania funkcjonalne oddzielamy od późniejszego doboru interfejsów i torów. |

Klakson należy do przyjętego zakresu SYS-004. Obecność klaksonu 12 V w dokumentacji Bety jest potwierdzona w [analizie instrukcji i suplementu](../interfaces/beta-2015-analiza-dokumentacji.md). ECU steruje odbiornikiem, a HMI przekazuje polecenia kierowcy. Nie ustalono tu jeszcze pełnej obsługi przycisku ani wszystkich stanów po restarcie.

## Klakson po utracie HMI lub CAN

Brak łączności może uniemożliwić przekazanie polecenia wyłączenia. W odpowiedzi **A na pytanie 244** (2026-11-24) właściciel przyjął SYS-236: po potwierdzeniu utraty HMI/CAN ECU wyłącza aktywny klakson, lokalnie i bez komputera.

Zasada nie zmienia samodzielnej pracy silnika według SYS-046. Nie ustanawia nowego DTC; ponowne załączenie po powrocie łączności podlega SYS-237. Czas wykrycia utraty, kryteria ważności komunikacji i czas wyłączenia wymagają określenia w etapie 4 i procedury z etapu 5.

### Plan próby SYS-236

1. Na stanowisku rzeczywistego ECU i sprawnego toru klaksonu odtworzyć prawidłową komunikację HMI. Załączyć klakson zaakceptowanym poleceniem. Rejestrować komunikację, stan ECU i rzeczywiste napięcie/prąd wyjścia.
2. Osobno odtworzyć wyłączenie HMI, przerwę komunikacji CAN oraz zatrzymanie wymaganych komunikatów HMI przy pozostającym zasilaniu. Dla każdego przypadku potwierdzić lokalne rozpoznanie utraty i wyłączenie klaksonu według kryteriów projektu. Zmierzyć czas od potwierdzenia utraty do wyłączenia; granice liczbowe ustalić przed wykonaniem.
3. Powtórzyć bez sesji Windows oraz z symulowaną pracą i zatrzymaniem silnika. Wyłączenie klaksonu ma nie wymagać nowego polecenia z HMI lub PC; sama utrata HMI nie wyłącza sterowania silnikiem według SYS-046.
4. Sprawdzić utratę łączności przy już wyłączonym klaksonie i niezależne działanie istniejących zabezpieczeń wyjścia. Zachowanie po odzyskaniu łączności sprawdzić odrębnie według planu SYS-237. Wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

Plan wymaga procedury wykonawczej, stanowiska i kryteriów liczbowych. Nie ma wyników prób produktu.

## Klakson po odzyskaniu łączności

W odpowiedzi **A na pytanie 245** (2026-11-24) właściciel przyjął SYS-237: powrót HMI/CAN nie wznawia klaksonu wyłączonego po utracie łączności. Przy trzymanym przycisku klakson pozostaje wyłączony; ponowne użycie wymaga zwolnienia i nowego naciśnięcia.

ECU egzekwuje tę regułę na podstawie wiarygodnych danych HMI. Stany przycisku, rozpoznanie nowego naciśnięcia i odrzucanie wcześniejszych poleceń rozwiniemy w etapie 4. Ustalenie dotyczy odzyskania komunikacji po SYS-236; obsługę nadal trzymanego przycisku po restarcie ECU określa SYS-238.

### Plan próby SYS-237

1. Na stanowisku ECU–HMI załączyć klakson, przerwać łączność i potwierdzić wyłączenie według SYS-236. Trzymając przycisk, przywrócić prawidłową komunikację. Potwierdzić, że rzeczywiste wyjście pozostaje wyłączone mimo informacji o nadal naciśniętym przycisku.
2. Zwolnić przycisk, potwierdzić odebranie prawidłowego stanu zwolnienia i ponownie go nacisnąć. Przy spełnionych pozostałych warunkach potwierdzić załączenie klaksonu. Osobno odtworzyć powrót łączności z przyciskiem już zwolnionym.
3. Odtworzyć wcześniejsze polecenia załączenia oraz ponowną utratę i powrót łączności przed nowym naciśnięciem. Sprawdzić brak samoczynnego wznowienia i brak uznania powtarzanego stanu „naciśnięty” za nowe naciśnięcie. Szczegóły danych i kryteria ważności ustalić z protokołem przed wykonaniem.
4. Powtórzyć po utracie zasilania samego HMI oraz bez sesji Windows, przy aktywnych zabezpieczeniach wyjścia. Rejestrować CAN, stan kwalifikacji w ECU i rzeczywiste napięcie/prąd klaksonu. Wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Klakson po restarcie ECU

W odpowiedzi **A na pytanie 246** (2026-11-24) właściciel przyjął SYS-238: po odzyskaniu gotowości ECU nie wznawia klaksonu na podstawie przycisku trzymanego od czasu sprzed restartu. Ponowne użycie wymaga zwolnienia i nowego naciśnięcia.

Reguła dotyczy obsługi poleceń użytkownika po restarcie. Zwykłe wybudzenie określa SYS-239; autotest bez samoczynnego dźwięku podlega SYS-240. Kwalifikację stanów przycisku i moment dopuszczenia poleceń opracujemy w etapie 4.

### Plan próby SYS-238

1. Na stanowisku ECU–HMI załączyć klakson i wywołać kontrolowany restart ECU, pozostawiając HMI działające oraz przycisk trzymany. Po odzyskaniu gotowości ECU i prawidłowej komunikacji potwierdzić brak zwykłego załączenia klaksonu ze starego stanu przycisku. Rejestrować komunikację, gotowość ECU i rzeczywiste napięcie/prąd wyjścia.
2. Zwolnić przycisk i nacisnąć go ponownie. Przy potwierdzonych stanach i spełnionych pozostałych warunkach potwierdzić dopuszczenie nowego użycia klaksonu. Osobno rozpocząć od zwolnionego przycisku i sprawdzić pierwsze nowe naciśnięcie po gotowości.
3. Powtórzyć dla reprezentatywnych przyczyn restartu objętych projektem oraz wcześniejszych poleceń załączenia odtwarzanych przez HMI. Po każdym restarcie potwierdzić tę samą kwalifikację; nie traktować ponownego komunikatu o nadal trzymanym przycisku jako nowego naciśnięcia.
4. Powtórzyć bez sesji Windows i z aktywną odrębną ochroną wyjścia. Zabezpieczenia nadal obowiązują. Zwykłe wybudzenie sprawdzić odrębnie według SYS-239; brak samoczynnej próby dźwiękowej potwierdzić według SYS-240. Przed wykonaniem ustalić kryteria, połączenia i sposób restartu; wyniki powiązać z HW/FW oraz konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Klakson przy zwykłym wybudzeniu

W odpowiedzi **B na pytanie 247** (2026-11-24) właściciel przyjął SYS-239. Pierwsze naciśnięcie klaksonu wybudza HMI i ECU, ale nie załącza sygnału. Po gotowości trzeba zwolnić przycisk i nacisnąć go ponownie, również gdy przed snem nie było blokady.

Przyjęta obsługa klaksonu różni się od obsługi START na tym samym przytrzymaniu według SYS-204. Zasady rozruchu silnika pozostają odrębne. SYS-239 dotyczy polecenia kierowcy; autotest bez samoczynnego dźwięku podlega SYS-240.

### Plan próby SYS-239

1. Doprowadzić stanowisko ECU–HMI do prawidłowego snu, bez wcześniejszego warunku nowego naciśnięcia po usterce. Nacisnąć i trzymać klakson. Potwierdzić wybudzenie obu urządzeń i brak zwykłego załączenia z tego naciśnięcia także po gotowości. Rejestrować stany przycisku, komunikację, gotowość i rzeczywiste wyjście.
2. Osobno zwolnić przycisk przed uzyskaniem gotowości oraz po niej. Potwierdzić brak odłożonego sygnału z pierwszego naciśnięcia. Po gotowości wykonać nowe naciśnięcie; przy pozostałych spełnionych warunkach potwierdzić dopuszczenie klaksonu.
3. Powtarzać prawidłowe cykle snu i wybudzenia, również bez sesji Windows. Sprawdzić, że powtarzane dane o nadal trzymanym przycisku nie są uznawane za nowe naciśnięcie. Obecność odrębnego warunku SYS-237/238 nie może zostać pominięta przez sen.
4. Oddzielnie rejestrować zwykłe polecenia użytkownika i sprawdzenia autotestu; potwierdzić brak samoczynnego sygnału według SYS-240. Przed wykonaniem ustalić kryteria gotowości, połączenia i pomiar wyjścia; wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Autotest bez samoczynnego dźwięku klaksonu

W odpowiedzi **A na pytanie 248** (2026-11-24) właściciel przyjął SYS-240: autotest nie wywołuje samoczynnego sygnału klaksonu. Próbę dźwiękową wywołuje świadomie użytkownik. Automatyczne sprawdzenia obejmują zakres dostępny bez dźwięku, zweryfikowany dla rzeczywistego toru i odbiornika.

Przykład możliwości sprzętowej: [Infineon — diagnostyka open-load w stanie OFF](https://community.infineon.com/t5/Knowledge-Base-Articles/How-an-open-load-condition-can-be-detected-by-PROFET-2-12V-devices/ta-p/458652) opisuje badanie obwodu małym prądem bez uruchomienia obciążenia, z koniecznością dopasowania do odbiornika i weryfikacji. To podstawa do analizy, a nie potwierdzenie konkretnego rozwiązania DustONE. Metodę i układy dobierzemy wspólnie; wynik elektryczny nie potwierdza prawidłowego dźwięku.

### Plan próby SYS-240

1. Na stanowisku rzeczywistego ECU–HMI z klaksonem wykonać autotest przy wszystkich źródłach wybudzenia objętych SYS-054–056/079–080 oraz reprezentatywnych uruchomieniach ECU. Bez świadomego polecenia próby dźwiękowej potwierdzić brak sygnału. Rejestrować polecenia, napięcie/prąd wyjścia i ocenę akustyczną według kryteriów ustalonych przed próbą.
2. Dla zaprojektowanej diagnostyki odtworzyć nominalny obwód oraz wykrywalne przerwy i zwarcia na właściwym stanowisku, w granicach zabezpieczeń. Sprawdzić rzeczywiste pokrycie, wyniki i brak dźwięku podczas automatycznych sprawdzeń. Wynik musi odpowiadać sprawdzonym cechom; nie uznawać samej poprawnej odpowiedzi elektrycznej za potwierdzenie prawidłowego dźwięku.
3. Wywołać świadomie próbę dźwiękową, wykorzystując przyjętą obsługę przycisku albo istniejący test serwisowy po jego dopuszczeniu. Potwierdzić reakcję na polecenie i zachowanie zabezpieczeń. Po powrocie łączności, restarcie i śnie obowiązują także SYS-237–239.
4. Powtórzyć cykle snu/wybudzenia, przypadek ruchu koła i autotest bez sesji Windows. Nie dopuszczać do samoczynnego dźwięku jako efektu zakończenia autotestu lub gotowości HMI. Kryteria, połączenia i wyposażenie akustyczne oraz elektryczne ustalić przed wykonaniem; wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Przegląd przyjętej części dotyczącej klaksonu

| Przypadek | Przyjęta reguła | Podstawa |
| --- | --- | --- |
| Utrata HMI/CAN | ECU wyłącza aktywny klakson. | A na 244, SYS-236 |
| Odzyskanie łączności | Zwolnienie i nowe naciśnięcie zamiast wznowienia starego stanu. | A na 245, SYS-237 |
| Restart ECU | Zwolnienie i nowe naciśnięcie po stanie sprzed restartu. | A na 246, SYS-238 |
| Zwykłe wybudzenie klaksonem | Pierwsze naciśnięcie wybudza; sygnał wymaga zwolnienia i nowego naciśnięcia. | B na 247, SYS-239 |
| Autotest | Bez samoczynnego dźwięku; próbę dźwiękową wywołuje użytkownik. | A na 248, SYS-240 |

Sprawdzono spójność tych reguł z autonomią ECU, wybudzaniem SYS-055 i autotestem SYS-194. Naciśnięcie wybudzające nie omija kwalifikacji nowego użycia, a autotest nie zastępuje świadomego polecenia dźwięku. Każde z SYS-236–240 ma plan próby i przypisanie do bloków oraz grup weryfikacji.

Metody, progi, czasy i kwalifikację danych opracujemy w etapie 4; procedury w etapie 5, a tor mocy i jego diagnostykę w etapach 6–8. Wspólne reguły energii i pozostałych odbiorników nadal należą do F04. Przyjęta część SYS-236–240 nie zamyka całego pakietu.

## Dodatkowe wyjścia mocy

W odpowiedzi **B na doprecyzowane pytanie 249** (2026-11-24) właściciel przyjął SYS-241: dodatkowe oświetlenie oraz zasilanie zewnętrznych akcesoriów, np. GPS lub zewnętrznej ładowarki telefonu.

Wyjście mocy steruje prądem odbiornika. Sposób sterowania, np. ON/OFF lub PWM mocy, dobierzemy do zastosowania. Logiczny sygnał PWM do zewnętrznego modułu i interfejs komunikacyjny są odrębnymi funkcjami, do osobnego przeglądu I/O. Odpowiedź 249 określa zastosowania wyjść mocy.

W odpowiedzi **B na pytanie 250** (2026-11-24) właściciel przyjął **trzy niezależnie sterowane dodatkowe kanały mocy** (SYS-242), ponad wyjściami dla uzgodnionego osprzętu silnika i podstawowych akcesoriów. Wybór nie ustala stałego przypisania lamp lub akcesoriów do konkretnego kanału. Jeden kanał może zasilać grupę odbiorników załączanych razem; osobne sterowanie grupami wymaga osobnych kanałów. Konkretne urządzenia, prądy, dopuszczone kombinacje i warunki pracy określimy z danymi osprzętu oraz architekturą. Komponenty wybierzemy wspólnie na etapie doboru.

### Plan próby SYS-241

1. Po uzgodnieniu liczby i funkcji kanałów oraz parametrów wybrać reprezentatywną lampę dodatkową i zewnętrzny moduł zasilania akcesorium. Z ich dokumentacji wyznaczyć warunki, wartości dopuszczalne i kryteria sprawdzenia; najpierw zweryfikować tor ECU na stanowisku z właściwymi obciążeniami.
2. Dla każdej dopuszczonej konfiguracji załączyć i wyłączyć odbiorniki przyjętym interfejsem poleceń. Na rzeczywistym ECU mierzyć napięcie/prąd wyjścia oraz stan zasilanego urządzenia. Sprawdzić zgodność z zakresem deklarowanym dla danego kanału; nie zakładać obsługi dowolnego odbiornika.
3. Sprawdzić przyjęte konfiguracje w kwalifikowanym zakresie zasilania i temperatury, z zachowaniem zabezpieczeń oraz uzgodnionych reguł energii. Sposób sterowania i reakcje na usterki mają odpowiadać później przyjętej specyfikacji kanału. Prądy rozruchowe i równoczesność odbiorników uwzględnić w kryteriach.
4. Po kwalifikacji stanowiskowej potwierdzić zasilanie rzeczywistych urządzeń i obsługę w HMI/Windows zgodnie z ich przyjętym zakresem. Przygotować połączenia, wyposażenie i warunki przerwania przed wykonaniem; wyniki powiązać z HW/FW, konfiguracją i modelami odbiorników. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan zakresu do rozwinięcia po ustaleniu kanałów i parametrów. Nie ma wyników prób produktu.

## Trzy dodatkowe kanały mocy

SYS-242 ustala liczbę kanałów. Ich przeznaczenie podlega konfiguracji i dopuszczonym zastosowaniom SYS-241. Parametry, dozwolone kombinacje oraz rzeczywiste obciążenia określimy z danymi osprzętu w architekturze; nie wybrano topologii, układów ani pinów złącza.

### Plan próby SYS-242

1. Po określeniu specyfikacji podłączyć do rzeczywistego ECU trzy obciążenia stanowiskowe w dopuszczonym zakresie. Z przyjętego interfejsu załączać i wyłączać każdy kanał osobno; mierzyć rzeczywisty stan napięcia/prądu wszystkich trzech.
2. Sprawdzić niezależność zwykłych poleceń: zmiana jednego kanału nie zmienia zadanych stanów pozostałych dwóch. Przejść przez dopuszczone kombinacje trzech stanów ON/OFF, w tym równoczesne załączenie w granicach obciążeń określonych przez projekt.
3. Powtórzyć sprawdzenie dla przyjętych konfiguracji oświetlenia i akcesoriów oraz kwalifikowanego zasilania i temperatur. Odrębnie sprawdzić granice wspólnych i indywidualnych zabezpieczeń według ich specyfikacji; sama niezależność zwykłego sterowania nie określa jeszcze izolacji usterek.
4. Potwierdzić poprawne przypisanie poleceń i odczytów HMI/Windows do każdego kanału oraz właściwy fizyczny tor. Przed wykonaniem ustalić kryteria, połączenia, obciążenia i warunki przerwania; wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

Plan wymaga danych i procedury wykonawczej; prób produktu jeszcze nie wykonano.

## Dodatkowe kanały po utracie HMI lub CAN

W odpowiedzi **A na pytanie 251** (2026-11-25) właściciel przyjął SYS-243: przy działającym ECU trzy dodatkowe kanały mocy zachowują własne ostatnie stany pracy po potwierdzonej utracie HMI/CAN. Zabezpieczenia i ochrona energii mogą nadal zmienić stan według swoich reguł.

Zasada utrzymuje dodatkowe oświetlenie i zasilanie akcesoriów mimo niedostępnego interfejsu. Jest spójna z autonomią ECU SYS-046 i przyjętym zachowaniem świateł podstawowych SYS-050. Nie określa stanów po resecie procesora lub zaniku zasilania. Kryteria łączności i czasy opracujemy z protokołem w etapie 4.

### Plan próby SYS-243

1. Na stanowisku ECU–HMI ustawić dopuszczone kombinacje stanów trzech kanałów, także mieszane ON/OFF. Osobno odtworzyć odłączenie zasilania HMI, przerwanie CAN oraz brak wymaganych komunikatów HMI. Po potwierdzeniu utraty sprawdzić zachowanie stanu pracy każdego kanału; rejestrować komunikację, stan zadany i rzeczywiste napięcie/prąd wyjść.
2. Powtórzyć przy symulowanej pracy i zatrzymaniu silnika oraz bez sesji Windows. Sama utrata HMI/CAN nie ma wyłączać dodatkowych kanałów ani sterowania silnikiem według SYS-046. Potwierdzić lokalną realizację stanów przez ECU.
3. Przy utraconej łączności odtworzyć warunki zadziałania przewidzianych zabezpieczeń wyjść i ochrony energii. Potwierdzić właściwe odcięcia; zachowanie stanu po utracie HMI nie może omijać ochrony. Warunki i wartości ustalić przed próbą według specyfikacji profilu i kanałów.
4. Przywrócić komunikację i odczytać rzeczywiste stany ECU. Sprawdzić zgodność odczytów bez zmiany wyjść z samego odczytu; obsługę nowych poleceń kwalifikować według protokołu. Osobno sprawdzamy restart ECU po decyzji z pytania 252. Kryteria, połączenia i warunki przerwania przygotować przed wykonaniem; wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Następna decyzja

**Pytanie 252:** jakie stany trzech dodatkowych kanałów dopuścić po restarcie ECU i odzyskaniu gotowości: wyłączone do nowego polecenia czy odtworzone z wcześniejszego zapamiętanego stanu? Dotyczy ponownego uruchomienia ECU, nie ciągłej pracy bez HMI ani zwykłego wybudzenia ze snu. Zabezpieczenia i ochrona energii nadal obowiązują.
