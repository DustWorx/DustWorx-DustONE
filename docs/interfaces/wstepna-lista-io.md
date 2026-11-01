# Wstępna lista funkcji wejść i wyjść

Data: 2026-10-18. Status: materiał roboczy do architektury, bez zatwierdzonego pinoutu i liczby kanałów. Podstawa: [wymagania systemu](../01-zakres-systemu.md).

Wiersz oznacza funkcję, nie pojedynczy pin ani kanał. Kanałów nie sumujemy przed analizą jednoczesnej pracy, wariantów silnika i współdzielenia zasobów. „Opcjonalny czujnik” oznacza możliwość pracy bez niego, przy zachowaniu wymaganej obsługi sprzętowej na PCB.

Wiązkę i złącze ECU projektujemy od nowa (SYS-045), według potrzebnych funkcji, prądów i gabarytów. Pinout starego ECU nie jest ograniczeniem projektu. Potrzebne są parametry i połączenia zachowywanych czujników oraz odbiorników; dla zapłonu przygotowano [kartę cewki IG5128](beta-cewka-zaplonowa-ig5128.md).

## Funkcje wynikające z ustalonego zakresu

| Funkcja | Miejsce / kierunek | Podstawa | Dane potrzebne do projektu |
| --- | --- | --- | --- |
| Zasilanie HMI | Sterowane wyjście zasilania z ECU do HMI | SYS-064, 065, 066 | W normalnym śnie wyjście pozostaje włączone. Kontrolowane odłączenie jako ostateczność przy awarii lub zdefiniowanych ograniczeniach. Podtrzymanie stanu wyjścia podczas snu ECU, pobór toru w obu stanach, zabezpieczenia i wybudzanie przyciskami po odłączeniu do projektu. |
| Zapłon CDI i indukcyjny TCI/IDI | Jeden niezależnie sterowany kanał ECU; realizacja otwarta | SYS-001, 002, 015, 067, 068 | Cewki/moduły referencyjne i zgodność potwierdzana analizą/testami; sposób zasilania, energia, prądy, czasy i interfejs sterowania oraz granica integracji stopni mocy. Liczba pinów i elementów mocy nie wynika wprost z liczby kanałów. |
| Położenie/prędkość wału | Wejście ECU: czujnik VR albo Hall z wyjściem cyfrowym | SYS-001, 069 | Modele i interfejsy czujników, zasilanie, amplitudy, polaryzacja, progi, filtracja, układy znaczników i odniesienie do GMP; zakres od kopania/rozruchu do maksymalnych obrotów. Zgodność potwierdzana analizą i testami. |
| Faza cyklu silnika 4T | Dodatkowe wejście ECU; Hall z wyjściem cyfrowym | SYS-070 | Czujnik opcjonalny w konfiguracjach niewykorzystujących fazy. Modele, zasilanie, rodzaj wyjścia i podciąganie, poziomy, progi, filtracja, położenie znacznika względem wału/GMP i diagnostyka do ustalenia. VR nie jest obsługiwany na tym wejściu. |
| Wtrysk paliwa | Wyjścia ECU; aktywne w wariantach wtryskowych | SYS-012, 015 | Liczba wtryskiwaczy działających jednocześnie, typy, prądy, czasy i sposób sterowania. |
| Układ pompy paliwa | Sterowanie ECU; zakres toru mocy otwarty | SYS-012, 015 | Pompy referencyjne, prądy robocze/rozruchowe, sposób wyłączania i diagnostyka. |
| Elektroniczny zawór wydechowy 2T | Sterowanie ECU i ewentualne wejścia zwrotne | SYS-034 | Typ napędu, zasilanie, interfejs, zakres ruchu i sygnały położenia. |
| Regulacja powietrza biegu jałowego IAC | Wyjścia sterujące napędem krokowym; aktywne w odpowiednich konfiguracjach 4T | SYS-071 | Modele napędów, uzwojenia, prądy, zasilanie, zakres ruchu i kalibracja, liczba linii sterowania, stopień mocy, pozycja przy rozruchu/sen i diagnostyka do określenia. Konfiguracje bez IAC pracują bez napędu. |
| TPS | Wejście ECU; zależnie od wyposażenia | SYS-014, 038 | Typ sygnału, poziomy, zasilanie i kalibracja; obsługa wariantu bez TPS. |
| IAT | Wejście ECU | SYS-031 | Czujniki referencyjne, charakterystyki i sposób podłączenia. |
| Temperatura płynu chłodzącego | Wejście pomiarowe ECU; dane do HMI | SYS-044 | Czujniki OEM lub dodatkowe, charakterystyki, zakres, dokładność i montaż. Sam termowłącznik nie zapewnia pomiaru wartości. |
| Ciśnienie paliwa | Wejście pomiarowe ECU | SYS-029 | Zakres ciśnienia, sygnał, zasilanie i wymagana dokładność. |
| Czujnik rezerwy paliwa | Opcjonalny tor odczytu ECU; stan do HMI | SYS-073 | Zgodne modele, rodzaj sygnału, zasilanie/ewentualne pobudzenie, pomiar, filtracja i diagnostyka do określenia. Odróżnić stan rezerwy, usterkę i konfigurację bez czujnika; nie zakładać zwykłego wejścia 0/1 bez analizy czujnika. |
| Ciśnienie oleju obecne/brak | Wejście binarne ECU | SYS-029 | Polaryzacja, poziomy, czujnik/wyłącznik i diagnostyka przewodów. |
| Sprzęgło | Opcjonalny sygnał do ECU; dane i wskazania, bez blokady rozrusznika | SYS-041 | Rodzaj przełącznika/sygnału i parametry elektryczne. |
| Położenie poszczególnych biegów | Opcjonalny czujnik do ECU; dane i wskazania, bez blokady rozrusznika | SYS-041 | Typ interfejsu, liczba pozycji, sygnały i kalibracja. |
| Przednie i tylne światła pozycyjne | Wyjścia ECU; automatyka po uruchomieniu i zatrzymaniu silnika | SYS-004, 050, 081, 082, 083, 084 | Włączenie po uruchomieniu i przejściu z mijania/drogowych po zgaszeniu; wyłączenie przed prawidłowym snem oraz w oszczędzaniu przy niskim napięciu. Po wybudzeniu ze zgaszonym silnikiem oczekują na polecenie HMI. Kanały, odbiorniki, prądy, połączenia, progi i stan po resecie do określenia. |
| Światła mijania i drogowe | Wyjścia ECU; polecenia użytkownika z HMI | SYS-004, 016, 050, 081, 082, 083, 084 | Po zatrzymaniu silnika przejście na pozycyjne; przy zgaszonym silniku możliwe ponowne włączenie z HMI. Zwykłe ponowne ON w aktywnym odcięciu oszczędzania blokuje ECU (SYS-085), HMI przy zgaszonym silniku wskazuje wymagane uruchomienie (SYS-086). Lista odbiorników, progi i powrót do uzgodnienia. Podział kanałów, dozwolone kombinacje, prądy i połączenia wymagają specyfikacji. |
| Hamulec przedni | Osobne przewodowe wejście ECU | SYS-051 | Wyłącznik i jego interfejs, poziomy, polaryzacja, filtracja oraz diagnostyka. Działanie bez HMI/CAN. |
| Hamulec tylny | Osobne przewodowe wejście ECU | SYS-051 | Wyłącznik i jego interfejs, poziomy, polaryzacja, filtracja oraz diagnostyka. Odczyt rozróżniany od hamulca przedniego. |
| Światło hamowania | Wyjście ECU; załączane po użyciu któregokolwiek hamulca | SYS-004, 051 | Działanie bez HMI/CAN. Odbiornik, prąd, połączenia, zabezpieczenia i reakcje na usterki do określenia. |
| Kierunkowskazy | Wyjścia ECU; miganie realizowane lokalnie | SYS-004, 052 | Wyłączenie aktywnego kierunkowskazu po potwierdzeniu utraty komunikacji z HMI. Obwody, prądy, parametry migania, kryterium/czas utraty łączności i zachowanie po jej przywróceniu do określenia. |
| Klakson | Wyjście ECU | SYS-004 | Obwód, prąd, sposób sterowania i wymagania diagnostyczne. |
| Wentylator | Wyjście ECU; dodatkowe żądanie włączenia z HMI przez CAN | SYS-004, 043, 044, 053, 060, 061 | Po utracie HMI/CAN anulowanie ręcznego wymuszenia i sterowanie automatyczne. Po zgaszeniu wspólne limity czasu i napięcia dla automatyki oraz ręcznego wymuszenia. Parametry kanału, temperatury, czasy, napięcia i reakcje na usterki do określenia. |
| Nadzór napięcia akumulatora | Tor pomiarowy ECU; odcięcie wentylatora i oszczędzanie energii | SYS-060, 061, 084 | Bieżący nadzór napięcia podczas pracy ECU. Pomiar, progi, dokładność, filtracja, czasy potwierdzenia, histereza, uszkodzenia toru i profil akumulatora do określenia. Lista odbiorników trybu oszczędzania i priorytety wymagają uzgodnienia. |
| Dodatkowe wyjścia konfigurowalne | Wyjścia ECU | SYS-004 | Liczba, dopuszczalne obciążenia i funkcje. |
| Przycisk START | Osobne przewodowe wejście ECU; wybudzenie ECU i HMI z priorytetem ECU | SYS-048, 054 | Żądanie rozruchu podczas przytrzymywania; puszczenie kończy sterowanie rozrusznikiem. Rozruch niezależny od gotowości HMI. Tor wybudzania, sekwencja, czasy, poziomy, polaryzacja, filtracja i diagnostyka do określenia. |
| Rozrusznik | Wyjście ECU → tor wykonawczy | SYS-004, 048, 049 | Odcięcie po potwierdzeniu pracy silnika lub przekroczeniu czasu kręcenia; kolejna próba wymaga puszczenia i ponownego naciśnięcia START. Stycznik/przekaźnik, prąd, tor dużego prądu, metoda detekcji, limity i pozostałe warunki rozruchu do określenia. |
| Przyciski obsługi HMI i przełączniki akcesoriów | Wejścia HMI; przyciski obsługi wybudzają HMI i ECU | SYS-016, 017, 055 | Lista elementów i funkcji, styki, poziomy oraz przekazanie wybudzenia do ECU. Żądania akcesoriów po CAN; START i STOP mają osobne tory według SYS-048/037. |
| Ręczny STOP | Osobny obwód przewodowy, niezależny od HMI/CAN | SYS-037 | Sposób odcięcia, interfejs i reakcje na zwarcie/przerwę. |
| Wykrywanie przewrócenia | Lokalizacja i tor pomiarowy otwarte | SYS-039, 040 | Pomiar, montaż, kryteria, czasy reakcji i odblokowania. |
| Prędkość motocykla i naliczanie ODO | Obroty przedniego koła do ECU; detekcja wybudzania działająca w śnie | SYS-018, 075, 076, 079, 080 | Czujnik i jego sygnał, zasilanie, tor wejściowy, pobór w śnie, filtracja, obsługa pierwszych impulsów, kalibracja i dokładność do określenia. ODO działa również przy zgaszonym silniku, niezależnie od HMI. ECU wybudza także HMI, bez czekania na jego gotowość; tor i czasy przekazania wybudzenia pozostają do projektu. Uwzględnić ochronę parametrów i danych przed niekontrolowaną zmianą przez narzędzia. |
| Barometr i temperatura ECU | Pomiary na PCB ECU | SYS-030 | Zakres, dokładność, interfejsy wewnętrzne i obudowa; nie są zewnętrznymi wejściami czujników. |

