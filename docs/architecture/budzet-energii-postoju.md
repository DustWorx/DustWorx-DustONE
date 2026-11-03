# Budżet energii podczas postoju

Data: 2026-11-03. Status: cel zatwierdzony odpowiedzią A na pytanie 96; odpowiedź B na pytanie 97 określa kopniak dla wariantu z obiema metodami, a A na pytanie 98 — rozruch elektryczny dla wariantu bez kopniaka. Odpowiedź A na pytanie 99 ustala otoczenie od −10°C do +40°C dla postoju i późniejszego rozruchu. Budżet liczbowy i procedury do opracowania. Wymaganie źródłowe: [SYS-093](../01-zakres-systemu.md); typy akumulatorów: [SYS-092 / ADR-010](../decisions/adr-010-akumulatory-agm-lifepo4.md).

## Cel i warunki

Minimum 4 tygodnie = 28 dni = 672 h postoju bez doładowania, z zachowaniem rezerwy na rozruch. Temperatura otoczenia podczas postoju i późniejszego rozruchu: od −10°C do +40°C (odpowiedź A na pytanie 99). Początek: sprawny i naładowany akumulator zgodny z projektem, ECU oraz HMI po prawidłowym uśpieniu. W czasie próby brak korzystania z motocykla i HMI; komputer odłączony.

Cel dotyczy uzgodnionych konfiguracji AGM i LiFePO4. Dla motocykla z rozrusznikiem i kopniakiem, jak Beta, właściciel wybrał rozruch kopniakiem: akumulator nadal zasila ECU i osprzęt potrzebny do uruchomienia. Dla motocykla wyposażonego wyłącznie w rozrusznik elektryczny wymagany jest rozruch elektryczny po tym samym czasie postoju (odpowiedź A na pytanie 98). Minimalne pojemności, kryterium sprawności/naładowania oraz liczba i dopuszczalny czas prób wymagają ustalenia. Zakres pracy elektroniki podczas jazdy określimy odrębnie. Obsługę po rzeczywistym ruchu koła lub przyciskach weryfikujemy odrębnie według wymagań wybudzania.

## Dane do wyboru minimalnych pojemności

