# Oprogramowanie ECU

Miejsce na kod sterowania silnikiem i akcesoriami, pomiary, komunikację, diagnostykę i aktualizację ECU.

Stan: brak implementacji. Procesor, język, środowisko budowania i organizacja czasu wykonania pozostają do ustalenia.

Po rozpoczęciu implementacji ten dokument opisuje budowanie, uruchamianie i testowanie komponentu. Testy jednostkowe przechowujemy przy kodzie.

ECU nalicza i przechowuje [chronione całkowite motogodziny i ODO](../../docs/architecture/chronione-liczniki.md), SYS-074–077. Ochronę egzekwuje firmware i architektura sprzętu, obejmując protokół, narzędzia testowe, pamięć, bootloader i odzyskiwanie. Chroniona procedura producenta/serwisu ma umożliwiać inicjalizację nowego ECU i przenoszenie udokumentowanych wartości, z rejestrem każdej operacji. Przy przeniesieniu używanego ECU do innego motocykla firmware egzekwuje odrębne uprawnienie producenta do zmiany liczników i zapewnia rejestr operacji według SYS-153. Szczegóły autoryzacji i konkretne mechanizmy pozostają do projektu; nie przyjęto nieodwracalnego blokowania debuggera.

[SYS-078 i ADR-008](../../docs/decisions/adr-008-dostep-do-firmware-ecu.md) określają dostęp do firmware: w trybie użytkowym wyłącznie wersje zatwierdzone przez producenta projektu, z zachowaniem programowania i debugowania dla twórców. Kontrolę trzeba zaprojektować po stronie ECU, obejmując uruchamianie, aktualizację, programowanie i odzyskiwanie zgodnie z uzgodnionym modelem zagrożeń. Autoryzacja dostępu rozwojowego, polityka starszych wersji i przejść między trybami są otwarte.

SYS-075/079 wymagają wybudzenia ECU obrotami przedniego koła i naliczania ODO także przy zgaszonym silniku oraz niedostępnym HMI. Zaprojektować obsługę pierwszych impulsów i przejść sen–praca zgodnie z przyszłym limitem błędu. Motogodziny nadal wymagają pracy silnika; samo koło nie żąda rozruchu. [Analiza i zakres prób](../../docs/architecture/chronione-liczniki.md).

SYS-081 wymaga wyłączenia świateł przednich i tylnych pozycyjnych przed prawidłowym uśpieniem oraz pozostawienia ich wyłączonych po wybudzeniu ze zgaszonym silnikiem do polecenia HMI. Obsługa snu nie przywraca automatycznie stanu sprzed snu; należy ją uzgodnić z ważnością żądań HMI. [Przebieg i zakres prób](../../docs/architecture/usypianie-ecu-hmi.md).

SYS-082 wymaga automatycznego włączenia przednich i tylnych pozycyjnych po potwierdzonym uruchomieniu silnika, również bez gotowego lub sprawnego HMI. Mijania i drogowe włącza użytkownik z HMI. W logice rozdzielić samo wybudzenie od potwierdzonego uruchomienia silnika i poleceń oświetlenia. [Zakres prób](../../docs/architecture/usypianie-ecu-hmi.md).

SYS-083/084 dodają przejście z mijania/drogowych na pozycyjne po zatrzymaniu silnika oraz tryb oszczędzania przed snem na podstawie bieżącego pomiaru napięcia. Sterowanie i decyzje pozostają w ECU. SYS-085 wymaga odrzucania zwykłych żądań ponownego ON dla odbiorników objętych aktywnym odcięciem, także poza HMI. Do HMI przekazywana jest rzeczywista odmowa do prezentacji według SYS-086. SYS-087 wymaga utrzymania odcięcia w normalnym użytkowaniu do potwierdzonej pracy silnika i utrzymania napięcia powrotu przez ustalony czas; automatyka pozycyjnych nie omija tego warunku. Lista odłączanych odbiorników, kwalifikacja spadku, wartości progu/czasu są otwarte. SYS-088/089 rozdzielają powrót: odbiorniki użytkownika czekają na nowe polecenie, automatyczne funkcje ochrony silnika działają według aktualnego zapotrzebowania oraz własnych zabezpieczeń. Ręczne wymuszenie wentylatora nie wraca samo: [analiza i plan prób](../../docs/architecture/oszczedzanie-energii.md).