Preferowany kierunek wyjść akcesoriów: [SmartFET-y na PCB](../architecture/wyjscia-akcesoriow-porownanie.md). Nie oznacza wyboru high-side/low-side dla wszystkich odbiorników ani potwierdzenia ich parametrów.

Pierwszy motocykl: według właściciela Beta Racing 2015 nie ma TPS. [Analiza przekazanych instrukcji](beta-2015-analiza-dokumentacji.md) zawiera mapę obwodów i odniesienia do osprzętu; suplement jest wewnętrznie oznaczony MY14 i nie potwierdza pinoutu tego egzemplarza. Opis CDI w instrukcji wymaga uwzględnienia przy analizie stopnia zapłonowego. Docelowy zakres PCB pozostaje bez zmian.

## Tory proponowane do analizy inżynierskiej

Poniższe pozycje nie są nowymi zatwierdzonymi wymaganiami właściciela.

| Tor | Cel analizy | Do określenia |
| --- | --- | --- |
| Faza cyklu 4T | Ocena potrzeby dodatkowego sygnału synchronizacji | Strategia sterowania i źródło fazy; nie zakładamy obowiązkowego czujnika wałka. |
| Inne zastosowania temperatury silnika | Ocena kompensacji i funkcji ochronnych poza uzgodnionym sterowaniem wentylatorem | Potrzebne funkcje i kryteria do ustalenia. Pomiar płynu i sterowanie wentylatorem są już wymagane według SYS-043/044. |
| Ciśnienia wymagane przez wybrane strategie wtrysku | Ustalenie kompletnego zestawu sygnałów | Potrzeba MAP/ciśnienia skrzyni korbowej i interfejsy dla konkretnych jednostek. |
| Pomiar wartości napięcia zasilania do dodatkowych zastosowań | Diagnostyka i kompensacja zależna od napięcia | Zakres, dokładność i częstotliwość do analizy; nadzór wymagany do odcięcia wentylatora ujęto wyżej jako funkcję potwierdzoną. |

