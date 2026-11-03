# Domknięcie zakresu funkcjonalnego

Stan na: 2026-11-03. Roboczy przegląd na podstawie [94 wymagań systemowych](../01-zakres-systemu.md), [mapy 17 obszarów](pokrycie-funkcjonalne.md) i [macierzy wariantów silnika](../architecture/macierz-wariantow-silnika.md). Źródłem zatwierdzonych funkcji pozostaje rejestr SYS i ADR.

## Ile pozostało

Do końcowego przeglądu zakresu grupujemy **8 pakietów F01–F08**, a następnie wykonujemy przegląd zamykający G0 z [ścieżki projektu](../00-proces-i-status.md). Każdy pakiet może zawierać kilka decyzji; liczba pakietów nie jest liczbą kolejnych pytań. Wiele funkcji wewnątrz pakietów jest już uzgodnionych.

Lista określa pozostałą pracę nad zamknięciem zakresu. Wskazanie tematu do przeglądu nie zatwierdza nowej funkcji ani nie oznacza gotowej realizacji.

## Pakiety do domknięcia

| Pakiet | Co sprawdzić i doprecyzować | Wynik pozwalający zamknąć pakiet |
| --- | --- | --- |
| F01 — Komplet funkcji silnikowych | Sprawdzić komplet wymaganych pomiarów i sterowania dla 2T/4T, gaźnika z/bez TPS i TPI/TBI, w tym IAC i power valve. Brakujące funkcje lub wyłączenia wymagają potwierdzenia na podstawie dokumentacji enduro. | Macierz funkcji dla wariantów i jawny zakres docelowej obsługi. |
| F02 — Mapy, konfiguracja i strojenie | Ustalić listę map w niezależnych zestawach oraz operacje dopuszczone przy pracującym silniku: edycję, przesyłanie, zapis i zmianę krytycznej konfiguracji. Maks. trzy kompletne, niezależne zestawy, ich przełączanie i strojenie na żywo są przyjęte (SYS-028/094). [Specyfikacja operacji](../interfaces/mapy-i-konfiguracja.md): warunki i utrwalanie pozostają otwarte. | Tabela operacji i warunków ich dopuszczenia. |
| F03 — Ochrona i reakcje na usterki | Domknąć zachowanie przy utracie istotnych pomiarów, problemach z zasilaniem i restarcie oraz reakcje chroniące silnik. Zachować uzgodnione STOP, rozruch, przewrócenie i działanie bez HMI/CAN. | Macierz sytuacja → reakcja → warunek powrotu. |
| F04 — Akcesoria i dodatkowe I/O | Określić zastosowania i potrzebną liczbę dodatkowych funkcji wejść/wyjść oraz brakujące zachowanie klaksonu i wyjść konfigurowalnych po utracie HMI/CAN lub restarcie. Prądy i stopnie mocy wyznaczymy w architekturze. | Zamknięta lista funkcji I/O i stanów odbiorników. |
| F05 — Funkcje i obsługa HMI | Potwierdzić minimalny zestaw danych/ekranów, obsługę menu i map przyciskami, priorytet ostrzeżeń oraz zasady ich prezentacji w ekranach użytkownika. Fizyczne przyciski i edytowalne ekrany są już przyjęte. | Opis ekranów, poleceń i scenariuszy obsługi. |
| F06 — Windows, serwis i development tool | Domknąć scenariusze konfiguracji, strojenia z pomiarami zewnętrznymi, importu/eksportu oraz dopuszczenia testów I/O i wysyłania CAN przy różnych stanach pojazdu. Podstawowy zakres narzędzi i zachowanie testu po utracie sesji są przyjęte. | Lista przypadków użycia i warunków wykonania poleceń. |
| F07 — Diagnostyka, aktualizacje i dostęp | Przejrzeć przyjęty rdzeń DTC/liczników i domknąć wyjątki użytkowe, odzyskiwanie po nieudanej aktualizacji, role twórcy/serwisu/użytkownika oraz politykę firmware HMI. Mechanizmy pamięci i ochrony dobierzemy później. | Reguły dostępu, utrzymania danych i odzyskiwania urządzeń. |
| F08 — Warunki użytkowania i cele działania | Przyjąć granice pracy podczas jazdy i cele użytkowe potrzebne do projektowania ECU/HMI. Postój 4 tygodnie przy −10°C…+40°C, minimum 3 Ah AGM / 2 Ah LiFePO4 oraz podstawowe warunki wodne są już ustalone. | Zestaw warunków pracy i celów do przypisania kryteriom testowym. |

