# Sprzęt ECU

Miejsce na edytowalne schematy i PCB, BOM oraz kontrolowane eksporty produkcyjne ECU.

Wymaganie bazowe: jedna platforma sprzętowa dla jednocylindrowych silników 2T i 4T. Parametry i interfejsy obsługiwanych układów zapłonu, paliwa, czujników i obciążeń oraz granice warunków zasilania wymagają szczegółowej specyfikacji.

Narzędzie EDA: **Autodesk Fusion Electronics**, płatna subskrypcja właściciela projektu. Komponenty nie zostały jeszcze wybrane.

Wymagania i otwarte decyzje: [zakres systemu](../../docs/01-zakres-systemu.md). Definicje interfejsów rozwijamy w `docs/interfaces/`.

Dobór MCU, pamięci i zasilania musi uwzględnić [chronione motogodziny i ODO](../../docs/architecture/chronione-liczniki.md), SYS-074–076: trwałość zapisu, utratę zasilania, ochronę dostępu i mechanizmy uruchamiania/aktualizacji. Konkretne mechanizmy i ważne komponenty wybieramy wspólnie z właścicielem po ustaleniu granic ochrony.
