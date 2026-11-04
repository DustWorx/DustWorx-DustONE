# DustWorx — zakres systemu ECU / HMI / aplikacja Windows

Status: punkt wyjścia do wymagań; zakres zapisany na podstawie opisu właściciela projektu. Propozycje i otwarte decyzje wymagają dalszego uzgodnienia.

## 1. Cel

Opracowanie systemu sterowania motocyklem obejmującego ECU, HMI na kierownicy oraz jedną aplikację Windows do konfiguracji, strojenia, personalizacji HMI, diagnostyki, aktualizacji i prac rozwojowych.

**Przeznaczenie potwierdzone przez właściciela:** wyłącznie sport i testy poza drogami publicznymi.

**Bieżący etap projektu:** opracowanie prototypu ECU + HMI i aplikacji Windows. Właściciel pozostawia dalsze przeznaczenie projektu do późniejszej decyzji (ustalenie z 2026-10-18). Wymagania produkcyjne doprecyzujemy po określeniu dalszego kierunku i skali.

## 2. Wymagania wynikające z opisu

| ID | Wymaganie |
| --- | --- |
| SYS-001 | ECU steruje pracą silnika jednocylindrowego. |
| SYS-002 | Ten sam wariant sprzętowy ECU obsługuje silniki dwusuwowe i czterosuwowe bez zmian na PCB. |
| SYS-003 | Wybór silnika 2T lub 4T jest dostępny przez konfigurację w aplikacji Windows. |
| SYS-004 | ECU obsługuje światła przednie, tylne i STOP, wentylator, rozrusznik, kierunkowskazy, klakson oraz dodatkowe wyjścia konfigurowalne, np. do dodatkowego oświetlenia. Liczba wyjść, ich parametry i sposób podłączenia obciążeń pozostają do ustalenia. |
| SYS-005 | ECU komunikuje się z HMI na kierownicy przez CAN. |
| SYS-006 | Jedna aplikacja Windows obsługuje ECU oraz HMI. |
| SYS-007 | Aplikacja umożliwia konfigurację ECU i strojenie silnika za pomocą map. |
| SYS-008 | Aplikacja Windows umożliwia tworzenie własnych ekranów HMI przez dobór układu wskaźników i pól danych, kolorów, czcionek oraz grafik. Dostępne są również gotowe szablony. |
| SYS-009 | Aplikacja umożliwia diagnostykę ECU i HMI. |
| SYS-010 | Aplikacja umożliwia aktualizację oprogramowania ECU i HMI. |
| SYS-011 | Development tool w aplikacji Windows umożliwia podgląd danych i logów, testy wejść/wyjść oraz analizę, wysyłanie i rejestrowanie ramek CAN. Debugowanie kodu przez debugger procesora odbywa się w osobnym środowisku programistycznym. |
| SYS-012 | ECU obsługuje silniki z gaźnikiem oraz z wtryskiem paliwa. Rodzaje i parametry układów wtryskowych pozostają do ustalenia. |
| SYS-013 | ECU jest przeznaczone do instalacji elektrycznej motocykla klasy 12 V, z akumulatorem AGM lub LiFePO4 według SYS-092. Zakres napięć pracy i zachowanie podczas rozruchu pozostają do określenia. |
| SYS-014 | ECU obsługuje silniki z gaźnikiem bez TPS oraz z gaźnikiem z TPS (czujnikiem położenia przepustnicy). |
| SYS-015 | Wspólna PCB ECU zawiera sprzęt do obsługi wariantów gaźnikowych oraz wtrysku TPI/TBI, bez przeróbek PCB ani wymiany obsady komponentów między zastosowaniami. Warianty 2T podlegają warunkom smarowania SYS-032 i SYS-033. Modele, roczniki i parametry elektryczne pozostają do określenia; zgodność konwersji TPI nie została potwierdzona. |
| SYS-016 | Przyciski obsługi HMI oraz przełączniki kierownicy sterujące akcesoriami, np. światłami i kierunkowskazami, są podłączone do HMI. HMI przekazuje żądania sterowania akcesoriami do ECU przez CAN, a ECU steruje odbiornikami. START i STOP mają niezależne od HMI połączenia według SYS-048 i SYS-037. |
| SYS-017 | Menu i przełączanie ekranów HMI są obsługiwane fizycznymi przyciskami. Ekran HMI nie ma funkcji dotykowej. |
| SYS-018 | HMI zastępuje fabryczny licznik i stanowi główny panel motocykla, prezentujący prędkość, przebieg, dane silnika i stan motocykla. Źródła danych, zakres wskazań i parametry pomiarów pozostają do ustalenia. |
| SYS-019 | ECU rejestruje występujące usterki jako DTC i zapisuje zamrożone ramki danych (freeze frame) powiązane z danym DTC, opisujące warunki jego wystąpienia. |
| SYS-020 | Diagnostyka w aplikacji Windows umożliwia odczyt zapisanych DTC i powiązanych freeze frame oraz rozróżnienie usterek aktualnie aktywnych i zapisanych w historii. |
| SYS-021 | Zapis DTC i powiązanej freeze frame zawiera rzeczywistą datę i godzinę, czas od uruchomienia ECU oraz informację o ważności czasu rzeczywistego. Brak wiarygodnej daty i godziny nie wstrzymuje zapisu DTC, freeze frame ani czasu od uruchomienia. |
| SYS-022 | Historia DTC i powiązanych freeze frame nie jest automatycznie kasowana wskutek ustąpienia usterki, upływu czasu, kolejnych cykli pracy ani ponownego uruchomienia ECU. Zapisy diagnostyczne są zachowywane w pamięci nieulotnej. Ręczne kasowanie według SYS-025; obsługa zapełnienia pamięci pozostaje do ustalenia. |
| SYS-023 | Ostrzeżenie o danym DTC na HMI wygasa po potwierdzonym ustąpieniu usterki, zgodnie z kryteriami diagnostycznymi przypisanymi do tego DTC. Wygaszenie ostrzeżenia nie usuwa historycznego DTC ani jego freeze frame. |
| SYS-024 | Dla każdego DTC ECU przechowuje czas i freeze frame pierwszego oraz ostatniego wystąpienia i licznik wystąpień. Pierwszy zapis jest zachowywany, ostatni aktualizowany przy kolejnym wystąpieniu; nie jest wymagany osobny rekord każdego nawrotu. |
| SYS-025 | Aplikacja Windows umożliwia eksport historii DTC i freeze frame oraz świadome ręczne skasowanie historii po wyraźnym potwierdzeniu użytkownika. Eksport jest dostępny przed kasowaniem, ale nie jest obowiązkowym warunkiem kasowania. |
| SYS-026 | Komputer z aplikacją Windows łączy się z systemem ECU i HMI przewodowo. Konkretny interfejs i topologia połączenia pozostają do ustalenia. |
| SYS-027 | Podczas standardowej obsługi jeden kabel podłączony do jednego wspólnego punktu zapewnia aplikacji Windows dostęp do ECU i HMI, obejmujący konfigurację, diagnostykę i aktualizacje obu urządzeń. |
| SYS-028 | ECU przechowuje maksymalnie 3 niezależne, kompletne zestawy uzgodnionych map dla jednej konfiguracji silnika. Każdy zestaw zawiera własne wartości obsługiwanych map, np. zapłonu i paliwa w konfiguracji wtryskowej. Użytkownik może przełączać aktywny zestaw z HMI także podczas pracy silnika. Szczegółowa zawartość, warunki i sposób przełączenia wymagają określenia w specyfikacji sterowania. |
| SYS-029 | ECU posiada tor pomiaru wartości ciśnienia paliwa oraz wejście binarne czujnika/wyłącznika ciśnienia oleju, rozróżniające obecność i brak ciśnienia. Parametry elektryczne, zakres pomiaru paliwa i logika wejścia oleju pozostają do ustalenia. |
| SYS-030 | PCB ECU zawiera pomiar ciśnienia atmosferycznego do kompensacji pracy wtrysku oraz osobny pomiar temperatury ECU. |
| SYS-031 | Pomiar temperatury powietrza dolotowego do kompensacji wtrysku jest realizowany przez fabryczny lub zewnętrzny czujnik IAT. Temperatura mierzona na PCB stanowi osobny pomiar ECU. |
| SYS-032 | Sterowanie pompą dozującą olej do silnika 2T pozostaje poza zakresem ECU; nie projektujemy dla niej dedykowanej funkcji sprzętowej ani programowej. |
| SYS-033 | Warunkiem montażu ECU w motocyklu 2T jest przystosowanie silnika do mieszanki paliwowo-olejowej przygotowanej w zbiorniku. W motocyklu z oddzielnym dozowaniem wymagane jest sprzętowe usunięcie pompy i odpowiednie przystosowanie układu paliwowego/smarowania. Zgodność danej konwersji wymaga oceny i walidacji; sam demontaż pompy jej nie potwierdza. |
| SYS-034 | ECU steruje elektronicznym zaworem wydechowym (power valve) w silnikach 2T wyposażonych w taki napęd. Typy napędów, wymagane sygnały sterujące i ewentualne sprzężenie zwrotne dobierzemy do docelowych silników. |
| SYS-035 | Priorytetem projektowym jest możliwie maksymalna kompaktowość ECU do motocykli enduro. Ocenie podlega kompletne urządzenie: PCB, obudowa, złącza i przestrzeń instalacyjna na wyprowadzenie wiązki. Liczbowe limity gabarytów pozostają do określenia po analizie miejsca montażu i architektury sprzętu. |
| SYS-036 | Kompletne ECU i HMI mają znosić deszcz, błoto, zachlapania oraz chwilowe zanurzenie, np. podczas brodzenia lub upadku w wodzie. Wymaganie obejmuje obudowy, złącza i przepusty. Głębokość, czas, warunki zanurzenia i kryteria prób pozostają do określenia. |
| SYS-037 | Przycisk gaszenia silnika STOP ma osobny obwód przewodowy, umożliwiający zgaszenie silnika także przy awarii HMI lub komunikacji CAN. Realizacja obwodu i zachowanie przy uszkodzeniu przewodów pozostają do określenia. |
| SYS-038 | Platforma ECU obsługuje przepustnicę poruszaną mechanicznie linką, z odczytem TPS w wariantach wyposażonych w ten czujnik. Sterowanie napędem przepustnicy elektronicznej (ride-by-wire) pozostaje poza zakresem sprzętu i firmware. Obsługa gaźnika bez TPS pozostaje wymagana według SYS-014. |
| SYS-039 | System wykrywa przewrócenie motocykla i automatycznie wyłącza silnik po potwierdzeniu tego stanu. Sposób wykrywania i warunki zadziałania pozostają do określenia z uwzględnieniem normalnej jazdy enduro. Ponowny rozruch według SYS-040. |
| SYS-040 | Po automatycznym wyłączeniu silnika wskutek przewrócenia, postawieniu motocykla i spełnieniu warunków bezpieczeństwa możliwy jest ponowny rozruch przyciskiem START lub kopniakiem, bez wyłączania i ponownego włączania zasilania systemu. Samo postawienie motocykla nie uruchamia silnika; ponowny rozruch wymaga świadomego działania kierowcy. Szczegółowe warunki odblokowania pozostają do określenia. |
| SYS-041 | PCB ECU umożliwia podłączenie opcjonalnego sygnału sprzęgła oraz opcjonalnego czujnika położenia biegu, rozróżniającego poszczególne biegi, nie tylko luz. Czujniki można dołączyć w przyszłości bez zmian PCB; ich obecność nie jest wymagana do pracy ECU. Sygnały służą do danych i wskazań, bez blokad rozrusznika zależnych od sprzęgła lub położenia biegu. Interfejsy elektryczne i zakres obsługiwanych czujników pozostają do określenia. Wejście stopki bocznej jest poza zakresem. |
| SYS-042 | Obsługa quickshiftera pozostaje poza zakresem tej platformy ECU. Nie przewidujemy dedykowanego wejścia jego czujnika ani funkcji wspomagania zmiany biegu w firmware. |
| SYS-043 | ECU automatycznie steruje wentylatorem według temperatury i umożliwia wymuszenie jego włączenia z HMI przez CAN. Wycofanie ręcznego wymuszenia przywraca sterowanie automatyczne; nie wyłącza wentylatora, gdy automatyka nadal wymaga chłodzenia. |
| SYS-044 | W silnikach chłodzonych cieczą ECU mierzy rzeczywistą temperaturę płynu chłodzącego i udostępnia jej wskazanie na HMI. Progi temperaturowe sterowania wentylatorem są konfigurowalne w aplikacji Windows. Interfejs czujnika, zakres i dokładność pomiaru oraz dopuszczalne ustawienia pozostają do określenia. |
| SYS-045 | DustONE otrzymuje nową wiązkę motocykla i nowe złącze ECU, dobrane do funkcji i parametrów systemu. Zachowanie złącza fabrycznego ECU ani zgodność z jego pinoutem nie są wymagane. Zachowywane czujniki i osprzęt wymagają potwierdzenia własnych interfejsów elektrycznych. |
| SYS-046 | ECU działa samodzielnie bez HMI, zarówno gdy HMI jest nieobecne od włączenia zasilania, jak i po utracie komunikacji podczas pracy. Sama nieobecność HMI lub utrata CAN ECU–HMI nie wyłącza silnika. Sterowanie silnikiem i jego zabezpieczenia są realizowane w ECU na podstawie danych dostępnych bez HMI. |
| SYS-047 | ECU jest właścicielem i źródłem prawdy danych sterowania i eksploatacji motocykla, konfiguracji silnika, map oraz diagnostyki. HMI odczytuje dane i wysyła żądania, np. zmiany mapy lub sterowania akcesoriami; ECU rozstrzyga ich wykonanie i udostępnia rzeczywisty stan. |
| SYS-048 | Przycisk START jest połączony przewodowo z wejściem ECU, niezależnie od HMI i CAN ECU–HMI. Umożliwia żądanie rozruchu przy nieobecnym, wyłączonym lub niesprawnym HMI oraz bez komunikacji z HMI. Żądanie trwa podczas przytrzymywania START; puszczenie przycisku kończy sterowanie rozrusznikiem. ECU realizuje warunki rozruchu; przytrzymywanie nie omija blokad i odcięć. Automatyczne odcięcia i ponowienie próby według SYS-049. |
| SYS-049 | ECU wyłącza sterowanie rozrusznikiem po potwierdzeniu pracy silnika lub po przekroczeniu maksymalnego czasu kręcenia, także gdy START pozostaje wciśnięty. Po takim odcięciu kolejna próba wymaga puszczenia i ponownego naciśnięcia START oraz spełnienia warunków rozruchu; dalsze trzymanie przycisku nie wywołuje kolejnej próby. Metoda potwierdzania pracy silnika, limity czasu i pozostałe warunki rozruchu pozostają do określenia. |
| SYS-050 | Przy nieprzerwanej pracy ECU utrata HMI lub komunikacji CAN ECU–HMI nie zmienia ostatniego stanu świateł przednich i tylnych pozycyjnych. Stan jest zachowywany do kolejnego przyjętego polecenia, z zachowaniem nadrzędnych zabezpieczeń wyjść. Usypianie, wybudzanie, automatyka świateł i oszczędzanie energii podlegają SYS-081–091. Wymaganie dotyczy bieżącej pracy ECU; stany po restarcie lub zaniku zasilania ECU pozostają do ustalenia. |
| SYS-051 | ECU ma osobne wejścia przewodowe wyłączników hamulca przedniego i tylnego, umożliwiające rozróżnienie ich stanów. Przy prawidłowych sygnałach i sprawnym torze wyjściowym światło hamowania jest włączone, gdy aktywny jest co najmniej jeden hamulec, i wyłączone, gdy oba są nieaktywne. Obsługa działa bez HMI i komunikacji CAN ECU–HMI. Parametry elektryczne, filtracja i reakcje na usterki pozostają do określenia. |
| SYS-052 | Miganiem kierunkowskazów steruje lokalnie ECU. Po potwierdzeniu utraty komunikacji z HMI ECU wyłącza aktywny kierunkowskaz. Kryterium i czas potwierdzenia utraty łączności oraz zachowanie po jej przywróceniu pozostają do określenia. |
| SYS-053 | Po potwierdzeniu utraty komunikacji z HMI ECU anuluje ręczne wymuszenie włączenia wentylatora i pozostawia sterowanie automatyce temperatury. Anulowanie wymuszenia nie wyłącza wentylatora, gdy automatyka nadal wymaga chłodzenia. Kryterium i czas potwierdzenia utraty łączności pozostają do określenia. |
| SYS-054 | System nie wymaga osobnego włącznika ani stacyjki do codziennej obsługi. Naciśnięcie przewodowego START oraz rozruch kopniakiem wybudzają automatycznie ECU i HMI. Gotowość ECU do rozruchu ma priorytet; rozruch nie wymaga zakończenia uruchamiania ani sprawności HMI. Źródło detekcji kopania, sekwencja zasilania oraz czasy wybudzania i gotowości pozostają do określenia i weryfikacji. |
| SYS-055 | Użycie przycisków obsługi HMI wybudza samo HMI oraz ECU. Sposób przekazania wybudzenia do ECU pozostaje do określenia; obsługa przycisków HMI nadal odbywa się w HMI. |
| SYS-056 | Przy dostępnym zasilaniu według SYS-058 podłączenie komputera przez przewodowy interfejs serwisowy wybudza ECU i HMI, bez wcześniejszego użycia START lub przycisków HMI. Interfejs i detekcja podłączenia pozostają do określenia. |
| SYS-057 | Przez czas połączenia z komputerem usypianie ECU i HMI jest zablokowane, aby umożliwić pracę z urządzeniami, w tym konfigurację, diagnostykę i aktualizacje. Sposób podtrzymania blokady w obu urządzeniach oraz warunki jej zwolnienia po rozłączeniu pozostają do określenia. |
| SYS-058 | Podczas konfiguracji, diagnostyki i aktualizacji z komputera wymagane jest zasilanie ECU i HMI z akumulatora instalacji nominalnie 12 V lub odpowiedniego zasilacza warsztatowego. Kabel PC zapewnia komunikację i wybudzenie; zasilanie elektroniki obu urządzeń wyłącznie z kabla PC pozostaje poza przyjętym zakresem. Parametry zasilania i wymagana wydajność prądowa będą określone w projekcie. |
| SYS-059 | Gdy silnik nie pracuje i komputer jest odłączony, ECU uruchamia skoordynowane usypianie systemu po konfigurowalnym czasie bezczynności i zakończeniu zadań wymagających dalszej pracy. Używanie przycisków, próby rozruchu oraz rzeczywista aktywność użytkownika w HMI rozpoczynają odliczanie od nowa. Sekwencję określają SYS-062/063; zakres i wartość domyślna czasu oraz szczegółowe blokady pozostają do określenia. |
| SYS-060 | ECU umożliwia konfigurowalną, automatyczną pracę wentylatora po zgaszeniu silnika, z limitem czasu oraz odcięciem przy niskim napięciu akumulatora. Funkcja działa lokalnie w ECU i wstrzymuje jego uśpienie na czas obsługi. Progi, limit czasu, warunki zakończenia i zastosowanie w konkretnym układzie chłodzenia wymagają określenia i weryfikacji. |
| SYS-061 | Przy zgaszonym silniku, w normalnej obsłudze, ręczne wymuszenie wentylatora z HMI podlega tym samym limitom czasu i napięcia co automatyczna praca po zgaszeniu według SYS-060. ECU egzekwuje te ograniczenia również przy aktywnym ręcznym żądaniu; ręczne wymuszenie nie omija odcięć. |
| SYS-062 | ECU jest koordynatorem usypiania systemu. HMI pozostaje aktywne razem z ECU podczas obsługi wymaganych zadań, w tym wentylatora po zgaszeniu, i przechodzi w uśpienie na polecenie ECU po spełnieniu warunków SYS-059. HMI nie podejmuje samodzielnej decyzji o uśpieniu po bezczynności. |
| SYS-063 | Po przyjęciu polecenia uśpienia HMI wysyła ECU aplikacyjną ramkę CAN potwierdzającą przyjęcie polecenia. Po zakończeniu wysyłania potwierdzenia HMI przestaje nadawać i przechodzi w sen. W normalnej sekwencji ECU usypia po uzyskaniu tego potwierdzenia i zakończeniu uzgodnionej fazy usypiania HMI, przy nadal spełnionych warunkach uśpienia. Czasy i identyfikacja bieżącej sekwencji pozostają do określenia; ścieżkę braku potwierdzenia określa SYS-065. |
| SYS-064 | Zasilanie HMI jest wyprowadzone z ECU i kontrolowane przez ECU poprzez sterowany tor zasilania. Awaryjne odłączenie części aktywnej HMI działa niezależnie od aplikacji HMI i komunikacji CAN. Przy odłączonej części aktywnej trzeba zachować wybudzanie przyciskami HMI oraz pozostałe źródła wybudzania według SYS-054–056. Topologia toru zasilania i wybudzania oraz parametry elektryczne pozostają do projektu. |
| SYS-065 | Gdy HMI nie potwierdzi polecenia uśpienia, ECU po ograniczonym oczekiwaniu i próbach awaryjnie odłącza zasilanie części aktywnej HMI, rejestruje problem i może zasnąć przy nadal spełnionych warunkach SYS-059. Awaryjne odłączenie jest rozróżniane od normalnej sekwencji potwierdzonej przez HMI. Czasy, liczba prób, ewentualny cykl odzyskania oraz warunki ponownego załączenia pozostają do określenia. |
| SYS-066 | Po poprawnej sekwencji usypiania wyjście zasilania HMI z ECU pozostaje włączone, a ECU i HMI przechodzą w swoje stany niskiego poboru. Kontrolowane odłączenie zasilania HMI jest ostatecznym środkiem przy awarii albo wynika z jawnie zdefiniowanej polityki ograniczeń dla HMI; nie jest zwykłym etapem usypiania. Kryteria takiej polityki oraz parametry stanów niskiego poboru pozostają do określenia. |
| SYS-067 | Platforma ECU obsługuje zapłon pojemnościowy CDI oraz indukcyjny TCI/IDI. Zgodność konkretnych cewek i torów sterowania wymaga analizy i testów. Liczbę kanałów określa SYS-068; realizacja stopni mocy pozostaje do określenia. |
| SYS-068 | ECU ma jeden niezależnie sterowany kanał zapłonu dla silnika jednocylindrowego. Kanał pracuje z wybranym dla danego silnika typem zapłonu w zakresie SYS-067. Obsługa dwóch niezależnie sterowanych kanałów nie jest objęta zakresem. |
| SYS-069 | Wejście synchronizacji wału korbowego ECU obsługuje czujniki indukcyjne VR oraz czujniki Halla z wyjściem cyfrowym na wspólnej PCB. Parametry elektryczne, zasilanie i zgodność konkretnych czujników wymagają określenia oraz potwierdzenia przez analizę i testy. |
| SYS-070 | PCB ECU zawiera dodatkowe, odrębne od wejścia wału wejście fazy silnika 4T dla czujnika Halla z wyjściem cyfrowym. Czujnik jest opcjonalny w konfiguracjach niewykorzystujących tego sygnału. Wejście fazy nie obsługuje VR. Parametry elektryczne i zgodność konkretnych czujników pozostają do określenia. |
| SYS-071 | ECU obsługuje elektroniczną regulację powietrza biegu jałowego IAC z napędem krokowym dla wybranych modeli enduro 4T z przepustnicą na linkę. Zgodne modele i parametry napędów wymagają potwierdzenia przed doborem elektroniki. Konfiguracje niewykorzystujące IAC pracują bez podłączonego napędu. |
| SYS-072 | Funkcja kontroli trakcji (TC) pozostaje poza zakresem DustONE. ECU nie realizuje algorytmu kontroli poślizgu koła napędzanego. |
| SYS-073 | ECU umożliwia podłączenie opcjonalnego czujnika rezerwy paliwa, odczytuje jego stan i przekazuje dane do ostrzeżenia na HMI. Konfiguracje bez czujnika działają bez tej funkcji. Zgodne czujniki, ich zasilanie i interfejs elektryczny wymagają potwierdzenia. |
| SYS-074 | ECU prowadzi trwały, całkowity licznik czasu pracy silnika (motogodzin), naliczany podczas potwierdzonej pracy silnika i udostępniany HMI oraz aplikacji Windows. Kryteria naliczania, dokładność i utrwalanie wymagają specyfikacji. |
| SYS-075 | ECU prowadzi trwały, całkowity licznik drogi ODO, udostępniany HMI oraz aplikacji Windows. Źródłem pomiaru drogi są obroty przedniego koła; naliczanie przy zgaszonym silniku i wybudzanie określa SYS-079. Kalibracja i dokładność wymagają specyfikacji. Inicjalizacja i przenoszenie wartości według SYS-077. |
| SYS-076 | Całkowite motogodziny i ODO są chronione przed manipulacją użytkownika końcowego. Użytkownik nie może ustawiać, korygować ani kasować ich wartości przez HMI, aplikację Windows, diagnostykę, development tool ani dostępne mu interfejsy ECU. Konfiguracja, operacje serwisowe użytkownika i aktualizacje nie mogą stanowić obejścia tej ochrony. |
| SYS-077 | Chroniona procedura producenta/serwisu umożliwia inicjalizację całkowitych motogodzin i ODO w nowym ECU oraz przeniesienie udokumentowanych wartości przy wymianie ECU. Każda operacja jest rejestrowana. Użytkownik końcowy nie uzyskuje prawa ustawiania, korekty ani kasowania liczników. Szczegóły autoryzacji, dokumentowania i rejestru wymagają specyfikacji. |
| SYS-078 | W trybie użytkowym ECU dopuszcza wyłącznie firmware zatwierdzony przez producenta projektu. Twórcy projektu zachowują dostęp rozwojowy do programowania i debugowania ECU. Realizacja rozdzielenia uprawnień, autoryzacja, uruchamianie, aktualizacja, odzyskiwanie i przejścia między trybami wymagają specyfikacji z zachowaniem ochrony liczników przed użytkownikiem końcowym. |
| SYS-079 | Przy dostępnym zasilaniu wykrycie obrotów przedniego koła wybudza ECU z uśpienia. ECU nalicza ODO podczas toczenia lub pchania motocykla także przy zgaszonym silniku, niezależnie od HMI. Czujnik, tor detekcji w śnie, kryteria wykrycia, czasy i dokładność wymagają specyfikacji. Wybudzanie HMI od tego zdarzenia określa SYS-080. |
| SYS-080 | Po wykryciu obrotów przedniego koła ECU wybudza również HMI. Naliczanie ODO w ECU nie czeka na uruchomienie ani gotowość HMI i działa również przy jego nieobecności lub awarii. Tor przekazania wybudzenia i czasy reakcji wymagają specyfikacji. |
| SYS-081 | Przed prawidłowym przejściem ECU w uśpienie ECU wyłącza światła przednie i tylne pozycyjne. Po wybudzeniu przy zgaszonym silniku światła te pozostają wyłączone do przyjęcia polecenia włączenia z HMI; zapamiętany stan sprzed snu nie przywraca ich automatycznie. |
| SYS-082 | Po potwierdzonym uruchomieniu silnika ECU automatycznie włącza przednie i tylne światła pozycyjne. Światła mijania i drogowe włącza użytkownik z HMI. Automatyka pozycyjnych działa niezależnie od obecności i gotowości HMI, z zachowaniem nadrzędnego odcięcia oszczędzania do spełnienia SYS-087. |
| SYS-083 | Po potwierdzonym zatrzymaniu silnika, gdy włączone są światła mijania lub drogowe, ECU wyłącza je i przechodzi na przednie i tylne światła pozycyjne. Przy zgaszonym silniku użytkownik może ponownie włączyć mijania lub drogowe z HMI; podczas aktywnego odcięcia oszczędzania obowiązują SYS-085/086. |
| SYS-084 | ECU na bieżąco nadzoruje napięcie akumulatora podczas pracy. Przy zgaszonym silniku, jeszcze przed uśpieniem, po wykryciu napięcia poniżej progu uruchamia tryb oszczędzania energii i wyłącza światła pozycyjne oraz zbędne odbiorniki załączone przez użytkownika z HMI. Próg, kryteria wykrycia i lista odbiorników wymagają specyfikacji; wyjście w normalnym użytkowaniu określa SYS-087. |
| SYS-085 | Podczas aktywnego trybu oszczędzania energii ECU odrzuca zwykłe żądania ponownego włączenia odbiorników odłączonych przez ten tryb. Polecenie z HMI lub standardowego interfejsu obsługi nie omija odcięcia; blokadę egzekwuje ECU. |
| SYS-086 | Gdy przy zgaszonym silniku użytkownik próbuje z HMI włączyć odbiornik objęty aktywnym odcięciem oszczędzania energii, HMI wyświetla odmowę i informację, że wymagane jest uruchomienie silnika. Komunikat odzwierciedla stan i decyzję ECU. |
| SYS-087 | W normalnym użytkowaniu ECU zwalnia odcięcie trybu oszczędzania dopiero po potwierdzeniu pracy silnika i utrzymaniu napięcia akumulatora powyżej progu powrotu przez ustalony czas. Do spełnienia obu warunków odbiorniki objęte odcięciem pozostają wyłączone, także przy automatycznym żądaniu ich włączenia. Próg, czas i szczegóły potwierdzenia wymagają specyfikacji. |
| SYS-088 | Po wyjściu z oszczędzania światła mijania, drogowe i dodatkowe odbiorniki załączane przez użytkownika z HMI pozostają wyłączone do nowego polecenia użytkownika. Nie przywracają automatycznie stanów sprzed odcięcia. Światła pozycyjne działają według automatyki SYS-082/087. |
| SYS-089 | Po wyjściu z oszczędzania uzgodnione automatyczne funkcje ochrony silnika, w tym wentylator, działają według aktualnego zapotrzebowania i własnych zabezpieczeń, bez wymogu nowego polecenia HMI. Ręczne wymuszenie wentylatora nie jest automatycznie przywracane; automatyka temperatury działa niezależnie od tego wymuszenia. Nadal obowiązują ograniczenia właściwe dla danej funkcji, w tym SYS-060/061 po zgaszeniu silnika. |
| SYS-090 | Jawnie włączony tryb serwisowy umożliwia zwolnienie odcięcia oszczędzania bez pracy silnika po potwierdzeniu stabilnego zasilania warsztatowego, do testów odbiorników z aplikacji Windows. Samo podłączenie PC nie zwalnia odcięcia. Zabezpieczenia wyjść pozostają aktywne; parametry kwalifikacji, uprawnienia i cykl życia trybu wymagają specyfikacji. |
| SYS-091 | Po potwierdzonej utracie sesji Windows podczas aktywnego testu wyjścia ECU nie przyjmuje nowych testów, a rozpoczęty test może dokończyć pracę do wcześniej ustalonego limitu nadzorowanego w ECU. Utrata sesji nie wydłuża limitu. Po zakończeniu testu ECU wycofuje wyjątek serwisowy i wraca do normalnego sterowania. Zabezpieczenia oraz właściwe warunki przerwania pozostają nadrzędne. |
| SYS-092 | ECU obsługuje zasilanie z motocyklowych akumulatorów AGM oraz LiFePO4 w instalacjach klasy 12 V na wspólnej PCB, bez zmiany obsady komponentów. Oba typy mają osobne profile ochrony akumulatora i podlegają testom zgodności. Modele akumulatorów, zgodne konfiguracje regulatorów, zakresy napięć i temperatur oraz parametry profili wymagają specyfikacji i weryfikacji. |
| SYS-093 | Przy sprawnym, początkowo naładowanym akumulatorze oraz ECU i HMI w prawidłowym uśpieniu wymagany minimalny postój bez doładowania i korzystania z motocykla, z rezerwą na rozruch, wynosi 4 tygodnie (28 dni), przy temperaturze otoczenia od −10°C do +40°C podczas postoju i późniejszego rozruchu. W konfiguracji z rozrusznikiem i kopniakiem, jak Beta, wystarcza rozruch kopniakiem; akumulator zasila ECU i niezbędny osprzęt. W konfiguracji wyposażonej wyłącznie w rozrusznik elektryczny po tym samym postoju wymagany jest rozruch elektryczny. Dla celu postoju minimalne pojemności znamionowe wynoszą 3 Ah dla AGM i 2 Ah dla LiFePO4 (wartości C10). Wymaganie obejmuje zatwierdzone konfiguracje obu typów; stan początkowy, szczegóły próby i limit prądu czuwania wymagają ustalenia oraz testów. |
| SYS-094 | Aplikacja Windows umożliwia stosowanie zmian wybranych wartości map podczas pracy silnika (strojenie na żywo). ECU rozstrzyga dopuszczenie i zastosowanie danych. Po utracie połączenia z Windows ostatnio zastosowane wartości pozostają aktywne w bieżącej pracy ECU, bez automatycznego trwałego zapisu. Zakres edytowalnych wartości, warunki dopuszczenia, walidacja, moment zastosowania, ponowne połączenie i zachowanie po restarcie lub zaniku zasilania wymagają specyfikacji. Przełączanie maksymalnie trzech zestawów według SYS-028 pozostaje odrębną funkcją; trwały zapis podlega SYS-095. |
| SYS-095 | Trwały zapis zmian map w ECU jest dopuszczony wyłącznie przy zgaszonym silniku, po wyraźnym poleceniu użytkownika z aplikacji Windows. ECU egzekwuje warunki dopuszczenia zapisu. Stosowanie zmian podczas strojenia na żywo według SYS-094 nie powoduje ich automatycznego trwałego zapisu. Metoda potwierdzenia zatrzymania silnika, warunki zasilania i zachowanie przy przerwaniu zapisu wymagają specyfikacji. |
| SYS-096 | Wspólna PCB ECU umożliwia odczyt MAP, czyli ciśnienia bezwzględnego w kolektorze dolotowym, z kompatybilnego czujnika OEM lub dodatkowego. Konfiguracje niewymagające tego pomiaru mogą pracować bez podłączonego czujnika. Zgodne czujniki, parametry elektryczne i pomiarowe oraz sposób wykorzystania w danej konfiguracji wymagają specyfikacji. |
| SYS-097 | Wspólna PCB ECU umożliwia odczyt ciśnienia gazów w skrzyni korbowej silnika 2T (CCPS) z kompatybilnego czujnika. Konfiguracje niewymagające tego pomiaru mogą działać bez podłączonego czujnika. Zgodne czujniki, źródło i sposób poboru ciśnienia, parametry elektryczne i pomiarowe oraz wykorzystanie w danej konfiguracji wymagają specyfikacji. Wyłączenie sterowania dozownikiem oleju 2T według SYS-032/033 pozostaje w mocy. |
| SYS-098 | Docelowy zakres silnikowy ECU obejmuje wyłącznie jednocylindrowe silniki 2T i 4T chłodzone cieczą. Silniki chłodzone powietrzem pozostają poza zakresem tej platformy. Wymagany pomiar temperatury płynu chłodzącego określa SYS-044. |
| SYS-099 | Po ponownym uruchomieniu ECU automatycznie aktywuje ostatnio wybrany prawidłowy zestaw map spośród zestawów trwale zapisanych w ECU, również przy nieobecnym lub niegotowym HMI. ECU zapamiętuje wybór zestawu. Mechanizm i warunki zapamiętywania wyboru, walidacja oraz postępowanie przy niepoprawnych danych wymagają specyfikacji. |
| SYS-100 | Po prawidłowym uśpieniu i ponownym wybudzeniu ECU, również bez restartu, niezapisane trwale zmiany wartości map są odrzucane, a ECU korzysta z trwale zapisanych wartości wybranego zestawu. Uśpienie i wybudzenie nie powodują automatycznego trwałego zapisu edycji map. Reguła dotyczy wartości map; wybór zestawu i warunki sekwencji snu zachowują własne wymagania. |
| SYS-101 | Podczas pracy silnika ECU przyjmuje z aplikacji Windows robocze zmiany wybranych wartości map zarówno aktywnego, jak i nieaktywnych zestawów. Edycja nie zmienia wyboru aktywnego zestawu. Zmienione wartości nieaktywnego zestawu wpływają na sterowanie silnikiem dopiero po jego świadomym wybraniu. Trwały zapis nadal podlega SYS-095; lista edytowalnych wartości, walidacja i moment spójnego zastosowania danych wymagają specyfikacji. |
| SYS-102 | Krytyczna konfiguracja silnika, obejmująca m.in. wybór 2T/4T, CDI/TCI oraz typu czujnika i dekodera wału, może być przesyłana do ECU i wdrażana wyłącznie przy zgaszonym silniku, na wyraźne polecenie użytkownika. Przez całą operację ECU blokuje rozrusznik, zapłon i wtrysk. Plik można wcześniej przygotować lokalnie w Windows. Reguła nie ogranicza zatwierdzonego strojenia wartości map na żywo według SYS-094/101. Dokładna lista pól, kryterium zatrzymania, realizacja blokad i zachowanie po przerwaniu operacji wymagają specyfikacji. |
| SYS-103 | Po potwierdzonej utracie sesji Windows podczas nieukończonego transferu krytycznej konfiguracji, przed rozpoczęciem wdrażania, ECU anuluje niepełny transfer, zachowuje dotychczasową konfigurację i zwalnia blokady związane z tą operacją według SYS-102, pod warunkiem że dotychczasowa konfiguracja pozostaje poprawna i nienaruszona. Zwolnienie blokad nie uruchamia rozrusznika ani silnika; rozruch wymaga nowej świadomej próby. Kryteria wykrycia utraty sesji i czasy wymagają specyfikacji. Reguła nie rozstrzyga utraty sesji po rozpoczęciu wdrażania, zaniku zasilania ani przypadku niepotwierdzonej poprawności dotychczasowej konfiguracji. |
| SYS-104 | Jeżeli ECU odebrało komplet krytycznej konfiguracji i przyjęło wyraźne polecenie wdrożenia, po utracie sesji Windows przy prawidłowym zasilaniu samodzielnie kończy sprawdzanie danych oraz wdrożenie dopuszczonej konfiguracji. Dopiero po potwierdzonym powodzeniu zwalnia blokady związane z tą operacją według SYS-102. Rozruch wymaga nowej świadomej próby; samo zwolnienie blokad nie uruchamia rozrusznika ani silnika. Reguła nie określa reakcji na błąd sprawdzania/wdrażania ani zanik zasilania. |
| SYS-105 | Po błędzie sprawdzania danych lub wdrażania krytycznej konfiguracji ECU automatycznie wraca do poprzedniej konfiguracji i zwalnia blokady związane z tą operacją według SYS-102, jeżeli może odtworzyć tę konfigurację i potwierdzić jej poprawność. Rozruch wymaga nowej świadomej próby; samo zwolnienie blokad nie uruchamia rozrusznika ani silnika. Jeśli ECU nie może potwierdzić żadnej poprawnej konfiguracji, utrzymuje blokady rozrusznika, zapłonu i wtrysku oraz dostęp serwisowy do naprawy konfiguracji z Windows. Mechanizmy odtwarzania/walidacji i zachowanie po ponownym uruchomieniu po zaniku zasilania wymagają doprecyzowania. |
| SYS-106 | Po ponownym uruchomieniu po zaniku zasilania podczas zmiany krytycznej konfiguracji ECU odtwarza wyłącznie kompletną i poprawną konfigurację: nową, jeżeli jej wdrożenie zostało trwale potwierdzone przez ECU; w przeciwnym razie poprzednią poprawną. Po sprawdzeniu i odtworzeniu poprawnej konfiguracji samodzielnie zwalnia blokady związane z tą operacją według SYS-102, bez wymagania połączenia lub potwierdzenia Windows. Rozruch wymaga nowej świadomej próby; samo zwolnienie blokad nie uruchamia rozrusznika ani silnika. Bez potwierdzonej poprawnej konfiguracji pozostają blokady rozrusznika, zapłonu i wtrysku oraz dostęp serwisowy do naprawy danych z Windows. Kryteria walidacji, trwałe potwierdzenie wdrożenia i mechanizm odtwarzania wymagają projektu. |
| SYS-107 | ECU przyjmuje i roboczo zastępuje pełny zestaw map, np. przesłany z pliku Windows w ramach tej samej konfiguracji silnika, wyłącznie przy zgaszonym silniku. ECU egzekwuje warunek dopuszczenia operacji. Podczas pracy silnika pozostaje dostępna edycja dopuszczonych wybranych wartości aktywnego i nieaktywnych zestawów według SYS-094/101. Robocze zastąpienie zestawu nie powoduje automatycznego trwałego zapisu; utrwalenie podlega SYS-095. Potwierdzanie zatrzymania, walidacja zgodności/kompletności, spójność zastosowania oraz reakcje na próbę rozruchu i przerwanie operacji wymagają specyfikacji. |

