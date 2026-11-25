# Zasady pracy

## Dokumentacja

- Dokumentację prowadzimy po polsku, krótko i rzeczowo, w Markdown UTF-8. Nazwy katalogów i plików: małe litery ASCII, słowa rozdzielane myślnikiem.
- Każdy temat ma jedno miejsce źródłowe. W innych dokumentach stosujemy odsyłacze.
- Rozróżniamy: wymaganie właściciela, propozycję, zatwierdzoną decyzję i informację do ustalenia. Nie przedstawiamy założeń jako faktów.
- Wymagania otrzymują trwałe identyfikatory, początkowo SYS-001 itd. Identyfikatorów nie zmieniamy ani nie używamy ponownie po wycofaniu wymagania.
- Istotne decyzje zapisujemy w `docs/decisions/`, z uzasadnieniem i skutkami. Zatwierdzenie wymaga wskazania faktycznego potwierdzenia właściciela projektu.
- Wersję roboczą oznaczamy jako roboczą. Nie dopisujemy „final”, „final2” ani numerów kopii do nazw; historię zapewnia Git.
- Normy i rozbudowane elementy procesu wprowadzamy, gdy wynikają z zastosowania produktu lub dają konkretną wartość. Nie deklarujemy zgodności bez podstaw i weryfikacji.

## Kolejność pracy

Ustalenie właściciela z 2026-11-04: etapy i pakiety prowadzimy kolejno, zamykając bieżący przed następnym. Aktywny jest jeden pakiet; wpływ na dalszy etap zapisujemy w jego kolejce. Aktualną kolejność, kryteria zamknięcia i status utrzymujemy w [dokumencie procesowym](docs/00-proces-i-status.md).

Pytanie z propozycjami poprzedzamy krótkim wyjaśnieniem problemu i uzasadnieniem rekomendacji według [sposobu przedstawiania pytań](docs/00-proces-i-status.md#sposób-przedstawiania-pytań).

## Zmiany w repozytorium

`main` przechowuje aktualną, spójną dokumentację i pliki projektu. Dokument roboczy może tam trafić z jawnym statusem, propozycjami i otwartymi parametrami. Publikacja ustaleń przez PR jest odrębna od zatwierdzenia zamknięcia pakietu lub etapu przez właściciela.

### Gałęzie tematyczne

| Obszar zmiany | Wzorzec gałęzi | Miejsce plików |
| --- | --- | --- |
| Dokumentacja i uzgodnienia | `docs/<pakiet>-<temat>`, np. `docs/f03-diagnostyka-ogranicznika` | Odpowiedni podkatalog `docs/`; indeksy i opisy komponentów aktualizowane razem. |
| Elektronika | `hardware/<urzadzenie>-<temat>` | `hardware/ecu/` lub `hardware/hmi/`. |
| Firmware | `firmware/<urzadzenie>-<temat>` | `firmware/ecu/` lub `firmware/hmi/`. |
| Aplikacja Windows | `software/windows-<temat>` | `software/windows/`. |
| Mechanika | `mechanical/<temat>` | `mechanical/`. |
| Testy i narzędzia | `tests/<temat>` lub `tools/<temat>` | `tests/`, `tools/` lub testy przy danym komponencie. |

### Publikacja i porządkowanie

1. Zakładamy krótką gałąź z aktualnego `main` dla jednej spójnej porcji pracy. Nazwa opisuje temat; aktywny pakiet może mieć kilka kolejnych PR-ów.
2. W tej samej zmianie aktualizujemy wymagania, odpowiednie decyzje/interfejsy, plan weryfikacji i status procesu. Każdy temat zachowuje jedno miejsce źródłowe; pozostałe dokumenty odsyłają do niego.
3. PR opisuje wynik, otwarte kwestie i wykonane sprawdzenia. Draft służy przygotowaniu konkretnej zmiany; oczekiwanie na zamknięcie całego aktywnego pakietu nie jest powodem utrzymywania gotowego PR-u w drafcie.
4. Po przeglądzie i odpowiednich sprawdzeniach scalamy spójną porcję do `main`. Według zgody właściciela z 2026-11-25 asystent samodzielnie scala sprawdzone PR-y dokumentujące przyjęte ustalenia. Aktywny pakiet może nadal trwać; decyzje projektowe i jego formalne zamknięcie nadal zatwierdza właściciel.
5. Po potwierdzeniu scalenia i zachowania commitów w historii usuwamy zakończoną gałąź tematyczną. Historię i uzasadnienie zachowuje PR. Kolejny temat zaczynamy w nowej gałęzi.
6. Przed zapisem lub usunięciem gałęzi sprawdzamy aktualny stan. Aktywne PR-y i zmiany nieobecne w `main` pozostają do osobnego rozpatrzenia.

Zasady doprecyzował właściciel 2026-11-24 przy porządkowaniu repozytorium i 2026-11-25 przy zgodzie na samodzielne scalanie sprawdzonej dokumentacji. Sekwencja etapów i formalne warunki ich zamknięcia pozostają w [dokumencie procesowym](docs/00-proces-i-status.md).

## Pliki źródłowe i wyniki

- Pliki edytowalne są źródłem projektu. PDF, obrazy i pliki produkcyjne są eksportami powiązanymi z konkretną rewizją.
- Wyniki kompilacji publikujemy jako zasoby wydań GitHub, gdy powstanie proces wydawniczy. Nie przechowujemy ich jako kolejnych kopii w katalogach źródłowych.
- Nie dodajemy haseł, kluczy, danych dostępowych, prywatnych logów ani dokumentów bez prawa do ich publikacji.
- Testy jednostkowe przechowujemy przy danym komponencie; testy obejmujące współpracę urządzeń w `tests/`.
- Materiały lokalnego katalogu `sources/` są referencjami tylko do odczytu; nie kopiujemy ich automatycznie do repozytorium.
