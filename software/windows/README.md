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

Strojenie na żywo wybranych wartości jest przyjęte w SYS-094. ECU rozstrzyga zastosowanie i zachowuje ostatnio zastosowane wartości po utracie Windows, bez automatycznego trwałego zapisu. Aplikacja odzwierciedla rzeczywiste dane ECU; uzgodnienie po ponownym połączeniu i pozostałe reguły są do projektu: [ADR-011](../../docs/decisions/adr-011-strojenie-na-zywo.md).

Edytor obsługuje maks. trzy niezależne, kompletne zestawy uzgodnionych map jednej konfiguracji silnika (SYS-028). Reguły operacji rozwijamy w [specyfikacji map](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-095: trwały zapis zmian map wymaga wyraźnego polecenia użytkownika i zgaszonego silnika. ECU rozstrzyga dopuszczenie; samo zastosowanie zmian na żywo nie utrwala ich automatycznie. [Specyfikacja F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-102: krytyczną konfigurację można przygotować lokalnie podczas pracy silnika, ale transfer do ECU i wdrożenie wymagają jego zgaszenia oraz wyraźnego polecenia. ECU egzekwuje warunki i blokuje rozrusznik, zapłon i wtrysk przez całą operację. Dopuszczone strojenie wartości map na żywo pozostaje dostępne. Szczegóły: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-103: po utracie Windows w nieukończonym transferze krytycznej konfiguracji, przed wdrożeniem, ECU samodzielnie anuluje transfer i zwalnia jego blokady przy poprawnej, nienaruszonej dotychczasowej konfiguracji. Rozruch wymaga nowej świadomej próby. Szczegóły: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-104: po odebraniu kompletu danych i przyjęciu wyraźnego polecenia wdrożenia ECU przy prawidłowym zasilaniu kończy sprawdzanie/wdrożenie samodzielnie mimo utraty Windows. Po potwierdzonym powodzeniu zwalnia blokady bez oczekiwania na powrót aplikacji; rozruch wymaga nowej świadomej próby. Błędy podlegają SYS-105, a powrót po zaniku zasilania SYS-106. Szczegóły: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-105: po błędzie sprawdzania/wdrażania ECU automatycznie wraca do poprzedniej potwierdzonej poprawnej konfiguracji i zwalnia blokady operacji bez oczekiwania na potwierdzenie z Windows. Rozruch wymaga nowej świadomej próby. Bez poprawnych danych blokady pozostają, a aplikacja zachowuje dostęp do naprawy konfiguracji. Szczegóły: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-106: po zaniku zasilania podczas zmiany krytycznej konfiguracji ECU odtwarza wyłącznie kompletną i poprawną nową konfigurację po trwałym potwierdzeniu wdrożenia przez ECU, inaczej poprzednią poprawną. Po sprawdzeniu dopuszcza nową świadomą próbę rozruchu bez połączenia lub potwierdzenia Windows. Bez poprawnych danych pozostają blokady i dostęp do naprawy konfiguracji. Szczegóły: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-107: przesłanie i robocze zastąpienie pełnego zestawu map w ECU wymaga zgaszonego silnika, w ramach tej samej konfiguracji silnika. Przygotowanie pliku lokalnie jest odrębną czynnością. Podczas pracy pozostaje edycja dopuszczonych wybranych wartości aktywnego i nieaktywnych zestawów. Brak automatycznego trwałego zapisu; obowiązuje SYS-095. Szczegóły: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-108: aplikacja może zażądać trwałego zapisu wybranego kompletnego zestawu, aktywnego lub nieaktywnego, bez utrwalania roboczych zmian pozostałych, albo wszystkich skonfigurowanych zestawów jednym poleceniem. Obowiązują zgaszony silnik i wyraźne polecenie użytkownika według SYS-095. Po zaniku zasilania ECU odtwarza jedną kompletną wersję grupy (SYS-109). Plik Windows może zawierać sekcje zestawów i map. Format należy do projektu danych. [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-110 wiąże przyjęcie pełnej podmiany zestawu lub trwałego zapisu map z blokadą rozruchu w ECU. Aplikacja obsługuje dane i status operacji. ECU samodzielnie kończy blokadę po potwierdzeniu poprawnych danych. [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-111 udostępnia w statusie operacji flagę błędnej sumy kontrolnej pakietu map. Windows może odczytać ją po przywróceniu poprzednich wartości przez ECU. [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

Status z ECU zgodny z SYS-112 odzwierciedla skasowanie flagi po kolejnym zweryfikowanym trwałym zapisie map.

SYS-101: Windows może przesyłać do ECU robocze zmiany wybranych wartości aktywnego i nieaktywnych zestawów podczas pracy silnika. Edycja nie przełącza zestawu; nieaktywny zaczyna wpływać na silnik dopiero po jego świadomym wybraniu. Obowiązuje SYS-095 dla trwałego zapisu. Szczegóły: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-099: wybór zestawu po restarcie realizuje ECU, również bez HMI/PC; jest to ostatnio wybrany prawidłowy zestaw spośród trwale zapisanych. Aplikacja po połączeniu odczytuje rzeczywisty stan. Po prawidłowym śnie/wybudzeniu niezapisane zmiany zostają odrzucone zgodnie z SYS-100. Uzgodnienie po powrocie sesji i walidacja danych pozostają do określenia w [F02](../../docs/interfaces/mapy-i-konfiguracja.md).
