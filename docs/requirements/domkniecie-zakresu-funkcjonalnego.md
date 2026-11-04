# Domknięcie zakresu funkcjonalnego

Stan na: 2026-11-04. Roboczy przegląd na podstawie [98 wymagań systemowych](../01-zakres-systemu.md), [mapy 17 obszarów](pokrycie-funkcjonalne.md) i [macierzy wariantów silnika](../architecture/macierz-wariantow-silnika.md). Źródłem zatwierdzonych funkcji pozostaje rejestr SYS i ADR.

## Ile pozostało

Przegląd obejmuje **8 pakietów F01–F08**, a następnie G0. Po przeglądzie asystenta właściciel poprosił o kontrolę pełnego F01 przed przejściem do F02; F01 jest bieżącym pakietem kontroli z [ścieżki projektu](../00-proces-i-status.md). Każdy pakiet może zawierać kilka decyzji; liczba pakietów nie jest liczbą kolejnych pytań. Wiele funkcji wewnątrz pakietów jest już uzgodnionych.

Aktywny jest **F01 — kontrola ustaleń przez właściciela**. Wynik przeglądu asystenta z 2026-11-04 jest zachowany; F02 wrócił do kolejki na czas kontroli. Pakiety realizujemy kolejno **F01 → F02 → F03 → F04 → F05 → F06 → F07 → F08**, a następnie wykonujemy G0. Przechodzimy dalej po zapisanym zamknięciu bieżącego pakietu zgodnie z [procesem](../00-proces-i-status.md).

Lista określa pozostałą pracę nad zamknięciem zakresu. Wskazanie tematu do przeglądu nie zatwierdza nowej funkcji ani nie oznacza gotowej realizacji.

## Pakiety do domknięcia

| Pakiet | Status | Co sprawdzić i doprecyzować | Wynik pozwalający zamknąć pakiet |
| --- | --- | --- | --- |
| F01 — Komplet funkcji silnikowych | Aktywny | [Podsumowanie kontrolne](f01-podsumowanie-kontrolne.md): zakres, pomiary, sterowanie, wyłączenia i kwestie techniczne przekazane dalej. | Zakończona kontrola ustaleń właściciela, zapis uwag i spójny zakres. |
| F02 — Mapy, konfiguracja i strojenie | W kolejce | Ustalić listę map w niezależnych zestawach oraz operacje dopuszczone przy pracującym silniku: edycję, przesyłanie, zapis i zmianę krytycznej konfiguracji. Maks. trzy niezależne zestawy, przełączanie i strojenie na żywo są przyjęte (SYS-028/094). Trwały zapis tylko na jawne polecenie przy zgaszonym silniku (SYS-095). [Specyfikacja operacji](../interfaces/mapy-i-konfiguracja.md): po utracie Windows zastosowane wartości pozostają aktywne; ponowne połączenie, restart i pozostałe warunki otwarte. | Tabela operacji i warunków ich dopuszczenia. |
| F03 — Ochrona i reakcje na usterki | W kolejce | Domknąć zachowanie przy utracie istotnych pomiarów, problemach z zasilaniem i restarcie oraz reakcje chroniące silnik. Zachować uzgodnione STOP, rozruch, przewrócenie i działanie bez HMI/CAN. | Macierz sytuacja → reakcja → warunek powrotu. |
| F04 — Akcesoria i dodatkowe I/O | W kolejce | Określić zastosowania i potrzebną liczbę dodatkowych funkcji wejść/wyjść oraz brakujące zachowanie klaksonu i wyjść konfigurowalnych po utracie HMI/CAN lub restarcie. Prądy i stopnie mocy wyznaczymy w architekturze. | Zamknięta lista funkcji I/O i stanów odbiorników. |
| F05 — Funkcje i obsługa HMI | W kolejce | Potwierdzić minimalny zestaw danych/ekranów, obsługę menu i map przyciskami, priorytet ostrzeżeń oraz zasady ich prezentacji w ekranach użytkownika. Fizyczne przyciski i edytowalne ekrany są już przyjęte. | Opis ekranów, poleceń i scenariuszy obsługi. |
| F06 — Windows, serwis i development tool | W kolejce | Domknąć scenariusze konfiguracji, strojenia z pomiarami zewnętrznymi, importu/eksportu oraz dopuszczenia testów I/O i wysyłania CAN przy różnych stanach pojazdu. Podstawowy zakres narzędzi i zachowanie testu po utracie sesji są przyjęte. | Lista przypadków użycia i warunków wykonania poleceń. |
| F07 — Diagnostyka, aktualizacje i dostęp | W kolejce | Przejrzeć przyjęty rdzeń DTC/liczników i domknąć wyjątki użytkowe, odzyskiwanie po nieudanej aktualizacji, role twórcy/serwisu/użytkownika oraz politykę firmware HMI. Mechanizmy pamięci i ochrony dobierzemy później. | Reguły dostępu, utrzymania danych i odzyskiwania urządzeń. |
| F08 — Warunki użytkowania i cele działania | W kolejce | Przyjąć granice pracy podczas jazdy i cele użytkowe potrzebne do projektowania ECU/HMI. Postój 4 tygodnie przy −10°C…+40°C, minimum 3 Ah AGM / 2 Ah LiFePO4 oraz podstawowe warunki wodne są już ustalone. | Zestaw warunków pracy i celów do przypisania kryteriom testowym. |

