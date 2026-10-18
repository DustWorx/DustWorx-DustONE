# DustWorx — zakres systemu ECU / HMI / aplikacja Windows

Status: punkt wyjścia do wymagań; zakres zapisany na podstawie opisu właściciela projektu. Propozycje i otwarte decyzje wymagają dalszego uzgodnienia.

## 1. Cel

Opracowanie systemu sterowania motocyklem obejmującego ECU, HMI na kierownicy oraz jedną aplikację Windows do konfiguracji, strojenia, personalizacji HMI, diagnostyki, aktualizacji i prac rozwojowych.

**Przeznaczenie potwierdzone przez właściciela:** wyłącznie sport i testy poza drogami publicznymi.

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
| SYS-008 | Aplikacja umożliwia dostosowanie wyglądu ekranu HMI. |
| SYS-009 | Aplikacja umożliwia diagnostykę ECU i HMI. |
| SYS-010 | Aplikacja umożliwia aktualizację oprogramowania ECU i HMI. |
| SYS-011 | Aplikacja zawiera narzędzia rozwojowe do testowania i debugowania ECU oraz komunikacji CAN. |
| SYS-012 | ECU obsługuje silniki z gaźnikiem oraz z wtryskiem paliwa. Rodzaje i parametry układów wtryskowych pozostają do ustalenia. |
| SYS-013 | ECU jest przeznaczone do instalacji motocykla z akumulatorem o napięciu nominalnym 12 V. Zakres napięć pracy i zachowanie podczas rozruchu pozostają do określenia. |
| SYS-014 | ECU obsługuje silniki z gaźnikiem bez TPS oraz z gaźnikiem z TPS (czujnikiem położenia przepustnicy). |
| SYS-015 | Wspólna PCB ECU zawiera sprzęt potrzebny do obsługi wariantów gaźnikowych oraz KTM TPI i TBI, bez przeróbek PCB ani wymiany obsady komponentów między tymi zastosowaniami. Konkretne modele, roczniki i granice parametrów elektrycznych pozostają do określenia przed zamknięciem projektu sprzętu. |
| SYS-016 | Przyciski i przełączniki kierownicy sterujące akcesoriami, np. światłami, kierunkowskazami i rozrusznikiem, są podłączone do HMI. HMI przekazuje polecenia do ECU przez CAN, a ECU steruje odbiornikami. |
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

## 3. Proponowany podział odpowiedzialności

- **ECU:** sterowanie silnikiem i akcesoriami, pomiary, wykrywanie usterek oraz reakcje na błędy. Sterowanie wymagające precyzyjnego czasu realizowane lokalnie w ECU.
- **HMI:** główny panel zastępujący fabryczny licznik: prezentacja prędkości, przebiegu, danych silnika i stanu motocykla; odczyt przycisków i przełączników kierownicy oraz przekazywanie poleceń do ECU przez CAN. Menu i ekrany obsługiwane fizycznymi przyciskami; ekran bez dotyku.
- **Aplikacja Windows:** wspólne środowisko z modułami konfiguracji, map, edycji HMI, diagnostyki, aktualizacji i narzędzi rozwojowych.

Propozycje do uwzględnienia w wymaganiach szczegółowych:

- Określić działanie ECU po utracie HMI, CAN lub połączenia z komputerem.
- Oddzielić konfigurację silnika, kalibrację map i projekt wyglądu HMI; określić ich wersje i zgodność z oprogramowaniem urządzeń.
- Ustalić warunki dopuszczające zapis map, zmianę typu silnika, aktualizację i testy wyjść.
- Zdefiniować ograniczenia narzędzi rozwojowych i sposób wejścia w tryb testowy.
- Zdefiniować odzyskiwanie urządzenia po przerwaniu aktualizacji.

### Wspólne połączenie z aplikacją Windows — ustalenie właściciela

Standardowa obsługa wymaga podłączenia jednego kabla w jednym punkcie. Aplikacja ma uzyskać dostęp do ECU i HMI przez to połączenie (SYS-026, SYS-027). Nie wybrano jeszcze interfejsu, rodzaju złącza, jego lokalizacji ani urządzenia pośredniczącego w komunikacji.

Przy projektowaniu aktualizacji określimy dostępność wspólnego połączenia podczas programowania każdego urządzenia oraz procedury odzyskiwania po przerwanej aktualizacji lub uszkodzeniu oprogramowania. Wymaganie jednego kabla dotyczy standardowej obsługi; architektura awaryjnego odzyskiwania i dostępu debuggera pozostaje do określenia.

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

### Polecenia z kierownicy i utrata komunikacji

Ustalony tor sterowania akcesoriami: przyciski i przełączniki → HMI → CAN → ECU → odbiorniki. Interfejsy wejściowe HMI muszą zostać dobrane do zachowywanych elementów obsługi kierownicy. Podłączenie zwykłych przełączników akcesoriów bezpośrednio do ECU nie jest wymagane w wybranym wariancie.

