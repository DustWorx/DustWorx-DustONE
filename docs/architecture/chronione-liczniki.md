# Chronione liczniki eksploatacyjne

Data: 2026-11-01. Status: zatwierdzony cel ochrony, zakres dwóch liczników i procedura producenta/serwisu; szczegóły, model zagrożeń i kryteria prób do opracowania. Podstawa: [SYS-074–077](../01-zakres-systemu.md), [ADR-007](../decisions/adr-007-chronione-liczniki.md).

## Uzgodnione zasady

- ECU jest źródłem całkowitych motogodzin i ODO. Naturalne naliczanie zmienia wartości; użytkownik końcowy nie może ich dowolnie ustawiać, korygować ani kasować. HMI i Windows odczytują dane ECU.
- Ochrona obejmuje również dostępne użytkownikowi protokoły, diagnostykę, development tool, reset ustawień, import konfiguracji, kasowanie DTC, aktualizację i odzyskiwanie urządzenia. Kopia map lub konfiguracji nie może służyć przywróceniu starszych sum.
- Motogodziny mają wynikać z potwierdzonej pracy silnika. Źródło i reguły naliczania ODO oraz dokładność obu liczników trzeba określić. Kasowalne liczniki A/B nie zostały przyjęte.
- Chroniona procedura producenta/serwisu umożliwia inicjalizację nowego ECU lub przeniesienie udokumentowanych wartości przy jego wymianie; każda operacja jest rejestrowana (SYS-077, odpowiedź A na pytanie 81 z 2026-11-01). Użytkownik końcowy pozostaje przy odczycie. Szczegóły procedury są otwarte.
- W trybie użytkowym ECU dopuszcza tylko firmware zatwierdzony przez producenta projektu. Twórcy zachowują dostęp do programowania i debugowania (SYS-078, [ADR-008](../decisions/adr-008-dostep-do-firmware-ecu.md), odpowiedź A na pytanie 82 z 2026-11-01). Uprawnienie rozwojowe nie może stanowić obejścia ochrony przez użytkownika końcowego; szczegóły jego autoryzacji pozostają otwarte.

## Wymagane analizy przed doborem sprzętu

1. Realizacja SYS-077: autoryzacja producenta/serwisu, wiarygodność udokumentowanych wartości oraz postępowanie przy niedostępnym lub uszkodzonym starym ECU. Do ustalenia: źródło i powód operacji, identyfikatory ECU, wartości przed/po, oznaczenie czasu i jego wiarygodność, tożsamość wykonawcy, ochrona i trwałość rejestru. Określić ponowienia i przerwanie zasilania/łączności, aby nie powstał nieodnotowany lub częściowy zapis. To lista do specyfikacji, nie zatwierdzony format rejestru ani ogólne uprawnienie do dowolnej korekty.
2. Model zagrożeń: interfejsy użytkownika, własny firmware, debug/programowanie, dostęp do pamięci i podmiana danych lub sygnałów pomiarowych. Granice odporności fizycznej wymagają uzgodnienia. Zakres dostępu użytkowego i rozwojowego określa SYS-078. Szczegóły autoryzacji i przejść między trybami wymagają projektu, bez automatycznego zatwierdzania trwałych blokad.
3. MCU, pamięć i cykl życia: izolacja danych i uprawnień, wiarygodność uruchamianego firmware/aktualizacji, integralność oraz wykrywanie nieuprawnionych zmian i odtwarzania starych zapisów. Samo zabezpieczenie pliku aktualizacji nie określa ochrony stanu liczników.
4. Zapis i zasilanie: zużycie pamięci, spójność przy zaniku napięcia, rozdzielczość trwałego zapisu i dozwolony błąd. Powtarzane wyłączanie nie może być pominiętą ścieżką obchodzenia naliczania. Uszkodzone dane nie mogą być bez informacji przedstawione jako wiarygodne zero.
5. Zależności pomiarowe: kalibracja wpływająca na naliczanie, np. obwód koła, oraz odróżnienie sygnałów rzeczywistych od symulacji. Samo połączenie PC nie oznacza, że silnik nie pracuje; polityka trybów testowych musi to uwzględnić.

Ważne komponenty i mechanizmy wybieramy wspólnie z właścicielem. Przykład dokumentacji producenta o ochronie pamięci, debugowaniu, rozruchu i interfejsach: [ST AN5156 — Software isolation](https://www.st.com/content/st_com/en/technical-documents/an5156-introduction-to-security-for-stm32-mcus-stmicroelectronics_asset/chunk-004-topic-an5156-dev-prot-software-isolation.html). Jest to materiał do analizy, nie wybór STM32 ani deklaracja odporności DustONE.

## Plan weryfikacji do uszczegółowienia

| Obszar | Próby / oczekiwane potwierdzenie |
| --- | --- |
| Naliczanie | Znany czas pracy i droga; dokładność w ustalonych warunkach. Oddzielić pracę silnika, postój, sen, sesję PC i dane symulowane. |
| Uprawnienia | Próby ustawienia, korekty i kasowania przez HMI, Windows i bezpośrednie interfejsy użytkownika, w tym development tool: brak nieuprawnionej zmiany. |
| Inicjalizacja i przenoszenie | Autoryzowana inicjalizacja nowego ECU i przeniesienie udokumentowanych wartości: zgodne sumy oraz zapis operacji. Próby bez uprawnienia: brak zmiany. Przerwanie i ponowienie procedury: spójność liczników i rejestru według uszczegółowionej polityki SYS-077. |
| Cykl życia | Reset ustawień, import konfiguracji, kasowanie DTC, ponowne uruchomienie, sen, wymiana HMI oraz aktualizacja/odzyskiwanie: zachowana historia liczników. Wymiana ECU korzysta z chronionej procedury SYS-077. |
| Zapis i zasilanie | Zaniki w różnych fazach zapisu, powtarzane resety, uszkodzony lub starszy rekord: wynik zgodny z ustaloną polityką, bez cichego wyzerowania lub cofnięcia historii. |
| Obejścia ochrony | Próby przez firmware, debug i pamięć w uzgodnionym modelu zagrożeń; zweryfikować ograniczenia wersji użytkowej i odrębnych uprawnień inżynierskich. |

Stanowiska, przyrządy, granice zaliczenia, procedury i dowody zostaną przygotowane przed próbami. Powyższy plan nie jest gotową procedurą ani dowodem uzyskania odporności.
