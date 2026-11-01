# ADR-006 — IAC z napędem krokowym w enduro 4T

Data: 2026-11-01. Status: zatwierdzony zakres funkcji; zgodne napędy, parametry i realizacja otwarte.

## Problem, opcje i podstawa

Przy zachowaniu osprzętu OEM niektóre enduro 4T wymagają sterowania powietrzem biegu jałowego przez ECU. Instrukcja Beta RR 350/390/430/480 EFI 2016, s. 33, potwierdza elektroniczną regulację; schemat dla tej rodziny wskazuje napęd krokowy (poz. 46). Rozważano jego obsługę lub wyłączenie IAC z dopuszczeniem adaptacji osprzętu.

W odpowiedzi na poprawione pytanie 77 z 2026-11-01, po sprawdzeniu zastosowania w enduro, właściciel wybrał IAC z napędem krokowym dla potwierdzonych modeli. Wymaganie: [SYS-071](../01-zakres-systemu.md). Zakres nie oznacza potwierdzonej zgodności DustONE z każdym napędem IAC.

## Konsekwencje i otwarte dane

- Wspólna PCB ma uwzględnić sterowanie napędem dla odpowiednich wariantów 4T. Konfiguracje bez IAC działają bez niego; główna przepustnica nadal jest sterowana linką (SYS-038).
- Przed doborem elektroniki potwierdzić modele, uzwojenia i połączenia, prądy, zasilanie, zakres ruchu, kalibrację oraz wymaganą liczbę wyjść. Rozważyć wykorzystanie zasobów między wariantami; współdzielenie z power valve nie zostało wybrane.
- Uwzględnić pozycjonowanie/kalibrację w czasie wybudzania i gotowości do rozruchu, szczególnie kopniakiem (SYS-054), oraz pracę napędu i pobór energii przy usypianiu (SYS-059). Warunki i czasy wymagają analizy.
- Określić sterowanie, limity, diagnostykę i reakcje na usterki. Ważne komponenty wybieramy wspólnie z właścicielem po porównaniu; obsługa innych odmian IAC wymaga osobnych podstaw i uzgodnienia.

## Proponowana weryfikacja

Najpierw charakterystyka napędu i próby stanowiskowe: pozycjonowanie, kalibracja, prądy i temperatura, zaniki zasilania oraz ustalone uszkodzenia. Następnie próby regulacji biegu jałowego na odpowiedniej jednostce 4T w przyjętym zakresie temperatur i obciążeń oraz sprawdzenie rozruchu i snu. Osobno potwierdzić pracę konfiguracji bez IAC i reakcję na usterkę napędu używanego przez konfigurację. Kryteria liczbowe, przyrządy i procedury pozostają do opracowania; prób nie wykonano.

Źródła: [instrukcja Beta RR 4T EFI 2016, s. 33](https://betausa.com/content/SUPPORT_PDF%27s/2016%20RR%204%20stroke%20owners%20manual_0.pdf), [schematy Beta USA RR/Race 4T, strony PDF 8–9, poz. 46](https://betausa.com/content/WIRING%20DIAGRAM%204T%202%2024%20new.pdf). Dokumentacja potwierdza wyposażenie motocykli; parametry napędu i zgodność DustONE wymagają analizy oraz testów.