SYS-090: jawny tryb serwisowy dopuszcza zwolnienie odcięcia do testów bez pracy silnika przy potwierdzonym stabilnym zasilaniu warsztatowym. ECU egzekwuje warunki i aktywne zabezpieczenia wyjść. Samo połączenie PC nie zwalnia odcięcia; uruchomienie testu wymaga osobnego polecenia. SYS-091 wymaga po utracie sesji blokady nowych testów, dokończenia rozpoczętego najpóźniej do limitu przyjętego przed startem i następnie cofnięcia wyjątku serwisowego. ECU nadzoruje limit niezależnie od Windows; utrata/powrót sesji nie odracza końca. Zabezpieczenia pozostają nadrzędne. Uprawnienia, detekcja sesji, reakcje na zanik zasilania i stany końcowe pozostają do projektu: [analiza i plan prób](../../docs/architecture/oszczedzanie-energii.md).

SYS-092: osobne profile ochrony akumulatorów AGM i LiFePO4 przy wspólnym sprzęcie. Do projektu: parametry, wybór i zapis profilu oraz jego współpraca z istniejącymi zasadami oszczędzania i serwisu. Zatwierdzenie i otwarte szczegóły: [ADR-010](../../docs/decisions/adr-010-akumulatory-agm-lifepo4.md).

SYS-094: przyjmowanie i stosowanie zmian wybranych wartości map podczas pracy silnika. Po utracie Windows ostatnio zastosowane wartości pozostają aktywne w bieżącej pracy ECU, bez automatycznego trwałego zapisu. Zakres, walidacja, moment zastosowania, ponowne połączenie i restart/zanik zasilania pozostają do specyfikacji: [ADR-011](../../docs/decisions/adr-011-strojenie-na-zywo.md).

