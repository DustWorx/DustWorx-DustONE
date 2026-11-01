# Chronione liczniki eksploatacyjne

Data: 2026-11-01. Status: zatwierdzony cel ochrony i zakres dwóch liczników; szczegóły, model zagrożeń i kryteria prób do opracowania. Podstawa: [SYS-074–076](../01-zakres-systemu.md), [ADR-007](../decisions/adr-007-chronione-liczniki.md).

## Uzgodnione zasady

- ECU jest źródłem całkowitych motogodzin i ODO. Naturalne naliczanie zmienia wartości; użytkownik końcowy nie może ich dowolnie ustawiać, korygować ani kasować. HMI i Windows odczytują dane ECU.
- Ochrona obejmuje również dostępne użytkownikowi protokoły, diagnostykę, development tool, reset ustawień, import konfiguracji, kasowanie DTC, aktualizację i odzyskiwanie urządzenia. Kopia map lub konfiguracji nie może służyć przywróceniu starszych sum.
- Motogodziny mają wynikać z potwierdzonej pracy silnika. Źródło i reguły naliczania ODO oraz dokładność obu liczników trzeba określić. Kasowalne liczniki A/B nie zostały przyjęte.

## Wymagane analizy przed doborem sprzętu

1. Inicjalizacja przy pierwszym montażu oraz ciągłość po wymianie ECU. Ustalić uprawnienia producenta/serwisu i dowody takich operacji; nie przyjęto jeszcze żadnej ścieżki korekty.
2. Model zagrożeń: interfejsy użytkownika, własny firmware, debug/programowanie, dostęp do pamięci i podmiana danych lub sygnałów pomiarowych. Granice odporności fizycznej wymagają uzgodnienia. Rozwój firmware przez właściciela musi być uwzględniony w odrębnej polityce dostępu, bez automatycznego zatwierdzania trwałych blokad.
3. MCU, pamięć i cykl życia: izolacja danych i uprawnień, wiarygodność uruchamianego firmware/aktualizacji, integralność oraz wykrywanie nieuprawnionych zmian i odtwarzania starych zapisów. Samo zabezpieczenie pliku aktualizacji nie określa ochrony stanu liczników.
4. Zapis i zasilanie: zużycie pamięci, spójność przy zaniku napięcia, rozdzielczość trwałego zapisu i dozwolony błąd. Powtarzane wyłączanie nie może być pominiętą ścieżką obchodzenia naliczania. Uszkodzone dane nie mogą być bez informacji przedstawione jako wiarygodne zero.
5. Zależności pomiarowe: kalibracja wpływająca na naliczanie, np. obwód koła, oraz odróżnienie sygnałów rzeczywistych od symulacji. Samo połączenie PC nie oznacza, że silnik nie pracuje; polityka trybów testowych musi to uwzględnić.

Ważne komponenty i mechanizmy wybieramy wspólnie z właścicielem. Przykład dokumentacji producenta o ochronie pamięci, debugowaniu, rozruchu i interfejsach: [ST AN5156 — Software isolation](https://www.st.com/content/st_com/en/technical-documents/an5156-introduction-to-security-for-stm32-mcus-stmicroelectronics_asset/chunk-004-topic-an5156-dev-prot-software-isolation.html). Jest to materiał do analizy, nie wybór STM32 ani deklaracja odporności DustONE.

## Plan weryfikacji do uszczegółowienia

| Obszar | Próby / oczekiwane potwierdzenie |
| --- | --- |
| Naliczanie | Znany czas pracy i droga; dokładność w ustalonych warunkach. Oddzielić pracę silnika, postój, sen, sesję PC i dane symulowane. |
| Uprawnienia | Próby ustawienia, korekty i kasowania przez HMI, Windows i bezpośrednie interfejsy użytkownika, w tym development tool: brak nieuprawnionej zmiany. |
| Cykl życia | Reset ustawień, import konfiguracji, kasowanie DTC, ponowne uruchomienie, sen, wymiana HMI oraz aktualizacja/odzyskiwanie: zachowana historia liczników. Migracja po wymianie ECU według osobno uzgodnionej polityki. |
| Zapis i zasilanie | Zaniki w różnych fazach zapisu, powtarzane resety, uszkodzony lub starszy rekord: wynik zgodny z ustaloną polityką, bez cichego wyzerowania lub cofnięcia historii. |
| Obejścia ochrony | Próby przez firmware, debug i pamięć w uzgodnionym modelu zagrożeń; zweryfikować ograniczenia wersji użytkowej i odrębnych uprawnień inżynierskich. |

Stanowiska, przyrządy, granice zaliczenia, procedury i dowody zostaną przygotowane przed próbami. Powyższy plan nie jest gotową procedurą ani dowodem uzyskania odporności.
