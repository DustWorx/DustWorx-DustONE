# Budżet energii podczas postoju

Data: 2026-11-03. Status: cel zatwierdzony odpowiedzią A na pytanie 96; odpowiedź B na pytanie 97 określa rozruch kopniakiem dla wariantu z obiema metodami. Budżet liczbowy i procedury do opracowania. Wymaganie źródłowe: [SYS-093](../01-zakres-systemu.md); typy akumulatorów: [SYS-092 / ADR-010](../decisions/adr-010-akumulatory-agm-lifepo4.md).

## Cel i warunki

Minimum 4 tygodnie = 28 dni = 672 h postoju bez doładowania, z zachowaniem rezerwy na rozruch. Początek: sprawny i naładowany akumulator zgodny z projektem, ECU oraz HMI po prawidłowym uśpieniu. W czasie próby brak korzystania z motocykla i HMI; komputer odłączony.

Cel dotyczy uzgodnionych konfiguracji AGM i LiFePO4. Dla motocykla z rozrusznikiem i kopniakiem, jak Beta, właściciel wybrał rozruch kopniakiem: akumulator nadal zasila ECU i osprzęt potrzebny do uruchomienia. Kryterium dla konfiguracji bez kopniaka pozostaje otwarte. Minimalne pojemności, temperatury, kryterium sprawności/naładowania oraz liczba i dopuszczalny czas prób wymagają ustalenia. Obsługę po rzeczywistym ruchu koła lub przyciskach weryfikujemy odrębnie według wymagań wybudzania.

## Bilans do projektu

Pobór mierzymy od strony akumulatora dla ECU, HMI i wszystkich ich torów czuwania, w tym regulatorów, pomiarów, komunikacji i wykrywania wybudzenia. Uwzględniamy rzeczywiste stany oraz ewentualne okresowe zadania przewidziane w projekcie. Normalny sen zachowuje włączone wyjście zasilania HMI zgodnie z SYS-066.

Wstępny bilans ładunku, z prądem w A i ładunkiem w Ah:

`I_ECU_HMI_średni × 672 h + Q_inne + Q_samorozładowania + Q_rezerwa_rozruchu ≤ Q_dostępne_początkowo`

- `Q_dostępne_początkowo`: użyteczny ładunek zgodnej baterii przy uzgodnionej temperaturze i sprawności.
- `Q_inne`: zużycie pozostałych podłączonych obwodów motocykla, nieuwzględnionych w pomiarze ECU/HMI.
- `Q_samorozładowania`: utrata ładunku samego akumulatora przez okres próby; uwzględnić też pobór jego elektroniki, jeżeli występuje.
- `Q_rezerwa_rozruchu`: ładunek potrzebny ECU i niezbędnemu osprzętowi do rozruchu kopniakiem w wariancie z obiema metodami. Kryterium dla konfiguracji bez kopniaka ustalimy osobno; wartości zależą od warunków i badanego osprzętu.

Przykład samego rachunku: średnio 100 µA przez 672 h daje 67,2 mAh. Wartość docelowego limitu prądu pozostaje do wyliczenia. Sam bilans Ah wymaga uzupełnienia próbą rozruchu, bo o wyniku decyduje także zdolność oddania prądu przy wymaganym napięciu i temperaturze.

## Plan weryfikacji

| Etap | Zakres i dowód |
| --- | --- |
| Dane i analiza | Ustalić zgodne akumulatory, pojemności, stan początkowy, temperatury oraz kryteria próby kopniakiem. Uwzględnić pobór ECU, czujników, zapłonu i zastosowanego układu paliwowego. Wyliczyć budżet z rezerwą i przypisać go do bloków. Kryterium bez kopniaka wymaga osobnego uzgodnienia. |
| Uruchomienie sprzętu | Zmierzyć pobór całego ECU/HMI po prawidłowej sekwencji snu i w wymaganych wariantach napięcia/temperatury. Tor pomiarowy i rejestrator nie mogą dodatkowo zasilać ani wybudzać badanego systemu. |
| Próba długotrwała | Pozostawić kompletny zestaw przez co najmniej 28 dni bez doładowania i obsługi. Rejestrować warunki i zużycie metodą uzgodnioną dla stanowiska, zachowując normalne zasilanie HMI w śnie. |
| Rozruch po postoju | W wariancie z obiema metodami wykonać próbę kopniakiem bez uprzedniego doładowania; zapisać uruchomienie silnika, wybudzenie i przebieg zasilania ECU/osprzętu. Liczba/czas prób, temperatury i granice zostaną ustalone przed wykonaniem. |
| Pokrycie i regresja | Objąć AGM oraz LiFePO4, dopuszczone granice pojemności/temperatur i rzeczywisty osprzęt. Zmiany poboru sprzętu lub firmware ocenić względem budżetu i dobrać potrzebne powtórzenia. |

Procedury wykonawcze, przyrządy, połączenia, tolerancje i warunki przerwania przygotujemy według [zasad weryfikacji](../verification/README.md) po ustaleniu danych. Pomiar krótkotrwały i obliczenia wspierają próbę długotrwałą produktu. Nie wykonano pomiarów ani testów; nie potwierdzono jeszcze spełnienia celu.
