# Oprogramowanie ECU

Miejsce na kod sterowania silnikiem i akcesoriami, pomiary, komunikację, diagnostykę i aktualizację ECU.

Stan: brak implementacji. Procesor, język, środowisko budowania i organizacja czasu wykonania pozostają do ustalenia.

Po rozpoczęciu implementacji ten dokument opisuje budowanie, uruchamianie i testowanie komponentu. Testy jednostkowe przechowujemy przy kodzie.

ECU nalicza i przechowuje [chronione całkowite motogodziny i ODO](../../docs/architecture/chronione-liczniki.md), SYS-074–077. Ochronę egzekwuje firmware i architektura sprzętu, obejmując protokół, narzędzia testowe, pamięć, bootloader i odzyskiwanie. Chroniona procedura producenta/serwisu ma umożliwiać inicjalizację nowego ECU i przenoszenie udokumentowanych wartości, z rejestrem każdej operacji. Szczegóły autoryzacji i konkretne mechanizmy pozostają do projektu; nie przyjęto nieodwracalnego blokowania debuggera.

[SYS-078 i ADR-008](../../docs/decisions/adr-008-dostep-do-firmware-ecu.md) określają dostęp do firmware: w trybie użytkowym wyłącznie wersje zatwierdzone przez producenta projektu, z zachowaniem programowania i debugowania dla twórców. Kontrolę trzeba zaprojektować po stronie ECU, obejmując uruchamianie, aktualizację, programowanie i odzyskiwanie zgodnie z uzgodnionym modelem zagrożeń. Autoryzacja dostępu rozwojowego, polityka starszych wersji i przejść między trybami są otwarte.
