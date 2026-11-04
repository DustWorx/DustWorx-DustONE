# Oprogramowanie ECU

Miejsce na kod sterowania silnikiem i akcesoriami, pomiary, komunikację, diagnostykę i aktualizację ECU.

Stan: brak implementacji. Procesor, język, środowisko budowania i organizacja czasu wykonania pozostają do ustalenia.

Po rozpoczęciu implementacji ten dokument opisuje budowanie, uruchamianie i testowanie komponentu. Testy jednostkowe przechowujemy przy kodzie.

ECU nalicza i przechowuje [chronione całkowite motogodziny i ODO](../../docs/architecture/chronione-liczniki.md), SYS-074–077. Ochronę egzekwuje firmware i architektura sprzętu, obejmując protokół, narzędzia testowe, pamięć, bootloader i odzyskiwanie. Chroniona procedura producenta/serwisu ma umożliwiać inicjalizację nowego ECU i przenoszenie udokumentowanych wartości, z rejestrem każdej operacji. Szczegóły autoryzacji i konkretne mechanizmy pozostają do projektu; nie przyjęto nieodwracalnego blokowania debuggera.

[SYS-078 i ADR-008](../../docs/decisions/adr-008-dostep-do-firmware-ecu.md) określają dostęp do firmware: w trybie użytkowym wyłącznie wersje zatwierdzone przez producenta projektu, z zachowaniem programowania i debugowania dla twórców. Kontrolę trzeba zaprojektować po stronie ECU, obejmując uruchamianie, aktualizację, programowanie i odzyskiwanie zgodnie z uzgodnionym modelem zagrożeń. Autoryzacja dostępu rozwojowego, polityka starszych wersji i przejść między trybami są otwarte.

SYS-075/079 wymagają wybudzenia ECU obrotami przedniego koła i naliczania ODO także przy zgaszonym silniku oraz niedostępnym HMI. Zaprojektować obsługę pierwszych impulsów i przejść sen–praca zgodnie z przyszłym limitem błędu. Motogodziny nadal wymagają pracy silnika; samo koło nie żąda rozruchu. [Analiza i zakres prób](../../docs/architecture/chronione-liczniki.md).

SYS-081 wymaga wyłączenia świateł przednich i tylnych pozycyjnych przed prawidłowym uśpieniem oraz pozostawienia ich wyłączonych po wybudzeniu ze zgaszonym silnikiem do polecenia HMI. Obsługa snu nie przywraca automatycznie stanu sprzed snu; należy ją uzgodnić z ważnością żądań HMI. [Przebieg i zakres prób](../../docs/architecture/usypianie-ecu-hmi.md).

SYS-082 wymaga automatycznego włączenia przednich i tylnych pozycyjnych po potwierdzonym uruchomieniu silnika, również bez gotowego lub sprawnego HMI. Mijania i drogowe włącza użytkownik z HMI. W logice rozdzielić samo wybudzenie od potwierdzonego uruchomienia silnika i poleceń oświetlenia. [Zakres prób](../../docs/architecture/usypianie-ecu-hmi.md).

SYS-083/084 dodają przejście z mijania/drogowych na pozycyjne po zatrzymaniu silnika oraz tryb oszczędzania przed snem na podstawie bieżącego pomiaru napięcia. Sterowanie i decyzje pozostają w ECU. SYS-085 wymaga odrzucania zwykłych żądań ponownego ON dla odbiorników objętych aktywnym odcięciem, także poza HMI. Do HMI przekazywana jest rzeczywista odmowa do prezentacji według SYS-086. SYS-087 wymaga utrzymania odcięcia w normalnym użytkowaniu do potwierdzonej pracy silnika i utrzymania napięcia powrotu przez ustalony czas; automatyka pozycyjnych nie omija tego warunku. Lista odłączanych odbiorników, kwalifikacja spadku, wartości progu/czasu są otwarte. SYS-088/089 rozdzielają powrót: odbiorniki użytkownika czekają na nowe polecenie, automatyczne funkcje ochrony silnika działają według aktualnego zapotrzebowania oraz własnych zabezpieczeń. Ręczne wymuszenie wentylatora nie wraca samo: [analiza i plan prób](../../docs/architecture/oszczedzanie-energii.md).

SYS-090: jawny tryb serwisowy dopuszcza zwolnienie odcięcia do testów bez pracy silnika przy potwierdzonym stabilnym zasilaniu warsztatowym. ECU egzekwuje warunki i aktywne zabezpieczenia wyjść. Samo połączenie PC nie zwalnia odcięcia; uruchomienie testu wymaga osobnego polecenia. SYS-091 wymaga po utracie sesji blokady nowych testów, dokończenia rozpoczętego najpóźniej do limitu przyjętego przed startem i następnie cofnięcia wyjątku serwisowego. ECU nadzoruje limit niezależnie od Windows; utrata/powrót sesji nie odracza końca. Zabezpieczenia pozostają nadrzędne. Uprawnienia, detekcja sesji, reakcje na zanik zasilania i stany końcowe pozostają do projektu: [analiza i plan prób](../../docs/architecture/oszczedzanie-energii.md).

SYS-092: osobne profile ochrony akumulatorów AGM i LiFePO4 przy wspólnym sprzęcie. Do projektu: parametry, wybór i zapis profilu oraz jego współpraca z istniejącymi zasadami oszczędzania i serwisu. Zatwierdzenie i otwarte szczegóły: [ADR-010](../../docs/decisions/adr-010-akumulatory-agm-lifepo4.md).

SYS-094: przyjmowanie i stosowanie zmian wybranych wartości map podczas pracy silnika. Po utracie Windows ostatnio zastosowane wartości pozostają aktywne w bieżącej pracy ECU, bez automatycznego trwałego zapisu. Zakres, walidacja, moment zastosowania, ponowne połączenie i restart/zanik zasilania pozostają do specyfikacji: [ADR-011](../../docs/decisions/adr-011-strojenie-na-zywo.md).

SYS-028 określa maks. trzy niezależne, kompletne zestawy uzgodnionych map jednej konfiguracji silnika. Przydział pamięci i obsługę edycji rozwijamy według [specyfikacji map](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-095: ECU dopuszcza trwały zapis zmian map wyłącznie przy zgaszonym silniku i po wyraźnym poleceniu użytkownika z Windows. Strojenie na żywo nie uruchamia automatycznego utrwalania. Potwierdzenie zatrzymania, warunki zasilania, przerwanie zapisu i równoczesny rozruch wymagają specyfikacji w [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-101: ECU przyjmuje robocze zmiany wybranych wartości aktywnego i nieaktywnych zestawów podczas pracy silnika. Edycja nie przełącza zestawu; zmiany nieaktywnego wpływają na silnik dopiero po jego świadomym wybraniu. Trwały zapis nadal podlega SYS-095. Szczegóły: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).

SYS-099: po restarcie ECU aktywuje ostatnio wybrany prawidłowy zestaw spośród trwale zapisanych, także bez HMI. Zapamiętanie wyboru i zapis wartości map mają odrębne reguły; brak automatycznego utrwalania edycji na żywo. SYS-100 wymaga po prawidłowym śnie/wybudzeniu odrzucenia roboczej edycji i użycia trwale zapisanych wartości, bez automatycznego utrwalania. Mechanizm pamięci wyboru, walidacja, gotowość do rozruchu i przerwana sekwencja snu są do projektu: [F02](../../docs/interfaces/mapy-i-konfiguracja.md).
