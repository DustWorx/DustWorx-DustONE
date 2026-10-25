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
| SYS-013 | ECU jest przeznaczone do instalacji motocykla z akumulatorem o napięciu nominalnym 12 V. Zakres napięć pracy i zachowanie podczas rozruchu pozostają do określenia. |
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
| SYS-028 | ECU przechowuje maksymalnie 3 zestawy map dla skonfigurowanego silnika. Użytkownik może przełączać aktywny zestaw z HMI także podczas pracy silnika. Warunki i sposób przełączenia wymagają określenia w specyfikacji sterowania. |
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
| SYS-050 | Przy nieprzerwanej pracy ECU utrata HMI lub komunikacji CAN ECU–HMI nie zmienia ostatniego stanu świateł przednich i tylnych pozycyjnych. Stan jest zachowywany do kolejnego przyjętego polecenia, z zachowaniem nadrzędnych zabezpieczeń wyjść. Wymaganie dotyczy bieżącej pracy ECU; stany po restarcie lub zaniku zasilania ECU pozostają do ustalenia. |
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
| SYS-063 | Po przyjęciu polecenia uśpienia HMI wysyła ECU aplikacyjną ramkę CAN potwierdzającą przyjęcie polecenia. Po zakończeniu wysyłania potwierdzenia HMI przestaje nadawać i przechodzi w sen. W normalnej sekwencji ECU usypia po uzyskaniu tego potwierdzenia i zakończeniu uzgodnionej fazy usypiania HMI, przy nadal spełnionych warunkach uśpienia. Czasy, identyfikacja bieżącej sekwencji i reakcja na brak potwierdzenia pozostają do określenia. |

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

### Smarowanie 2T — ustalenie właściciela z 2026-10-18

Sterowanie pompą dozującą olej 2T jest wyłączone z ECU. Montaż wymaga pracy silnika na mieszance przygotowanej w zbiorniku, a w motocyklach z dozownikiem — jego sprzętowego usunięcia i odpowiedniego przystosowania układu (SYS-032, SYS-033).

Zakres pompy został rozstrzygnięty. **Konfiguracja TPI po samej eliminacji pompy nie jest zatwierdzona do montażu.** Sposób konwersji i jej walidacja pozostają otwarte; nie wybrano zastępczego rozwiązania smarowania. Uzasadnienie i źródła: [ADR-001 — smarowanie 2T](decisions/adr-001-smarowanie-2t-mieszanka.md).

### Przepustnica — ustalenie właściciela z 2026-10-18

Przepustnica jest poruszana mechanicznie linką. ECU może odczytywać TPS; nie steruje napędem przepustnicy elektronicznej (SYS-038). Zakres obejmuje również gaźniki bez TPS (SYS-014). Parametry wejścia TPS, kalibrację i diagnostykę określimy przy projektowaniu interfejsów czujników. Zakres TPI/TBI według SYS-015 podlega temu ograniczeniu; nie oznacza obsługi ride-by-wire.

### Zestawy map silnika — ustalenie właściciela

ECU ma obsługiwać maksymalnie 3 zapisane zestawy map i wybór aktywnego zestawu podczas pracy silnika (SYS-028). Polecenie wyboru pochodzi z HMI i trafia do ECU przez CAN. Zestawy dotyczą zestrojenia aktualnej konfiguracji silnika.

Do określenia: zawartość zestawu dla poszczególnych wariantów silnika, walidacja zgodności i kompletności danych, warunki dopuszczenia przełączenia, spójny moment zastosowania nowych danych, ewentualny sposób przejścia, potwierdzenie aktywnego zestawu na HMI oraz wybór po ponownym uruchomieniu ECU. Warunki zapisu/edycji map z aplikacji Windows określimy oddzielnie.

### Wspólne połączenie z aplikacją Windows — ustalenie właściciela

