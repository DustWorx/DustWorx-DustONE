# ADR-008 — dostęp do firmware ECU w użytkowaniu i rozwoju

Data: 2026-11-01. Status: zatwierdzony podział dostępu; realizacja do projektu.

## Decyzja i źródło

W odpowiedzi A na pytanie 82 właściciel wybrał: w trybie użytkowym ECU wyłącznie firmware zatwierdzony przez producenta projektu, przy zachowaniu dostępu twórców do programowania i debugowania. Wymaganie: [SYS-078](../01-zakres-systemu.md). Polityka firmware HMI nie została rozstrzygnięta tą odpowiedzią.

Decyzja wspiera ochronę całkowitych motogodzin i ODO według [ADR-007](adr-007-chronione-liczniki.md), zachowując możliwość rozwijania firmware przez właściciela i Codex. Użytkownik końcowy nie uzyskuje uprawnień twórców przez narzędzie diagnostyczne lub development tool.

## Konsekwencje i otwarte szczegóły

- Egzekwowanie polityki trzeba zaprojektować w ECU, w tym dla uruchamiania, aktualizacji i odzyskiwania; zakres interfejsów sprzętowych i odporności fizycznej wynika z modelu zagrożeń. Sama kontrola w Windows nie wystarcza.
- Przed doborem MCU należy określić autoryzację dostępu inżynierskiego, oznaczanie zatwierdzonych wersji, zgodność i politykę starszych wersji oraz zasady przejść między trybami i zachowania historii liczników.
- Mechanizmy, komponenty oraz ewentualne zarządzanie kluczami wybieramy wspólnie później. Nie przyjęto konkretnej kryptografii, zewnętrznego układu zabezpieczającego ani nieodwracalnych blokad debuggera.
- Zasady producenta/serwisu dotyczące inicjalizacji i przenoszenia liczników pozostają zgodne z SYS-077; dostęp rozwojowy nie stanowi automatycznego uprawnienia serwisowego do korekty historii.

## Plan weryfikacji do uszczegółowienia

| Próba | Oczekiwane potwierdzenie |
| --- | --- |
| Zatwierdzona aktualizacja | Poprawna aktualizacja zgodnego ECU, zachowanie liczników i możliwość normalnej pracy. |
| Niezatwierdzony lub zmieniony obraz | Brak dopuszczenia do pracy w trybie użytkowym; sprawdzić aplikację i bezpośredni interfejs ECU. |
| Dostęp rozwojowy | Twórcy mogą programować i debugować zgodnie z polityką; użytkownik końcowy nie może przejąć ich uprawnień. |
| Przerwanie, odzyskiwanie i starsze wersje | Zachowanie zgodne z opracowaną polityką, bez obejścia zatwierdzania firmware lub ochrony liczników. |

Kryteria zaliczenia, stanowiska i procedury powstaną przed próbami. To plan, nie wykonana implementacja ani potwierdzona odporność.