## 3. Podział odpowiedzialności

- **ECU:** samodzielne sterowanie silnikiem i akcesoriami, pomiary, wykrywanie usterek oraz reakcje na błędy. Właściciel danych i wykonawca żądań według SYS-046 i SYS-047. Sterowanie wymagające precyzyjnego czasu realizowane lokalnie w ECU.
- **HMI:** główny panel zastępujący fabryczny licznik: prezentacja prędkości, przebiegu, danych silnika i stanu motocykla; odczyt przycisków i przełączników kierownicy oraz przekazywanie poleceń do ECU przez CAN. Menu i ekrany obsługiwane fizycznymi przyciskami; ekran bez dotyku.
- **Aplikacja Windows:** wspólne środowisko z modułami konfiguracji, map, edycji HMI, diagnostyki, aktualizacji i narzędzi rozwojowych.

Propozycje do uwzględnienia w wymaganiach szczegółowych:

- Określić stany poszczególnych wyjść akcesoriów i ważność żądań po utracie HMI/CAN oraz zachowanie po utracie połączenia z komputerem. Samodzielność ECU i dalsza praca silnika bez HMI są już ustalone (SYS-046/047).
- Oddzielić konfigurację silnika, kalibrację map i projekt wyglądu HMI; określić ich wersje i zgodność z oprogramowaniem urządzeń.
- Ustalić warunki dopuszczające zapis map, zmianę typu silnika, aktualizację i testy wyjść.
- Zdefiniować ograniczenia narzędzi rozwojowych i sposób wejścia w tryb testowy.
- Zdefiniować odzyskiwanie urządzenia po przerwaniu aktualizacji.