## Kontrola F01 przed F02

Przegląd prowadzącego inżynierię z 2026-11-04 jest zapisany w kartach [pomiarów](f01-pomiary-silnika.md) i [sterowania](f01-sterowanie-silnikiem.md). Na prośbę właściciela wracamy do kontroli pełnego zakresu przed F02. [Podsumowanie kontrolne](f01-podsumowanie-kontrolne.md) zbiera ustalenia bez zmiany wymagań.

F02 oczekuje. Pytanie 108 nie otrzymało odpowiedzi o wyborze zestawu po restarcie; odpowiedź właściciela była poleceniem kontroli F01. Ewentualne korekty zakresu z tego przeglądu zapisujemy wraz z ich wpływem na dalsze etapy.

## Jak zamykamy pakiet

Asystent przygotowuje krótką kartę: przyjęte wymagania, rzeczywiste luki, propozycje z uzasadnieniem, wpływ na ECU/HMI/Windows i przewidywaną weryfikację. Właściciel rozstrzyga pozostałe decyzje produktowe; pytania nadal zadajemy pojedynczo z propozycjami odpowiedzi. Nowe funkcje silnika/osprzętu poprzedzamy [weryfikacją zastosowania w enduro](weryfikacja-funkcji-enduro.md).

Pakiet zamykamy po zapisaniu decyzji lub jawnego wyłączenia, źródła oraz powiązanych wymagań. Techniczne niewiadome mają otrzymać miejsce rozstrzygnięcia w dalszym etapie i właściciela zadania. Nową lukę ujawnioną przez dokumentację lub pomiar zapisujemy z przyczyną i wpływem na zakres; aktualizujemy plan.

## Parametry należące do dalszego projektowania

Liczby wynikające z obliczeń i danych osprzętu rozwijamy w architekturze: zakresy elektryczne, prądy, czasy, rozdzielczości map, zasoby pamięci/procesorów, parametry CAN i formaty danych. Schematy, wartości elementów, zabezpieczenia, footprinty, złącza, warstwy i routing należą do kolejnych etapów projektu.

Bieżący pakiet obejmuje dane i analizy potrzebne do rozstrzygnięcia jego zakresu. Wpływ na późniejsze etapy zapisujemy w ich dokumentach i kolejce. Inwentaryzację, architekturę, obliczenia i dobór części prowadzimy po dojściu do właściwego etapu. Ważne komponenty i kompromisy wybieramy wspólnie, zgodnie z [modelem współpracy](../00-proces-i-status.md).

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

Stan: **F01 aktywny w kontroli właściciela, F02–F08 w kolejce**; wcześniejszy wynik przeglądu F01 pozostaje zachowany. Decyzje map 101–104 pozostają zapisane w [ADR-011](../decisions/adr-011-strojenie-na-zywo.md). Etap 2 trwa do zamknięcia wszystkich pakietów i G0.
