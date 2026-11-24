# DustWorx DustONE

System sterowania motocyklem: ECU dla silników jednocylindrowych 2T/4T na wspólnej platformie sprzętowej, HMI po CAN oraz aplikacja Windows do konfiguracji, strojenia, diagnostyki, aktualizacji i prac rozwojowych.

**Aktywny etap 2 — zakres funkcjonalny.** F01 i F02 zamknięto w zakresie funkcji. Aktywny jest **F03 — ochrona i reakcje na usterki**. F04–F08 i kolejne etapy oczekują w kolejce. [Ścieżka projektu i aktualny status](docs/00-proces-i-status.md) opisują etapy, warunki ich zakończenia i najbliższe rezultaty.

## Dokumentacja

| Szukana informacja | Gdzie zacząć |
| --- | --- |
| Aktualny etap, kolejka i najbliższy krok | [Proces i status](docs/00-proces-i-status.md#bieżąca-praca-i-kolejka). |
| Przyjęte wymaganie SYS | [Rejestr wymagań](docs/01-zakres-systemu.md#2-wymagania-wynikające-z-opisu). |
| Sterowanie silnikiem, mapy i konfiguracja | Zamknięte przeglądy [F01](docs/requirements/f01-podsumowanie-kontrolne.md) i [F02](docs/requirements/f02-przeglad-zakresu.md). |
| Ochrona, reakcje na usterki i plany prób F03 | [Indeks tematów F03](docs/requirements/f03-ochrona-i-usterki.md#szybka-nawigacja). |
| Uzasadnienie decyzji | [Rejestr ADR](docs/decisions/README.md). |
| I/O, czujniki, osprzęt i dokumentacja Bety | [Interfejsy](docs/interfaces/README.md). |
| Diagramy, warianty i bilanse | [Wstępna architektura](docs/architecture/README.md). |
| Powiązanie wymagania z próbami | [Weryfikacja](docs/verification/README.md) i [macierz SYS → blok → grupa](docs/verification/macierz-wymagan.md). |
| Pozostałe dokumenty i statusy | [Indeks dokumentacji](docs/README.md). |
| Gałęzie, PR-y i miejsce plików | [Zasady pracy](CONTRIBUTING.md#zmiany-w-repozytorium). |

Aktualny wspólny stan projektu znajduje się na `main`. Kolejne zmiany rozwijamy w krótkich gałęziach tematycznych i publikujemy przez PR. Otwarte zagadnienia oraz statusy etapów są zapisane w dokumentach.

To repozytorium jest głównym miejscem przechowywania dokumentacji i plików projektu. Ustalenia z rozmów należy zapisywać tutaj, z rozróżnieniem wymagań, propozycji i zatwierdzonych decyzji.

## Struktura

| Katalog | Zawartość |
| --- | --- |
| `docs/` | Zakres, wymagania, architektura, interfejsy, decyzje i plan weryfikacji. |
| `hardware/ecu/` | Schematy, PCB, BOM i pliki produkcyjne ECU. |
| `hardware/hmi/` | Schematy, PCB, BOM i pliki produkcyjne HMI. |
| `mechanical/` | Obudowy, mocowania i rysunki mechaniczne. |
| `firmware/ecu/` | Oprogramowanie wbudowane ECU. |
| `firmware/hmi/` | Oprogramowanie wbudowane HMI. |
| `software/windows/` | Wspólna aplikacja Windows. |
| `tools/` | Skrypty i narzędzia pomocnicze projektu. |
| `tests/` | Testy integracyjne i systemowe oraz dane testowe. |

Katalogi zawierają obecnie opisy przeznaczenia. Ich obecność nie oznacza gotowej implementacji.