SYS-028 określa maks. trzy niezależne, kompletne zestawy uzgodnionych map jednej konfiguracji silnika. Przydział pamięci i obsługę edycji rozwijamy według [specyfikacji map](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-095: ECU dopuszcza trwały zapis zmian map wyłącznie przy zgaszonym silniku i po wyraźnym poleceniu użytkownika z Windows. Strojenie na żywo nie uruchamia automatycznego utrwalania. Potwierdzenie zatrzymania, warunki zasilania, przerwanie zapisu i równoczesny rozruch wymagają specyfikacji w [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-102: ECU egzekwuje przyjmowanie i wdrażanie krytycznej konfiguracji wyłącznie przy zgaszonym silniku i na wyraźne polecenie. Przez całą operację blokuje rozrusznik, zapłon i wtrysk; samo podłączenie PC nie uruchamia blokady. Dopuszczone strojenie map na żywo jest zachowane. Lista pól, realizacja blokad i mechanizmy reakcji SYS-105 wymagają specyfikacji: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-103: po potwierdzonej utracie Windows przed odebraniem całości krytycznej konfiguracji i przed wdrożeniem ECU anuluje transfer, zachowuje poprawną i nienaruszoną dotychczasową konfigurację oraz zwalnia blokady operacji. Rozruch wymaga nowej świadomej próby; samo zwolnienie blokad go nie uruchamia. Detekcja/czasy i realizacja ponownego dopuszczenia rozruchu pozostają do określenia; samodzielne dokończenie z kompletem danych podlega SYS-104: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-104: z kompletem danych i przyjętym wyraźnym poleceniem wdrożenia ECU przy prawidłowym zasilaniu samodzielnie kończy sprawdzanie/wdrożenie mimo utraty Windows. Blokady operacji zwalnia dopiero po potwierdzonym powodzeniu; rozruch wymaga nowej świadomej próby. Błędy podlegają SYS-105, a powrót po zaniku zasilania SYS-106: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-105: po błędzie sprawdzania/wdrażania ECU automatycznie wraca do poprzedniej konfiguracji, jeżeli może ją odtworzyć i potwierdzić jej poprawność; zwalnia blokady operacji, a rozruch wymaga nowej świadomej próby. Bez żadnej potwierdzonej poprawnej konfiguracji utrzymuje blokady rozrusznika, zapłonu i wtrysku oraz dostęp do naprawy konfiguracji z Windows. Mechanizm powrotu i walidacji do projektu: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

Zgodnie z SYS-152 po potwierdzonym resecie przy zmianie profilu ECU usuwa poprzednią konfigurację użytkową i mapy, przywraca fabryczne nastawy i udostępnia pierwszą konfigurację z Windows. W trybie użytkownika zachowuje całkowite ODO i motogodziny. Blokady rozruchu przy braku poprawnej konfiguracji wynikają z SYS-105. Potwierdzenie obejmujące historię DTC umożliwia usunięcie jej w ramach tego samego resetu według SYS-154. Według SYS-155 ECU trwale przyjmuje reset przed czyszczeniem i wykonuje go samodzielnie. Po powrocie zasilania wznawia przyjęty reset z aktywnymi blokadami rozrusznika, zapłonu i wtrysku.

Według SYS-156 ECU trwale przechowuje nieaktywny projekt po resecie i udostępnia go Windows po restarcie. Dopiero zgodny „Standard”, jawne wdrożenie i potwierdzenie poprawnego zapisu kompletnego profilu pozwalają zwolnić blokady pierwszej konfiguracji.

SYS-106: po zaniku zasilania podczas zmiany krytycznej konfiguracji ECU odtwarza tylko kompletną i poprawną konfigurację: nową po trwałym potwierdzeniu wdrożenia przez ECU, inaczej poprzednią poprawną. Po sprawdzeniu zwalnia blokady operacji bez Windows i dopuszcza nową świadomą próbę rozruchu. Bez poprawnych danych pozostają blokady i dostęp serwisowy. Mechanizm trwałego potwierdzenia, odtwarzania i ponownego dopuszczenia rozruchu do projektu: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-107: pełny zestaw map, w ramach tej samej konfiguracji silnika, ECU przyjmuje i roboczo zastępuje tylko przy zgaszonym silniku. Warunek egzekwuje ECU. Na żywo pozostaje edycja dopuszczonych wybranych wartości według SYS-094/101; trwały zapis nadal podlega SYS-095. Walidacja, spójność, reakcje na próbę rozruchu i przerwanie do specyfikacji: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-108: ECU dopuszcza trwały zapis wybranego kompletnego zestawu map, aktywnego lub nieaktywnego, zachowując pozostałe dane robocze i trwale zapisane, oraz zapis wszystkich skonfigurowanych jednym poleceniem. Każdy zapis podlega SYS-095. Po zaniku zasilania w trakcie zapisu wszystkich zestawów ECU wybiera jedną wersję całej grupy według sumy i kompletności pakietu (SYS-109). Mechanizm pamięci doprecyzujemy w projekcie. [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-110 obejmuje blokadę rozrusznika, zapłonu i wtrysku oraz odrzucenie zwykłych poleceń kierowcy od przyjęcia pełnej podmiany zestawu lub trwałego zapisu map. Po sprawdzeniu sumy poprawnych danych ECU zwalnia blokady operacji. Rozruch wymaga nowej świadomej próby. [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-111 określa reakcję na błędną sumę trwałego zapisu map przy zachowanym zasilaniu. ECU odrzuca pakiet, odtwarza robocze wartości objętych zestawów z poprzedniego poprawnego zapisu i udostępnia flagę wyniku po odzyskaniu danych. [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-112 określa kasowanie flagi w bieżącym statusie po potwierdzeniu poprawności kolejnego trwałego zapisu map.

SYS-113 wymaga dokończenia przyjętego trwałego zapisu po odłączeniu Windows, przy komplecie danych i prawidłowym zasilaniu. ECU zatwierdza zapis po weryfikacji sumy i danych.

SYS-114 określa anulowanie nieukończonego transferu zestawu po utracie Windows i zachowanie dotychczasowych map.

SYS-115 wymaga udostępnienia bieżącego stanu map, flagi błędu sumy i statusu operacji po ponownym połączeniu Windows z działającym ECU.

SYS-116 wymaga stosowania całej poprawnej grupy roboczych zmian jako jednej aktualizacji. Przy błędzie ECU odrzuca całe polecenie i udostępnia przyczynę.

SYS-117 określa przywrócenie wybranego zestawu do pamięci roboczej z poprawnego zapisu, przy zgaszonym silniku i blokadach według SYS-110.

SYS-118 rozdziela mapy aktywnego zestawu od pojedynczych nastaw wspólnych dla konfiguracji silnika.

SYS-119 określa wybór mapy położenia zadanego elektronicznego zaworu wydechowego wraz z pozostałymi mapami aktywnego zestawu w wyposażonych konfiguracjach 2T.

SYS-120 określa bazowy zapłon gaźnika z aktywnego zestawu według obrotów bez TPS albo według obrotów i położenia przepustnicy z TPS.

SYS-157 wymaga odcięcia zapłonu, a w profilach wtryskowych także wtrysku, po potwierdzonej utracie synchronizacji wału podczas pracy. Powrót sterowania wymaga zatrzymania i nowej świadomej próby ze zweryfikowaną synchronizacją. [Macierz F03](../../docs/requirements/f03-ochrona-i-usterki.md).

Według SYS-158 potwierdzona utrata wcześniej uzyskanej synchronizacji podczas rozruchu elektrycznego przed rozpoznaniem pracy silnika kończy próbę. Firmware odłącza rozrusznik także przy trzymanym START. Kolejna próba wymaga zatrzymania, zwolnienia i nowego naciśnięcia START.

Według SYS-159 potwierdzona utrata synchronizacji podczas rozruchu kopniakiem przed rozpoznaniem pracy silnika kończy próbę. Odcięcie zapłonu i wtrysku trwa do zatrzymania wału i dopuszczenia nowej świadomej próby z wiarygodną synchronizacją.

Według SYS-160 naciśnięcie START przy zgaszonym silniku i aktywnym przewodowym STOP utrzymuje rozrusznik wyłączony. Po zwolnieniu STOP potrzebne jest nowe naciśnięcie START. [Macierz F03](../../docs/requirements/f03-ochrona-i-usterki.md).

Według SYS-161 przewodowy STOP wykryty podczas kręcenia wyłącza rozrusznik i kończy próbę. Po zwolnieniu STOP ECU wymaga ponownego naciśnięcia START.

Według SYS-162 zwolnienie przewodowego STOP przy nadal obracającym się wale utrzymuje odcięcie. Ponowne dopuszczenie zapłonu i wtrysku wymaga zatrzymania wału i nowej świadomej próby z wiarygodną synchronizacją.

Według SYS-163 wybudzone ECU rozróżnia zwolniony i naciśnięty przycisk STOP w sprawnym obwodzie oraz przerwę w obwodzie. Nadzór działa niezależnie od HMI i CAN. [Macierz F03](../../docs/requirements/f03-ochrona-i-usterki.md).

SYS-164 wymaga zapisu DTC z zamrożoną ramką przy potwierdzonej przerwie w STOP. ECU kontynuuje pracę i dopuszcza nową próbę rozruchu przy spełnieniu pozostałych warunków.

Według SYS-165 ECU klasyfikuje zwarcie przewodu sygnałowego STOP do masy jako stan usterki odrębny od naciśnięcia sprawnego przycisku i pozostałych stanów według SYS-163.

SYS-166 wymaga zapisu DTC z zamrożoną ramką po potwierdzonym zwarciu STOP do masy. ECU kontynuuje pracę i dopuszcza nową próbę rozruchu przy spełnieniu pozostałych warunków.

SYS-167 wymaga działania odcięcia zapłonu i wtrysku przez STOP przy zawieszeniu głównego firmware. Po użyciu STOP podczas pracy silnika firmware uwzględnia warunki ponownego dopuszczenia sterowania według SYS-162.

SYS-168 wymaga odłączenia rozrusznika przez STOP przy zawieszonym głównym firmware i przytrzymanym START. Nowa próba po odzyskaniu działania wymaga zwolnienia STOP oraz puszczenia i ponownego naciśnięcia START według SYS-161.

Według SYS-169 niezależny nadzór po wykryciu zawieszenia głównego firmware odcina zapłon, wtrysk i rozrusznik oraz osobno inicjuje reset.

Według SYS-170 ECU po takim resecie utrzymuje odcięcie zapłonu i wtrysku przy obracającym się wale, również po odzyskaniu synchronizacji. Powrót sterowania wymaga potwierdzonego zatrzymania i nowej świadomej próby z wiarygodną synchronizacją oraz spełnienia pozostałych warunków.

Według SYS-171 ECU po resecie nadzoru odrzuca START naciśnięty przed potwierdzeniem zatrzymania wału. Załączenie rozrusznika wymaga nowego naciśnięcia po zatrzymaniu i spełnienia pozostałych warunków rozruchu.

Według SYS-172 ECU zapisuje DTC i zamrożoną ramkę po potwierdzeniu resetu nadzoru. Ramka zawiera przyczynę resetu i wiarygodne dane związane ze zdarzeniem w zakresie ich dostępności.

Według SYS-173 nadzór ogranicza automatyczne próby uruchomienia przy powtarzających się resetach przed ukończeniem startu ECU. Kryterium zakończenia uruchamiania będzie wejściem do projektu komunikacji firmware z nadzorem.

Według SYS-174 ECU po limicie standardowych prób samoczynnie rozpoczyna odzyskiwanie przy utrzymanym odcięciu zapłonu, wtrysku i rozrusznika. Powrót do rozruchu podlega SYS-170 i SYS-171. Mechanizm uruchamiania odzyskiwania wymaga projektu.

Według SYS-175 ECU najpierw podejmuje samodzielne odzyskiwanie gotowości. Po niepowodzeniu udostępnia przewodowy tryb naprawy dla Windows także przy nieuruchomionym głównym firmware.

Według SYS-176 odzyskiwanie ma osobny limit kilku prób. ECU kończy sekwencję po potwierdzeniu gotowości albo przechodzi do naprawy z Windows po wyczerpaniu limitu. Wartość limitu i kryteria zakończenia próby wymagają projektu.

Według SYS-177 ECU po zaniku zasilania w stanie oczekiwania na naprawę odtwarza ten stan i bezpośrednio udostępnia tryb naprawy z Windows. Odcięcie obowiązuje od chwili powrotu zasilania.

Według SYS-178 po zaniku zasilania w trakcie samodzielnej próby ECU odtwarza wykorzystanie limitu i zalicza przerwaną próbę jeden raz. Po wyczerpaniu limitu udostępnia naprawę z Windows.

Według SYS-179 ECU po zaniku zasilania w trakcie standardowej próby zachowuje liczbę zakończonych prób i ponawia przerwaną w tym samym miejscu limitu. Po wyczerpaniu limitu bez gotowości rozpoczyna odzyskiwanie.

Według SYS-180 ECU zamyka serię standardowych prób lub samodzielnego odzyskiwania po potwierdzeniu gotowości i ustalonym okresie stabilnej pracy. Ponowne zawieszenie w tym okresie obciąża bieżącą serię.

Według SYS-181 po zaniku zasilania podczas pracy silnika i powrocie zasilania przy obracającym się wale ECU utrzymuje odcięcie zapłonu i wtrysku. Dopuszczenie sterowania wymaga potwierdzonego zatrzymania wału i nowej świadomej próby z wiarygodną synchronizacją.

Według SYS-182 zanik zasilania podczas rozruchu elektrycznego kończy próbę. Po powrocie zasilania rozrusznik pozostaje wyłączony do potwierdzenia zatrzymania wału i nowego naciśnięcia START, przy spełnieniu pozostałych warunków.

Według SYS-183 po zaniku zasilania podczas rozpoczętej próby kopniakiem i powrocie przy obracającym się wale ECU utrzymuje odcięcie zapłonu i wtrysku. Dopuszcza sterowanie w nowej próbie kopniakiem po potwierdzonym zatrzymaniu i z wiarygodną synchronizacją.

Według SYS-184 potwierdzona usterka pomiaru temperatury płynu powoduje zapis DTC z zamrożoną ramką. W wyposażonym profilu ECU lokalnie włącza sprawny wentylator podczas pracy silnika przy utrzymującej się potwierdzonej usterce. Po potwierdzeniu zatrzymania silnika kończy to wymuszenie także przy włączonym chłodzeniu po zgaszeniu (SYS-185). Przy zgaszonym silniku ECU przyjmuje ręczne żądanie z HMI przy potwierdzonej usterce zgodnie z SYS-186. Egzekwuje limit czasu i odcięcie napięciowe według SYS-061 oraz zabezpieczenia wyjścia. Przy potwierdzeniu usterki podczas automatycznego chłodzenia po zgaszeniu wycofuje żądanie automatyczne. Ręczne żądanie może podtrzymać pracę na warunkach SYS-186 (SYS-187). Po odzyskaniu wiarygodnego pomiaru automatyczne chłodzenie może wrócić według SYS-188, z zachowaniem pierwotnego terminu zakończenia.

Przy potwierdzonym przegrzaniu podczas pracy silnika z wiarygodnego pomiaru ECU przekazuje stan do HMI i prowadzi sterowanie według bieżącego profilu oraz obowiązujących zabezpieczeń (SYS-189).

Po odłączeniu wyjścia wentylatora z powodu potwierdzonego przeciążenia ECU zapisuje DTC i zamrożoną ramkę oraz przekazuje stan usterki do HMI według SYS-190.

SYS-121 określa zgłoszenie usterki TPS i awaryjny zapłon gaźnika ze zweryfikowanej krzywej zależnej od obrotów, przy prawidłowej synchronizacji wału.

SYS-122 przypisuje krzywą awaryjną do konfiguracji silnika jako wspólną dla jej zestawów map.

SYS-123 określa utrzymanie krzywej awaryjnej do zatrzymania silnika i powrót do mapy z TPS przy następnym rozruchu z wiarygodnym sygnałem.

SYS-124 określa warunki rozruchu gaźnika na krzywej awaryjnej przy potwierdzonej usterce TPS i zgłoszenie tej usterki.

SYS-125 określa dwie osie bazowej mapy dawki w strategii z jednym pomiarem obciążenia.

SYS-126 określa bazowy zapłon we wtrysku i wspólne źródło obciążenia w profilach z jednym wymaganym pomiarem.

SYS-127 uzależnia wymagane pomiary obciążenia i ich udział w pracy nominalnej od konfiguracji referencyjnego silnika.

SYS-128 określa zgłoszenie pojedynczej usterki wymaganego TPS lub pomiaru ciśnienia oraz kontynuowanie pracy na zweryfikowanej kalibracji właściwej dla tej utraty.

SYS-129 określa kontrolowane zatrzymanie wtrysku przy pojedynczej usterce wymaganego pomiaru, gdy brakuje zweryfikowanej kalibracji właściwej dla tej usterki.

SYS-130 określa pozostanie na kalibracji awaryjnej do zatrzymania silnika i powrót do sterowania nominalnego przy następnym uruchomieniu z wiarygodnymi pomiarami.

SYS-131 dopuszcza rozruch wtrysku z pojedynczą usterką na kalibracji zweryfikowanej do rozruchu, z zachowaniem pozostałych warunków i zgłoszeniem usterki.

SYS-132 określa kontrolowane zatrzymanie i blokadę rozruchu przy utracie obu pomiarów obciążenia. Po odzyskaniu jednego pomiaru i zatrzymaniu nowa próba rozruchu podlega SYS-131.

SYS-133 domyślnie wymaga kontrolowanego zatrzymania i blokady rozruchu po utracie jedynego wymaganego pomiaru obciążenia. Wyjątek dla konkretnego silnika podlega udokumentowaniu przez OEM i weryfikacji na DustONE.

SYS-134 wymaga osobnego dopuszczenia rozruchu bez jedynego pomiaru w ramach wyjątku według SYS-133. Przy wyjątku dotyczącym wyłącznie dalszej pracy ECU utrzymuje blokadę rozruchu do potwierdzenia wiarygodności pomiaru.

SYS-135 przypisuje ECU odrzucenie żądania zmiany zestawu map podczas pracy awaryjnej po usterce TPS lub pomiaru ciśnienia i przekazanie przyczyny do HMI.

SYS-136 określa automatyczny wybór „Standard” do pracy nominalnej po usterce wymaganego TPS albo pomiaru ciśnienia. W pracy awaryjnej ECU stosuje zweryfikowaną kalibrację dla danej usterki.

SYS-137 określa wymuszenie „Standard” i blokadę zmiany zestawu z HMI dla potwierdzonych usterek wymagających pracy awaryjnej lub zatrzymania silnika.

SYS-138 wymaga zachowania wymuszonego wyboru „Standard” po restarcie ECU. ECU używa prawidłowego, trwale zapisanego zestawu po spełnieniu warunków pracy nominalnej.

SYS-139 wymaga zgłoszenia błędu i blokady rozruchu przy braku poprawnego wymuszonego zestawu „Standard” po restarcie, także przy dostępnym innym poprawnym zestawie.

SYS-140 wymaga zgłoszenia błędu zestawu wybranego przez kierowcę przy restarcie i dopuszcza rozruch na poprawnym zapisanym „Standard” tej konfiguracji przy spełnieniu pozostałych warunków.

SYS-141 wymaga zgłoszenia błędu i blokady rozruchu przy odrzuceniu po restarcie wszystkich wersji zestawu kierowcy i „Standard”. Blokada obowiązuje do potwierdzenia poprawnego zapisu jednego z tych zestawów, także przy dostępnym trzecim zestawie.

SYS-142 wymaga trwałego zapamiętania „Standard” wybranego zastępczo po błędzie zestawu kierowcy. Powrót do odzyskanego zestawu wymaga nowego wyboru kierowcy.

SYS-143 określa przyjęcie poprawnego żądania podczas jazdy, przekazanie statusu oczekiwania do HMI i wykonanie zmiany w dopuszczonym momencie tej jazdy.

SYS-144 wymaga odmierzenia limitu od przyjęcia oczekującego żądania, jego wygaśnięcia po upływie limitu i przekazania wyniku do HMI.

SYS-145 określa zastąpienie oczekującego wyboru nowym poprawnym żądaniem, odmierzenie limitu od jego przyjęcia i przekazanie aktualnego oczekującego wyboru do HMI.

SYS-146 wymaga anulowania oczekującej zmiany po wyborze aktywnego zestawu i przekazania potwierdzenia do HMI.

SYS-147 wymaga anulowania oczekującej zmiany przy wymuszeniu „Standard” po usterce i nowego wyboru kierowcy po powrocie do pracy nominalnej.

SYS-148 określa zachowanie przyjętego żądania po utracie łączności z HMI i wykonanie go w dopuszczonym momencie przed upływem pierwotnego limitu.

SYS-149 określa wykonanie poprawnego wyboru na postoju przy zgaszonym silniku i zasilanym ECU, także dla nadal ważnego żądania z jazdy.

SYS-150 wymaga zakończenia ważności oczekującego żądania i odtworzenia ostatnio zastosowanego zestawu z poprawnego zapisu po restarcie ECU.

SYS-151 wymaga zachowania pierwotnego terminu oczekiwania po ponownym wyborze tego samego oczekującego zestawu.

SYS-101: ECU przyjmuje robocze zmiany wybranych wartości aktywnego i nieaktywnych zestawów podczas pracy silnika. Edycja nie przełącza zestawu; zmiany nieaktywnego wpływają na silnik dopiero po jego świadomym wybraniu. Trwały zapis nadal podlega SYS-095. Szczegóły: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-099: po restarcie ECU aktywuje ostatnio wybrany prawidłowy zestaw spośród trwale zapisanych, także bez HMI. Zapamiętanie wyboru i zapis wartości map mają odrębne reguły; brak automatycznego utrwalania edycji na żywo. SYS-100 wymaga po prawidłowym śnie/wybudzeniu odrzucenia roboczej edycji i użycia trwale zapisanych wartości, bez automatycznego utrwalania. Mechanizm pamięci wyboru, walidacja, gotowość do rozruchu i przerwana sekwencja snu są do projektu: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).
