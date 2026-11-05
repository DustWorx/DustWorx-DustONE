# Sprzęt ECU

Miejsce na edytowalne schematy i PCB, BOM oraz kontrolowane eksporty produkcyjne ECU.

Wymaganie bazowe: jedna platforma sprzętowa dla jednocylindrowych silników 2T i 4T chłodzonych cieczą (SYS-098); wymagany jest pomiar temperatury płynu według SYS-044. Parametry i interfejsy obsługiwanych układów zapłonu, paliwa, czujników i obciążeń oraz granice warunków zasilania wymagają szczegółowej specyfikacji.

Narzędzie EDA: **Autodesk Fusion Electronics**, płatna subskrypcja właściciela projektu. Komponenty nie zostały jeszcze wybrane.

Wymagania i otwarte decyzje: [zakres systemu](../../docs/01-zakres-systemu.md). Definicje interfejsów rozwijamy w `docs/interfaces/`.

Dobór MCU, pamięci i zasilania musi uwzględnić [chronione motogodziny i ODO](../../docs/architecture/chronione-liczniki.md), SYS-074–076: trwałość zapisu, utratę zasilania, ochronę dostępu i mechanizmy uruchamiania/aktualizacji. Konkretne mechanizmy i ważne komponenty wybieramy wspólnie z właścicielem po ustaleniu granic ochrony.

Dobór MCU i interfejsów programowania musi również uwzględnić [SYS-078 i ADR-008](../../docs/decisions/adr-008-dostep-do-firmware-ecu.md): w trybie użytkowym tylko firmware zatwierdzony przez producenta oraz zachowany dostęp rozwojowy twórców. Sposób autoryzacji i przejścia między trybami wymaga projektu; nie wybrano układów, algorytmów ani nieodwracalnych blokad.

Tor przedniego koła musi umożliwiać wykrywanie obrotów podczas snu i wybudzanie ECU do naliczania ODO także przy zgaszonym silniku (SYS-075/079, [I/O](../../docs/interfaces/wstepna-lista-io.md)). Czujnik, interfejs i elementy dobierzemy wspólnie; uwzględnić pobór w śnie i obsługę początku ruchu.

SYS-092 wymaga obsługi AGM i motocyklowych LiFePO4 na wspólnej PCB bez zmiany obsady. Zakres wejścia, ochrona, pomiar i budżet czuwania wymagają obliczeń oraz prób dla uzgodnionych konfiguracji; komponenty wybieramy wspólnie. [ADR-010 i plan weryfikacji](../../docs/decisions/adr-010-akumulatory-agm-lifepo4.md).

Budżet poboru ECU, zasilanego z niego HMI i torów czuwania musi wynikać z celu minimum 4 tygodni postoju bez doładowania z rezerwą na rozruch przy otoczeniu od −10°C do +40°C podczas postoju i późniejszego uruchomienia (SYS-093). Dla tego celu przyjęto pojemności znamionowe od 3 Ah AGM i 2 Ah LiFePO4 (C10). Limit prądu i szczegóły pomiaru wyliczymy dla zgodnych modeli oraz kryteriów rozruchu; zakres pracy elektroniki podczas jazdy ustalimy osobno: [analiza i plan prób](../../docs/architecture/budzet-energii-postoju.md).

Do późniejszego projektu: SYS-096 wymaga możliwości odczytu MAP z kompatybilnego czujnika OEM lub dodatkowego na wspólnej PCB. Konfiguracje niewymagające MAP pracują bez czujnika; model, parametry toru i komponenty dobierzemy we właściwych etapach. [Karta MAP](../../docs/interfaces/cisnienie-dolotu-map.md).

Do późniejszego projektu: SYS-097 wymaga możliwości odczytu ciśnienia gazów w skrzyni korbowej 2T (CCPS) z kompatybilnego czujnika. Model, parametry i podział zasobów z MAP określimy w etapach projektowych; [karta CCPS](../../docs/interfaces/cisnienie-skrzyni-korbowej.md).