Do osobnej analizy pozostają: awaryjne gaszenie silnika, zachowanie przy awarii HMI lub CAN, aktualność i poprawność poleceń, stany wyjść po utracie komunikacji oraz warunki sterowania rozrusznikiem. Wybór toru CAN dla akcesoriów nie rozstrzyga architektury awaryjnego gaszenia ani sposobu reakcji na te awarie.

### Zasada integracji z motocyklem — ustalenie właściciela

Priorytetem jest zachowanie seryjnych czujników i osprzętu silnika w możliwie największym zakresie, o ile pozwala na to zgodność techniczna z ECU. Nie oznacza to potwierdzonej zgodności ze wszystkimi elementami OEM ani bezwzględnego zakazu ich wymiany. Ewentualne odstępstwa należy uzasadnić wynikami analizy.

Wiązka motocykla może być modyfikowana lub zaprojektowana od nowa, w tym przez zastosowanie adapterów i zmianę złączy. Samo dopasowanie wiązki nie stanowi potwierdzenia zgodności elektrycznej.

Dla wybranych modeli przed doborem interfejsów PCB należy zinwentaryzować i sprawdzić parametry czujników, cewek, wtryskiwaczy oraz pozostałych elementów wykonawczych. Wynik analizy ma wskazywać elementy zachowywane, potrzebne adaptacje i ewentualne wymiany wraz z uzasadnieniem.

### Pożądana funkcja: rozruch kopniakiem przy osłabionym akumulatorze

Intencja właściciela: umożliwić rozruch silnika kopniakiem, gdy podłączony akumulator 12 V nie wystarcza do użycia rozrusznika, ale nadal zasila elektronikę. Praca bez energii z akumulatora nie jest wymagana w ramach tej funkcji.

Status: funkcja pożądana, do analizy wykonalności i określenia mierzalnych kryteriów. Nie jest jeszcze gwarantowaną zdolnością systemu. Ocena ma objąć cały tor rozruchu: ECU, czujniki, zapłon oraz — przy wtrysku — układ paliwowy. Wariant gaźnikowy i wtryskowy należy ocenić oddzielnie.

