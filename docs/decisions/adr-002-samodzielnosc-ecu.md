# ADR-002 — samodzielność ECU i HMI jako klient

Data: 2026-10-25. Status: zatwierdzona zasada architektury; szczegóły realizacji otwarte.

## Problem i opcje

Utrata HMI lub CAN może oznaczać wyłączenie silnika albo pozostawienie sterowania w samodzielnym ECU. Należy ustalić właściciela danych i odpowiedzialność za wykonywanie żądań.

## Decyzja i podstawa zatwierdzenia

Właściciel projektu w odpowiedzi na pytanie 55 z 2026-10-25 wskazał, że ECU ma działać niezależnie od komunikacji z HMI, jest właścicielem danych, a HMI wysyła żądania odczytu lub polecenia, np. zmiany map. W odpowiedzi na pytanie 56 i późniejszym doprecyzowaniu tego samego dnia potwierdził, że przyciski obsługi HMI pozostają podłączone do HMI, natomiast START i STOP są od niego niezależne.

ECU samodzielnie steruje silnikiem i jego zabezpieczeniami, zarządza konfiguracją, mapami, diagnostyką oraz danymi eksploatacyjnymi motocykla. HMI jest klientem: prezentuje dane i przekazuje żądania użytkownika. ECU rozstrzyga wykonanie żądania i podaje rzeczywisty stan. Obecność HMI nie jest warunkiem pracy ECU; sama utrata HMI/CAN nie gasi silnika. Powiązania: [SYS-046 i SYS-047](../01-zakres-systemu.md).

## Konsekwencje

- Dane i pomiary wymagane do autonomicznego sterowania silnikiem oraz jego zabezpieczeń muszą być dostępne ECU bez udziału HMI. Uwzględnić to przy wyborze miejsca podłączenia czujników.
- Pracujące ECU korzysta z własnej konfiguracji i aktywnych map. Odczyt lub odświeżanie ekranu nie steruje cyklem pracy silnika.
- Przyciski obsługi HMI i zwykłe przełączniki akcesoriów pozostają podłączane do HMI według SYS-016. START ma osobne przewodowe wejście ECU (SYS-048), a STOP osobny obwód gaszenia (SYS-037). Oba działają bez HMI i komunikacji CAN ECU–HMI.
- Szczegóły trwałości poszczególnych danych, rozmieszczenia zasobów graficznych i pamięci podręcznej HMI pozostają do specyfikacji; ECU musi posiadać dane wymagane do samodzielnej pracy.

## Do określenia

Ważność i potwierdzanie żądań, wykrywanie utraty komunikacji, stany akcesoriów i rozrusznika, zachowanie przy ponownym połączeniu oraz ewentualne DTC komunikacyjne. Model odczytu/publikacji danych, czasy, formaty i szybkość CAN nie zostały wybrane.

## Proponowana weryfikacja

Próby stanowiskowe: ECU z HMI nieobecnym od włączenia zasilania; utrata połączenia i restart HMI podczas symulowanej pracy silnika; odczyt konfiguracji i aktywnej mapy po przywróceniu komunikacji. Kryterium SYS-046: sam brak HMI/CAN nie wyłącza sterowania ani lokalnych zabezpieczeń. Dla SYS-047 sprawdzić, że HMI odczytuje rzeczywisty stan ECU, a wykonanie żądania jest rozstrzygane w ECU. Sprawdzić obsługę START i STOP przy odłączonym lub wyłączonym HMI oraz przerwanej komunikacji ECU–HMI; zachować warunki rozruchu wynikające z konfiguracji ECU. Szczegółowe warunki i limity ustalić przed próbami. Nie wykonano jeszcze testów sprzętu ani firmware.