Standardowa obsługa wymaga podłączenia jednego kabla w jednym punkcie. Aplikacja ma uzyskać dostęp do ECU i HMI przez to połączenie (SYS-026, SYS-027). Nie wybrano jeszcze interfejsu, rodzaju złącza, jego lokalizacji ani urządzenia pośredniczącego w komunikacji.

Przy projektowaniu aktualizacji określimy dostępność wspólnego połączenia podczas programowania każdego urządzenia oraz procedury odzyskiwania po przerwanej aktualizacji lub uszkodzeniu oprogramowania. Wymaganie jednego kabla dotyczy standardowej obsługi; architektura awaryjnego odzyskiwania i dostępu debuggera pozostaje do określenia.

### Wybudzanie i praca z komputerem — ustalenie właściciela z 2026-10-25

W odpowiedzi na pytanie 64 właściciel wybrał obsługę bez osobnego włącznika: START i kopniak wybudzają ECU, a przyciski HMI wybudzają HMI oraz ECU. Podłączenie komputera wybudza urządzenia i blokuje ich usypianie na czas połączenia, w tym pracy diagnostycznej i aktualizacji (SYS-054–057). Blokady nie ograniczamy wyłącznie do aktywnego przesyłania danych.

Po porównaniu wariantów w odpowiedzi na pytanie 65 właściciel wybrał zasilanie serwisowe z akumulatora lub zasilacza warsztatowego 12 V. Kabel PC służy do komunikacji i wybudzenia (SYS-058); wybrano wariant A z [porównania zasilania serwisowego](architecture/zasilanie-serwisowe-porownanie.md).

W odpowiedzi na pytanie 66 z 2026-10-25 właściciel potwierdził automatyczne wybudzanie również HMI od START i kopniaka, z priorytetem gotowości ECU do rozruchu (SYS-054). ECU nie czeka na uruchomienie HMI ani potwierdzenie komunikacji.

W odpowiedzi na pytanie 67 z 2026-10-25 właściciel wybrał automatyczne usypianie ECU i HMI po konfigurowalnym czasie bezczynności, przy zgaszonym silniku i odłączonym komputerze. Używanie przycisków rozpoczyna odliczanie od nowa; zadania wymagające dalszej pracy wstrzymują uśpienie (SYS-059).

W odpowiedzi na pytanie 70 z 2026-10-25 właściciel ustalił ECU jako koordynatora usypiania: HMI czeka na jego polecenie, potwierdza przyjęcie ramką CAN, kończy nadawanie i zasypia, po czym zasypia ECU (SYS-062/063). Próby rozruchu i aktywność użytkownika w HMI odnawiają bezczynność według SYS-059. Normalny przebieg i otwarte wyjątki: [sekwencja usypiania ECU–HMI](architecture/usypianie-ecu-hmi.md).

Podstawa architektury, źródła wybudzania i propozycje prób: [ADR-003 — wybudzanie bez osobnego włącznika](decisions/adr-003-wybudzanie-bez-wlacznika.md). Parametry czasu bezczynności, pozostałe blokady, pobór prądu w czuwaniu, parametry zasilania, czasy przejść i obsługa błędów sekwencji pozostają do projektu. Nie wybrano jeszcze komponentów ani torów wybudzania.

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

### Pożądana funkcja: rozruch kopniakiem przy osłabionym akumulatorze

Intencja właściciela: umożliwić rozruch silnika kopniakiem, gdy podłączony akumulator 12 V nie wystarcza do użycia rozrusznika, ale nadal zasila elektronikę. Praca bez energii z akumulatora nie jest wymagana w ramach tej funkcji.

Status: funkcja pożądana, do analizy wykonalności i określenia mierzalnych kryteriów. Nie jest jeszcze gwarantowaną zdolnością systemu. Ocena ma objąć cały tor rozruchu: ECU, czujniki, zapłon oraz — przy wtrysku — układ paliwowy. Wariant gaźnikowy i wtryskowy należy ocenić oddzielnie.

