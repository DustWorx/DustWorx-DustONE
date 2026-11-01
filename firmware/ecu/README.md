# Oprogramowanie ECU

Miejsce na kod sterowania silnikiem i akcesoriami, pomiary, komunikację, diagnostykę i aktualizację ECU.

Stan: brak implementacji. Procesor, język, środowisko budowania i organizacja czasu wykonania pozostają do ustalenia.

Po rozpoczęciu implementacji ten dokument opisuje budowanie, uruchamianie i testowanie komponentu. Testy jednostkowe przechowujemy przy kodzie.

ECU nalicza i przechowuje [chronione całkowite motogodziny i ODO](../../docs/architecture/chronione-liczniki.md), SYS-074–077. Ochronę egzekwuje firmware i architektura sprzętu, obejmując protokół, narzędzia testowe, pamięć, bootloader i odzyskiwanie. Chroniona procedura producenta/serwisu ma umożliwiać inicjalizację nowego ECU i przenoszenie udokumentowanych wartości, z rejestrem każdej operacji. Szczegóły autoryzacji i konkretne mechanizmy pozostają do projektu; nie przyjęto nieodwracalnego blokowania debuggera.

[SYS-078 i ADR-008](../../docs/decisions/adr-008-dostep-do-firmware-ecu.md) określają dostęp do firmware: w trybie użytkowym wyłącznie wersje zatwierdzone przez producenta projektu, z zachowaniem programowania i debugowania dla twórców. Kontrolę trzeba zaprojektować po stronie ECU, obejmując uruchamianie, aktualizację, programowanie i odzyskiwanie zgodnie z uzgodnionym modelem zagrożeń. Autoryzacja dostępu rozwojowego, polityka starszych wersji i przejść między trybami są otwarte.

SYS-075/079 wymagają wybudzenia ECU obrotami przedniego koła i naliczania ODO także przy zgaszonym silniku oraz niedostępnym HMI. Zaprojektować obsługę pierwszych impulsów i przejść sen–praca zgodnie z przyszłym limitem błędu. Motogodziny nadal wymagają pracy silnika; samo koło nie żąda rozruchu. [Analiza i zakres prób](../../docs/architecture/chronione-liczniki.md).

SYS-081 wymaga wyłączenia świateł przednich i tylnych pozycyjnych przed prawidłowym uśpieniem oraz pozostawienia ich wyłączonych po wybudzeniu ze zgaszonym silnikiem do polecenia HMI. Obsługa snu nie przywraca automatycznie stanu sprzed snu; należy ją uzgodnić z ważnością żądań HMI. [Przebieg i zakres prób](../../docs/architecture/usypianie-ecu-hmi.md).

SYS-082 wymaga automatycznego włączenia przednich i tylnych pozycyjnych po potwierdzonym uruchomieniu silnika, również bez gotowego lub sprawnego HMI. Mijania i drogowe włącza użytkownik z HMI. W logice rozdzielić samo wybudzenie od potwierdzonego uruchomienia silnika i poleceń oświetlenia. [Zakres prób](../../docs/architecture/usypianie-ecu-hmi.md).

SYS-083/084 dodają przejście z mijania/drogowych na pozycyjne po zatrzymaniu silnika oraz tryb oszczędzania przed snem na podstawie bieżącego pomiaru napięcia. Sterowanie i decyzje pozostają w ECU. SYS-085 wymaga odrzucania zwykłych żądań ponownego ON dla odbiorników objętych aktywnym odcięciem, także poza HMI. Do HMI przekazywana jest rzeczywista odmowa do prezentacji według SYS-086. Lista odłączanych odbiorników, kwalifikacja spadku i warunki powrotu są otwarte: [analiza i plan prób](../../docs/architecture/oszczedzanie-energii.md).
