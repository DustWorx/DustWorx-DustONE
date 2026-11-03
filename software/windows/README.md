# Aplikacja Windows

Jedna aplikacja obsługująca ECU oraz HMI, z obszarami:
- konfiguracja urządzeń i wybór silnika 2T/4T;
- strojenie map i podgląd danych;
- personalizacja wyglądu HMI;
- diagnostyka i aktualizacje;
- narzędzia rozwojowe do testów ECU i analizy CAN.

Stan: brak implementacji. Technologia aplikacji i fizyczne połączenie z urządzeniami pozostają do ustalenia.

Całkowite motogodziny i ODO są udostępniane użytkownikowi końcowemu do odczytu, bez ustawiania, korekty lub kasowania, także w diagnostyce i development tool. Ochrona musi być egzekwowana przez ECU, a nie wyłącznie interfejs aplikacji. Odrębne uprawnienie producenta/serwisu obejmuje chronioną inicjalizację nowego ECU i przenoszenie udokumentowanych wartości, z rejestrem każdej operacji; szczegóły dostępu są otwarte. Zasady i otwarte decyzje: [chronione liczniki](../../docs/architecture/chronione-liczniki.md), SYS-074–077.

Aktualizacja ECU w trybie użytkowym ma dopuszczać wyłącznie firmware zatwierdzony przez producenta projektu ([SYS-078 i ADR-008](../../docs/decisions/adr-008-dostep-do-firmware-ecu.md)). Sama kontrola pliku przez aplikację nie zastępuje egzekwowania polityki w ECU. Dostęp rozwojowy twórców do programowania i debugowania pozostaje wymagany; szczegóły autoryzacji są otwarte. Decyzja nie określa jeszcze polityki firmware HMI.

Testy odbiorników: jawnie wybierany tryb serwisowy umożliwia zwolnienie odcięcia oszczędzania bez uruchamiania silnika przy potwierdzonym stabilnym zasilaniu warsztatowym (SYS-090). Samo połączenie PC nie odblokowuje odbiorników. Aplikacja przedstawia wynik dopuszczenia przez ECU; zwolnienie odcięcia nie uruchamia testu samo. Zabezpieczenia wyjść pozostają aktywne. SYS-091: po potwierdzonej utracie sesji ECU nie przyjmuje nowych testów, a rozpoczęty może dokończyć do pierwotnego limitu; następnie wyjątek jest wycofywany. Aplikacja nie może samym ponowieniem/odtworzeniem połączenia wydłużać testu ani uruchamiać następnego w fazie dokańczania. Uprawnienia, detekcja sesji i dokładne stany końcowe do projektu: [analiza i plan prób](../../docs/architecture/oszczedzanie-energii.md).

Konfiguracja zasilania uwzględnia osobne profile ochrony AGM/LiFePO4 według SYS-092. Dane i egzekwowanie profilu należą do ECU; wybór, uprawnienia, zapis i warunki zmiany doprecyzujemy w projekcie interfejsu. [Zakres i otwarte szczegóły](../../docs/decisions/adr-010-akumulatory-agm-lifepo4.md).

Strojenie na żywo jest przyjęte w SYS-094: wybrane wartości map można zmieniać podczas pracy silnika. ECU rozstrzyga zastosowanie, a aplikacja ma odzwierciedlać rzeczywisty stan; zakres, walidacja i utrwalanie pozostają do specyfikacji: [ADR-011](../../docs/decisions/adr-011-strojenie-na-zywo.md).