Do ustalenia: minimalne napięcie i dostępny prąd pod obciążeniem, chemia i stan akumulatora, temperatura, obciążenia aktywne podczas rozruchu oraz warunki mechaniczne rozruchu. Nie przyjmujemy arbitralnego progu 12 V jako granicy działania rozrusznika. Napięcie spoczynkowe nie zastępuje oceny pod obciążeniem: [Yuasa — badanie akumulatora ołowiowego](https://www.yuasabatteries.com.au/resources/expert-advice/how-to-test-a-lead-acid-battery).

## 4. Decyzje potrzebne przed doborem sprzętu

| Obszar | Do ustalenia |
| --- | --- |
| Silnik | Pierwszy motocykl testowy: Beta 300 RR Racing / Race Edition, 2015, wskazany przez właściciela. Według właściciela gaźnik, zapłon i instalacja są fabryczne. Do potwierdzenia podczas inwentaryzacji: parametry i stan osprzętu. Do ustalenia: maksymalne obroty oraz reprezentatywne jednostki 4T, TPI i TBI. Obsługa gaźnika z TPS i bez TPS oraz TPI/TBI jest wymagana (SYS-012, SYS-014, SYS-015). |
| Zapłon | Typy obsługiwanych układów i cewek; wymagane interfejsy sterujące. |
| Synchronizacja | Czujniki wału i ewentualnie wałka, ich sygnały oraz układy znaczników. |
| Układ paliwowy | Rodzaj układu wtryskowego, liczba i parametry wtryskiwaczy, sterowanie pompą. |
| Instalacja | Akumulator nominalnie 12 V (SYS-013). Do określenia: zakres napięć, chemia akumulatora i warunki rozruchu. Pożądany rozruch kopniakiem z osłabionym, podłączonym akumulatorem; rozruch bez energii z akumulatora nie jest wymagany. |
| Akcesoria | Zakres rozszerzony według SYS-004. Do określenia: podział świateł przednich na funkcje, liczba niezależnych kanałów i wyjść konfigurowalnych, prądy robocze i rozruchowe, sterowanie bezpośrednie lub przez przekaźniki/styczniki, zabezpieczenia i diagnostyka wyjść. |
| Pomiary | Lista czujników, zakresy i wymagana dokładność. |
| HMI | Odczyt przełączników kierownicy i polecenia do ECU przez CAN (SYS-016); menu i ekrany obsługiwane fizycznymi przyciskami, ekran bez dotyku (SYS-017). Główny panel zastępujący licznik (SYS-018). Do ustalenia: ekran, liczba i rodzaje wejść przycisków, szczegółowy zakres i źródła danych, sposób zachowania przebiegu oraz zakres personalizacji. |
| Połączenie z PC | Połączenie przewodowe (SYS-026), jeden wspólny punkt i jeden kabel do standardowej obsługi ECU/HMI (SYS-027). Do ustalenia: interfejs fizyczny, lokalizacja złącza, realizacja dostępu do obu urządzeń i zasady aktualizacji/odzyskiwania. CAN między ECU i HMI nie przesądza interfejsu komputera. |
| Diagnostyka | Zapis DTC i powiązanych freeze frame w ECU; odczyt w aplikacji Windows i rozróżnienie usterek aktywnych oraz historycznych (SYS-019, SYS-020). Oznaczanie czasu według SYS-021. Trwałość historii i wygaszanie ostrzeżeń według SYS-022 i SYS-023. Pierwsze/ostatnie wystąpienie i licznik według SYS-024; eksport i ręczne kasowanie według SYS-025. Szczegóły rejestracji, obsługi pełnej pamięci i realizacji zegara do określenia. |
| Debugowanie | Rozróżnić podgląd danych, testy wyjść i analizę CAN od debugowania programu przez interfejs debuggera. |
| Warunki pracy | Zastosowanie ustalone: sport i testy poza drogami publicznymi. Do określenia: temperatura, woda, pył, drgania i miejsce montażu. |

## 5. Następny rezultat inżynierski

Po inwentaryzacji Bety 300 RR Racing 2015 i określeniu docelowych wariantów 4T, TPI i TBI oraz instalacji elektrycznej: opracować listę wejść/wyjść ECU, granice obsługiwanego sprzętu oraz architekturę blokową. Następnie ustalić mierzalne kryteria weryfikacji wymagań i plan prób. Dobór komponentów PCB następuje po zamknięciu tych danych.

## 6. Sposób realizacji i współpracy

Ustalenia właściciela projektu z 2026-10-15:

- Cały proces inżynierski prowadzimy wspólnie w rozmowie: organizację projektu, wymagania, funkcjonalność, architekturę, elektronikę, dobór każdego komponentu, schematy, projekt PCB, mechanikę oraz weryfikację.
- Firmware przygotowuje właściciel projektu z Codexem. Wspólna praca inżynierska obejmuje wymagania, interfejsy i kryteria weryfikacji potrzebne do jego implementacji.
- Pytania przedstawiamy pojedynczo, z przygotowanymi wariantami odpowiedzi. Gdy wybór wymaga danych technicznych lub porównania, przedstawiamy podstawy i konsekwencje przed decyzją.
- Ustalenia i wyniki prac zapisujemy w repozytorium DustWorx/DustWorx-DustONE zgodnie z jego strukturą.
- Obsługa gaźnika z TPS i bez TPS oraz KTM TPI/TBI została potwierdzona przez właściciela. Pierwszym motocyklem testowym jest jego Beta 300 RR Racing / Race Edition z 2015 r.; jednostki referencyjne 4T i konkretne generacje układów wtryskowych pozostają do ustalenia.

## 7. Motocykl referencyjny i zakres weryfikacji

**Potwierdzone przez właściciela:** dostępny jest cały motocykl Beta 300 RR Racing / Race Edition, rocznik 2015, przeznaczony do pierwszych testów. Wersję Racing / Race Edition wskazał właściciel. Według jego wiedzy gaźnik, układ zapłonowy i instalacja elektryczna są fabryczne. Jest to deklaracja właściciela; oznaczenia, parametry i zgodność ze stanem fabrycznym wymagają potwierdzenia podczas inwentaryzacji. Producent udostępnia instrukcje tej rodziny w [indeksie dokumentacji Beta](https://www.betamotor.com.au/support/off-road/); parametry konkretnego egzemplarza wymagają inwentaryzacji.

Beta służy do pierwszej integracji. Jej wyposażenie nie ogranicza docelowego zakresu PCB. Wymagania dotyczące gaźnika z TPS i bez TPS, 4T oraz TPI/TBI muszą być uwzględnione przed zamknięciem projektu sprzętu, również gdy nie można ich sprawdzić na tym motocyklu.

Weryfikację dzielimy na próby dostępne na Becie oraz próby stanowiskowe i późniejsze próby na innych jednostkach. Wynik na Becie nie potwierdza zgodności z pozostałymi wariantami. Właściciel dopuszcza późniejsze testy funkcji nieweryfikowalnych na dostępnym motocyklu; plan weryfikacji należy przygotować wraz z wymaganiami.

### Podstawy do dalszej analizy sprzętu

- KTM opisuje TPI MY2018 jako wtrysk z dwoma wtryskiwaczami w kanałach przepłukujących: [KTM — prezentacja TPI](https://press.ktm.com/News_Detail.aspx?id=49472&menueid=3050).
- KTM EXC MY2024 stosuje TBI oraz elektroniczne sterowanie zaworem wydechowym: [KTM — prezentacja EXC MY2024](https://press.ktm.com/news-challenge-accepted-the-2024-ktm-exc-range-is-here-to-redefine-limits?id=179901&l=uk&menueid=5904).

Są to przykłady do ustalenia zakresu, nie zatwierdzona lista wspieranych motocykli ani kompletna specyfikacja elektryczna. Do analizy: kanały wtrysku, zapłon, pompa paliwa, ewentualna pompa oleju, sterowanie zaworem wydechowym, czujniki i synchronizacja. Nie wybrano jeszcze liczby kanałów, sterowników wyjściowych ani szczegółowych interfejsów elektrycznych do osprzętu OEM.
