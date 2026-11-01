# Aplikacja Windows

Jedna aplikacja obsługująca ECU oraz HMI, z obszarami:
- konfiguracja urządzeń i wybór silnika 2T/4T;
- strojenie map i podgląd danych;
- personalizacja wyglądu HMI;
- diagnostyka i aktualizacje;
- narzędzia rozwojowe do testów ECU i analizy CAN.

Stan: brak implementacji. Technologia aplikacji i fizyczne połączenie z urządzeniami pozostają do ustalenia.

Całkowite motogodziny i ODO są udostępniane użytkownikowi końcowemu do odczytu, bez ustawiania, korekty lub kasowania, także w diagnostyce i development tool. Ochrona musi być egzekwowana przez ECU, a nie wyłącznie interfejs aplikacji. Odrębne uprawnienie producenta/serwisu obejmuje chronioną inicjalizację nowego ECU i przenoszenie udokumentowanych wartości, z rejestrem każdej operacji; szczegóły dostępu są otwarte. Zasady i otwarte decyzje: [chronione liczniki](../../docs/architecture/chronione-liczniki.md), SYS-074–077.
