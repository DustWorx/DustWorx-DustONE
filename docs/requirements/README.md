# Wymagania

Miejsce na wymagania systemowe oraz wymagania ECU, HMI i aplikacji Windows.

Na tym etapie wymagania SYS-001–SYS-263 znajdują się w [zakresie systemu](../01-zakres-systemu.md). Przy rozbudowie przenosimy je tutaj, zachowując identyfikatory i aktualizując odsyłacze; nie utrzymujemy dwóch niezależnych rejestrów.

Wymaganie szczegółowe powinno mieć identyfikator, jednoznaczną treść, źródło, status oraz kryterium i sposób weryfikacji. Parametry nieustalone oznaczamy wprost jako do ustalenia.

Robocza [mapa obszarów i otwartych tematów](pokrycie-funkcjonalne.md) służy do kontroli zakresu pytań i przeglądów. [Model współpracy](../00-proces-i-status.md) określa podział pracy i podstawę pytań.

| Pakiet | Dokument źródłowy przeglądu | Status |
| --- | --- | --- |
| F01 — sterowanie silnikiem | [Podsumowanie kontrolne](f01-podsumowanie-kontrolne.md) | Zamknięty po kontroli właściciela. |
| F02 — mapy i konfiguracja | [Karta przeglądu](f02-przeglad-zakresu.md) | Zamknięty po kontroli właściciela. |
| F03 — ochrona i reakcje | [Karta przeglądu](f03-przeglad-zakresu.md), [reakcje i plany prób](f03-ochrona-i-usterki.md#szybka-nawigacja) | Zamknięty po akceptacji właściciela w pytaniu 243: 2026-11-24. |
| F04 — akcesoria i dodatkowe I/O | [Karta przeglądu](f04-przeglad-zakresu.md), [ustalenia i plany](f04-akcesoria-i-io.md) | Zamknięty po akceptacji właściciela w odpowiedzi na pytanie 271: 2026-11-26. |
| F05 — funkcje i obsługa HMI | [Podstawy, kolejność tematów i ustalenia](f05-funkcje-i-obsluga-hmi.md) | Aktywny; przyjęto SYS-263 i pierwszy plan próby. Kolejna decyzja 273 — zachowanie paska ostrzeżenia. |

F01–F04 zamknięto w zakresie funkcji. [F05 — funkcje i obsługa HMI](f05-funkcje-i-obsluga-hmi.md) jest aktywny, F06–F08 oczekują. Pakiety zamykamy kolejno według [rejestru domknięcia](domkniecie-zakresu-funkcjonalnego.md) i bramki G0 ze [ścieżki projektu](../00-proces-i-status.md). Publikacja bieżących ustaleń nie zamyka pakietu. Otwarte parametry realizacji rozwijamy na właściwych etapach.

[Macierz SYS → blok → grupa weryfikacji](../verification/macierz-wymagan.md) zawiera pierwszy przydział wszystkich 263 wymagań. Przydział i zatwierdzenie treści są odrębne od późniejszego potwierdzenia na produkcie.
