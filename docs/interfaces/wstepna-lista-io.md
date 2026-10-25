# Wstępna lista funkcji wejść i wyjść

Data: 2026-10-18. Status: materiał roboczy do architektury, bez zatwierdzonego pinoutu i liczby kanałów. Podstawa: [wymagania systemu](../01-zakres-systemu.md).

Wiersz oznacza funkcję, nie pojedynczy pin ani kanał. Kanałów nie sumujemy przed analizą jednoczesnej pracy, wariantów silnika i współdzielenia zasobów. „Opcjonalny czujnik” oznacza możliwość pracy bez niego, przy zachowaniu wymaganej obsługi sprzętowej na PCB.

Wiązkę i złącze ECU projektujemy od nowa (SYS-045), według potrzebnych funkcji, prądów i gabarytów. Pinout starego ECU nie jest ograniczeniem projektu. Potrzebne są parametry i połączenia zachowywanych czujników oraz odbiorników; dla zapłonu przygotowano [kartę cewki IG5128](beta-cewka-zaplonowa-ig5128.md).

## Funkcje wynikające z ustalonego zakresu

| Funkcja | Miejsce / kierunek | Podstawa | Dane potrzebne do projektu |
| --- | --- | --- | --- |
| Zapłon | Wyjście ECU; realizacja otwarta | SYS-001, 002, 015 | Układy i cewki referencyjne, sposób zasilania, energia i interfejs sterowania. |
| Wtrysk paliwa | Wyjścia ECU; aktywne w wariantach wtryskowych | SYS-012, 015 | Liczba wtryskiwaczy działających jednocześnie, typy, prądy, czasy i sposób sterowania. |
| Układ pompy paliwa | Sterowanie ECU; zakres toru mocy otwarty | SYS-012, 015 | Pompy referencyjne, prądy robocze/rozruchowe, sposób wyłączania i diagnostyka. |
| Elektroniczny zawór wydechowy 2T | Sterowanie ECU i ewentualne wejścia zwrotne | SYS-034 | Typ napędu, zasilanie, interfejs, zakres ruchu i sygnały położenia. |
| TPS | Wejście ECU; zależnie od wyposażenia | SYS-014, 038 | Typ sygnału, poziomy, zasilanie i kalibracja; obsługa wariantu bez TPS. |
| IAT | Wejście ECU | SYS-031 | Czujniki referencyjne, charakterystyki i sposób podłączenia. |
| Temperatura płynu chłodzącego | Wejście pomiarowe ECU; dane do HMI | SYS-044 | Czujniki OEM lub dodatkowe, charakterystyki, zakres, dokładność i montaż. Sam termowłącznik nie zapewnia pomiaru wartości. |
| Ciśnienie paliwa | Wejście pomiarowe ECU | SYS-029 | Zakres ciśnienia, sygnał, zasilanie i wymagana dokładność. |
| Ciśnienie oleju obecne/brak | Wejście binarne ECU | SYS-029 | Polaryzacja, poziomy, czujnik/wyłącznik i diagnostyka przewodów. |
| Sprzęgło | Opcjonalny sygnał do ECU; dane i wskazania, bez blokady rozrusznika | SYS-041 | Rodzaj przełącznika/sygnału i parametry elektryczne. |
| Położenie poszczególnych biegów | Opcjonalny czujnik do ECU; dane i wskazania, bez blokady rozrusznika | SYS-041 | Typ interfejsu, liczba pozycji, sygnały i kalibracja. |
| Światła przednie i tylne pozycyjne | Wyjścia ECU | SYS-004, 050 | Po utracie HMI/CAN zachowanie ostatniego stanu przy działających zabezpieczeniach, w bieżącej sesji ECU. Podział funkcji i kanałów, odbiorniki, prądy, połączenia oraz stany po restarcie do określenia. |
| Hamulec przedni | Osobne przewodowe wejście ECU | SYS-051 | Wyłącznik i jego interfejs, poziomy, polaryzacja, filtracja oraz diagnostyka. Działanie bez HMI/CAN. |
| Hamulec tylny | Osobne przewodowe wejście ECU | SYS-051 | Wyłącznik i jego interfejs, poziomy, polaryzacja, filtracja oraz diagnostyka. Odczyt rozróżniany od hamulca przedniego. |
| Światło hamowania | Wyjście ECU; załączane po użyciu któregokolwiek hamulca | SYS-004, 051 | Działanie bez HMI/CAN. Odbiornik, prąd, połączenia, zabezpieczenia i reakcje na usterki do określenia. |
| Kierunkowskazy | Wyjścia ECU; miganie realizowane lokalnie | SYS-004, 052 | Wyłączenie aktywnego kierunkowskazu po potwierdzeniu utraty komunikacji z HMI. Obwody, prądy, parametry migania, kryterium/czas utraty łączności i zachowanie po jej przywróceniu do określenia. |
| Klakson | Wyjście ECU | SYS-004 | Obwód, prąd, sposób sterowania i wymagania diagnostyczne. |
| Wentylator | Wyjście ECU; dodatkowe żądanie włączenia z HMI przez CAN | SYS-004, 043, 044 | Automatyka według temperatury i wymuszenie włączenia; parametry kanału, progi/histereza i reakcje na usterki do określenia. |
| Dodatkowe wyjścia konfigurowalne | Wyjścia ECU | SYS-004 | Liczba, dopuszczalne obciążenia i funkcje. |
| Przycisk START | Osobne przewodowe wejście ECU, niezależne od HMI/CAN | SYS-048 | Żądanie rozruchu podczas przytrzymywania; puszczenie kończy sterowanie rozrusznikiem. Poziomy i polaryzacja, styki, filtracja, diagnostyka przewodów oraz limity i blokady do określenia. |
| Rozrusznik | Wyjście ECU → tor wykonawczy | SYS-004, 048, 049 | Odcięcie po potwierdzeniu pracy silnika lub przekroczeniu czasu kręcenia; kolejna próba wymaga puszczenia i ponownego naciśnięcia START. Stycznik/przekaźnik, prąd, tor dużego prądu, metoda detekcji, limity i pozostałe warunki rozruchu do określenia. |
| Przyciski obsługi HMI i przełączniki akcesoriów | Wejścia HMI; żądania sterowania akcesoriami do ECU po CAN | SYS-016, 017 | Lista elementów i funkcji, styki, wspólne przewody, poziomy. START i STOP mają osobne tory według SYS-048/037. |
| Ręczny STOP | Osobny obwód przewodowy, niezależny od HMI/CAN | SYS-037 | Sposób odcięcia, interfejs i reakcje na zwarcie/przerwę. |
| Wykrywanie przewrócenia | Lokalizacja i tor pomiarowy otwarte | SYS-039, 040 | Pomiar, montaż, kryteria, czasy reakcji i odblokowania. |
| Prędkość motocykla | Źródło i miejsce podłączenia otwarte | SYS-018 | Czujnik lub inne źródło, sygnał, kalibracja i wymagana dokładność. |
| Barometr i temperatura ECU | Pomiary na PCB ECU | SYS-030 | Zakres, dokładność, interfejsy wewnętrzne i obudowa; nie są zewnętrznymi wejściami czujników. |

