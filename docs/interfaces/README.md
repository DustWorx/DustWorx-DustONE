# Interfejsy

Miejsce na definicje wspólne dla urządzeń i aplikacji:
- wejścia/wyjścia, złącza i pinout;
- komunikacja CAN ECU–HMI;
- połączenie z komputerem;
- konfiguracja, mapy, diagnostyka i aktualizacja;
- formaty danych i reguły zgodności wersji.

Stan: przygotowano [wstępną listę funkcji I/O](wstepna-lista-io.md), rozdzielając zakres ustalony i tory proponowane do analizy. Liczba kanałów, parametry i pinout pozostają otwarte. Magistrala CAN ECU–HMI jest wymaganiem; interfejs komputera oraz protokoły aplikacyjne pozostają otwarte.

Zasada ECU–HMI: ECU jest właścicielem danych i samodzielnie wykonuje sterowanie; HMI odczytuje dane i wysyła żądania. Brak HMI nie wyłącza silnika. Podstawa: [ADR-002](../decisions/adr-002-samodzielnosc-ecu.md), SYS-046/047. Model publikacji danych, formaty wiadomości, potwierdzenia żądań i zachowanie po ponownym połączeniu wymagają specyfikacji.

Specyfikacje i przyszłe pliki maszynowe, np. DBC lub schematy danych, przechowujemy razem w tym katalogu.

Opracowania referencyjne:

- [Moduł zapłonowy Kokusan CU7542 w Becie](beta-modul-zaplonowy-kokusan-cu7542.md): odczyty zdjęć, numer Beta 026400038 300 oraz dane do analizy zapłonu.
- [Cewka zapłonowa IG5128 w Becie](beta-cewka-zaplonowa-ig5128.md): odczyty zdjęcia, odniesienia katalogowe i parametry potrzebne do projektu stopnia zapłonowego.
- [Czujnik temperatury B57301K0103A001 w Becie](beta-czujnik-temperatury-b57301k0103a001.md): dane producenta i otwarte kwestie integracji własnego zestawu wentylatora właściciela.
- [Beta Racing 2015 - analiza przekazanej dokumentacji](beta-2015-analiza-dokumentacji.md): mapa obwodów, osprzęt, braki i obiekty do pomiarów. Suplement ma oznaczenie MY14; zgodność z egzemplarzem niepotwierdzona.
