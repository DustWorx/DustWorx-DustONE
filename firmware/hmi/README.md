# Oprogramowanie HMI

Miejsce na kod prezentacji danych, obsługi kierowcy, komunikacji CAN, diagnostyki i aktualizacji HMI.

Stan: brak implementacji. Platforma i technologia interfejsu pozostają do ustalenia. Personalizacja ekranu z aplikacji Windows jest wymaganiem; jej zakres wymaga doprecyzowania.

Po wykryciu obrotów przedniego koła ECU wybudza również HMI (SYS-080). Naliczanie ODO w ECU nie czeka na gotowość HMI i działa przy jego awarii. Sposób przekazania wybudzenia i czasy reakcji są otwarte. Weryfikacja obejmie wybudzenie obu urządzeń i odrębne próby ODO z opóźnionym oraz niedostępnym HMI: [ADR-003](../../docs/decisions/adr-003-wybudzanie-bez-wlacznika.md).

SYS-086: przy próbie włączenia odbiornika objętego aktywnym odcięciem oszczędzania, przy zgaszonym silniku HMI wyświetla odmowę i informację „Wymagane uruchomienie silnika”. Źródłem decyzji jest ECU (SYS-085); panel nie znosi blokady lokalną zmianą stanu. Gdy silnik już pracuje, a warunek napięcia/czasu z SYS-087 nadal nie jest spełniony, HMI powinno przedstawiać aktualny powód dalszej blokady. Proponowany opis: „Oczekiwanie na stabilne zasilanie”. Aktualność statusów, kodowanie przyczyny i dokładny opis tego stanu wymagają specyfikacji: [analiza i plan prób](../../docs/architecture/oszczedzanie-energii.md).

HMI wyświetla przyczynę odrzucenia zmiany zestawu map otrzymaną z ECU po usterce wymagającej pracy awaryjnej lub zatrzymania silnika (SYS-135 i SYS-137). Szczegóły scenariusza i próby zawiera [specyfikacja F02](../../docs/interfaces/mapy-i-konfiguracja.md).