### Zakres zapłonu — ustalenie właściciela z 2026-11-01

W odpowiedzi na pytanie 73 właściciel wybrał obsługę CDI oraz zapłonu indukcyjnego TCI/IDI, z potwierdzeniem zgodności konkretnych cewek przez analizę i testy (SYS-067). [ADR-004](decisions/adr-004-zaplon-cdi-indukcyjny.md) zapisuje zakres decyzji, otwarte parametry i plan weryfikacji. W odpowiedzi na pytanie 74 tego samego dnia właściciel wybrał jeden niezależny kanał zapłonu, z priorytetem kompaktowości ECU (SYS-068). Integracja stopni mocy pozostaje otwarta. Kanał oznacza niezależnie sterowany tor zapłonu; liczba jego fizycznych wyprowadzeń i elementów mocy wynika z realizacji.

### Synchronizacja wału i fazy 4T — ustalenia właściciela z 2026-11-01

W odpowiedzi na pytanie 75 właściciel wybrał obsługę czujników wału VR oraz Halla z wyjściem cyfrowym na wspólnej PCB (SYS-069). [ADR-005](decisions/adr-005-interfejsy-synchronizacji.md) określa zakres decyzji, otwarte dane i proponowaną weryfikację. W odpowiedzi na pytanie 76 właściciel wybrał dodatkowe, opcjonalne wejście fazy 4T tylko dla Halla z wyjściem cyfrowym (SYS-070). Zakres VR/Hall z SYS-069 dotyczy wejścia wału. Obsługiwane układy znaczników i dekodery pozostają do określenia.