## Jak zamykamy pakiet

Asystent przygotowuje krótką kartę: przyjęte wymagania, rzeczywiste luki, propozycje z uzasadnieniem, wpływ na ECU/HMI/Windows i przewidywaną weryfikację. Właściciel rozstrzyga pozostałe decyzje produktowe; pytania nadal zadajemy pojedynczo z propozycjami odpowiedzi. Nowe funkcje silnika/osprzętu poprzedzamy [weryfikacją zastosowania w enduro](weryfikacja-funkcji-enduro.md).

Pakiet zamykamy po zapisaniu decyzji lub jawnego wyłączenia, źródła oraz powiązanych wymagań. Techniczne niewiadome mają otrzymać miejsce rozstrzygnięcia w dalszym etapie i właściciela zadania. Nową lukę ujawnioną przez dokumentację lub pomiar zapisujemy z przyczyną i wpływem na zakres; aktualizujemy plan.

## Parametry należące do dalszego projektowania

Liczby wynikające z obliczeń i danych osprzętu rozwijamy w architekturze: zakresy elektryczne, prądy, czasy, rozdzielczości map, zasoby pamięci/procesorów, parametry CAN i formaty danych. Schematy, wartości elementów, zabezpieczenia, footprinty, złącza, warstwy i routing należą do kolejnych etapów projektu.

Asystent przygotowuje dane, obliczenia i propozycje. Ważne komponenty i istotne kompromisy wybieramy wspólnie, zgodnie z [modelem współpracy](../00-proces-i-status.md). Domknięcie funkcji może przebiegać równolegle z pierwszą architekturą i inwentaryzacją; parametry wpływające na dany blok muszą być ustalone przed jego zamrożeniem.

## Powiązanie z mapą 17 obszarów

| Obszar istniejącej mapy | Gdzie jest domykany |
| --- | --- |
| Warianty i ograniczenia platformy | F01; dobór modeli i dane OEM w etapach 3–4. |
| Zapłon i synchronizacja | F01/F03; parametry torów i zasoby w etapach 3–4. |
| Paliwo i strategie silnikowe | F01/F02; dane osprzętu i realizacja w etapach 3–4. |
| Konfiguracja i mapy | F02. |
| Czujniki i dane wejściowe | F01/F04; charakterystyki i tory pomiarowe w etapach 3–6. |
| Zawór wydechowy 2T | F01/F03; modele napędów i stopnie mocy w etapach 3–6. |
| Rozruch, STOP i przewrócenie | F03; przyjęte zasady zachowujemy, domykamy wyjątki. |
| Akcesoria i chłodzenie | F04/F03. |
| Zasilanie, wybudzanie i sen | Bazowe funkcje uzgodnione; przypadki brzegowe F03, cele działania F08, bilanse i sekwencje techniczne w etapie 4. |
| CAN i podział odpowiedzialności | Podział ECU/HMI uzgodniony; scenariusze F03/F06, protokół i parametry magistrali w etapie 4. |
| HMI i licznik | F05/F08. |
| Liczniki eksploatacyjne i ruch przedniego koła | F07; przyjęte funkcje zachowujemy, dokładność i realizacja w etapach 4–6. |
| Diagnostyka i trwałość danych | F07; katalog i organizacja zapisów w etapie 4. |
| Windows, połączenie i narzędzia | F06; interfejs fizyczny i formaty w etapie 4. |
| Aktualizacja i odzyskiwanie | F07. |
| Mechanika, PCB i instalacja | Cele użytkowe F08; pomiary, obudowy, złącza i layout w etapach 3/7/8. |
| Zachowanie przy uszkodzeniach | F03/F07. |

Stan: **F01 i F02 w opracowaniu**, F03–F08 oczekują przeglądu zamykającego. Dla F01 przygotowano [funkcje wariantów i pierwszy przydział zasobów](../architecture/macierz-wariantow-silnika.md); modele, parametry i zgodność pozostają otwarte. Dla F02 zapisano odpowiedzi A na pytania 101 i 102 w [ADR-011](../decisions/adr-011-strojenie-na-zywo.md). Żaden pakiet nie jest jeszcze zamknięty. Nie wyznaczono procentu kompletności; zakończenie etapu wynika z wyników pakietów i bramki G0.