[Instrukcja producenta KTM 2009, 3211353en — kopia u dystrybutora](https://dirtypart.com/dirtypart_files/Manualer/KTM/KTM%20125%20EXC%202-takt%202009%20Manual%20UK.pdf), tabela podwozia 250/300 XC/XC-W/EXC/EXC Six Days na s. 55 PDF, podaje dla wersji z rozrusznikiem akumulator 12 V, 3 Ah. Przykładowy [AGM Yuasa YTX4L-BS](https://www.yuasa.com/uk/ytx4l-bs) ma 3 Ah przy rozładowaniu 10-godzinnym (3,2 Ah przy 20-godzinnym). [Beta USA — BSLi-02](https://betausa.com/bs-heavy-duty-lithium-battery/) podaje LiFePO4 2 Ah przy 10 godzinach.

To referencje dokumentowe do rozważenia minimalnych pojemności 3 Ah AGM / 2 Ah LiFePO4 dla celu postoju. Granice pojemności i konkretne modele pozostają do decyzji i kwalifikacji; dane nominalne nie potwierdzają jeszcze spełnienia 4 tygodni oraz rozruchu w całym przyjętym zakresie temperatur.

## Bilans do projektu

Pobór mierzymy od strony akumulatora dla ECU, HMI i wszystkich ich torów czuwania, w tym regulatorów, pomiarów, komunikacji i wykrywania wybudzenia. Uwzględniamy rzeczywiste stany oraz ewentualne okresowe zadania przewidziane w projekcie. Normalny sen zachowuje włączone wyjście zasilania HMI zgodnie z SYS-066.

Wstępny bilans ładunku, z prądem w A i ładunkiem w Ah:

`I_ECU_HMI_średni × 672 h + Q_inne + Q_samorozładowania + Q_rezerwa_rozruchu ≤ Q_dostępne_początkowo`

- `Q_dostępne_początkowo`: użyteczny ładunek zgodnej baterii przy uzgodnionej sprawności i temperaturach wynikających z zakresu otoczenia −10°C…+40°C.
- `Q_inne`: zużycie pozostałych podłączonych obwodów motocykla, nieuwzględnionych w pomiarze ECU/HMI.
- `Q_samorozładowania`: utrata ładunku samego akumulatora przez okres próby; uwzględnić też pobór jego elektroniki, jeżeli występuje.
- `Q_rezerwa_rozruchu`: ładunek potrzebny ECU i niezbędnemu osprzętowi do uruchomienia; dla wariantu wyłącznie z rozrusznikiem elektrycznym obejmuje także jego pobór. Wartości zależą od warunków, metody i badanego silnika/osprzętu.

Przykład samego rachunku: średnio 100 µA przez 672 h daje 67,2 mAh. Wartość docelowego limitu prądu pozostaje do wyliczenia. Sam bilans Ah wymaga uzupełnienia próbą rozruchu, bo o wyniku decyduje także zdolność oddania prądu przy wymaganym napięciu i temperaturze.

## Plan weryfikacji

| Etap | Zakres i dowód |
| --- | --- |
| Dane i analiza | Ustalić zgodne akumulatory, pojemności, stan początkowy i szczegóły prób obu metod przy otoczeniu −10°C…+40°C. Uwzględnić ECU, czujniki, zapłon i zastosowany układ paliwowy oraz pobór rozrusznika w wariancie bez kopniaka. Wyliczyć budżet z rezerwą i przypisać go do bloków. |
| Uruchomienie sprzętu | Zmierzyć pobór całego ECU/HMI po prawidłowej sekwencji snu i w wymaganych wariantach napięcia/temperatury. Tor pomiarowy i rejestrator nie mogą dodatkowo zasilać ani wybudzać badanego systemu. |
| Próba długotrwała | Pozostawić kompletny zestaw przez co najmniej 28 dni bez doładowania i obsługi, dla przypadków wynikających z otoczenia −10°C…+40°C. Rejestrować warunki i zużycie metodą uzgodnioną dla stanowiska, zachowując normalne zasilanie HMI w śnie. |
| Rozruch po postoju | Bez uprzedniego doładowania wykonać próbę kopniakiem w wariancie z obiema metodami, a rozrusznikiem w wariancie wyłącznie elektrycznym. Zapisać uruchomienie silnika, wybudzenie i przebieg zasilania ECU/osprzętu; dla elektrycznego także obciążenie rozrusznikiem i spadki napięcia. Liczba/czas prób, stabilizacja cieplna, tolerancje i granice pomiarowe do ustalenia przed wykonaniem. |
| Pokrycie i regresja | Objąć AGM oraz LiFePO4, obie wymagane metody rozruchu, dopuszczone granice pojemności/temperatur i osprzęt właściwy badanemu silnikowi. Zmiany poboru sprzętu lub firmware ocenić względem budżetu i dobrać potrzebne powtórzenia. |

Przypadki analizy i prób mają uwzględnić temperaturę w czasie postoju oraz temperaturę późniejszego rozruchu. Przejścia i stabilizację cieplną akumulatora/urządzeń oraz tolerancje doprecyzujemy w procedurach. Zakres otoczenia jest celem do potwierdzenia dla zgodnych konfiguracji, a nie potwierdzonym parametrem dowolnego akumulatora. Przed próbą potwierdzić w dokumentacji konkretnej baterii i regulatora dopuszczalność rozruchu oraz następującego po nim ładowania w danej temperaturze.

Procedury wykonawcze, przyrządy, połączenia, tolerancje i warunki przerwania przygotujemy według [zasad weryfikacji](../verification/README.md) po ustaleniu danych. Pomiar krótkotrwały i obliczenia wspierają próbę długotrwałą produktu. Nie wykonano pomiarów ani testów; nie potwierdzono jeszcze spełnienia celu.