### Regulacja powietrza biegu jałowego IAC — ustalenie właściciela z 2026-11-01

Po sprawdzeniu wyposażenia Beta RR 4T EFI 2016 właściciel w odpowiedzi na poprawione pytanie 77 wybrał obsługę IAC z napędem krokowym dla potwierdzonych modeli enduro (SYS-071). [ADR-006](decisions/adr-006-iac-naped-krokowy.md) zapisuje podstawę, zakres i proponowaną weryfikację. Modele i parametry napędów oraz tor sterowania pozostają do potwierdzenia; nie przyjęto obsługi wszystkich odmian IAC. Sterowanie główną przepustnicą pozostaje mechaniczne według SYS-038.

### Kontrola trakcji — wyłączenie z zakresu z 2026-11-01

Po przedstawieniu potwierdzonego zastosowania opcjonalnej TC w KTM EXC-F MY2024 właściciel w odpowiedzi na pytanie 78 wyłączył kontrolę trakcji z DustONE (SYS-072). Nie planujemy dedykowanych zasobów ani funkcji sterowania TC. Metoda weryfikacji: przegląd zakresu, architektury i późniejszej implementacji pod kątem tego wyłączenia. Pozostałe uzgodnione pomiary i funkcje sterowania zachowują swoje wymagania.

### Sygnalizacja rezerwy paliwa — ustalenie właściciela z 2026-11-01

Po przedstawieniu potwierdzonego przykładu Beta RR 4T EFI MY2016 właściciel w odpowiedzi na pytanie 79 przyjął opcjonalną obsługę czujnika rezerwy przez ECU i ostrzeżenie na HMI (SYS-073). Funkcja dotyczy stanu rezerwy; nie ustalono ciągłego pomiaru ilości paliwa. Rodzaj czujnika, ewentualne pobudzenie, tor wejściowy, filtracja/histereza, warunki ostrzegania i diagnostyka pozostają do projektu. Informacja użytkowa o rezerwie nie przesądza o typie wejścia sprzętowego.

Proponowana weryfikacja: dla zgodnego czujnika sprawdzić oba stany i ostrzeżenie na HMI, konfigurację bez czujnika oraz odróżnianie usterek toru od prawidłowej informacji o rezerwie. Dla wybranego zbiornika i czujnika ocenić wpływ przechyłów i ruchu paliwa. Kryteria i procedury ustalić po charakterystyce interfejsu; prób nie wykonano.

### Całkowite motogodziny i ODO — ustalenie właściciela z 2026-11-01

W odpowiedzi na pytanie 80 i doprecyzowaniu właściciel wybrał całkowite motogodziny oraz ODO i wymaga odporności obu liczników na manipulację użytkownika końcowego, bez możliwości zmiany lub korekty z jego poziomu (SYS-074–076). ECU pozostaje właścicielem danych. Liczniki pomocnicze A/B nie wchodzą do tego ustalenia. W odpowiedzi A na pytanie 81 właściciel zatwierdził chronioną procedurę producenta/serwisu do inicjalizacji nowego ECU i przenoszenia udokumentowanych wartości, z rejestrem każdej operacji (SYS-077). [ADR-007](decisions/adr-007-chronione-liczniki.md) zapisuje decyzję; [architektura ochrony i plan weryfikacji](architecture/chronione-liczniki.md) określa obszary do projektu. Szczegóły autoryzacji, dowodów i rejestru oraz granice ochrony sprzętowej pozostają do uzgodnienia przed wyborem mechanizmów i komponentów.

W odpowiedzi na pytanie 83 z 2026-11-01 właściciel wskazał obroty przedniego koła jako źródło wybudzania ECU oraz naliczanie drogi również przy zgaszonym silniku (SYS-075/079). [ADR-003](decisions/adr-003-wybudzanie-bez-wlacznika.md) uzupełnia źródła wybudzania, a [architektura liczników](architecture/chronione-liczniki.md) zawiera zakres analizy i prób. W odpowiedzi A na pytanie 84 właściciel potwierdził również wybudzanie HMI przez ECU, bez oczekiwania z naliczaniem drogi na uruchomienie HMI (SYS-080). Sposób wykrywania obrotów, przekazanie wybudzenia i czasy reakcji pozostają do projektu.

### Dostęp do firmware ECU — ustalenie właściciela z 2026-11-01

W odpowiedzi A na pytanie 82 właściciel zatwierdził w trybie użytkowym wyłącznie firmware ECU zaakceptowany przez producenta projektu oraz zachowanie dostępu twórców do programowania i debugowania (SYS-078). [ADR-008](decisions/adr-008-dostep-do-firmware-ecu.md) zapisuje decyzję i zakres przyszłych testów. Dotyczy ona ECU; polityka firmware HMI wymaga osobnego ustalenia. Mechanizmy, komponenty i szczegóły przejść między trybami pozostają do wspólnego wyboru.

### Samodzielność ECU — ustalenie właściciela z 2026-10-25

ECU działa niezależnie od obecności i komunikacji z HMI. Dane i decyzje sterujące należą do ECU; HMI odczytuje dane oraz wysyła żądania (SYS-046/047). Brak HMI nie przerywa pracy silnika, lokalnej diagnostyki ani zabezpieczeń ECU. Dane wymagane do tej pracy muszą być dostępne bez udziału HMI. Ustalenie i konsekwencje architektoniczne: [ADR-002 — samodzielne ECU i HMI jako klient](decisions/adr-002-samodzielnosc-ecu.md).

W odpowiedzi na pytanie 56 i późniejszym doprecyzowaniu z 2026-10-25 właściciel potwierdził: przyciski obsługi HMI pozostają podłączone do HMI, natomiast START i STOP działają niezależnie od HMI. START trafia przewodowo do ECU (SYS-048), a STOP ma osobny obwód gaszenia (SYS-037). Zaktualizowano SYS-016. W odpowiedzi na pytanie 57 właściciel wybrał pracę rozrusznika podczas przytrzymywania START i zakończenie kręcenia po puszczeniu przycisku. W pytaniu 58 zatwierdził oba automatyczne odcięcia i wymóg puszczenia oraz ponownego naciśnięcia START przed kolejną próbą (SYS-049). Metoda potwierdzania pracy silnika, wartości limitów czasu i pozostałe warunki rozruchu, ważność żądań akcesoriów, zachowanie po ponownym połączeniu i szczegóły protokołu pozostają do określenia.

Proponowana weryfikacja SYS-048/049: na stanowisku sprawdzić zakończenie sterowania po puszczeniu START, po zasymulowaniu potwierdzonej pracy silnika i po upływie ustalonego limitu kręcenia. Po obu automatycznych odcięciach podtrzymany START nie może ponownie załączyć rozrusznika; po puszczeniu i ponownym naciśnięciu obowiązują warunki dopuszczenia rozruchu. Powtórzyć próby przy odłączonym HMI. Mierzalne czasy reakcji i warunki symulacji określić przed próbami; testów nie wykonano.

### Dodatkowe pomiary — doprecyzowanie właściciela z 2026-10-18

Wcześniejsze ogólne wymaganie dodatkowych wejść uszczegółowiono do następującego zakresu:

- **Na PCB:** barometr do kompensacji wtrysku oraz osobny pomiar temperatury ECU. Temperaturę dolotu mierzy IAT.
- **Zewnętrzny czujnik ciśnienia paliwa:** tor pomiaru wartości ciśnienia.
- **Czujnik/wyłącznik ciśnienia oleju:** wejście binarne „ciśnienie obecne / brak ciśnienia”, bez wymaganego pomiaru jego wartości.
- **EGT i szerokopasmowa lambda:** pomiary przyrządami zewnętrznymi podczas strojenia; nie są wymagane zintegrowane tory tych pomiarów w ECU.

Do określenia przed projektem torów: interfejs i zakres czujnika paliwa, poziomy i polaryzacja wejścia oleju, diagnostyka przewodów i czujników, zasady aktywacji pomiarów w danym wariancie silnika oraz dokładność i częstotliwość pomiarów. Pomiar barometryczny wymaga uwzględnienia wyrównywania ciśnienia z otoczeniem w projekcie obudowy.

**Podział temperatur potwierdzony przez właściciela:** do kompensacji wtrysku wykorzystujemy fabryczny lub zewnętrzny IAT, a temperaturę na PCB traktujemy jako osobny pomiar ECU (SYS-030, SYS-031). Parametry IAT i sposób pomiaru temperatury ECU określimy przy doborze interfejsów i komponentów. Uzasadnienie rozdzielenia: wpływ temperatury płytki i samonagrzewania na pomiar ilustruje [dokumentacja Bosch BME280, uwaga 7 do dokładności temperatury](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme280-ds002.pdf); przywołanie dokumentu nie jest wyborem komponentu.