Do ustalenia: minimalne napięcie i dostępny prąd pod obciążeniem, chemia i stan akumulatora, temperatura, obciążenia aktywne podczas rozruchu oraz warunki mechaniczne rozruchu. Nie przyjmujemy arbitralnego progu 12 V jako granicy działania rozrusznika. Napięcie spoczynkowe nie zastępuje oceny pod obciążeniem: [Yuasa — badanie akumulatora ołowiowego](https://www.yuasabatteries.com.au/resources/expert-advice/how-to-test-a-lead-acid-battery).

## 4. Decyzje potrzebne przed doborem sprzętu

| Obszar | Do ustalenia |
| --- | --- |
| Silnik | Pierwszy motocykl testowy: Beta 300 RR Racing / Race Edition, 2015, wskazany przez właściciela. Według właściciela gaźnik, zapłon i instalacja są fabryczne. Do potwierdzenia podczas inwentaryzacji: parametry i stan osprzętu. Do ustalenia: maksymalne obroty oraz reprezentatywne jednostki 4T, TPI i TBI. Obsługa gaźnika z TPS i bez TPS oraz TPI/TBI według SYS-012, SYS-014 i SYS-015, z warunkami smarowania 2T według SYS-032 i SYS-033. |
| Zapłon | Typy obsługiwanych układów i cewek; wymagane interfejsy sterujące. |
| Przepustnica | Mechaniczna, poruszana linką; odczyt TPS zależnie od wyposażenia (SYS-038). Ride-by-wire poza zakresem. Do określenia: parametry, kalibracja i diagnostyka TPS. Gaźnik bez TPS obsługiwany według SYS-014. |
| Sprzęgło i położenie biegu | Opcjonalne wejścia do danych i wskazań według SYS-041, bez blokad rozrusznika zależnych od tych sygnałów; czujnik biegu ma rozróżniać poszczególne biegi, nie tylko luz. Stopka boczna poza zakresem. Do określenia: czujniki referencyjne, interfejsy, kalibracja, diagnostyka i szczegóły prezentacji danych. |
| Wykrywanie przewrócenia | Automatyczne wyłączenie silnika według SYS-039; ponowny rozruch po postawieniu motocykla bez cyklu zasilania według SYS-040. Do określenia: tor pomiarowy, lokalizacja, kryteria i czasy detekcji, sposób wyłączenia silnika, diagnostyka oraz szczegółowe warunki odblokowania. |
| Synchronizacja | Czujniki wału i ewentualnie wałka, ich sygnały oraz układy znaczników. |
| Układ paliwowy | Rodzaj układu wtryskowego, liczba i parametry wtryskiwaczy, sterowanie pompą paliwa. Dla 2T warunek pracy na mieszance według SYS-033; konwersja TPI wymaga osobnej oceny. |
| Smarowanie 2T | Pompa dozująca olej wyłączona z ECU (SYS-032). Montaż po przystosowaniu silnika do mieszanki (SYS-033); sposób i walidacja konwersji TPI pozostają otwarte. |
| Zawór wydechowy 2T | Sterowanie elektronicznym power valve wymagane według SYS-034. Do określenia: typ napędu i interfejs, parametry zasilania i sterowania, sygnały położenia, kalibracja, diagnostyka oraz zachowanie przy usterce. |
| Instalacja | Akumulator nominalnie 12 V (SYS-013). Do określenia: zakres napięć, chemia akumulatora i warunki rozruchu. Pożądany rozruch kopniakiem z osłabionym, podłączonym akumulatorem; rozruch bez energii z akumulatora nie jest wymagany. |
| Akcesoria | Zakres rozszerzony według SYS-004. Do określenia: podział świateł przednich na funkcje, liczba niezależnych kanałów i wyjść konfigurowalnych, prądy robocze i rozruchowe, sterowanie bezpośrednie lub przez przekaźniki/styczniki, zabezpieczenia i diagnostyka wyjść. |
| Pomiary | Dodatkowy zakres według SYS-029–SYS-031: ciśnienie atmosferyczne i temperatura na PCB, tor ciśnienia paliwa oraz wejście ciśnienia oleju 0/1. Temperatura dolotu pochodzi z IAT, temperatura PCB jest osobnym pomiarem ECU. Do określenia: parametry, czujniki, dokładność, zabezpieczenia, kalibracja i diagnostyka. EGT i lambda są pomiarami zewnętrznymi podczas strojenia. |
| HMI | Odczyt przełączników kierownicy i polecenia do ECU przez CAN (SYS-016); menu i ekrany obsługiwane fizycznymi przyciskami, ekran bez dotyku (SYS-017). Główny panel zastępujący licznik (SYS-018). Do ustalenia: ekran, liczba i rodzaje wejść przycisków, szczegółowy zakres danych prezentowanych z ECU, trwałość danych przebiegu i ograniczenia zasobów ekranów. Zakres personalizacji według SYS-008; do określenia edytor, format projektu ekranów oraz prezentacja ostrzeżeń w układach użytkownika. |
| Połączenie z PC | Połączenie przewodowe (SYS-026), jeden wspólny punkt i jeden kabel do standardowej obsługi ECU/HMI (SYS-027). Do ustalenia: interfejs fizyczny, lokalizacja złącza, realizacja dostępu do obu urządzeń i zasady aktualizacji/odzyskiwania. CAN między ECU i HMI nie przesądza interfejsu komputera. |
| Diagnostyka | Zapis DTC i powiązanych freeze frame w ECU; odczyt w aplikacji Windows i rozróżnienie usterek aktywnych oraz historycznych (SYS-019, SYS-020). Oznaczanie czasu według SYS-021. Trwałość historii i wygaszanie ostrzeżeń według SYS-022 i SYS-023. Pierwsze/ostatnie wystąpienie i licznik według SYS-024; eksport i ręczne kasowanie według SYS-025. Szczegóły rejestracji, obsługi pełnej pamięci i realizacji zegara do określenia. |
| Mapy silnika | Maksymalnie 3 zestawy map w ECU i przełączanie z HMI także podczas pracy silnika (SYS-028). Do określenia: zakres map, warunki i sposób przełączenia, walidacja zestawów oraz warunki ich zapisu. |
| Narzędzia rozwojowe | Zakres aplikacji ustalony według SYS-011; debugowanie kodu w osobnym środowisku. Do określenia: szczegóły testów wejść/wyjść, warunki dopuszczenia i przerwania testu, funkcje analizy CAN, format logów, przepustowość oraz sprzętowy dostęp debuggera. |
| Warunki pracy | Zastosowanie: sport i testy poza drogami publicznymi. Deszcz, błoto, zachlapania i chwilowe zanurzenie według SYS-036. Bezpośredni strumień myjki ciśnieniowej wyłączony z wymagań. Do określenia: parametry i kryteria prób wodnych, temperatura, pył, drgania i miejsce montażu. |
| Gabaryty i montaż ECU | Priorytet: maksymalna kompaktowość według SYS-035. Właściciel nie wskazał wymiarów ani wybranej obudowy. Do określenia: miejsce i dostępna przestrzeń montażowa, obrys PCB i obudowy, złącza, wyprowadzenie wiązki, mocowanie oraz bilans cieplny. |

## 5. Następny rezultat inżynierski

Przygotowano robocze materiały: [listę funkcji wejść/wyjść](interfaces/wstepna-lista-io.md), [macierz wariantów silnika](architecture/macierz-wariantow-silnika.md) i [plan inwentaryzacji Bety 300 RR Racing 2015](verification/beta-2015-plan-inwentaryzacji.md). Nie są one zatwierdzonym pinoutem ani potwierdzeniem zgodności sprzętu.

Najbliższy krok: inwentaryzacja Bety i określenie modeli referencyjnych pozostałych wariantów, następnie zamknięcie parametrów i liczby kanałów oraz opracowanie architektury blokowej. Wymagania szczegółowe mają otrzymać mierzalne kryteria weryfikacji i plan prób. Dobór komponentów PCB następuje po ustaleniu danych potrzebnych dla danego bloku.

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
