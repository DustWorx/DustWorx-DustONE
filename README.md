# DustWorx DustONE

System sterowania motocyklem: ECU dla silników jednocylindrowych 2T/4T na wspólnej platformie sprzętowej, HMI po CAN oraz aplikacja Windows do konfiguracji, strojenia, diagnostyki, aktualizacji i prac rozwojowych.

**Aktywny etap:** 2 — zakres funkcjonalny. **Aktywny pakiet:** F01 — funkcje silnikowe. Pozostałe pakiety i etapy oczekują w kolejce. [Ścieżka projektu i aktualny status](docs/00-proces-i-status.md) opisują etapy, warunki ich zakończenia i najbliższe rezultaty.

## Dokumentacja

- [Ścieżka projektu, etapy i status](docs/00-proces-i-status.md)
- [Pakiety domknięcia funkcjonalności](docs/requirements/domkniecie-zakresu-funkcjonalnego.md)
- [Indeks dokumentacji](docs/README.md)
- [Zakres systemu i otwarte decyzje](docs/01-zakres-systemu.md)
- [Zasady pracy](CONTRIBUTING.md)

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
