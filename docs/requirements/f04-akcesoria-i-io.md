# F04 — akcesoria i dodatkowe I/O

Stan na 2026-11-26. **F04 aktywny po zamknięciu F03 w pytaniu 243.** Aktualny temat: stany świateł awaryjnych wskazanych w odpowiedzi 265, przed przeglądem zamykającym F04. Zasady klaksonu SYS-236–240 są już przyjęte i zachowane poniżej. Źródłem wymagań jest [rejestr SYS](../01-zakres-systemu.md); kolejność i warunki zamknięcia określa [proces](../00-proces-i-status.md).

## Zakres i kolejność

| Temat | Stan |
| --- | --- |
| Klakson po utracie HMI/CAN | Przyjęty SYS-236, odpowiedź A na pytanie 244. |
| Klakson po odzyskaniu łączności | Przyjęty SYS-237, odpowiedź A na pytanie 245: zwolnienie i nowe naciśnięcie. |
| Klakson po restarcie ECU | Przyjęty SYS-238, odpowiedź A na pytanie 246: zwolnienie i nowe naciśnięcie. |
| Klakson przy zwykłym wybudzeniu ze snu | Przyjęty SYS-239, odpowiedź B na pytanie 247: pierwsze naciśnięcie wybudza; sygnał wymaga zwolnienia i nowego naciśnięcia. |
| Autotest klaksonu | Przyjęty SYS-240, odpowiedź A na pytanie 248: bez samoczynnego dźwięku; próba dźwiękowa na świadome polecenie użytkownika. |
| Pozostałe stany akcesoriów | W toku w F04. Przyjęty SYS-250, A na pytanie 258: podstawowe światła po nieplanowanym restarcie i przy zgaszonym silniku OFF do nowego polecenia. Zachowujemy SYS-050–053 oraz SYS-081–091. |
| Kierunkowskazy po powrocie HMI/CAN | Przyjęty SYS-251, odpowiedź A na pytanie 259: pozostają OFF do nowego świadomego wyboru użytkownika, bez wznowienia dawnych stanów. |
| Kierunkowskazy po restarcie i prawidłowym śnie | Przyjęty SYS-252, odpowiedź A na pytanie 260: wyłączenie przed snem; po wybudzeniu i restarcie OFF do nowego świadomego wyboru. |
| Próby podstawowego oświetlenia, kierunkowskazów i klaksonu po ochronnym odcięciu | Przyjęty SYS-253, odpowiedź A na pytanie 261: jedna świadoma próba, po niepowodzeniu blokada danego kanału jak SYS-247/248; bez samoczynnych ponowień. |
| Inicjowanie próby światła hamowania | Przyjęty SYS-254, odpowiedź A na pytanie 262: nowe użycie któregokolwiek hamulca po zwolnieniu obu może zlecić jedną próbę bez HMI, przy dostępnym limicie i spełnionych warunkach. |
| Dodatkowe wyjścia mocy | Zastosowania SYS-241 i 3 niezależne kanały SYS-242 przyjęte odpowiedziami B na pytania 249–250. |
| Dodatkowe kanały po utracie HMI/CAN | Zachowują własne stany według SYS-243, odpowiedź A na pytanie 251. |
| Dodatkowe kanały po restarcie ECU | Start od wyłączonych według SYS-244, odpowiedź A na pytanie 252. |
| Dodatkowe kanały przy prawidłowym śnie i wybudzeniu | Wyłączone przed snem i po wybudzeniu do nowego polecenia według SYS-245, odpowiedź A na pytanie 253. |
| Sposób sterowania dodatkowymi lampami | Przyjęty SYS-246, odpowiedź A na pytanie 254: ON/OFF i opcjonalny PWM mocy dla zgodnych lamp; GPS i ładowarki w trybie ON/OFF. |
| Ponowne załączenie dodatkowego kanału po ochronnym odcięciu | Przyjęty SYS-247, odpowiedź A na pytanie 255: ograniczona próba wyłącznie na nowe świadome polecenie, bez samoczynnych ponowień. |
| Limit świadomych prób po niepowodzeniu | Przyjęty SYS-248, odpowiedź A na pytanie 256: po jednej nieudanej próbie blokada danego kanału do pełnego cyklu snu lub zaniku i powrotu zasilania. |
| Wpływ usterki jednego kanału na pozostałe | Przyjęty SYS-249, odpowiedź A na pytanie 257: odcięcie tylko uszkodzonego kanału przy prawidłowych warunkach pozostałych; wspólne zagrożenia pozostają nadrzędne. |
| Sygnałowe I/O i komunikacja | Przyjęty SYS-255, odpowiedź A na pytanie 263: zewnętrzne porty wynikają z uzgodnionych funkcji; bez rezerwy do nieokreślonych urządzeń. Parametry, zasoby i pinout do architektury. |
| Wybudzanie przez hamulce | Przyjęty SYS-256, odpowiedź A na pytanie 264: nowe użycie dowolnego hamulca wybudza ECU i HMI; światło działa bez oczekiwania na HMI. |
| Lista odcięcia oszczędzania | Przyjęty SYS-257, odpowiedź na 265 i A na doprecyzowanie: światło hamowania oraz awaryjne dostępne, pojedyncze kierunkowskazy i klakson odcięte razem ze światłami stałymi i trzema dodatkowymi kanałami. |
| Stany awaryjnych | Przyjęte SYS-258–260: podtrzymanie bez HMI/CAN, blokada snu i OFF po restarcie/powrocie zasilania do nowego polecenia. Współdziałanie z wyborem strony nadal otwarte; następna decyzja 269. |

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

1. Na stanowisku rzeczywistego ECU–HMI z klaksonem wykonać autotest przy wszystkich źródłach wybudzenia objętych SYS-054–056/079–080/256 oraz reprezentatywnych uruchomieniach ECU. Bez świadomego polecenia próby dźwiękowej potwierdzić brak sygnału. Rejestrować polecenia, napięcie/prąd wyjścia i ocenę akustyczną według kryteriów ustalonych przed próbą.
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

Wyjście mocy steruje prądem odbiornika. Sposób sterowania określa późniejsze SYS-246: ON/OFF i opcjonalny PWM mocy zgodnych lamp; parametry dobierzemy do zastosowania. Logiczny sygnał PWM do zewnętrznego modułu i interfejs komunikacyjny są odrębnymi funkcjami, do osobnego przeglądu I/O. Odpowiedź 249 określa zastosowania wyjść mocy.

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

Zasada utrzymuje dodatkowe oświetlenie i zasilanie akcesoriów mimo niedostępnego interfejsu. Jest spójna z autonomią ECU SYS-046 i przyjętym zachowaniem świateł podstawowych SYS-050. Stany po nieplanowanym restarcie lub powrocie zasilania określa SYS-244. Kryteria łączności i czasy opracujemy z protokołem w etapie 4.

### Plan próby SYS-243

1. Na stanowisku ECU–HMI ustawić dopuszczone kombinacje stanów trzech kanałów, także mieszane ON/OFF. Osobno odtworzyć odłączenie zasilania HMI, przerwanie CAN oraz brak wymaganych komunikatów HMI. Po potwierdzeniu utraty sprawdzić zachowanie stanu pracy każdego kanału; rejestrować komunikację, stan zadany i rzeczywiste napięcie/prąd wyjść.
2. Powtórzyć przy symulowanej pracy i zatrzymaniu silnika oraz bez sesji Windows. Sama utrata HMI/CAN nie ma wyłączać dodatkowych kanałów ani sterowania silnikiem według SYS-046. Potwierdzić lokalną realizację stanów przez ECU.
3. Przy utraconej łączności odtworzyć warunki zadziałania przewidzianych zabezpieczeń wyjść i ochrony energii. Potwierdzić właściwe odcięcia; zachowanie stanu po utracie HMI nie może omijać ochrony. Warunki i wartości ustalić przed próbą według specyfikacji profilu i kanałów.
4. Przywrócić komunikację i odczytać rzeczywiste stany ECU. Sprawdzić zgodność odczytów bez zmiany wyjść z samego odczytu; obsługę nowych poleceń kwalifikować według protokołu. Restart ECU sprawdzić odrębnie według planu SYS-244. Kryteria, połączenia i warunki przerwania przygotować przed wykonaniem; wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Dodatkowe kanały po restarcie ECU

W odpowiedzi **A na pytanie 252** (2026-11-25) właściciel przyjął SYS-244: po nieplanowanym restarcie lub powrocie zasilania ECU rozpoczyna sterowanie trzema dodatkowymi kanałami od stanów wyłączonych. Wcześniejsze stany nie są odtwarzane; ponowne załączenie wymaga nowego dopuszczonego polecenia.

Utrata samego HMI/CAN podczas ciągłej pracy podlega odrębnej regule zachowania stanów SYS-243. Stan po restarcie jest kwalifikowany przez ECU, a HMI odczytuje go zgodnie z przyjętym podziałem ról. Warunki gotowości, kwalifikację poleceń i przebieg inicjalizacji wyjść opracujemy w architekturze.