## Zasilanie i komunikacja

- Akumulator nominalnie 12 V: zakres pracy, złącza zasilania, masy, ochrona i rezerwa energii do ustalenia (SYS-013). Obsługa bez osobnego włącznika; tory czuwania i wybudzania ECU oraz HMI według SYS-054/055 i [ADR-003](../decisions/adr-003-wybudzanie-bez-wlacznika.md).
- Kopniak: wymagane automatyczne wybudzenie ECU i HMI, z priorytetem gotowości ECU do rozruchu (SYS-054). Źródło detekcji, tory wybudzania i przekazania sygnału do HMI, sekwencja oraz czasy pozostają do projektu i weryfikacji.
- CAN ECU–HMI: interfejs wymagany; szybkość, przewody, terminacja i protokół otwarte (SYS-005). ECU pracuje bez HMI; dane konieczne do sterowania silnikiem i jego zabezpieczeń muszą być dostępne ECU bez udziału HMI (SYS-046/047, [ADR-002](../decisions/adr-002-samodzielnosc-ecu.md)).
- Jeden przewodowy punkt obsługi obu urządzeń: przy dostępnym zasilaniu 12 V podłączenie komputera wybudza ECU i HMI oraz blokuje usypianie obu urządzeń na czas połączenia (SYS-026, 027, 056, 057, 058). Serwis wymaga akumulatora lub odpowiedniego zasilacza warsztatowego. Interfejs, lokalizacja, detekcja podłączenia i parametry zasilania pozostają do określenia.
- Usypianie ECU i HMI: ECU po upływie bezczynności i zakończeniu zadań wydaje polecenie HMI, które potwierdza je ramką CAN, kończy nadawanie i zasypia; następnie zasypia ECU (SYS-059, 062, 063). Przyciski, próby rozruchu i rzeczywista aktywność użytkownika w HMI odnawiają czas. Formaty, czasy, sygnalizacja aktywności i wyjątki wymagają specyfikacji: [sekwencja ECU–HMI](../architecture/usypianie-ecu-hmi.md).
- Brak potwierdzenia HMI: ograniczone oczekiwanie/próby, awaryjne odłączenie części aktywnej z wyjścia zasilania ECU i dopuszczenie snu ECU (SYS-064/065). Tor wybudzania przyciskami musi działać także przy tym odłączeniu; szczegółowy sposób realizacji pozostaje do projektu.
- Dostęp debuggera i odzyskiwanie urządzeń: punkty serwisowe do określenia, niezależnie od standardowego kabla użytkownika.

Poza zakresem: dozownik oleju 2T, ride-by-wire, quickshifter, kontrola trakcji (SYS-072), wejście stopki bocznej oraz zintegrowane tory EGT/lambda. Ograniczenia i warunki smarowania 2T pozostają zgodne z wymaganiami systemu.