Preferowany kierunek wyjść akcesoriów: [SmartFET-y na PCB](../architecture/wyjscia-akcesoriow-porownanie.md). Nie oznacza wyboru high-side/low-side dla wszystkich odbiorników ani potwierdzenia ich parametrów.

Pierwszy motocykl: według właściciela Beta Racing 2015 nie ma TPS. [Analiza przekazanych instrukcji](beta-2015-analiza-dokumentacji.md) zawiera mapę obwodów i odniesienia do osprzętu; suplement jest wewnętrznie oznaczony MY14 i nie potwierdza pinoutu tego egzemplarza. Opis CDI w instrukcji wymaga uwzględnienia przy analizie stopnia zapłonowego. Docelowy zakres PCB pozostaje bez zmian.

## Tory proponowane do analizy inżynierskiej

Poniższe pozycje nie są nowymi zatwierdzonymi wymaganiami właściciela.

| Tor | Cel analizy | Do określenia |
| --- | --- | --- |
| Położenie/prędkość wału | Podstawa synchronizacji zapłonu i wtrysku | Układy znaczników, typy czujników, amplitudy, polaryzacja, zakres obrotów. |
| Faza cyklu 4T | Ocena potrzeby dodatkowego sygnału synchronizacji | Strategia sterowania i źródło fazy; nie zakładamy obowiązkowego czujnika wałka. |
| Inne zastosowania temperatury silnika | Ocena kompensacji i funkcji ochronnych poza uzgodnionym sterowaniem wentylatorem | Potrzebne funkcje i kryteria do ustalenia. Pomiar płynu i sterowanie wentylatorem są już wymagane według SYS-043/044. |
| Ciśnienia wymagane przez wybrane strategie wtrysku | Ustalenie kompletnego zestawu sygnałów | Potrzeba MAP/ciśnienia skrzyni korbowej i interfejsy dla konkretnych jednostek. |
| Napięcie zasilania | Diagnostyka i kompensacja zależna od napięcia | Punkt pomiaru, zakres, dokładność i częstotliwość. |

## Zasilanie i komunikacja

- Akumulator nominalnie 12 V: zakres pracy, złącza zasilania, masy, ochrona i rezerwa energii do ustalenia (SYS-013). HMI również wymaga określenia zasilania i stanów uśpienia.
- CAN ECU–HMI: interfejs wymagany; szybkość, przewody, terminacja i protokół otwarte (SYS-005). ECU pracuje bez HMI; dane konieczne do sterowania silnikiem i jego zabezpieczeń muszą być dostępne ECU bez udziału HMI (SYS-046/047, [ADR-002](../decisions/adr-002-samodzielnosc-ecu.md)).
- Jeden przewodowy punkt obsługi obu urządzeń: interfejs i lokalizacja otwarte (SYS-026, 027).
- Dostęp debuggera i odzyskiwanie urządzeń: punkty serwisowe do określenia, niezależnie od standardowego kabla użytkownika.

Poza zakresem: dozownik oleju 2T, ride-by-wire, quickshifter, wejście stopki bocznej oraz zintegrowane tory EGT/lambda. Ograniczenia i warunki smarowania 2T pozostają zgodne z wymaganiami systemu.