Zakres podstawowych czujników dla docelowych układów wtryskowych określimy osobno. Przykładowo [KTM EXC TBI MY2024](https://www.ktm.com/en-ca/2024-enduro-range-press-kit.html) wykorzystuje m.in. temperaturę powietrza, ciśnienie otoczenia i ciśnienie w skrzyni korbowej; samo wskazanie barometru nie definiuje kompletnego zestawu sygnałów sterowania.

### Zakres chłodzenia — ustalenie właściciela z 2026-11-04

W odpowiedzi B na pytanie 107 właściciel ograniczył platformę do silników chłodzonych cieczą, z pomiarem temperatury płynu. Zakres zapisuje SYS-098 i [ADR-012](decisions/adr-012-zakres-chlodzenia-ciecza.md); nie rozszerzamy pomiaru na silniki chłodzone powietrzem.

### MAP — ustalenie właściciela z 2026-11-04

W odpowiedzi A na pytanie 105 właściciel przyjął obsługę MAP na wspólnej PCB; konfiguracje niewymagające pomiaru działają bez czujnika (SYS-096). [Karta MAP](interfaces/cisnienie-dolotu-map.md) zawiera źródło OEM i dane do późniejszego projektowania. Dobór czujnika i parametrów pozostaje we właściwych etapach.

### CCPS — ustalenie właściciela z 2026-11-04

W odpowiedzi A na pytanie 106 właściciel przyjął obsługę pomiaru ciśnienia skrzyni korbowej 2T na wspólnej PCB; konfiguracje niewymagające pomiaru działają bez czujnika (SYS-097). [Karta CCPS](interfaces/cisnienie-skrzyni-korbowej.md) podaje źródło OEM i dane do późniejszego projektowania. Pomiar nie zmienia przyjętych warunków smarowania SYS-032/033.

### Smarowanie 2T — ustalenie właściciela z 2026-10-18

Sterowanie pompą dozującą olej 2T jest wyłączone z ECU. Montaż wymaga pracy silnika na mieszance przygotowanej w zbiorniku, a w motocyklach z dozownikiem — jego sprzętowego usunięcia i odpowiedniego przystosowania układu (SYS-032, SYS-033).

Zakres pompy został rozstrzygnięty. **Konfiguracja TPI po samej eliminacji pompy nie jest zatwierdzona do montażu.** Sposób konwersji i jej walidacja pozostają otwarte; nie wybrano zastępczego rozwiązania smarowania. Uzasadnienie i źródła: [ADR-001 — smarowanie 2T](decisions/adr-001-smarowanie-2t-mieszanka.md).

### Przepustnica — ustalenie właściciela z 2026-10-18

Przepustnica jest poruszana mechanicznie linką. ECU może odczytywać TPS; nie steruje napędem przepustnicy elektronicznej (SYS-038). Zakres obejmuje również gaźniki bez TPS (SYS-014). Parametry wejścia TPS, kalibrację i diagnostykę określimy przy projektowaniu interfejsów czujników. Zakres TPI/TBI według SYS-015 podlega temu ograniczeniu; nie oznacza obsługi ride-by-wire.

### Zestawy map silnika — ustalenie właściciela

ECU ma obsługiwać maksymalnie 3 niezależne, kompletne zestawy uzgodnionych map i wybór aktywnego zestawu podczas pracy silnika (SYS-028). Polecenie wyboru pochodzi z HMI i trafia do ECU przez CAN. Zestawy dotyczą zestrojenia jednej konfiguracji silnika. Strukturę pełnych, niezależnych zestawów właściciel potwierdził odpowiedzią A na pytanie 102 (2026-11-03); podstawa w [ADR-011](decisions/adr-011-strojenie-na-zywo.md), rozwijana [specyfikacja operacji na mapach](interfaces/mapy-i-konfiguracja.md).

Do określenia: zawartość zestawu dla poszczególnych wariantów silnika, walidacja zgodności i kompletności danych, warunki dopuszczenia przełączenia, spójny moment zastosowania nowych danych, ewentualny sposób przejścia, potwierdzenie aktywnego zestawu na HMI oraz techniczne warunki odtwarzania wyboru po ponownym uruchomieniu ECU (reguła wyboru przyjęta w SYS-099). Właściciel w odpowiedzi A na pytanie 101 (2026-11-03) przyjął stosowanie zmian wybranych wartości map podczas pracy silnika: SYS-094 i [ADR-011](decisions/adr-011-strojenie-na-zywo.md). Odpowiedź A na pytanie 103 (2026-11-03) określa trwały zapis zmian wyłącznie przy zgaszonym silniku i na wyraźne polecenie użytkownika (SYS-095). Odpowiedź A na pytanie 104 (2026-11-03) określa zachowanie ostatnio zastosowanych wartości w bieżącej pracy ECU po utracie połączenia z Windows, bez automatycznego utrwalania (SYS-094). Zakres edycji, walidację, moment zastosowania, warunki techniczne zapisu, ponowne połączenie i restart/zanik zasilania określimy w F02.

W odpowiedzi A na pytanie 108 (2026-11-04) właściciel przyjął zapamiętywanie wyboru i aktywowanie ostatnio wybranego prawidłowego zestawu po ponownym uruchomieniu ECU, również bez HMI (SYS-099). Wybór zestawu i utrwalanie edytowanych wartości mają odrębne reguły SYS-099/095; [specyfikacja F02](interfaces/mapy-i-konfiguracja.md) rozwija ich cykl życia.

W odpowiedzi A na pytanie 109 (2026-11-04) właściciel przyjął odrzucenie niezapisanych zmian i powrót do trwale zapisanych wartości map po zwykłym śnie/wybudzeniu, również bez restartu (SYS-100). ECU nie wykonuje automatycznego trwałego zapisu; w bieżącej pracy po utracie Windows nadal obowiązuje SYS-094.

W odpowiedzi A na pytanie 110 (2026-11-04) właściciel dopuścił roboczą edycję wybranych wartości aktywnego i nieaktywnych zestawów podczas pracy silnika. Edycja nie przełącza zestawu; zmiany nieaktywnego zestawu wpływają na silnik dopiero po jego świadomym wybraniu (SYS-101). Trwały zapis pozostaje odrębną operacją według SYS-095.

### Krytyczna konfiguracja silnika — ustalenie właściciela z 2026-11-04

Po porównaniu wariantów właściciel wybrał A na pytanie 111: transfer i wdrożenie tylko po zgaszeniu silnika, z blokadą rozrusznika, zapłonu i wtrysku przez całą operację (SYS-102). Plik można przygotować wcześniej na PC. Wcześniejsza odpowiedź B była prośbą o porównanie. Przyjęta reguła i sprawy otwarte mają źródło w [specyfikacji F02](interfaces/mapy-i-konfiguracja.md) oraz [ADR-011](decisions/adr-011-strojenie-na-zywo.md).

W odpowiedzi A na pytanie 112 (2026-11-04) właściciel przyjął anulowanie nieukończonego transferu po potwierdzonej utracie Windows, zachowanie poprawnej i nienaruszonej dotychczasowej konfiguracji oraz zwolnienie blokad operacji. Rozruch wymaga nowej świadomej próby (SYS-103). Wybór dotyczy utraty sesji przed wdrożeniem.

W odpowiedzi A na pytanie 113 (2026-11-04) właściciel przyjął samodzielne dokończenie sprawdzania i wdrożenia po utracie Windows, gdy ECU ma komplet danych, przyjęło polecenie wdrożenia, a zasilanie jest prawidłowe. Po potwierdzonym powodzeniu ECU zwalnia blokady operacji; rozruch wymaga nowej świadomej próby (SYS-104). Reakcję na błąd rozwija SYS-105, a powrót po zaniku zasilania SYS-106.

W odpowiedzi A na pytanie 114 (2026-11-04) właściciel przyjął automatyczny powrót do poprzedniej konfiguracji po błędzie sprawdzania/wdrażania, ze zwolnieniem blokad po potwierdzeniu jej poprawności. Rozruch wymaga nowej świadomej próby. Gdy nie da się potwierdzić żadnej poprawnej konfiguracji, pozostają blokady rozrusznika, zapłonu i wtrysku oraz dostęp do naprawy konfiguracji z Windows (SYS-105).

W odpowiedzi A na pytanie 115 (2026-11-04) właściciel przyjął po powrocie zasilania odtworzenie kompletnej i poprawnej nowej konfiguracji, jeżeli ECU trwale potwierdziło jej wdrożenie, inaczej poprzedniej poprawnej. Po jej sprawdzeniu ECU samodzielnie zwalnia blokady operacji i dopuszcza nową świadomą próbę rozruchu bez Windows. Bez poprawnych danych pozostają blokady i dostęp serwisowy (SYS-106).

W odpowiedzi „Opcja A” na pytanie 116 (2026-11-04) właściciel ograniczył przesyłanie i robocze zastępowanie pełnego zestawu map do zgaszonego silnika. Podczas pracy pozostaje edycja dopuszczonych wybranych wartości aktywnego i nieaktywnych zestawów. Zapisano SYS-107; trwały zapis nadal podlega SYS-095.

### Wspólne połączenie z aplikacją Windows — ustalenie właściciela

Standardowa obsługa wymaga podłączenia jednego kabla w jednym punkcie. Aplikacja ma uzyskać dostęp do ECU i HMI przez to połączenie (SYS-026, SYS-027). Nie wybrano jeszcze interfejsu, rodzaju złącza, jego lokalizacji ani urządzenia pośredniczącego w komunikacji.

Przy projektowaniu aktualizacji określimy dostępność wspólnego połączenia podczas programowania każdego urządzenia oraz procedury odzyskiwania po przerwanej aktualizacji lub uszkodzeniu oprogramowania. Wymaganie jednego kabla dotyczy standardowej obsługi; architektura awaryjnego odzyskiwania i dostępu debuggera pozostaje do określenia.

### Wybudzanie i praca z komputerem — ustalenie właściciela z 2026-10-25

W odpowiedzi na pytanie 64 właściciel wybrał obsługę bez osobnego włącznika: START i kopniak wybudzają ECU, a przyciski HMI wybudzają HMI oraz ECU. Podłączenie komputera wybudza urządzenia i blokuje ich usypianie na czas połączenia, w tym pracy diagnostycznej i aktualizacji (SYS-054–057). Blokady nie ograniczamy wyłącznie do aktywnego przesyłania danych.

Po porównaniu wariantów w odpowiedzi na pytanie 65 właściciel wybrał zasilanie serwisowe z akumulatora lub zasilacza warsztatowego 12 V. Kabel PC służy do komunikacji i wybudzenia (SYS-058); wybrano wariant A z [porównania zasilania serwisowego](architecture/zasilanie-serwisowe-porownanie.md).

W odpowiedzi na pytanie 66 z 2026-10-25 właściciel potwierdził automatyczne wybudzanie również HMI od START i kopniaka, z priorytetem gotowości ECU do rozruchu (SYS-054). ECU nie czeka na uruchomienie HMI ani potwierdzenie komunikacji.

W odpowiedzi na pytanie 67 z 2026-10-25 właściciel wybrał automatyczne usypianie ECU i HMI po konfigurowalnym czasie bezczynności, przy zgaszonym silniku i odłączonym komputerze. Używanie przycisków rozpoczyna odliczanie od nowa; zadania wymagające dalszej pracy wstrzymują uśpienie (SYS-059).

W odpowiedzi na pytanie 70 z 2026-10-25 właściciel ustalił ECU jako koordynatora usypiania: HMI czeka na jego polecenie, potwierdza przyjęcie ramką CAN, kończy nadawanie i zasypia, po czym zasypia ECU (SYS-062/063). Próby rozruchu i aktywność użytkownika w HMI odnawiają bezczynność według SYS-059. Normalny przebieg i otwarte wyjątki: [sekwencja usypiania ECU–HMI](architecture/usypianie-ecu-hmi.md).

W odpowiedzi na pytanie „71 — wybór po porównaniu” z 2026-10-25 właściciel zatwierdził kontrolę zasilania HMI i wskazał, że zasilanie HMI ma wychodzić z ECU. Wybrano awaryjne odłączenie części aktywnej HMI po nieudanej sekwencji, z zachowaniem wybudzania przyciskami (SYS-064/065). [Porównanie i uzasadnienie wyboru](architecture/brak-potwierdzenia-uspienia-hmi.md) zachowuje rozważone alternatywy.

W odpowiedzi na pytanie 72 z 2026-10-25 właściciel potwierdził pozostawienie zasilania HMI włączonego po poprawnej sekwencji. ECU i HMI pozostają w sleep; kontrolowane odłączenie zasilania jest ostateczną opcją przy awarii lub wynikiem zdefiniowanych ograniczeń dla HMI (SYS-066). Szczegóły polityki ograniczeń pozostają otwarte.

W odpowiedzi A na pytanie 85 z 2026-11-01 właściciel zatwierdził wyłączenie świateł przednich i tylnych pozycyjnych przed prawidłowym uśpieniem oraz pozostawienie ich wyłączonych po wybudzeniu ze zgaszonym silnikiem do polecenia z HMI (SYS-081). Zasada obejmuje wybudzenie ruchem koła; nie przywracamy automatycznie stanu sprzed snu. Stany po restarcie lub zaniku zasilania pozostają do ustalenia.

W odpowiedzi na pytanie 86 z 2026-11-01 właściciel wybrał automatyczne włączenie przednich i tylnych pozycyjnych po potwierdzonym uruchomieniu silnika. Mijania i drogowe włącza użytkownik z HMI (SYS-082). W liście I/O funkcje te są rozdzielone logicznie; liczba kanałów i zgodność z lampami wymagają projektu. W odpowiedzi na pytanie 87 właściciel wskazał przejście z mijania/drogowych na przednie i tylne pozycyjne po zgaszeniu silnika, możliwość ich ponownego ręcznego włączenia z HMI oraz odłączenie zbędnych odbiorników przy niskim napięciu przed uśpieniem (SYS-083/084). [ADR-009](decisions/adr-009-oszczedzanie-energii.md) zapisuje ten zakres; [analiza i plan prób](architecture/oszczedzanie-energii.md) rozdzielają wymagania od rekomendacji i otwartych decyzji. W odpowiedzi A na pytanie 88 właściciel zatwierdził odrzucanie takich poleceń przez ECU i dodał informację HMI o wymaganym uruchomieniu silnika (SYS-085/086). W odpowiedzi A na pytanie 89 właściciel zatwierdził wyjście w normalnym użytkowaniu dopiero przy potwierdzonej pracy silnika i napięciu powyżej progu powrotu przez ustalony czas; do tego momentu odcięcie pozostaje aktywne (SYS-087). W odpowiedzi na pytanie 90 właściciel rozdzielił odbiorniki użytkownika, które po wyjściu pozostają wyłączone do nowego polecenia, od funkcji ochrony silnika wracających pod sterowanie automatyki (SYS-088/089). Wentylator reaguje na aktualne zapotrzebowanie chłodzenia z zachowaniem swoich zabezpieczeń, bez automatycznego odtworzenia ręcznego wymuszenia. W odpowiedzi A na pytanie 91 właściciel dopuścił jawnie włączany tryb serwisowy do testów odbiorników bez pracy silnika, przy potwierdzonym stabilnym zasilaniu warsztatowym i aktywnych zabezpieczeniach wyjść; samo podłączenie PC nie zwalnia odcięcia (SYS-090). W odpowiedzi B na pytanie 92 właściciel dopuścił dokończenie rozpoczętego testu do ustalonego limitu po potwierdzonej utracie sesji Windows, bez przyjmowania nowych testów, po czym wyjątek serwisowy jest wycofywany (SYS-091). Wartości, szczegółowa lista odbiorników, uprawnienia, detekcja utraty sesji i reakcje konkretnych wyjść pozostają do ustalenia.

Podstawa architektury, źródła wybudzania i propozycje prób: [ADR-003 — wybudzanie bez osobnego włącznika](decisions/adr-003-wybudzanie-bez-wlacznika.md). Parametry czasu bezczynności, pozostałe blokady, pobór prądu w czuwaniu, parametry zasilania, czasy przejść, próby odzyskania i obsługa ponownego wybudzenia pozostają do projektu. Nie wybrano jeszcze komponentów ani torów wybudzania.

### Rejestracja diagnostyczna ECU — ustalenie właściciela z 2026-10-18

Potwierdzony zakres zapisu danych obejmuje występujące usterki, ich DTC i powiązane zamrożone ramki danych. Dane mają umożliwiać analizę momentu oraz warunków wystąpienia usterki i ocenę, czy pozostaje aktywna (SYS-019, SYS-020).

Do określenia w wymaganiach szczegółowych: lista i identyfikacja DTC, warunki wykrycia i ustąpienia usterki, zawartość freeze frame, szczegóły kwalifikacji kolejnych wystąpień, źródło i parametry czasu, pojemność i trwałość pamięci, zachowanie po utracie zasilania, obsługa pełnej pamięci i warunki kasowania serwisowego oraz sposób prezentacji zapisów w aplikacji Windows.

Oznaczanie czasu ustalone przez właściciela: rzeczywista data i godzina, czas od uruchomienia ECU oraz informacja, czy czas rzeczywisty jest ważny (SYS-021). Zapis z nieważnym czasem rzeczywistym pozostaje dostępny i jest tak oznaczony. Do określenia: źródło czasu, podtrzymanie, ustawianie i synchronizacja, format i referencja czasowa, dokładność oraz kryteria ważności zegara. Nie ustalono jeszcze wymagania ciągłego zapisu przebiegów jazdy.

### Historia DTC i ostrzeżenia HMI — ustalenie z 2026-10-18

Oddzielamy stan usterki, żądanie wyświetlenia ostrzeżenia oraz historyczny zapis diagnostyczny. Właściciel wymaga zachowania historii i ustąpienia ostrzeżenia HMI po ustąpieniu problemu (SYS-022, SYS-023).

Potwierdzenie ustąpienia wymaga poprawnego wyniku odpowiedniego testu w warunkach, w których może on ocenić dany problem. Brak wykonania testu, brak nowego komunikatu o błędzie lub utrata komunikacji nie są poprawnym wynikiem testu. Dla każdego DTC określimy warunki wykonania testu, potwierdzenia wykrycia i ustąpienia, filtrację/histerezę oraz warunki wygaszenia ostrzeżenia. Nie przyjmujemy jednej arbitralnej liczby cykli dla wszystkich usterek.

Odniesienie projektowe: [AUTOSAR Diagnostic Event Manager, CP R24-11, rozdziały 7.7.8 i 7.7.9](https://www.autosar.org/fileadmin/standards/R24-11/CP/AUTOSAR_CP_SWS_DiagnosticEventManager.pdf) rozdziela starzenie wpisów pamięci (aging) i wygaszanie ostrzeżeń (healing). Zachowanie historii bez automatycznego starzenia jest wyborem tego projektu. Odniesienie nie stanowi deklaracji wdrożenia platformy AUTOSAR ani pełnej zgodności z jej specyfikacją.

Ustalony model historii: dla każdego DTC zachowujemy czas i freeze frame pierwszego oraz ostatniego wystąpienia i licznik wystąpień (SYS-024). Oznaczenia czasu są zgodne z SYS-021. Pierwsze wystąpienie oznacza pierwsze od ostatniego świadomego kasowania historii. Przy pierwszym wystąpieniu oba rekordy opisują to samo zdarzenie; kolejne nowe wystąpienie aktualizuje rekord ostatni i zwiększa licznik.

Zliczamy nowe, potwierdzone wystąpienia, a nie kolejne wykonania testu stale aktywnej usterki. Ponowny nawrót wymaga wcześniejszego potwierdzenia ustąpienia. Restart ECU lub odtworzenie zapisu z pamięci nie stanowią same w sobie nowego wystąpienia. Szczegółowe zasady po przerwaniu zasilania oraz zakres i obsługę nasycenia licznika określimy w specyfikacji diagnostyki.

Aplikacja Windows udostępnia eksport danych oraz jawne kasowanie historii po wyraźnym potwierdzeniu użytkownika (SYS-025). Wcześniejszy eksport jest możliwością, a nie obowiązkowym krokiem. Automatyczne kasowanie historii po ustąpieniu problemu pozostaje wyłączone.

Otwarte decyzje: pojemność pamięci i zachowanie po jej zapełnieniu, zawartość i format eksportu, warunki dopuszczenia kasowania oraz zachowanie diagnostyki przy kasowaniu w obecności aktywnej usterki.

### Sterowanie wentylatorem i temperatura płynu — ustalenia właściciela z 2026-10-18

ECU załącza wentylator według temperatury; HMI umożliwia dodatkowe wymuszenie włączenia przez CAN (SYS-043). Żądanie automatyki i ręczne wymuszenie mogą niezależnie podtrzymywać pracę wentylatora. Wycofanie wymuszenia oznacza powrót do automatyki, bez blokowania jej żądania chłodzenia.

W silnikach chłodzonych cieczą wymagamy pomiaru wartości temperatury płynu, prezentacji na HMI i konfiguracji progów wentylatora w aplikacji Windows (SYS-044). Potrzebny jest czujnik pomiarowy; sam sygnał termowłącznika nie dostarcza wartości temperatury. Czujnik, jego charakterystykę i instalację dobierzemy z uwzględnieniem priorytetu zachowania osprzętu OEM. Istniejący automatyczny zestaw wentylatora Bety wymaga inwentaryzacji.

W odpowiedzi na pytanie 63 z 2026-10-25 właściciel wybrał anulowanie ręcznego wymuszenia po utracie HMI/CAN i pozostawienie sterowania automatyce temperatury (SYS-053). Przy utrzymanym żądaniu chłodzenia wentylator nadal pracuje.

Proponowana weryfikacja SYS-053: przy aktywnym ręcznym wymuszeniu przerwać komunikację ECU–HMI lub odłączyć HMI. Po potwierdzeniu utraty łączności wymuszenie ma być anulowane; przy sprawnym torze wyjściowym sprawdzić dalszą pracę wentylatora, gdy automatyka żąda chłodzenia, oraz wyłączenie, gdy automatyka go nie żąda. Kryterium i czas wykrywania ustalić przed próbami; testów nie wykonano.

W odpowiedzi na pytanie 68 z 2026-10-25 właściciel zatwierdził konfigurowalną funkcję automatycznej pracy wentylatora po zgaszeniu silnika, z limitem czasu i odcięciem przy niskim napięciu akumulatora (SYS-060). Jej obsługa wstrzymuje uśpienie ECU. Przydatność i ustawienia wymagają oceny dla konkretnego układu chłodzenia; nie potwierdzono ich jeszcze dla Bety.

Proponowana weryfikacja SYS-060: przy włączonej funkcji i nieaktywnym ręcznym wymuszeniu sprawdzić pracę po zgaszeniu silnika według automatyki temperatury, odcięcie po limicie czasu oraz odcięcie przy niskim napięciu mimo żądania chłodzenia. Potwierdzić wstrzymanie uśpienia ECU podczas obsługi funkcji i późniejszy powrót do zasad SYS-059. Progi, definicję limitu, czasy reakcji i warunki prób określić przed testami; prób nie wykonano.

W odpowiedzi na pytanie 69 z 2026-10-25 właściciel potwierdził te same ograniczenia czasu i napięcia dla ręcznego wymuszenia przy zgaszonym silniku (SYS-061). Żądanie HMI nie omija odcięć egzekwowanych przez ECU. Zakres pytania dotyczy normalnej obsługi; warunki testów serwisowych ustalimy osobno.

Proponowana weryfikacja SYS-061: sprawdzić działanie ręcznego wymuszenia w dopuszczonym czasie i przy prawidłowym napięciu także wtedy, gdy automatyka temperatury nie żąda chłodzenia. Osobno sprawdzić odcięcie po limicie czasu i przy niskim napięciu mimo utrzymanego żądania HMI. Użyć tych samych parametrów co w próbach SYS-060; aktywne odcięcie nie może zostać ominięte samym żądaniem ON z HMI. Warunki ponowienia i parametry ustalić przed próbami; testów nie wykonano.

Do określenia: zakres, dokładność i filtracja pomiaru, progi temperatury i histereza, ograniczenia ustawień, diagnostyka czujnika/wyjścia oraz reakcje na ich uszkodzenia. Dla pracy po zgaszeniu ustalić wspólny limit czasu i próg napięcia, filtrację i histerezę odcięcia, warunki zakończenia/ponowienia i przejście przy ponownym rozruchu. Doprecyzować zachowanie ręcznego wymuszenia po przywróceniu komunikacji, restarcie ECU i zmianach zasilania. Nie ustalono wartości liczbowych ani docelowego typu czujnika. Temperatura płynu jest odrębnym pomiarem od IAT i temperatury PCB.

### Wyjścia akcesoriów — preferowany kierunek

Po porównaniu wariantów właściciel zaproponował SmartFET-y zamiast przekaźników w celu ograniczenia miejsca. Preferowany kierunek to inteligentne klucze mocy na PCB ECU. [Porównanie i dalsza analiza](architecture/wyjscia-akcesoriow-porownanie.md) rozróżniają tę preferencję od potwierdzenia wykonalności pełnej integracji. Nie wybrano jeszcze komponentów, parametrów i podziału kanałów ani nie zatwierdzono wariantu mieszanego. Zakres akcesoriów SYS-004 i priorytet kompaktowości SYS-035 pozostają obowiązujące.

### Kontakt z wodą i mycie — ustalenia właściciela z 2026-10-18

Kompletne ECU i HMI mają znosić deszcz, błoto, zachlapania oraz chwilowe zanurzenie (SYS-036). Bezpośredni strumień myjki ciśnieniowej pozostaje poza wymaganym zakresem odporności; podczas mycia należy unikać kierowania go na ECU i HMI.

Przed projektem mechanicznym określimy głębokość i czas zanurzenia, warunki prób oraz kryteria akceptacji. Należy zdefiniować stan zasilania urządzeń, stan złączy i zaślepek oraz uwzględnić przepusty i wyrównywanie ciśnienia wymagane przez barometr ECU. Nie wybrano jeszcze stopnia IP ani rozwiązania uszczelnienia; deklaracja odporności wymaga weryfikacji kompletnego urządzenia.

### Automatyczne gaszenie po przewróceniu — ustalenie właściciela z 2026-10-18

System ma wykrywać przewrócenie motocykla i automatycznie wyłączać silnik (SYS-039). Przed doborem sprzętu określimy sposób i miejsce pomiaru, kryteria odróżniania upadku od normalnej jazdy enduro, czas potwierdzania oraz wymagany czas reakcji. Należy także określić realizację wyłączenia silnika i reakcję na usterkę toru wykrywania. Nie wybrano jeszcze czujnika ani toru pomiarowego; zabezpieczenie musi działać w ECU bez udziału HMI (SYS-046). Ręczny STOP według SYS-037 pozostaje osobną funkcją.

**Ponowny rozruch potwierdzony przez właściciela:** po postawieniu motocykla i spełnieniu warunków bezpieczeństwa kierowca może użyć START lub kopniaka bez wyłączania zasilania systemu (SYS-040). Samo postawienie motocykla nie uruchamia silnika. Do określenia: kryteria i czas potwierdzenia prawidłowego położenia, pozostałe warunki odblokowania oraz obsługa przycisku START, który pozostał wciśnięty podczas zadziałania funkcji. Podtrzymane polecenie START nie może być traktowane jako nowe żądanie rozruchu po odblokowaniu.

### Sprzęgło i położenie biegu — ustalenie właściciela z 2026-10-18

Przewidujemy na PCB ECU obsługę opcjonalnego sygnału sprzęgła i czujnika położenia biegu, z rozpoznawaniem poszczególnych biegów, nie tylko luzu (SYS-041). Ma to umożliwić późniejsze podłączenie czujników bez przebudowy PCB. Ich montaż nie jest obowiązkowy; wariant bez tych czujników musi działać. Nie przewidujemy wejścia stopki bocznej.

W odpowiedzi na pytanie 59 z 2026-10-25 właściciel wybrał wykorzystanie sygnałów sprzęgła i biegu do danych oraz wskazań, bez blokad rozrusznika zależnych od tych czujników (SYS-041). Proponowana weryfikacja: przy niezmienionych pozostałych warunkach rozruchu zmiany sygnałów sprzęgła i położenia biegu oraz wariant bez czujników nie zmieniają dopuszczenia pracy rozrusznika. Nie wykonano prób.

Do określenia przed doborem torów wejściowych: reprezentatywne czujniki OEM, typy sygnałów, poziomy elektryczne, liczba rozróżnianych pozycji, kalibracja, diagnostyka oraz konfiguracja obecności czujników. Szczegóły prezentacji danych pozostają do uzgodnienia. Należy odróżnić brak opcjonalnego czujnika od usterki czujnika zadeklarowanego w konfiguracji; brak danych nie może być traktowany jako potwierdzenie luzu ani określonego stanu sprzęgła.

Quickshifter pozostaje poza zakresem (SYS-042). Opcjonalne wejścia sprzęgła i położenia biegu nie oznaczają wymagania tej funkcji; ich obsługa według SYS-041 pozostaje wymagana.

### Polecenia z kierownicy i utrata komunikacji

Przyciski obsługi HMI są podłączone do HMI. Tor sterowania zwykłymi akcesoriami: przełączniki → HMI → CAN → ECU → odbiorniki (SYS-016). Interfejsy wejściowe HMI dobierzemy do zachowywanych elementów obsługi kierownicy. START ma osobny tor: przycisk → wejście ECU → sterowanie rozrusznikiem (SYS-048). Obecność HMI i komunikacja CAN ECU–HMI nie są potrzebne do obsługi START.

**Gaszenie potwierdzone przez właściciela:** przycisk STOP ma osobny obwód przewodowy i umożliwia zgaszenie silnika przy awarii HMI lub CAN (SYS-037). Jest to odrębny tor od zwykłych poleceń akcesoriów. Do określenia: sposób odcięcia zapłonu i podawania paliwa, interfejs elektryczny STOP, reakcja na przerwanie lub zwarcie przewodów i warunki ponownego uruchomienia. Samo wymaganie niezależności od HMI i CAN nie potwierdza jeszcze działania przy awarii procesora ECU.

Samodzielność ECU i dalsza praca silnika przy braku HMI/CAN są wymagane według SYS-046/047. START i odcięcia rozrusznika określają SYS-048/049. Do osobnej analizy pozostają: aktualność i poprawność żądań, zachowanie pozostałych akcesoriów po utracie komunikacji oraz szczegółowe parametry rozruchu.

W odpowiedzi na pytanie 60 z 2026-10-25 właściciel potwierdził zachowanie ostatniego stanu świateł przednich i tylnych pozycyjnych po utracie HMI/CAN, przy nadal działających zabezpieczeniach wyjść (SYS-050). Stany początkowe po restarcie lub zaniku zasilania ECU pozostają do ustalenia.

Proponowana weryfikacja SYS-050: przy działającym ECU i zasilaniu świateł przerwać komunikację oraz wyłączyć lub odłączyć HMI, sprawdzając zachowanie ostatniego stanu dla świateł wcześniej włączonych i wyłączonych. Sprawdzić przyjęcie nowego polecenia po przywróceniu komunikacji oraz zachowanie działania zabezpieczeń wyjść podczas braku HMI. Warunki i kryteria prób zabezpieczeń określić wraz z projektem stopni mocy; prób nie wykonano.

W odpowiedzi na pytanie 61 z 2026-10-25 właściciel wybrał osobne przewodowe wejścia ECU dla hamulca przedniego i tylnego; użycie któregokolwiek załącza światło hamowania, bez zależności od HMI/CAN (SYS-051). Do określenia pozostają interfejsy wyłączników, filtracja, diagnostyka i zachowanie przy uszkodzeniach.

Proponowana weryfikacja SYS-051: przy sprawnych wejściach i wyjściu sprawdzić wszystkie cztery kombinacje sygnałów — lampa wyłączona przy obu nieaktywnych i włączona w pozostałych trzech stanach. Potwierdzić osobny odczyt obu wejść oraz powtórzyć próby bez HMI i komunikacji ECU–HMI. Kryteria czasowe ustalić przed próbami; testów nie wykonano.

W odpowiedzi na pytanie 62 z 2026-10-25 właściciel wybrał wyłączenie aktywnego kierunkowskazu po potwierdzeniu utraty łączności z HMI (SYS-052). Kryterium i czas wykrywania utraty komunikacji oraz reakcja po jej przywróceniu pozostają otwarte.

Proponowana weryfikacja SYS-052: osobno dla włączonego lewego i prawego kierunkowskazu przerwać komunikację ECU–HMI oraz odłączyć lub wyłączyć HMI. Sprawdzić wyłączenie po potwierdzeniu utraty łączności, według ustalonego później kryterium i czasu. Próby obejmą utratę komunikacji podczas obu faz migania. Testów nie wykonano.

### Zasada integracji z motocyklem — ustalenie właściciela

Priorytetem jest zachowanie seryjnych czujników i osprzętu silnika w możliwie największym zakresie, o ile pozwala na to zgodność techniczna z ECU. Nie oznacza to potwierdzonej zgodności ze wszystkimi elementami OEM ani bezwzględnego zakazu ich wymiany. Ewentualne odstępstwa należy uzasadnić wynikami analizy.

Właściciel potwierdził nową wiązkę motocykla i nowe złącze ECU, dobrane do rozszerzonych funkcji DustONE (SYS-045). Nie wymagamy zachowania złącza starego ECU ani odtworzenia całej jego wiązki. Rozpoznajemy interfejsy zachowywanych czujników i osprzętu. Samo dopasowanie połączeń nie stanowi potwierdzenia zgodności elektrycznej.

Dla wybranych modeli przed doborem interfejsów PCB należy zinwentaryzować i sprawdzić parametry czujników, cewek, wtryskiwaczy oraz pozostałych elementów wykonawczych. Wynik analizy ma wskazywać elementy zachowywane, potrzebne adaptacje i ewentualne wymiany wraz z uzasadnieniem.

### Akumulatory AGM i LiFePO4 — ustalenie właściciela z 2026-11-03

Po porównaniu wariantów w pytaniu 95 właściciel wybrał A: AGM i LiFePO4, wspólna PCB, osobne profile ochrony i testy zgodności (SYS-092). [ADR-010](decisions/adr-010-akumulatory-agm-lifepo4.md) zapisuje zatwierdzenie i konsekwencje; [porównanie oraz plan prób](architecture/akumulatory-agm-lifepo4-porownanie.md) pozostawiają wartości parametrów i dobór komponentów do projektu. Typ AGM w Becie jest pierwszą konfiguracją testową, a nie ograniczeniem platformy.

### Postój bez doładowania — ustalenie właściciela z 2026-11-03

W odpowiedzi A na pytanie 96 właściciel wybrał minimalnie 4 tygodnie postoju z zachowaniem rezerwy na rozruch, przy sprawnym i początkowo naładowanym akumulatorze, ECU/HMI w uśpieniu i braku korzystania z motocykla (SYS-093). W odpowiedzi B na pytanie 97 właściciel doprecyzował dla motocykla z obiema metodami, jak Beta: wystarcza rozruch kopniakiem, z zasilaniem ECU i osprzętu niezbędnego do uruchomienia z akumulatora. W odpowiedzi A na pytanie 98 właściciel zatwierdził ten sam czas postoju dla konfiguracji mających wyłącznie rozrusznik elektryczny, z zachowaniem rezerwy na rozruch elektryczny. W odpowiedzi A na pytanie 99 właściciel przyjął dla tego celu temperaturę otoczenia od −10°C do +40°C podczas postoju i późniejszego rozruchu. Zakres pracy elektroniki podczas jazdy ustalimy osobno. W odpowiedzi A na pytanie 100 właściciel przyjął dla celu postoju minimum 3 Ah AGM i 2 Ah LiFePO4; są to pojemności znamionowe C10, a użyteczną pojemność i rezerwę w przyjętych warunkach potwierdzimy dla zgodnych modeli. Stan początkowy i szczegóły próby wymagają ustalenia. [Budżet energii oraz plan weryfikacji](architecture/budzet-energii-postoju.md) wiążą ten cel z poborem całego systemu i późniejszą próbą produktu.

### Pożądana funkcja: rozruch kopniakiem przy osłabionym akumulatorze

Intencja właściciela: umożliwić rozruch silnika kopniakiem, gdy podłączony akumulator 12 V nie wystarcza do użycia rozrusznika, ale nadal zasila elektronikę. Praca bez energii z akumulatora nie jest wymagana w ramach tej funkcji.

Status: funkcja pożądana, do analizy wykonalności i określenia mierzalnych kryteriów. Nie jest jeszcze gwarantowaną zdolnością systemu. Ocena ma objąć cały tor rozruchu: ECU, czujniki, zapłon oraz — przy wtrysku — układ paliwowy. Wariant gaźnikowy i wtryskowy należy ocenić oddzielnie.

Do ustalenia: minimalne napięcie i dostępny prąd pod obciążeniem, modele i profile AGM/LiFePO4 według SYS-092, stan akumulatora, temperatura, obciążenia aktywne podczas rozruchu oraz warunki mechaniczne rozruchu. Nie przyjmujemy arbitralnego progu 12 V jako granicy działania rozrusznika. Napięcie spoczynkowe nie zastępuje oceny pod obciążeniem: [Yuasa — badanie akumulatora ołowiowego](https://www.yuasabatteries.com.au/resources/expert-advice/how-to-test-a-lead-acid-battery).

## 4. Decyzje potrzebne przed doborem sprzętu

| Obszar | Do ustalenia |
| --- | --- |
| Silnik | Pierwszy motocykl testowy: Beta 300 RR Racing / Race Edition, 2015, wskazany przez właściciela. Według właściciela gaźnik, zapłon i instalacja są fabryczne. Do potwierdzenia podczas inwentaryzacji: parametry i stan osprzętu. Do ustalenia: maksymalne obroty oraz reprezentatywne jednostki 4T, TPI i TBI. Obsługa gaźnika z TPS i bez TPS oraz TPI/TBI według SYS-012, SYS-014 i SYS-015, z warunkami smarowania 2T według SYS-032 i SYS-033. |
| Zapłon | Jeden niezależny kanał według SYS-068, z obsługą CDI oraz indukcyjnego TCI/IDI według SYS-067. Do określenia: cewki/moduły referencyjne, parametry i interfejsy oraz integracja stopni mocy. |
| Przepustnica | Mechaniczna, poruszana linką; odczyt TPS zależnie od wyposażenia (SYS-038). Ride-by-wire poza zakresem. Do określenia: parametry, kalibracja i diagnostyka TPS. Gaźnik bez TPS obsługiwany według SYS-014. |
| Bieg jałowy IAC | Obsługa napędu krokowego w wybranych enduro 4T według SYS-071. Do określenia: modele i parametry napędów, kalibracja, zasoby i stopień mocy, wpływ na rozruch i sen, sterowanie oraz diagnostyka. |
| Sprzęgło i położenie biegu | Opcjonalne wejścia do danych i wskazań według SYS-041, bez blokad rozrusznika zależnych od tych sygnałów; czujnik biegu ma rozróżniać poszczególne biegi, nie tylko luz. Stopka boczna poza zakresem. Do określenia: czujniki referencyjne, interfejsy, kalibracja, diagnostyka i szczegóły prezentacji danych. |
| Wykrywanie przewrócenia | Automatyczne wyłączenie silnika według SYS-039; ponowny rozruch po postawieniu motocykla bez cyklu zasilania według SYS-040. Do określenia: tor pomiarowy, lokalizacja, kryteria i czasy detekcji, sposób wyłączenia silnika, diagnostyka oraz szczegółowe warunki odblokowania. |
| Synchronizacja | Wał: VR oraz Hall z wyjściem cyfrowym według SYS-069. Dodatkowe wejście fazy 4T: tylko Hall z wyjściem cyfrowym, opcjonalne zależnie od konfiguracji (SYS-070). Do określenia: parametry i modele czujników, układy znaczników, odniesienie do GMP, dekodery i reakcje na usterki. |
| Układ paliwowy | Rodzaj układu wtryskowego, liczba i parametry wtryskiwaczy, sterowanie pompą paliwa. Dla 2T warunek pracy na mieszance według SYS-033; konwersja TPI wymaga osobnej oceny. |
| Smarowanie 2T | Pompa dozująca olej wyłączona z ECU (SYS-032). Montaż po przystosowaniu silnika do mieszanki (SYS-033); sposób i walidacja konwersji TPI pozostają otwarte. |
| Zawór wydechowy 2T | Sterowanie elektronicznym power valve wymagane według SYS-034. Do określenia: typ napędu i interfejs, parametry zasilania i sterowania, sygnały położenia, kalibracja, diagnostyka oraz zachowanie przy usterce. |
| Instalacja | Instalacja klasy 12 V z AGM lub LiFePO4, wspólna PCB i osobne profile (SYS-013/092). Do określenia: zgodne modele i regulatory, zakres napięć, parametry profili i warunki rozruchu. Pożądany rozruch kopniakiem z osłabionym, podłączonym akumulatorem; rozruch bez energii z akumulatora nie jest wymagany. |
| Akcesoria | Zakres rozszerzony według SYS-004. Przednie i tylne pozycyjne włączają się automatycznie po uruchomieniu silnika; mijania i drogowe uruchamia użytkownik z HMI (SYS-082). Do określenia: liczba niezależnych kanałów i wyjść konfigurowalnych, prądy robocze i rozruchowe, sterowanie bezpośrednie lub przez przekaźniki/styczniki, zabezpieczenia i diagnostyka wyjść. |
| Pomiary | Zakres według SYS-029–SYS-031 i SYS-096/097: ciśnienie atmosferyczne i temperatura na PCB, tor ciśnienia paliwa, wejście ciśnienia oleju 0/1 oraz MAP i ciśnienie gazów w skrzyni korbowej 2T z kompatybilnych czujników. Temperatura dolotu pochodzi z IAT, temperatura PCB jest osobnym pomiarem ECU. Do określenia: parametry, czujniki, dokładność, zabezpieczenia, kalibracja i diagnostyka. EGT i lambda są pomiarami zewnętrznymi podczas strojenia. |
| HMI | Odczyt przełączników kierownicy i polecenia do ECU przez CAN (SYS-016); menu i ekrany obsługiwane fizycznymi przyciskami, ekran bez dotyku (SYS-017). Główny panel zastępujący licznik (SYS-018). Do ustalenia: ekran, liczba i rodzaje wejść przycisków, szczegółowy zakres danych prezentowanych z ECU, trwałość danych przebiegu i ograniczenia zasobów ekranów. Zakres personalizacji według SYS-008; do określenia edytor, format projektu ekranów oraz prezentacja ostrzeżeń w układach użytkownika. |
| Liczniki eksploatacyjne | Całkowite motogodziny i ODO w ECU, z ochroną użytkową i chronioną inicjalizacją/przenoszeniem przez producenta/serwis według SYS-074–077. ODO korzysta z obrotów przedniego koła, które wybudzają ECU także przy zgaszonym silniku (SYS-079). Do określenia: czujnik i tor w śnie, kryteria naliczania, kalibracja, dokładność, trwałość zapisu, autoryzacja, dowody i rejestr operacji oraz ochrona pamięci, uruchamiania i aktualizacji. |
| Połączenie z PC | Połączenie przewodowe (SYS-026), jeden wspólny punkt i jeden kabel do standardowej obsługi ECU/HMI (SYS-027). Do ustalenia: interfejs fizyczny, lokalizacja złącza, realizacja dostępu do obu urządzeń i zasady aktualizacji/odzyskiwania. CAN między ECU i HMI nie przesądza interfejsu komputera. |
| Dostęp i firmware ECU | Tryb użytkowy przyjmuje firmware zatwierdzony przez producenta; twórcy zachowują programowanie i debugowanie (SYS-078). Do określenia: autoryzacja, ochrona uruchamiania i programowania, odzyskiwanie, przejścia między trybami i polityka starszych wersji. Polityka HMI nie została rozstrzygnięta tą decyzją. |
| Diagnostyka | Zapis DTC i powiązanych freeze frame w ECU; odczyt w aplikacji Windows i rozróżnienie usterek aktywnych oraz historycznych (SYS-019, SYS-020). Oznaczanie czasu według SYS-021. Trwałość historii i wygaszanie ostrzeżeń według SYS-022 i SYS-023. Pierwsze/ostatnie wystąpienie i licznik według SYS-024; eksport i ręczne kasowanie według SYS-025. Szczegóły rejestracji, obsługi pełnej pamięci i realizacji zegara do określenia. |
| Mapy silnika | Maksymalnie 3 niezależne, kompletne zestawy uzgodnionych map w ECU i przełączanie z HMI także podczas pracy silnika (SYS-028); po restarcie ECU wybiera ostatnio wybrany prawidłowy zestaw spośród trwale zapisanych, bez zależności od HMI (SYS-099); Windows umożliwia strojenie na żywo wybranych wartości (SYS-094). Trwały zapis zmian tylko przy zgaszonym silniku i na wyraźne polecenie (SYS-095). Do określenia: zakres map/edycji, dopuszczenie i moment zastosowania zmian, walidacja, warunki techniczne zapisu, ponowne połączenie i restart/zanik zasilania. Utrata połączenia Windows zachowuje ostatnio zastosowane wartości w bieżącej pracy ECU (SYS-094). Po prawidłowym śnie/wybudzeniu ECU wraca do trwale zapisanych wartości (SYS-100). Robocze zmiany można przesyłać do aktywnego i nieaktywnych zestawów podczas pracy; edycja nie przełącza zestawu (SYS-101). Krytyczną konfigurację ECU przyjmuje i wdraża tylko przy zgaszonym silniku, z blokadami przez całą operację (SYS-102). Po utracie Windows w nieukończonym transferze ECU anuluje go i zwalnia blokady przy poprawnej, nienaruszonej dotychczasowej konfiguracji; rozruch wymaga nowej świadomej próby (SYS-103). Z kompletem danych i przyjętym poleceniem ECU przy prawidłowym zasilaniu samodzielnie kończy sprawdzanie/wdrożenie mimo utraty Windows i zwalnia blokady po powodzeniu (SYS-104). Błąd operacji: automatyczny powrót do poprzedniej konfiguracji po potwierdzeniu jej poprawności; brak poprawnej konfiguracji oznacza blokady i dostęp serwisowy (SYS-105). Po zaniku zasilania ECU odtwarza kompletną poprawną konfigurację według trwałego potwierdzenia wdrożenia i samodzielnie dopuszcza nową świadomą próbę rozruchu; bez poprawnych danych pozostają blokady i dostęp serwisowy (SYS-106). Pełny zestaw map można przesyłać i roboczo zastępować tylko przy zgaszonym silniku; na żywo pozostaje edycja dopuszczonych wybranych wartości (SYS-107). |
| Narzędzia rozwojowe | Zakres aplikacji ustalony według SYS-011; debugowanie kodu w osobnym środowisku. Do określenia: szczegóły testów wejść/wyjść, warunki dopuszczenia i przerwania testu, funkcje analizy CAN, format logów, przepustowość oraz sprzętowy dostęp debuggera. |
| Warunki pracy | Zastosowanie: sport i testy poza drogami publicznymi. Deszcz, błoto, zachlapania i chwilowe zanurzenie według SYS-036. Bezpośredni strumień myjki ciśnieniowej wyłączony z wymagań. Do określenia: parametry i kryteria prób wodnych, temperatura, pył, drgania i miejsce montażu. |
| Gabaryty i montaż ECU | Priorytet: maksymalna kompaktowość według SYS-035. Właściciel nie wskazał wymiarów ani wybranej obudowy. Do określenia: miejsce i dostępna przestrzeń montażowa, obrys PCB i obudowy, złącza, wyprowadzenie wiązki, mocowanie oraz bilans cieplny. |

## 5. Następny rezultat inżynierski

Przygotowano robocze materiały: [listę funkcji wejść/wyjść](interfaces/wstepna-lista-io.md), [macierz wariantów silnika](architecture/macierz-wariantow-silnika.md) i [plan inwentaryzacji Bety 300 RR Racing 2015](verification/beta-2015-plan-inwentaryzacji.md). Nie są one zatwierdzonym pinoutem ani potwierdzeniem zgodności sprzętu.

Przygotowano pierwszą [architekturę blokową](architecture/blokowa-systemu.md), funkcjonalny przydział zasobów w macierzy wariantów i [macierz SYS → blok → grupa weryfikacji](verification/macierz-wymagan.md). F01 zamknięto w zakresie funkcji; aktywny jest etap 2, pakiet F02: mapy i konfiguracja ECU, według [kolejności procesu](00-proces-i-status.md). Kolejne pakiety podejmujemy po zamknięciu poprzedniego; inwentaryzacja, architektura, bilanse i procedury wykonawcze oczekują we właściwych etapach. Zapisujemy tam wpływ decyzji. Ważne komponenty wybierzemy wspólnie po dojściu do etapu doboru i uzyskaniu jego danych.

## 6. Sposób realizacji i współpracy

Ustalenia właściciela projektu z 2026-10-15:

- Cały proces inżynierski prowadzimy wspólnie w rozmowie: organizację projektu, wymagania, funkcjonalność, architekturę, elektronikę, dobór każdego komponentu, schematy, projekt PCB, mechanikę oraz weryfikację.
- Firmware przygotowuje właściciel projektu z Codexem. Wspólna praca inżynierska obejmuje wymagania, interfejsy i kryteria weryfikacji potrzebne do jego implementacji.
- Pytania przedstawiamy pojedynczo, z przygotowanymi wariantami odpowiedzi. Gdy wybór wymaga danych technicznych lub porównania, przedstawiamy podstawy i konsekwencje przed decyzją.
- Ustalenia i wyniki prac zapisujemy w repozytorium DustWorx/DustWorx-DustONE zgodnie z jego strukturą.
- Obsługa gaźnika z TPS i bez TPS oraz wtrysku TPI/TBI pozostaje celem, z doprecyzowanym warunkiem pracy 2T na mieszance (SYS-032, SYS-033). Pierwszym motocyklem testowym jest jego Beta 300 RR Racing / Race Edition z 2015 r.; jednostki referencyjne 4T i konkretne generacje układów wtryskowych pozostają do ustalenia.

## 7. Motocykl referencyjny i zakres weryfikacji

**Potwierdzone przez właściciela:** dostępny jest cały motocykl Beta 300 RR Racing / Race Edition, rocznik 2015, przeznaczony do pierwszych testów. Wersję Racing / Race Edition wskazał właściciel. Według jego wiedzy gaźnik, układ zapłonowy i instalacja elektryczna są fabryczne. Jest to deklaracja właściciela; oznaczenia, parametry i zgodność ze stanem fabrycznym wymagają potwierdzenia podczas inwentaryzacji. Producent udostępnia instrukcje tej rodziny w [indeksie dokumentacji Beta](https://www.betamotor.com.au/support/off-road/); parametry konkretnego egzemplarza wymagają inwentaryzacji.

Właściciel potwierdził 2026-10-18 brak TPS w gaźniku oraz obecność wentylatora chłodnicy, obecnie załączanego automatycznie zależnie od temperatury, bez ręcznego włącznika. Osobny sterownik wentylatora jest własnym projektem właściciela; czujnik to [B57301K0103A001 - dane i ocena integracji](interfaces/beta-czujnik-temperatury-b57301k0103a001.md), zamontowany według właściciela w przewodzie łączącym obie chłodnice, z końcówką w płynie. Ten zestaw jest odstępstwem od wcześniejszej ogólnej deklaracji fabrycznej instalacji. Schemat modułu, oznaczenia wentylatora, prądy, przebieg i kierunek przepływu w miejscu pomiaru oraz połączenia pozostają do określenia. Docelowe sterowanie i pomiar temperatury płynu według SYS-043 i SYS-044. Przeanalizowano dostarczoną instrukcję użytkownika i suplement: [mapa obwodów, tabela osprzętu i brakujące dane](interfaces/beta-2015-analiza-dokumentacji.md). Suplement ma w treści oznaczenie MY14 i pokazuje TPS; zgodność jego schematu z motocyklem pozostaje niepotwierdzona.

Na zdjęciach właściciela rozpoznano [moduł zapłonowy Kokusan Denki CU7542](interfaces/beta-modul-zaplonowy-kokusan-cu7542.md) z boczną etykietą Beta 026400038 300 oraz [cewkę z oznaczeniami RC01 / IG5128 / 140822](interfaces/beta-cewka-zaplonowa-ig5128.md). Według właściciela we wtyczce starego modułu jest 8 przewodów; to informacja o osprzęcie referencyjnym. Parametry elektryczne cewki i synchronizacji pozostają do potwierdzenia. Nową wiązkę i złącze ECU projektujemy według SYS-045.

Beta służy do pierwszej integracji. Jej wyposażenie nie ogranicza docelowego zakresu PCB. Wymagania dotyczące gaźnika z TPS i bez TPS, 4T oraz TPI/TBI muszą być uwzględnione przed zamknięciem projektu sprzętu, również gdy nie można ich sprawdzić na tym motocyklu. Dla 2T obowiązują SYS-032 i SYS-033; konwersja TPI nie ma jeszcze potwierdzonej zgodności.

Weryfikację dzielimy na próby dostępne na Becie oraz próby stanowiskowe i późniejsze próby na innych jednostkach. Wynik na Becie nie potwierdza zgodności z pozostałymi wariantami. Właściciel dopuszcza późniejsze testy funkcji nieweryfikowalnych na dostępnym motocyklu; plan weryfikacji należy przygotować wraz z wymaganiami.

### Podstawy do dalszej analizy sprzętu

- KTM opisuje TPI MY2018 jako wtrysk z dwoma wtryskiwaczami w kanałach przepłukujących: [KTM — prezentacja TPI](https://press.ktm.com/News_Detail.aspx?id=49472&menueid=3050).
- KTM EXC MY2024 stosuje TBI oraz elektroniczne sterowanie zaworem wydechowym: [KTM — prezentacja EXC MY2024](https://press.ktm.com/news-challenge-accepted-the-2024-ktm-exc-range-is-here-to-redefine-limits?id=179901&l=uk&menueid=5904).

Są to przykłady do ustalenia zakresu, nie zatwierdzona lista wspieranych motocykli ani kompletna specyfikacja elektryczna. Do analizy: kanały wtrysku, zapłon, pompa paliwa, sterowanie zaworem wydechowym, czujniki i synchronizacja. Nie wybrano jeszcze liczby kanałów, sterowników wyjściowych ani szczegółowych interfejsów elektrycznych do osprzętu OEM.

## 8. Założenia kosztowe — ustalenie z 2026-10-18

Na tym etapie właściciel nie określa sztywnego limitu budżetu pierwszego kompletu prototypowego ECU + HMI. Kosztorys przygotujemy na podstawie projektu, obejmując komponenty, wykonanie PCB i montaż. Narzędzia oraz czas pracy są poza zakresem tego kosztorysu.

Przy doborze części i technologii uwzględniamy wymagane funkcje, dostępność oraz koszt. Szacunki należy powiązać z rewizją projektu, liczbą sztuk i datą pozyskania cen.

## 9. Narzędzia projektowe — ustalenie z 2026-10-18

Schematy i PCB ECU oraz HMI projektujemy w **Autodesk Fusion Electronics**. Właściciel korzysta z płatnej subskrypcji Autodesk Fusion. Wersję programu i zasady archiwizacji plików edytowalnych oraz bibliotek ustalimy przed rozpoczęciem projektu CAD.

Fusion Electronics wykorzystuje zintegrowaną technologię EAGLE: [informacja Autodesk](https://www.autodesk.com/support/technical/article/caas/sfdcarticles/sfdcarticles/Autodesk-EAGLE-Announcement-Next-steps-and-FAQ.html).

Dokumentacja projektu pozostaje w repozytorium. Archiwa projektów, biblioteki i eksporty produkcyjne należy powiązać z konkretną rewizją; sposób ich przygotowywania i formaty określimy w instrukcji pracy z CAD.