### Plan próby SYS-244

1. Na stanowisku ECU–HMI ustawić dopuszczone kombinacje stanów trzech kanałów, także ON/ON/ON. Wywołać kontrolowany nieplanowany restart ECU przy nadal działającym HMI. Po odzyskaniu gotowości potwierdzić wyłączenie wszystkich trzech kanałów i brak odtworzenia poprzednich stanów. Rejestrować gotowość, polecenia i rzeczywiste napięcie/prąd wyjść.
2. Powtórzyć dla powrotu zasilania i reprezentatywnych przyczyn restartu objętych projektem. Sprawdzić stan po gotowości bez HMI i bez sesji Windows. Przebieg inicjalizacji oraz ewentualne sprawdzenia diagnostyczne ocenić według osobnej specyfikacji toru.
3. Przywrócić komunikację i odczytać stany ECU. Odtworzyć wcześniejsze żądania załączenia lub dane buforowane przez HMI; nie mogą one zastąpić nowego polecenia po restarcie. Kryteria ważności danych i odróżnienia nowego żądania ustalić z protokołem przed wykonaniem.
4. Wydać nowe dopuszczone polecenie dla wybranego kanału. Przy spełnionych warunkach potwierdzić jego załączenie i poprawne stany pozostałych kanałów. Odrębnie sprawdzić, że zabezpieczenia i ochrona energii nadal mogą odmówić załączenia. Przed wykonaniem ustalić połączenia, obciążenia i warunki przerwania; wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Dodatkowe kanały przy prawidłowym śnie i wybudzeniu

W odpowiedzi **A na pytanie 253** (2026-11-25) właściciel przyjął SYS-245: przed prawidłowym uśpieniem ECU/HMI dodatkowe kanały są wyłączane, a po zwykłym wybudzeniu pozostają wyłączone do nowego dopuszczonego polecenia.

To reguła stanów pracy wyjść. Prawidłowy sen jest koordynowany według SYS-059/062/063; wybudzenie nie przywraca samoczynnie zasilania akcesoriów. Nieplanowany restart podlega SYS-244, a sama utrata HMI/CAN podczas ciągłej pracy podlega SYS-243. Warunki gotowości i wykonanie przejść opracujemy w architekturze.

Wniosek do architektury z SYS-194/245: autotest nie omija stanu wyłączonego ani warunku nowego polecenia. Przy wybudzeniu wykonuje dostępne kontrole zgodne ze stanem OFF; próby wymagające załączenia odbiornika czekają na spełnienie warunków zgodnie z SYS-194. Zakres takich kontroli zależy od rzeczywistego toru i odbiornika.

### Plan próby SYS-245

1. Na stanowisku ECU–HMI załączyć dopuszczone kombinacje dodatkowych kanałów. Doprowadzić do spełnienia warunków prawidłowego snu, bez aktywnej sesji PC i innych zadań blokujących usypianie. Potwierdzić rzeczywiste wyłączenie wszystkich trzech wyjść przed przejściem systemu w zdefiniowany stan uśpienia.
2. Sprawdzić wymagane źródła wybudzenia według SYS-054–056/079–080, w tym ruch koła i późniejsze podłączenie PC. Bez nowego polecenia dla dodatkowych kanałów potwierdzić ich stan wyłączony podczas wybudzania, autotestu i po gotowości ECU/HMI; autotest nie może omijać tej reguły. Rejestrować sekwencję, komunikację i rzeczywiste napięcie/prąd wyjść.
3. Sprawdzić stany sprzed snu i dawne dane lub żądania HMI: nie mogą przywracać wyjść w miejsce nowego polecenia. Następnie wydać nowe dopuszczone polecenie i potwierdzić właściwe załączenie. Zabezpieczenia i ochrona energii nadal mogą odmówić załączenia.
4. Powtarzać cykle snu/wybudzenia, również przy wcześniej potwierdzonej utracie HMI/CAN i przy aktywnej ochronie energii. Sprawdzić, że normalny sen nie jest traktowany jak ciągła praca z zachowywaniem stanów SYS-243. Przed wykonaniem ustalić połączenia, kryteria, wyposażenie i warunki przerwania; wyniki powiązać z HW/FW oraz konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## ON/OFF i opcjonalny PWM mocy

W odpowiedzi **A na pytanie 254** (2026-11-25) właściciel przyjął SYS-246. Każdy z trzech dodatkowych kanałów ma obsługiwać ON/OFF i opcjonalny PWM mocy do regulacji jasności zgodnych lamp. GPS i zewnętrzne ładowarki zasilamy w trybie ON/OFF. Nie jest to wybór układów ani gotowa specyfikacja elektryczna.

