# DustWorx — zakres systemu ECU / HMI / aplikacja Windows

Status: punkt wyjścia do wymagań; zakres zapisany na podstawie opisu właściciela projektu. Propozycje i otwarte decyzje wymagają dalszego uzgodnienia.

## 1. Cel

Opracowanie systemu sterowania motocyklem obejmującego ECU, HMI na kierownicy oraz jedną aplikację Windows do konfiguracji, strojenia, personalizacji HMI, diagnostyki, aktualizacji i prac rozwojowych.

## 2. Wymagania wynikające z opisu

| ID | Wymaganie |
| --- | --- |
| SYS-001 | ECU steruje pracą silnika jednocylindrowego. |
| SYS-002 | Ten sam wariant sprzętowy ECU obsługuje silniki dwusuwowe i czterosuwowe bez zmian na PCB. |
| SYS-003 | Wybór silnika 2T lub 4T jest dostępny przez konfigurację w aplikacji Windows. |
| SYS-004 | ECU steruje akcesoriami motocykla, w tym światłami, wentylatorem i rozrusznikiem; sposób podłączenia obciążeń pozostaje do ustalenia. |
| SYS-005 | ECU komunikuje się z HMI na kierownicy przez CAN. |
| SYS-006 | Jedna aplikacja Windows obsługuje ECU oraz HMI. |
| SYS-007 | Aplikacja umożliwia konfigurację ECU i strojenie silnika za pomocą map. |
| SYS-008 | Aplikacja umożliwia dostosowanie wyglądu ekranu HMI. |
| SYS-009 | Aplikacja umożliwia diagnostykę ECU i HMI. |
| SYS-010 | Aplikacja umożliwia aktualizację oprogramowania ECU i HMI. |
| SYS-011 | Aplikacja zawiera narzędzia rozwojowe do testowania i debugowania ECU oraz komunikacji CAN. |

## 3. Proponowany podział odpowiedzialności

- **ECU:** sterowanie silnikiem i akcesoriami, pomiary, wykrywanie usterek oraz reakcje na błędy. Sterowanie wymagające precyzyjnego czasu realizowane lokalnie w ECU.
- **HMI:** prezentacja informacji oraz obsługa poleceń kierowcy przesyłanych do ECU. Zakres poleceń do ustalenia.
- **Aplikacja Windows:** wspólne środowisko z modułami konfiguracji, map, edycji HMI, diagnostyki, aktualizacji i narzędzi rozwojowych.

Propozycje do uwzględnienia w wymaganiach szczegółowych:

- Określić działanie ECU po utracie HMI, CAN lub połączenia z komputerem.
- Oddzielić konfigurację silnika, kalibrację map i projekt wyglądu HMI; określić ich wersje i zgodność z oprogramowaniem urządzeń.
- Ustalić warunki dopuszczające zapis map, zmianę typu silnika, aktualizację i testy wyjść.
- Zdefiniować ograniczenia narzędzi rozwojowych i sposób wejścia w tryb testowy.
- Zdefiniować odzyskiwanie urządzenia po przerwaniu aktualizacji.

## 4. Decyzje potrzebne przed doborem sprzętu

| Obszar | Do ustalenia |
| --- | --- |
| Silnik | Modele referencyjne, maksymalne obroty, zasilanie paliwem: gaźnik lub wtrysk. |
| Zapłon | Typy obsługiwanych układów i cewek; wymagane interfejsy sterujące. |
| Synchronizacja | Czujniki wału i ewentualnie wałka, ich sygnały oraz układy znaczników. |
| Układ paliwowy | Jeżeli występuje wtrysk: liczba i parametry wtryskiwaczy, sterowanie pompą. |
| Instalacja | Napięcie nominalne, akumulator lub praca bez akumulatora, warunki zasilania podczas rozruchu. |
| Akcesoria | Pełna lista odbiorników, prądy robocze i rozruchowe, sterowanie bezpośrednie lub przez przekaźniki/styczniki. |
| Pomiary | Lista czujników, zakresy i wymagana dokładność. |
| HMI | Ekran, sposób obsługi, prezentowane dane i zakres personalizacji. |
| Połączenie z PC | Sposób fizycznego podłączenia do ECU/HMI; CAN między urządzeniami nie przesądza interfejsu komputera. |
| Debugowanie | Rozróżnić podgląd danych, testy wyjść i analizę CAN od debugowania programu przez interfejs debuggera. |
| Warunki pracy | Temperatura, woda, pył, drgania, miejsce montażu oraz docelowe zastosowanie motocykla. |

## 5. Następny rezultat inżynierski

Po określeniu silników referencyjnych i instalacji elektrycznej: opracować listę wejść/wyjść ECU, granice obsługiwanego sprzętu oraz architekturę blokową. Następnie ustalić mierzalne kryteria weryfikacji wymagań i plan prób. Dobór komponentów PCB następuje po zamknięciu tych danych.
