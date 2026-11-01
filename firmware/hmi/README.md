# Oprogramowanie HMI

Miejsce na kod prezentacji danych, obsługi kierowcy, komunikacji CAN, diagnostyki i aktualizacji HMI.

Stan: brak implementacji. Platforma i technologia interfejsu pozostają do ustalenia. Personalizacja ekranu z aplikacji Windows jest wymaganiem; jej zakres wymaga doprecyzowania.

Po wykryciu obrotów przedniego koła ECU wybudza również HMI (SYS-080). Naliczanie ODO w ECU nie czeka na gotowość HMI i działa przy jego awarii. Sposób przekazania wybudzenia i czasy reakcji są otwarte. Weryfikacja obejmie wybudzenie obu urządzeń i odrębne próby ODO z opóźnionym oraz niedostępnym HMI: [ADR-003](../../docs/decisions/adr-003-wybudzanie-bez-wlacznika.md).