PWM cyklicznie przełącza moc doprowadzaną do odbiornika. Obsługa lampy wymaga potwierdzenia jej zgodności i dopuszczonego zakresu; obecność elektroniki w lampie nie oznacza zgodności z dowolnym PWM. Przykład zastosowania w enduro potwierdza [Skene IQ-275-KTM](https://skenelights.com/iq-275-ktm.html), a producent opisuje [PWM dla odpowiednich lamp dwuprzewodowych](https://skenelights.com/skene-iq-275x-dimmer-with-integrated-wire-harness.html). To podstawa zakresu funkcji, nie wybór osprzętu DustONE.

Do etapów 3–6 przekazujemy: dane lamp i akcesoriów, zakres jasności, częstotliwość i rozdzielczość PWM, niezależne zasoby sterowania, zgodność diagnostyki ze sterowaniem impulsowym, prądy załączania oraz straty cieplne i zakłócenia przy dopuszczonych kombinacjach. Ważne komponenty wybierzemy wspólnie. Sygnałowy PWM do zewnętrznego modułu nadal jest osobnym tematem I/O.

Wniosek do projektu stanów: przy utracie HMI/CAN zachowany stan SYS-243 obejmuje przyjęte sterowanie kanału, także zadaną regulację PWM. Restart i sen nie przywracają wcześniejszego PWM; SYS-244/245 nadal wymagają nowego polecenia. PWM i autotest nie omijają zabezpieczeń ani ochrony energii.

### Plan próby SYS-246

1. Po doborze toru i uzgodnieniu parametrów podłączyć do rzeczywistego ECU kwalifikowane obciążenia, lampy oraz reprezentatywny GPS lub zewnętrzną ładowarkę. Z dokumentacji ustalić dopuszczone konfiguracje, warunki zasilania, temperatury i kryteria. Nie zakładać zgodności dowolnej lampy.
2. Dla każdego z trzech kanałów sprawdzić ON/OFF oraz PWM z kompatybilną lampą: stan wyłączony, dopuszczone granice regulacji i punkty pośrednie. Mierzyć przebieg napięcia/prądu, częstotliwość, wypełnienie i reakcję świetlną według kryteriów. Potwierdzić brak PWM zasilania kanału skonfigurowanego do GPS lub ładowarki w trybie ON/OFF.
3. Sprawdzić niezależne zadawanie i dopuszczone równoczesne kombinacje trzech kanałów. W kwalifikowanym zakresie zasilania i temperatury ocenić rozruch lamp, poprawność diagnostyki, nagrzewanie oraz wpływ przełączeń na zasilanie i inne funkcje ECU. Próby zakłóceń rozwinąć z projektem EMC; nie uznawać samej obserwacji przebiegu za potwierdzenie EMC.
4. Podczas PWM odtworzyć utratę HMI/CAN i sprawdzić zachowanie przyjętego stanu według SYS-243. Osobno sprawdzić restart oraz prawidłowy sen i wybudzenie: kanały pozostają wyłączone do nowego polecenia według SYS-244/245. Potwierdzić pierwszeństwo ochrony wyjść i energii; PWM nie może jej omijać. Przed wykonaniem określić stanowisko, kryteria, obciążenia i warunki przerwania; wyniki powiązać z HW/FW oraz konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Próba dodatkowego kanału po ochronnym odcięciu

W odpowiedzi **A na pytanie 255** (2026-11-25) właściciel przyjął SYS-247: po odłączeniu dodatkowego kanału wskutek potwierdzonego zwarcia lub przeciążenia ECU czeka na nowe świadome polecenie użytkownika albo serwisu. Nie wykonuje samoczynnych ponowień. Próba jest ograniczona, obejmuje ocenę obwodu i podlega zabezpieczeniom oraz ochronie energii. DTC z zamrożoną ramką i informacja HMI opisują usterkę.

Przywrócenie sprawności wymaga wyniku sprawdzenia; samo polecenie nie potwierdza naprawy. Progi, czas i energia próby, kryteria wyniku, warunki cieplne oraz współdziałanie zabezpieczeń układu mocy z ECU wymagają projektu. Należy odróżnić dopuszczony prąd załączenia odbiornika od usterki. Istniejące reguły SYS-243–246 nadal obowiązują; zakres dotyczy trzech dodatkowych kanałów, a nie odrębnych prób wentylatora z F03.

### Plan próby SYS-247

1. Na stanowisku rzeczywistego ECU z kwalifikowanymi obciążeniami odtworzyć wykrywalne zwarcie i przeciążenie każdego dodatkowego kanału osobno. Przed wykonaniem określić bezpieczny układ wymuszania usterek, limity źródła, kryteria oraz warunki przerwania. Potwierdzić ochronne odcięcie, DTC z zamrożoną ramką oraz informację HMI; rejestrować napięcie/prąd i stan zabezpieczenia.
2. Bez nowego świadomego polecenia obserwować kanał po ustąpieniu pobudzenia lub warunków termicznych oraz przy powtarzanych wcześniejszych danych sterujących, utracie i powrocie HMI/CAN. Potwierdzić brak samoczynnego ponowienia. Ocenić także współdziałanie wewnętrznej ochrony układu mocy z ECU i PWM; nie utożsamiać każdej fazy jego ochrony z nową próbą użytkownika.
3. Wydać nowe dopuszczone polecenie próby z HMI oraz osobno z uprawnionego trybu serwisowego. Przy trwającej usterce potwierdzić ograniczenie próby i odcięcie, a po usunięciu usterki ocenę obwodu według kryteriów. Sprawdzić odmowę przy niespełnionych warunkach zasilania, termicznych lub ochrony energii. Samo podłączenie PC nie omija warunków serwisowych.
4. Dla dopuszczonych odbiorników sprawdzić ON/OFF i PWM zgodnych lamp, także poprawny prąd ich załączenia. Potwierdzić zgodność odczytów HMI z ECU i zachowanie historii DTC. Limit świadomych prób oraz jego odnowienie sprawdzić według przyjętego SYS-248. Wyniki powiązać z HW/FW, konfiguracją i osprzętem. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Limit świadomych prób dodatkowego kanału

W odpowiedzi **A na pytanie 256** (2026-11-25) właściciel zatwierdził SYS-248, doprecyzowując propozycję zgłoszoną przy pytaniu 255. Po pierwszym ochronnym odcięciu dostępna jest jedna świadoma próba. Jeżeli potwierdzi nadal występujący problem, ECU odrzuca dalsze polecenia prób tego kanału aż do zakończonego cyklu prawidłowego snu i wybudzenia albo pełnego zaniku i powrotu zasilania. Limit i blokadę prowadzi osobno dla każdego kanału.

Odnowienie daje wyłącznie możliwość zlecenia jednej nowej próby według SYS-247. Wyjście pozostaje OFF według SYS-244/245. Nie kasuje się historii DTC; odnowienie limitu i potwierdzenie usunięcia usterki są odrębnymi zdarzeniami. Aktywny stan DTC podlega rzeczywistym kryteriom diagnostycznym SYS-023. Powrót CAN lub zwykły reset programu ECU nie odnawia limitu.

Reguła obejmuje polecenia użytkownika i serwisu z SYS-247. Kolejne komunikaty ani zmiana klienta HMI/Windows nie omijają blokady. Warunki zasilania i termiczne, wymagane ostygnięcie oraz ograniczenia energii próby mają pierwszeństwo także po śnie i zaniku zasilania. Nie oznacza to zdalnego omijania warunków prawidłowego snu; aktywna sesja PC nadal blokuje usypianie.

Do architektury przekazujemy rozpoznanie pełnego zaniku zasilania i ukończenia prawidłowego snu, zachowanie limitu przez reset programu, kwalifikację próby oraz współdziałanie z układem mocy. ECU rozpoznaje skutki zaniku zasilania; nie zakładamy rozpoznania samego fizycznego odpięcia akumulatora. Topologię, pamięć, parametry i komponenty wybierzemy we właściwych etapach.

### Plan próby SYS-248

1. Na kwalifikowanym stanowisku wywołać ochronne odcięcie jednego dodatkowego kanału przy trwającej usterce. Zlecić jedną dopuszczoną świadomą próbę i potwierdzić jej ograniczone niepowodzenie oraz blokadę dalszych prób. Wysyłać wielokrotnie nowe i powtarzane polecenia przez HMI oraz uprawniony tryb serwisowy; mierzyć rzeczywisty prąd/napięcie, potwierdzając brak kolejnych pobudzeń. Powtórzyć dla każdego kanału i sprawdzić odrębność liczników prób.
2. Przy aktywnej blokadzie odtworzyć utratę i powrót HMI/CAN, restart samego HMI oraz zwykły reset programu ECU bez kwalifikowanego pełnego zaniku zasilania. Potwierdzić brak odnowienia prawa do próby i pozostawienie wyjścia wyłączonego; odtworzone wcześniejsze żądania nie mogą zostać uznane za nowe polecenie po odnowieniu.
3. Bez sesji PC i po spełnieniu warunków systemu przeprowadzić prawidłowy sen i wybudzenie, w tym ruchem koła oraz przyciskami. Potwierdzić OFF także podczas autotestu i odnowienie wyłącznie prawa do jednej świadomej próby. Przy trwającej usterce nowa próba ponownie kończy się blokadą; po naprawie wynik ocenić według kryteriów SYS-247. Sam powrót gotowości nie załącza odbiornika.
4. Osobno odtworzyć pełny zanik i powrót zasilania według kryteriów projektu oraz zdarzenia, które tych kryteriów nie spełniają. Sprawdzić właściwe odnowienie lub zachowanie limitu, brak automatycznego ON i trwałość historii DTC. Powtarzać cykle przy niespełnionych warunkach termicznych i energetycznych: odnowione prawo nie może ominąć zabezpieczeń. Przed wykonaniem ustalić połączenia, warunki zaniku/resetu, limity pobudzeń, kryteria i warunki przerwania; wyniki powiązać z HW/FW oraz konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Usterka jednego dodatkowego kanału

W odpowiedzi **A na pytanie 257** (2026-11-25) właściciel zatwierdził SYS-249. Potwierdzone zwarcie lub przeciążenie jednego dodatkowego kanału powoduje odcięcie i blokadę tylko tego kanału, jeżeli pozostałe obwody, wspólne zasilanie i warunki termiczne pozwalają na ich dalszą pracę. Pozostałe kanały zachowują własne stany, w tym sterowanie PWM, z zachowaniem ich zabezpieczeń oraz ochrony energii.

Reguła nie wymaga utrzymania wyjść przy wspólnym zagrożeniu zasilania lub temperatury. Zakres takich reakcji i granice sprawności wymagają projektu. Licznik i blokada prób uszkodzonego kanału nadal podlegają SYS-247/248; usterka jednego toru nie jest sama w sobie poleceniem wyłączenia pozostałych.

Do architektury i doboru przekazujemy ocenę wspólnych ścieżek zasilania, ograniczenia prądu zwarciowego, sprzężeń cieplnych oraz wpływu usterki na sterowanie i diagnostykę sąsiednich kanałów. [ST opisuje lokalną ochronę termiczną wyjść i możliwość wpływu nagrzewania wspólnego układu na inne kanały](https://www.st.com/content/ccc/resource/technical/document/datasheet/fd/11/11/45/55/61/44/50/CD00003429.pdf/files/CD00003429.pdf/jcr:content/translations/en.CD00003429.pdf), sekcja 3.10. To uzasadnienie oceny, nie wybór komponentu ani dowód izolacji w DustONE. Ważne układy i kompromisy dobierzemy wspólnie.

### Plan próby SYS-249

1. Na kwalifikowanym stanowisku rzeczywistego ECU podłączyć trzy dopuszczone obciążenia. Ustawić reprezentatywne stany ON/OFF oraz PWM zgodnych lamp. Przy prawidłowym wspólnym zasilaniu i temperaturze odtworzyć wykrywalne zwarcie lub przeciążenie jednego kanału w zaprojektowanym obwodzie wymuszania usterek. Rejestrować napięcie/prąd wszystkich wyjść, zasilanie ECU i stany sterowania.
2. Potwierdzić odcięcie i blokadę uszkodzonego kanału, zapis diagnostyczny oraz informację HMI. Dla dwóch pozostałych potwierdzić zachowanie przyjętych stanów i sterowania w ich dopuszczonych granicach; polecenie odcięcia nie może obejmować ich wyłącznie z powodu lokalnej usterki sąsiada. Powtórzyć usterkę kolejno dla każdego kanału i kwalifikowanych kombinacji obciążeń.
3. Sprawdzić ograniczoną świadomą próbę uszkodzonego kanału i blokadę po niepowodzeniu według SYS-247/248. Potwierdzić, że te działania nie zmieniają zadanych stanów sprawnych sąsiednich kanałów przy prawidłowych warunkach. Ocenić wpływ nagrzewania oraz zakłóceń i spadków zasilania w zakresie zadeklarowanym przez projekt; nie uznawać poprawnego zwykłego sterowania za dowód izolacji usterki.
4. Osobno odtworzyć kwalifikowane przypadki wspólnego zagrożenia zasilania lub temperatury i sprawdzić szerszą reakcję przewidzianą przez projekt. Nie wymagać podtrzymania kanału wbrew jego własnym zabezpieczeniom lub ochronie energii. Przed wykonaniem ustalić granice obu klas przypadków, obciążenia, wyposażenie, limity wymuszania i warunki przerwania; wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Przegląd przyjętej części wyjść mocy

| Zakres | Przyjęta reguła | Podstawa |
| --- | --- | --- |
| Zastosowania | Dodatkowe oświetlenie i zasilanie zewnętrznych akcesoriów. | B na 249, SYS-241 |
| Liczba kanałów | Trzy niezależnie sterowane kanały ponad podstawowymi odbiornikami. | B na 250, SYS-242 |
| Utrata HMI/CAN | Zachowanie własnego stanu każdego kanału przy ciągłej pracy ECU. | A na 251, SYS-243 |
| Nieplanowany restart / powrót zasilania | Start od wyłączonych; załączenie wymaga nowego polecenia. | A na 252, SYS-244 |
| Prawidłowy sen i zwykłe wybudzenie | Wyłączenie przed snem; po wybudzeniu pozostają wyłączone do nowego polecenia. | A na 253, SYS-245 |
| Sterowanie lampami i akcesoriami | ON/OFF oraz opcjonalny PWM mocy zgodnych lamp; GPS i ładowarki bez PWM zasilania. | A na 254, SYS-246 |
| Próba po zwarciu lub przeciążeniu | Bez samoczynnych ponowień; ograniczona próba ze sprawdzeniem obwodu na nowe świadome polecenie. | A na 255, SYS-247 |
| Nieudana świadoma próba | Blokada dalszych prób danego kanału do pełnego cyklu snu lub zaniku i powrotu zasilania; odnowienie bez automatycznego ON. | A na 256, SYS-248 |
| Usterka jednego kanału | Odcięcie i blokada tylko uszkodzonego toru; pozostałe zachowują stany przy prawidłowych warunkach, z pierwszeństwem zabezpieczeń. | A na 257, SYS-249 |

Sprawdzono spójność reguł z autonomią ECU, rozróżnieniem restartu i snu oraz pierwszeństwem zabezpieczeń i ochrony energii. Każde z SYS-241–249 ma plan próby i przydział do bloków oraz grup weryfikacji.

Uzgodniona porcja SYS-241–245 ma historię w [PR #26](https://github.com/DustWorx/DustWorx-DustONE/pull/26). SYS-246 dodaje opcjonalny PWM zgodnych lamp, a SYS-247 określa próbę kanału po ochronnym odcięciu. SYS-248 ustala limit i jego odnawianie. SYS-249 określa zachowanie pozostałych kanałów przy lokalnej usterce. F04 pozostaje aktywny; podstawowe światła po nieplanowanym restarcie określa poniższe SYS-250. Powrót HMI/CAN oraz restart i sen kierunkowskazów określają dalsze SYS-251/252. Następny temat to próby pozostałych podstawowych wyjść po ochronnym odcięciu, a następnie pozostałe reguły akcesoriów i I/O. Parametry, topologię oraz pokrycie diagnostyki opracujemy we właściwych etapach, a ważne komponenty wybierzemy wspólnie.

## Podstawowe światła po nieplanowanym restarcie

W odpowiedzi **A na pytanie 258** (2026-11-25) właściciel przyjął SYS-250. Po odzyskaniu gotowości ECU po nieplanowanym restarcie, przy zgaszonym silniku, przednie i tylne pozycyjne, mijania i drogowe pozostają OFF do nowego polecenia użytkownika z HMI. Wcześniejsze stany i powtórzone dawne żądania nie są takim poleceniem.

To stan podstawowego oświetlenia, odrębny od trzech dodatkowych kanałów SYS-241–249. Zwykły sen i wybudzenie nadal podlegają SYS-081. Po potwierdzonym uruchomieniu silnika automatyka pozycyjnych działa według SYS-082/087, także bez HMI, z pierwszeństwem zabezpieczeń i ochrony energii. Światło hamowania nadal reaguje na bezpośrednie wejścia według SYS-051.

Motocykl pozostaje bez stacyjki; nie wprowadzamy przełącznika zasilania ani jego obsługi. Warunki gotowości, rozpoznanie przyczyny uruchomienia, inicjalizację wyjść i kwalifikację nowych poleceń rozwiniemy w architekturze i projekcie torów. Przyjęcie reguły nie oznacza potwierdzenia jej realizacji.

### Plan próby SYS-250

1. Na rzeczywistym stanowisku ECU–HMI z dopuszczonymi lampami odtworzyć reprezentatywne stany pozycyjnych, mijania i drogowych przy zgaszonym silniku. Wywołać nieplanowany restart według warunków projektu, także przy działającym HMI. Po odzyskaniu gotowości, bez nowego polecenia użytkownika, potwierdzić OFF wszystkich wymienionych świateł. Rejestrować gotowość ECU, komunikację i rzeczywiste napięcie/prąd torów.
2. Odtworzyć dawne stany i żądania HMI, również po jego ponownym połączeniu. Potwierdzić brak samoczynnego załączenia po restarcie. Wydać nowe dopuszczone polecenie użytkownika i sprawdzić właściwą reakcję. Powtórzyć bez dostępnego HMI; kryteria ważności i odróżnienia nowych poleceń ustalić z protokołem przed próbą.
3. Po potwierdzonym uruchomieniu silnika sprawdzić automatyczne przednie i tylne pozycyjne według SYS-082/087, także bez HMI. Mijania i drogowe nadal wymagają polecenia użytkownika. Osobno odtworzyć nadrzędne odcięcie oszczędzania i ochronę wyjść: gotowość po restarcie ani nowe polecenie nie mogą ich omijać.
4. Przy zgaszonym silniku i gotowym ECU uruchamiać osobno przedni oraz tylny hamulec i ich dopuszczone kombinacje. Potwierdzić światło hamowania według SYS-051, również bez HMI/CAN, mimo OFF pozycyjnych. Rozróżnić nieplanowany restart od prawidłowego snu i wybudzenia; sprawdzić reprezentatywne przyczyny restartu objęte projektem. Przed wykonaniem ustalić połączenia, obciążenia, kryteria, sposób resetu i warunki przerwania; wyniki powiązać z HW/FW oraz konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Kierunkowskazy po odzyskaniu HMI/CAN

W odpowiedzi **A na pytanie 259** (2026-11-25) właściciel przyjął SYS-251. Po wyłączeniu kierunkowskazu według SYS-052 powrót HMI/CAN nie wznawia sygnalizacji. Przy nieprzerwanej pracy ECU w bieżącym okresie wybudzenia wymagany jest nowy świadomy wybór użytkownika z HMI. Samo ponowne zgłoszenie poprzedniej strony ani odtworzone wcześniejsze żądanie nie są takim wyborem.

To reguła odzyskania komunikacji podczas pracy ECU; restart oraz prawidłowy sen i wybudzenie są osobnym następnym ustaleniem. Miganiem nadal steruje lokalnie ECU, a zabezpieczenia i ochrona energii mają pierwszeństwo. Kryteria powrotu łączności, kwalifikację danych i nowych wyborów opracujemy w architekturze/protokole. Ustalenie nie tworzy tu nowego DTC komunikacji.

### Plan próby SYS-251

1. Na rzeczywistym stanowisku ECU–HMI z dopuszczonymi lampami włączyć kierunkowskaz, utrzymując pracę i zasilanie ECU. Odtworzyć utratę HMI/CAN i potwierdzić wyłączenie według SYS-052. Przywrócić komunikację bez nowego działania kierowcy, także gdy HMI ponownie zgłasza poprzednią stronę. Potwierdzić brak wznowienia rzeczywistej sygnalizacji. Powtórzyć dla lewej i prawej strony.
2. Odtworzyć dawne stany oraz wcześniejsze żądania, ponowne zgłoszenie tego samego wyboru, kolejną utratę i powrót łączności oraz restart samego HMI przy nadal działającym ECU. Potwierdzić utrzymanie OFF do nowego świadomego wyboru. Kryteria ważności danych i odróżnienia wyborów ustalić z protokołem przed wykonaniem.
3. Po odzyskaniu łączności wykonać nowy świadomy wybór strony z HMI. Przy spełnionych pozostałych warunkach potwierdzić przyjęcie wyboru i właściwą lokalną sygnalizację ECU. Sprawdzić wybór strony poprzedniej oraz przeciwnej i odczyt rzeczywistych stanów przez HMI; nie wyznaczać tu jeszcze interwałów migania.
4. Powtórzyć przy pracy i zatrzymaniu silnika, bez sesji Windows i z nadrzędnymi zabezpieczeniami wyjść oraz ochroną energii zgodnie z zakresem projektu. Nowy wybór nie może omijać obowiązujących odcięć. Rejestrować komunikację, stany ECU i rzeczywiste napięcie/prąd skonfigurowanych lamp. Przed wykonaniem ustalić połączenia, obciążenia, kryteria oraz warunki przerwania; wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Kierunkowskazy po restarcie i prawidłowym śnie

W odpowiedzi **A na pytanie 260** (2026-11-25) właściciel przyjął SYS-252. Przed prawidłowym snem ECU wyłącza kierunkowskazy. Po zwykłym wybudzeniu oraz po odzyskaniu gotowości po nieplanowanym restarcie pozostają one OFF do nowego świadomego wyboru użytkownika z HMI. Poprzednia strona i odtworzone dawne żądania nie przywracają sygnalizacji.

To reguła stanów ECU, odrębna od powrotu HMI/CAN w bieżącym okresie wybudzenia z SYS-251. Zachowujemy automatyczny i koordynowany sen według SYS-059/062/063 oraz jego warunki. Miganiem nadal steruje ECU z pierwszeństwem zabezpieczeń i ochrony energii. Gotowość, kwalifikację nowych wyborów i ich przekazanie przez HMI rozwiniemy we właściwych etapach architektury, HMI i protokołu.

### Plan próby SYS-252

1. Na rzeczywistym stanowisku ECU–HMI załączyć lewy, a osobno prawy kierunkowskaz. Przy zgaszonym silniku, bez sesji PC i po spełnieniu pozostałych warunków przeprowadzić prawidłowe usypianie. Potwierdzić rzeczywiste wyłączenie kierunkowskazów przed stanem snu; rejestrować komunikację, stany ECU i napięcie/prąd skonfigurowanych lamp.
2. Wybudzić system wymaganymi źródłami, w tym ruchem koła, START, obsługą HMI bez nowego wyboru strony oraz podłączeniem PC. Bez nowego świadomego wyboru potwierdzić OFF po wybudzeniu i gotowości. Odtworzyć poprzednie dane i żądania strony; nie mogą przywrócić sygnalizacji. Następnie wykonać nowy dopuszczony wybór i potwierdzić właściwe miganie.
3. Podczas sygnalizacji wywołać nieplanowany restart ECU, także przy działającym HMI nadal zgłaszającym poprzednią stronę. Po odzyskaniu gotowości potwierdzić OFF do nowego świadomego wyboru, brak odtworzenia z dawnych stanów i właściwą reakcję na nowy wybór. Powtórzyć dla obu stron i reprezentatywnych przyczyn restartu objętych projektem.
4. Powtarzać cykle snu/wybudzenia i restartu, również po wcześniejszej utracie HMI/CAN oraz przy obowiązujących nadrzędnych odcięciach. Nowy wybór nie może omijać zabezpieczeń ani ochrony energii. Rozróżnić poprawne zakończenie snu od restartu; kryteria przejść, ważności danych, połączenia, obciążenia i warunki przerwania ustalić przed wykonaniem. Wyniki powiązać z HW/FW oraz konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Próby podstawowych wyjść po ochronnym odcięciu

W odpowiedzi **A na pytanie 261** (2026-11-25) właściciel przyjął SYS-253. Po potwierdzonym zwarciu lub przeciążeniu i ochronnym odcięciu zaprojektowanego kanału podstawowego oświetlenia, kierunkowskazów albo klaksonu ECU nie ponawia samoczynnie załączenia. Jedna ograniczona próba ze sprawdzeniem obwodu wymaga nowego świadomego polecenia użytkownika lub serwisu.

Po jej niepowodzeniu dalsze próby danego kanału są blokowane do pełnego cyklu prawidłowego snu i wybudzenia albo pełnego zaniku i powrotu zasilania, zgodnie z SYS-247/248. Zwykły reset programu ani powrót HMI/CAN nie odnawiają limitu. Odnowienie daje tylko prawo do nowej świadomej próby; nie załącza wyjścia i nie kasuje historii DTC. Dotyczy to także głównego oświetlenia.

Zabezpieczenia wyjścia, wymagane ostygnięcie, ochrona energii, DTC z zamrożoną ramką i informacja HMI pozostają aktywne. Podział na fizyczne kanały, kryteria diagnozy, energia i czas próby oraz współdziałanie z ochroną układu mocy wymagają architektury, danych odbiorników i weryfikacji. Nie wybrano komponentu ani liczby oddzielnych wyjść dla każdej lampy.

Wentylator i funkcje silnikowe zachowują zasady zamkniętego F03, a zasilanie HMI własne reguły. Normalne światło hamowania nadal działa z bezpośrednich wejść według SYS-051; sposób zlecenia próby bez HMI przyjęto w późniejszym SYS-254.

### Plan próby SYS-253

1. Na kwalifikowanym stanowisku rzeczywistego ECU odtworzyć wykrywalne zwarcie i przeciążenie każdego objętego kanału osobno, z dopuszczonymi lampami lub klaksonem. Potwierdzić ochronne odcięcie, DTC z zamrożoną ramką i informację HMI. Bez nowego świadomego polecenia sprawdzić brak samoczynnego ponowienia, także po ustąpieniu pobudzenia lub wymaganym ostygnięciu. Przed wykonaniem ustalić bezpieczny obwód wymuszania i limity energii.
2. Zlecić jedną dopuszczoną świadomą próbę według przyjętego sposobu obsługi. Przy trwającej usterce potwierdzić ograniczone niepowodzenie i blokadę dalszych prób. Powtarzać polecenia użytkownika oraz uprawnionego serwisu, odtwarzać dawne żądania, powrót HMI/CAN i zwykły reset programu: żadne z nich nie może odnowić limitu ani spowodować kolejnego pobudzenia. Inicjowanie próby światła hamowania sprawdzić według przyjętego SYS-254.
3. Osobno przeprowadzić pełny cykl prawidłowego snu i wybudzenia oraz pełny zanik i powrót zasilania według kryteriów projektu. Potwierdzić odnowienie wyłącznie prawa do próby, brak automatycznego ON, zachowanie historii DTC i nadal aktywne warunki termiczne oraz ochronę energii. Nowe polecenie po odnowieniu dopuszcza jedną próbę; po jej niepowodzeniu blokada wraca.
4. Po usunięciu usterki sprawdzić wynik ograniczonej próby i dalsze sterowanie według funkcji odbiornika, z zachowaniem reguł klaksonu, świateł i kierunkowskazów. Powtórzyć dla dopuszczonych obciążeń, w tym prądów załączania, oraz istotnych zakresów zasilania i temperatury. Rejestrować komunikację, stan próby i rzeczywiste napięcie/prąd wyjścia. Przed wykonaniem określić kryteria, połączenia, wyposażenie i warunki przerwania; wyniki powiązać z HW/FW oraz konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Próba światła hamowania bez HMI

W odpowiedzi **A na pytanie 262** (2026-11-25) właściciel przyjął SYS-254. Przy dostępnym limicie i spełnionych warunkach, po potwierdzonym zwolnieniu obu hamulców, nowe użycie któregokolwiek może zlecić jedną ograniczoną próbę toru światła hamowania bez HMI.

Samo trzymanie hamulca, powrót CAN lub odnowienie limitu nie inicjują próby. Po jej niepowodzeniu obowiązuje blokada SYS-253; kolejne użycia hamulców i polecenia HMI lub serwisu podlegają temu samemu limitowi kanału. Odnowienie prawa do próby nadal wymaga pełnego cyklu prawidłowego snu albo pełnego zaniku i powrotu zasilania. Zabezpieczenia, termika i ochrona energii zachowują pierwszeństwo.

Normalna praca sprawnego toru pozostaje według SYS-051. Po prawidłowym wyniku próby dalsze sterowanie musi odpowiadać bieżącym wejściom hamulców. Kryteria poprawności wejść, zwolnienia i nowego użycia, filtracja, ocena wyniku i parametry próby wymagają architektury, danych osprzętu i procedury. Ważne elementy wybierzemy wspólnie.

### Plan próby SYS-254

1. Na kwalifikowanym stanowisku rzeczywistego ECU odtworzyć ochronne odcięcie toru światła hamowania. Przy dostępnym limicie pozostawić jeden lub oba hamulce aktywne i potwierdzić brak samoczynnej próby. Zwolnienie tylko jednego przy drugim nadal aktywnym nie może spełnić warunku zwolnienia obu. Rejestrować wejścia, stan limitu oraz rzeczywiste napięcie/prąd toru.
2. Potwierdzić zwolnienie obu hamulców, a następnie osobno w kolejnych kwalifikowanych przypadkach użyć przedniego i tylnego. Bez HMI/CAN, przy spełnionych warunkach, potwierdzić jedną ograniczoną próbę i ocenę obwodu. Przy trwającej usterce potwierdzić niepowodzenie i blokadę dalszych prób; powtarzane użycia hamulców oraz polecenia HMI/serwisu nie mogą omijać wspólnego limitu. Zlecenie próby najpierw innym dopuszczonym interfejsem również zużywa ten sam limit.
3. Po pełnym cyklu snu albo pełnym zaniku i powrocie zasilania sprawdzić odnowienie tylko prawa do próby. Jeżeli hamulec pozostaje trzymany, nie wolno rozpocząć próby bez potwierdzonego zwolnienia obu i nowego użycia. Zwykły reset programu lub powrót CAN nie odnawia limitu. Powtórzyć przy niespełnionych warunkach zasilania, termicznych i ochrony energii; nowe użycie nie może ich ominąć.
4. Po naprawie obwodu i prawidłowym wyniku dopuszczonej próby potwierdzić sterowanie światłem według aktualnych wejść SYS-051, także po zwolnieniu hamulca przed zakończeniem sprawdzenia oraz bez HMI. Zachować historię DTC. Przed wykonaniem ustalić połączenia, obciążenia, kryteria wejść/wyniku, limity energii, wyposażenie i warunki przerwania; wyniki powiązać z HW/FW oraz konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Zakres zewnętrznych portów

W odpowiedzi **A na pytanie 263** (2026-11-25) właściciel przyjął SYS-255: każdy zewnętrzny port ma uzgodnione zastosowanie. Zakres nie obejmuje dodatkowych zewnętrznych portów sygnałowych ani magistral rezerwowych do nieokreślonych urządzeń.

Wymagane pozostają tory wszystkich przyjętych czujników i osprzętu silnika, trzy dodatkowe kanały mocy, CAN ECU–HMI, obsługa PC, programowanie i debugowanie według przyjętych ról. Nowa zatwierdzona funkcja może wymagać zmiany listy I/O według procesu kontroli zmian.

Rezerwa zasobów procesora, wewnętrzne magistrale, punkty testowe i niewykorzystane pozycje standardowego złącza wymagają oceny w architekturze/projekcie. Nie wybrano pinoutu ani komponentów; ważne układy nadal wybieramy wspólnie. Zewnętrzny tor wymaga powiązania z funkcją, wymaganiami i metodą weryfikacji.

### Plan próby SYS-255

1. W etapie architektury i projektu sporządzić zestawienie zewnętrznych portów oraz styków ECU/HMI, przypisując funkcje, zasilania, masy i interfejsy serwisowe do zatwierdzonego zakresu. Wykazać pokrycie wymaganych funkcji w wariantach silnika; oddzielnie oznaczyć wewnętrzne punkty testowe i niewykorzystane pozycje złączy.
2. W przeglądzie schematów, BOM, pinoutu i wiązki potwierdzić brak zewnętrznych portów dla nieokreślonych urządzeń oraz zachowanie przyjętych czujników, osprzętu, trzech dodatkowych kanałów mocy, CAN, PC i programowania/debugowania. Parametry i działanie sprawdzić właściwymi procedurami, nie samym istnieniem styku.
3. Na wykonanym prototypie porównać rzeczywiste złącza, obsadę i połączenia z zatwierdzoną dokumentacją. Potwierdzić przypisanie i oznaczenie portów oraz zgodność niewykorzystanych pozycji i punktów testowych z projektem. Inspekcja produktu uzupełnia przegląd dokumentacji i próby elektryczne.
4. Powiązanymi procedurami potwierdzić komunikację ECU–HMI, dostęp PC, programowanie/debugowanie w uprawnionych trybach i przyjęte funkcje I/O. Zachować ograniczenia ról oraz ochrony firmware/liczników. Przed wykonaniem określić rewizje, warianty, zestawienie portów, kryteria i wyposażenie; wyniki powiązać z HW/FW, konfiguracją i dokumentacją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan przeglądu, inspekcji produktu i powiązanych prób do rozwinięcia w procedury; nie wykonano weryfikacji produktu.

## Wybudzanie przez hamulce

W odpowiedzi **A na pytanie 264** (2026-11-26) właściciel przyjął SYS-256: nowe użycie przedniego albo tylnego hamulca wybudza ECU i HMI. Po gotowości wymaganych torów ECU obsługuje bieżące wejścia SYS-051 bez czekania na gotowość HMI i niezależnie od jego sprawności oraz CAN.

Zdarzenie wybudzenia nie jest żądaniem rozruchu silnika. Nie potwierdza naprawy toru światła i nie omija zabezpieczeń, warunków zasilania ani wspólnego limitu prób SYS-253/254. Przy sprawnym torze obowiązuje normalne sterowanie według wejść; przy wcześniejszym odcięciu ewentualna próba wymaga warunków SYS-254. Samo odnowienie limitu nie załącza światła.

W architekturze określimy detekcję nowego użycia w śnie, filtrację, obsługę długiego stanu aktywnego, gotowość toru światła, czasy i przekazanie wybudzenia HMI. Pobór detekcji obu hamulców włączymy do budżetu czuwania. Nie ustalono tu dodatkowych reguł odnawiania bezczynności przy już wybudzonym ECU ani wpływu trwale aktywnego wejścia na sen. Ważne układy wybierzemy wspólnie.

### Plan próby SYS-256

1. Doprowadzić rzeczywiste ECU i HMI do prawidłowego snu, przy nieruchomym kole, bez PC, START i używania przycisków HMI. Przy sprawnych torach osobno użyć przedniego i tylnego hamulca; potwierdzić wybudzenie obu urządzeń. Rejestrować wejścia, gotowość ECU/HMI, komunikację oraz rzeczywiste napięcie/prąd światła. Zmierzyć czas od nowego użycia do wybudzenia i reakcji światła; kryteria liczbowe przyjąć przed wykonaniem.
2. Przy przytrzymaniu hamulca przez wybudzenie potwierdzić działanie sprawnego światła po gotowości wymaganych torów, bez oczekiwania na HMI. Powtórzyć z celowo opóźnionym lub niesprawnym HMI oraz brakiem CAN: sprawdzić niezależną obsługę światła przez ECU. Przy sprawnej ścieżce wybudzenia potwierdzić także żądane wybudzenie HMI. Osobno zwolnić hamulec przed gotowością i zmienić stany obu wejść podczas wybudzania; wyjście ma odpowiadać bieżącym stanom SYS-051, bez odłożonego ON z zakończonego użycia.
3. Po wcześniejszym ochronnym odcięciu światła potwierdzić, że wybudzenie nie zastępuje sprawdzenia toru. Sprawdzić warunki zwolnienia obu hamulców i nowego użycia, dostępność wspólnego limitu, jedną ograniczoną próbę oraz blokadę po niepowodzeniu według SYS-253/254. Przy trzymanym hamulcu samo odnowienie limitu nie może uruchomić próby. Zachować historię DTC i pozostałe zabezpieczenia.
4. W zweryfikowanym zakresie napięć i temperatur sprawdzić detekcję obu wejść w śnie, prąd czuwania całego zestawu, kwalifikację zakłóceń i przypadki użycia podczas przejścia w sen. Odtworzyć niespełnione warunki zasilania i ochrony energii według przyjętych reguł; wybudzenie nie może ich omijać ani inicjować rozruchu. Obsługę długiego stanu aktywnego sprawdzić według przyszłej specyfikacji, bez założenia nieograniczonego podtrzymania pracy. Przed wykonaniem ustalić interfejsy, połączenia, kryteria, wyposażenie i warunki przerwania; wyniki powiązać z HW/FW, konfiguracją i profilem akumulatora. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Odbiorniki w oszczędzaniu energii

W odpowiedzi na pytanie 265 (2026-11-26) właściciel wybrał światło hamowania oraz możliwość włączenia awaryjnych, zamiast pojedynczych kierunkowskazów. W odpowiedzi **A na doprecyzowanie 265** potwierdził, że klakson jest wyłączony i niedostępny. Przyjęto SYS-257.

| Odbiornik | Podczas aktywnego odcięcia oszczędzania |
| --- | --- |
| Przednie i tylne pozycyjne, mijania i drogowe | Wyłączone; zwykłe żądanie ON odrzucone według SYS-085/086. |
| Trzy dodatkowe kanały mocy | Wyłączone; zwykłe żądanie ON odrzucone, niezależnie od przypisanego dodatkowego oświetlenia, GPS lub ładowarki. |
| Pojedyncze kierunkowskazy | Wyłączone; wybór tylko lewej lub tylko prawej strony niedostępny. |
| Klakson | Wyłączony; zwykłe żądanie załączenia odrzucone. |
| Światło hamowania | Dostępne według bezpośrednich wejść SYS-051 i wybudzenia SYS-256. |
| Światła awaryjne | Dostępne na świadome żądanie z HMI: wspólne miganie obu stron, realizowane lokalnie w ECU. Samo wejście w oszczędzanie ich nie włącza. |
| Wentylator | Zachowuje własne reguły SYS-060/061/089 i zamkniętego F03. |
| ECU, rozruch i zasilanie HMI | Zachowują własne reguły; nie przyjęto zwykłego odłączania HMI przez ten tryb. |

Zabezpieczenia, wymagane ostygnięcie, limity prób po usterce i dopuszczone zasilanie nadal obowiązują. Dostępność awaryjnych nie omija blokady żadnego kanału. HMI przekazuje żądanie i pokazuje rzeczywisty stan lub odmowę ECU. Wyjście z oszczędzania, powrót ręcznych odbiorników i wyjątek serwisowy pozostają według SYS-087–091. Prądy, progi, czasy i zdolność wspólnej pracy obu stron wymagają danych, bilansu i prób.

Awaryjne stanowią nowy, jawnie wskazany przez właściciela tryb. Podtrzymanie po utracie HMI/CAN określa SYS-258, a blokadę snu SYS-259. Restart/powrót zasilania określa SYS-260; współdziałanie z wyborem strony pozostaje otwarte w F04. Dotychczasowe SYS-052/251/252 ustalały zachowanie pojedynczego kierunkowskazu; nowe stany awaryjnych rozstrzygamy osobno.

### Plan próby SYS-257

1. Na stanowisku ECU–HMI ze sprawnymi dopuszczonymi obciążeniami, przy zgaszonym silniku, odtworzyć kwalifikowane wejście w oszczędzanie. W osobnych przypadkach rozpocząć od włączonych pozycyjnych, mijania/drogowych, każdego i wszystkich trzech dodatkowych kanałów, pojedynczej lewej/prawej strony oraz klaksonu. Potwierdzić odcięcie objętych odbiorników; samo wejście nie może włączyć awaryjnych. Rejestrować napięcie, stan odcięcia oraz rzeczywiste napięcia/prądy wyjść.
2. Podczas aktywnego odcięcia osobno użyć przedniego i tylnego hamulca; przy spełnionych warunkach potwierdzić światło według bieżących wejść, także przy niedostępnym HMI/CAN i po wybudzeniu SYS-256. Przy sprawnym HMI świadomie wybrać awaryjne i potwierdzić wspólne miganie obu stron. Zmierzyć przebieg, równoczesne obciążenie i zasilanie w dopuszczonych warunkach. Kryteria synchronizacji i czasu przyjąć przed próbą.
3. Przy aktywnym odcięciu zlecać zwykłe ON objętych wyjść, wybór wyłącznie lewej/prawej strony i klakson. Potwierdzić odmowę ECU oraz informację HMI według SYS-085/086, również dla ponowień i dawnych żądań. Zwykły interfejs PC nie omija blokady. Odróżnić żądanie awaryjnych od wyboru jednej strony; szczegóły obsługi i arbitrażu rozstrzygnąć w F04 przed wykonaniem.
4. Powtórzyć w zakwalifikowanym zakresie zasilania i temperatury oraz przy aktywnych ochronach/limitach toru światła hamowania i kierunkowskazów. Żądanie awaryjnych nie może omijać ich odcięcia ani limitów SYS-253/254. Sprawdzić warunki wyjścia SYS-087, brak automatycznego odtworzenia odciętych odbiorników według SYS-088 oraz własne reguły wentylatora i HMI. Wyjątek serwisowy sprawdzić odrębnie według SYS-090/091. Utratę łączności sprawdzić według SYS-258. Blokadę snu sprawdzić według SYS-259. Restart i powrót zasilania sprawdzić według SYS-260, a następnie progi/czasy, połączenia, obciążenia, wyposażenie i warunki przerwania w projekcie/procedurze. Wyniki powiązać z HW/FW, konfiguracją i profilem akumulatora. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Awaryjne po utracie HMI/CAN

W odpowiedzi **A na pytanie 266** (2026-11-26) właściciel przyjął SYS-258: działające nieprzerwanie ECU podtrzymuje włączone awaryjne po potwierdzeniu utraty HMI lub komunikacji CAN. Miganie obu stron wykonuje lokalnie; nie wymaga dalszych poleceń panelu ani PC. Reguła obowiązuje również w oszczędzaniu dopuszczającym awaryjne według SYS-257.

Utrata łączności sama nie włącza wyłączonych awaryjnych. Zabezpieczenia każdego toru, limity po usterce i dopuszczone zasilanie nadal obowiązują. Stan faktyczny pozostaje w ECU według SYS-047; przy braku komunikacji HMI nie może zlecić zmiany. Kryteria ważności komunikacji, parametry migania i kwalifikację poleceń opracujemy w architekturze.

SYS-258 dotyczy nieprzerwanej pracy w bieżącym okresie wybudzenia. Późniejszy SYS-259 określa blokadę snu; SYS-260 wyklucza samoczynne odtworzenie po restarcie/powrocie zasilania, a współdziałanie z wyborem pojedynczej strony pozostaje do ustalenia w F04; reguły pojedynczego kierunkowskazu SYS-052/251/252 pozostają zachowane.

### Plan próby SYS-258

1. Na stanowisku rzeczywistego ECU–HMI ze sprawnymi torami włączyć awaryjne i potwierdzić wspólne miganie obu stron. Osobno odtworzyć wyłączenie HMI, przerwę komunikacji CAN oraz brak wymaganych komunikatów przy pozostającym zasilaniu. Przy nieprzerwanej pracy ECU potwierdzić lokalne podtrzymanie migania po rozpoznaniu utraty, bez PC i dalszych poleceń panelu. Rejestrować komunikację, stan ECU i rzeczywiste napięcia/prądy obu stron.
2. Powtórzyć przy zgaszonym silniku, w aktywnym oszczędzaniu według SYS-257 oraz z symulowaną nominalną pracą silnika. Wywołać utratę w fazach ON i OFF migania; potwierdzić ciągłość funkcji w dopuszczonych warunkach. Powtórzyć przy wcześniej wyłączonych awaryjnych: sama utrata nie może ich włączyć. Przypadki pojedynczego kierunku sprawdzić odrębnie według SYS-052/251.
3. Przywrócić prawidłową komunikację i odczytać rzeczywisty stan awaryjnych z ECU, zgodnie z jego rolą właściciela danych. Sprawdzić zgodność prezentacji HMI z wyjściami; kwalifikację poleceń i synchronizację danych opracować z protokołem przed próbą. Bez restartu ECU potwierdzić, że podtrzymanie nie zależy od sesji Windows ani obsługi HMI.
4. Przy braku HMI/CAN zweryfikować nadal aktywne zabezpieczenia oraz limity wyjść według SYS-253, a także warunki zasilania. Podtrzymanie awaryjnych nie może omijać odcięcia właściwego toru; kryteria i bezpieczne wymuszanie usterek określić przed wykonaniem. Blokadę snu sprawdzić według SYS-259; restart/powrót zasilania według SYS-260, a wybór strony po jego ustaleniu w F04 odrębnym planem. Przed próbą przyjąć parametry migania, czasy/kryteria łączności, połączenia, obciążenia, wyposażenie i warunki przerwania; wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Awaryjne a usypianie

W odpowiedzi **A na pytanie 267** (2026-11-26) właściciel przyjął SYS-259. Przy zgaszonym silniku i odłączonym PC włączone awaryjne są zadaniem wymagającym dalszej obsługi; upływ bezczynności nie wyłącza ich ani nie uruchamia pełnego snu ECU/HMI. Sprawne HMI pozostaje aktywne razem z ECU zgodnie z SYS-062. Brak komunikacji nie zwalnia blokady, gdy ECU nadal obsługuje awaryjne według SYS-258.

Wyłączenie przez użytkownika albo zakończenie obsługi zgodnie z właściwą ochroną usuwa tylko blokadę od awaryjnych. ECU następnie ocenia zwykłe warunki SYS-059/062–066, w tym inne zadania wymagające pracy. Nie oznacza to bezwarunkowego natychmiastowego snu ani odnowienia limitów prób. Zabezpieczenia i dopuszczone zasilanie nadal obowiązują. Dodatkowego limitu czasu awaryjnych nie wybrano; restart i powrót zasilania określa SYS-260.

Pobór obu urządzeń i równoczesnego oświetlenia obu stron wymaga bilansu oraz pomiarów. Cel czterech tygodni postoju SYS-093 dotyczy uśpionych urządzeń bez korzystania z motocykla; pracujące awaryjne oceniamy osobno.

### Plan próby SYS-259

1. Na stanowisku rzeczywistego ECU/HMI przy zgaszonym silniku i odłączonym PC włączyć awaryjne. Bez dalszej obsługi przycisków odtworzyć upływ skonfigurowanej bezczynności i dalszą pracę ponad ten czas. Potwierdzić miganie oraz brak polecenia i wykonania skoordynowanego snu. Sprawne HMI ma pozostawać aktywne z ECU. Rejestrować CAN, stany snu i rzeczywiste prądy urządzeń oraz lamp.
2. Powtórzyć podczas oszczędzania dopuszczającego awaryjne SYS-257 oraz po utracie HMI/CAN według SYS-258. Brak interakcji użytkownika i brak komunikacji nie mogą same zwolnić blokady, gdy ECU nadal obsługuje awaryjne. Nie wymagać działania uszkodzonego HMI; niezależną pracę ECU sprawdzić według SYS-258.
3. Wyłączyć awaryjne świadomym poleceniem i potwierdzić ustąpienie ich blokady. Osobno sprawdzić spełnione i niespełnione pozostałe warunki snu: obsługę wentylatora, wymagany zapis danych i PC. Sen jest dopuszczany dopiero według SYS-059/062–066, z właściwą sekwencją HMI. Powtórzyć po zakończeniu obsługi awaryjnych przez właściwe ochronne odcięcie według zatwierdzonej specyfikacji; nie utożsamiać dowolnej usterki jednej strony z zakończeniem całego trybu.
4. Zmierzyć pobór ECU, HMI i obu stron w dopuszczonych warunkach zasilania oraz obciążeń, z uwzględnieniem oszczędzania i aktywnych zabezpieczeń. Potwierdzić, że blokada snu nie omija odcięć ochronnych ani limitów po usterce. Przed próbą przyjąć kryteria snu, czasy, obciążenia, połączenia i warunki przerwania; wyniki powiązać z HW/FW, konfiguracją i profilem akumulatora. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Awaryjne po restarcie i powrocie zasilania

W odpowiedzi **B na pytanie 268** (2026-11-26) właściciel przyjął SYS-260. Po restarcie programu bez przerwy zasilania oraz po powrocie zasilania przerwanego podczas działania ECU awaryjne pozostają wyłączone do nowego świadomego polecenia użytkownika z HMI.

Poprzedni ON, nadal włączony stan widoczny w HMI i ponowione dawne polecenie nie zastępują nowego działania użytkownika. ECU pozostaje właścicielem stanu; po odzyskaniu łączności HMI ma odczytać i prezentować rzeczywiste OFF według SYS-047. Zmianę po nowym poleceniu dopuścić dopiero przy gotowych torach i spełnionych warunkach zasilania oraz ochrony.

Dawne awaryjne nie odtwarzają po restarcie blokady snu SYS-259. Nie oznacza to bezwarunkowego snu: nadal obowiązują pozostałe warunki SYS-059/062–066. Reset programu nie odnawia limitu prób po usterce według SYS-253; powrót zasilania odnawia tylko prawa opisane w tym wymaganiu, bez samoczynnego ON. Reguły rozruchu silnika pozostają bez zmian.

Nowe polecenie, oddzielenie go od powtórzeń/starego stanu oraz inicjalizację torów określimy w architekturze i protokole. Współdziałanie z wyborem pojedynczej strony pozostaje otwarte w F04.

### Plan próby SYS-260

1. Na stanowisku ECU–HMI włączyć awaryjne i rejestrować rzeczywiste napięcia/prądy obu stron oraz komunikację. Osobno odtworzyć restart programu przy zachowanym zasilaniu i zanik zasilania przerywający działanie ECU z późniejszym powrotem. Po inicjalizacji i gotowości potwierdzić OFF bez odtworzenia wcześniejszego ON. Zarejestrować także przebieg wyjść podczas restartu; kryteria inicjalizacji i dopuszczalnych przebiegów ustalić przed wykonaniem.
2. Pozostawić HMI działające podczas restartu ECU ze starym stanem ON; po powrocie komunikacji odtworzyć wcześniejsze żądania i powtarzane dane panelu. Potwierdzić brak załączenia i zgodny odczyt OFF z ECU. Powtórzyć przy jednoczesnym restarcie HMI, opóźnionej łączności i niedostępnym panelu. Sam powrót HMI/CAN nie może uruchamiać awaryjnych.
3. Po gotowości zlecić nowe świadome włączenie z HMI. Przy spełnionych warunkach potwierdzić awaryjne oraz blokadę snu SYS-259, także w oszczędzaniu SYS-257. Odtworzyć wcześniejszą blokadę prób po usterce: reset programu jej nie odnawia, a nowe żądanie nie omija zabezpieczeń i limitu SYS-253. Powrót zasilania sam nie załącza wyjść ani próby; ewentualne odnowienie prawa sprawdzić według SYS-253.
4. Powtórzyć oba rodzaje przerwania przy wcześniejszym OFF, podczas podtrzymania bez HMI/CAN SYS-258 i podczas blokady snu SYS-259. Dawny stan nie może blokować późniejszego snu; pozostałe zadania, PC i warunki SYS-059/062–066 nadal obowiązują. Potwierdzić zachowanie odrębnych blokad rozruchu silnika. Przed próbą ustalić reprezentatywne przyczyny restartu, zakres zasilania, kwalifikację poleceń, połączenia, obciążenia i warunki przerwania; wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Kontrola pokrycia przed kartą F04

Stan kontroli: 2026-11-26, po decyzji 268. F04 pozostaje aktywny. Tabela rozdziela przyjęty zakres, kwestie funkcjonalne do doprecyzowania i dane techniczne.

| Obszar | Przyjęty zakres / stan | Dalsze rozstrzygnięcie |
| --- | --- | --- |
| Klakson | SYS-236–240, próby SYS-253 i odcięcie w oszczędzaniu SYS-257. | Tor, prądy, komunikacja i pokrycie diagnostyki w etapach 3–6. |
| Trzy dodatkowe kanały | SYS-241–249: zastosowania, stany, ON/OFF/PWM, próby, limit i lokalna usterka. | Obciążenia, zgodne lampy, bilanse, topologia i komponenty w etapach 3–6. |
| Podstawowe światła | SYS-050, SYS-081–091, SYS-250 i SYS-253. | Kombinacje i parametry lamp, podział kanałów, gotowość i diagnostyka z danymi osprzętu. |
| Kierunkowskazy | SYS-052 i SYS-251–253: utrata/powrót CAN, restart, sen i próby po usterce; pojedynczy kierunek odcięty w oszczędzaniu SYS-257. | Parametry migania i realizacja interfejsu w projekcie. |
| Awaryjne | SYS-257: dostępne w oszczędzaniu; SYS-258: podtrzymanie po utracie HMI/CAN; SYS-259: blokada snu; SYS-260: OFF po restarcie/powrocie zasilania do nowego polecenia. | Współdziałanie z wyborem pojedynczej strony otwarte w F04; następna decyzja 269. |
| Światło hamowania | SYS-051, SYS-253/254 i SYS-256: bezpośrednie wejścia, próba bez HMI oraz wybudzanie obu urządzeń. | Detekcja nowego użycia w śnie, filtracja, długi stan aktywny, czas reakcji i pobór do architektury oraz prób. |
| Wentylator | Zachowane funkcje i zamknięte reakcje F03, w tym SYS-043/044/053/060/061/089 i SYS-184–196. | Dane osprzętu, parametry i procedury na właściwych etapach; F03 pozostaje zamknięty. |
| Zewnętrzne porty | SYS-255: uzgodnione funkcje, bez dodatkowej rezerwy zewnętrznej dla nieokreślonych urządzeń. | Typy, liczby pozostałych torów, pinout i wewnętrzna rezerwa zasobów w architekturze. |
| Oszczędzanie energii | Przyjęte SYS-084–091 i lista SYS-257; klakson odcięty po doprecyzowaniu 265. | Progi, czasy, bilanse i realizacja w architekturze/projekcie. |

Wybudzanie przez hamulce rozstrzyga SYS-256. Odpowiedź 265 i jej doprecyzowanie określają listę odcięcia oraz dodają możliwość awaryjnych w oszczędzaniu (SYS-257). Odpowiedź A na pytanie 266 przyjmuje podtrzymanie po utracie HMI/CAN (SYS-258). Odpowiedź A na pytanie 267 przyjmuje blokadę skoordynowanego snu (SYS-259). Odpowiedź B na pytanie 268 przyjmuje OFF po restarcie i powrocie zasilania do nowego polecenia (SYS-260). Współdziałanie z wyborem strony pozostaje do rozstrzygnięcia w F04, w pytaniu 269. Po nich przeprowadzimy kontrolę spójności i kartę do zatwierdzenia przez właściciela. F04 pozostaje aktywny.

## Kontrola listy odcięcia energii

Lista jest przyjęta jako SYS-257 na podstawie odpowiedzi 265 oraz A na doprecyzowanie klaksonu. Zestawienie i granice znajdują się w [przyjętym zakresie](#odbiorniki-w-oszczędzaniu-energii). Nie oznacza to zamknięcia stanów awaryjnych ani wykonania prób. Wentylator, HMI i funkcje silnika zachowują własne reguły.

## Następna decyzja

**Pytanie 269:** poza oszczędzaniem energii awaryjne są włączone, a kierowca wybiera lewy albo prawy kierunkowskaz. Jak przejść do pojedynczej strony?

Propozycja A: awaryjne mają pierwszeństwo; ECU odrzuca wybór pojedynczej strony do świadomego wyłączenia awaryjnych. Dopiero kolejny nowy wybór strony uruchamia kierunkowskaz. Alternatywa B: nowy świadomy wybór lewo/prawo od razu wyłącza awaryjne i włącza wybraną stronę. Decyzja nie jest jeszcze podjęta.

W obu propozycjach świadome włączenie awaryjnych zastępuje aktywny pojedynczy kierunek, a wyłączenie awaryjnych kończy sygnalizację bez samoczynnego powrotu dawnej strony. W oszczędzaniu żądanie pojedynczej strony nadal jest odrzucane według SYS-257 i nie wyłącza dostępnych awaryjnych. A wymaga osobnego zakończenia trybu awaryjnych; B skraca przejście do jednej strony. Ochrony oraz kwalifikacja nowych poleceń nadal obowiązują. Sposób obsługi przycisków/HMI i parametry pozostają do projektu.
