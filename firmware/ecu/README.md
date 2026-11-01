# Oprogramowanie ECU

Miejsce na kod sterowania silnikiem i akcesoriami, pomiary, komunikację, diagnostykę i aktualizację ECU.

Stan: brak implementacji. Procesor, język, środowisko budowania i organizacja czasu wykonania pozostają do ustalenia.

Po rozpoczęciu implementacji ten dokument opisuje budowanie, uruchamianie i testowanie komponentu. Testy jednostkowe przechowujemy przy kodzie.

ECU nalicza i przechowuje [chronione całkowite motogodziny i ODO](../../docs/architecture/chronione-liczniki.md), SYS-074–076. Ochronę egzekwuje firmware i architektura sprzętu, obejmując protokół, narzędzia testowe, pamięć, bootloader i odzyskiwanie. Uprawnienia rozwojowe/serwisowe i konkretne mechanizmy pozostają do projektu; nie przyjęto nieodwracalnego blokowania debuggera.
