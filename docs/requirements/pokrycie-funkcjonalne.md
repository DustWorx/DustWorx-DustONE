# Mapa obszarów i otwartych tematów

Status: roboczy plan przeglądu, 2026-10-25. Źródłem treści wymagań pozostaje [zakres systemu](../01-zakres-systemu.md). Powiązania obejmują SYS-001–066, ale nie oznaczają kompletności funkcji ani ich weryfikacji. Ogólne wymaganie może potrzebować wielu wymagań szczegółowych. Poniższe pytania techniczne i tematy do oceny nie stanowią zatwierdzenia nowych funkcji.

## Obszary przeglądu

| Obszar | Powiązane wymagania | Otwarte tematy do analizy i decyzji |
| --- | --- | --- |
| Warianty i ograniczenia platformy | SYS-001, SYS-002, SYS-012, SYS-014, SYS-015, SYS-032, SYS-033, SYS-038, SYS-042 | Jednostki referencyjne, obroty i pozostałe granice pracy; zgodność zachowywanego osprzętu; wykonalność konwersji TPI na mieszankę. Zachować jawne wyłączenia funkcji. |
| Zapłon i synchronizacja | SYS-001, SYS-002, SYS-015 | Czujniki i znaczniki wału/wałka, rozpoznanie fazy i rozruch kopniakiem; obsługiwane rodzaje zapłonu, cewki, kanały, energia i czasy; utrata synchronizacji. |
| Paliwo i strategie silnikowe | SYS-007, SYS-012, SYS-015, SYS-028, SYS-029, SYS-030, SYS-031, SYS-033 | Liczba i typy wtryskiwaczy, parametry pompy; kryteria sterowania w stanach pracy silnika. Zakres regulacji biegu jałowego i dodatkowych strategii do oceny przed wyborem wymaganych wyjść i zasobów. |
| Konfiguracja i mapy | SYS-003, SYS-007, SYS-028, SYS-047 | Zawartość i osie map, zakresy ustawień, walidacja, przełączanie podczas pracy, warunki zapisu i zgodność konfiguracji z wariantem sprzętu/firmware. |
| Czujniki i dane wejściowe | SYS-014, SYS-029, SYS-030, SYS-031, SYS-041, SYS-044 | Typy sygnałów, liczba kanałów, zakresy, dokładność, filtracja i kalibracja; rozróżnienie braku opcjonalnego czujnika od uszkodzenia. |
| Zawór wydechowy 2T | SYS-034 | Napędy referencyjne, sterowanie, sprzężenie zwrotne, pozycje krańcowe, kalibracja i reakcje na usterki. |
| Rozruch, STOP i przewrócenie | SYS-037, SYS-039, SYS-040, SYS-048, SYS-049 | Interfejsy, warunki rozruchu i jego zakończenia, limity oraz ponowienie; kryteria przewrócenia/odblokowania i rzeczywiste działanie toru STOP. |
| Akcesoria i chłodzenie | SYS-004, SYS-043, SYS-044, SYS-050, SYS-051, SYS-052, SYS-053, SYS-060, SYS-061 | Podział kanałów, prądy i zabezpieczenia; stany początkowe i po restarcie; zachowanie klaksonu i wyjść dodatkowych przy braku CAN; progi, limity i diagnostyka wentylatora. |
| Zasilanie, wybudzanie i sen | SYS-013, SYS-054, SYS-055, SYS-056, SYS-057, SYS-058, SYS-059, SYS-062, SYS-063, SYS-064, SYS-065, SYS-066 | Zakres napięcia/prądów, pobór w śnie, czas gotowości i detekcja kopania; ochrona instalacji i budżet energii; topologia, czasy i wyścigi zdarzeń wybudzania/usypiania. |
| CAN i podział odpowiedzialności | SYS-005, SYS-016, SYS-046, SYS-047, SYS-052, SYS-053, SYS-063 | Protokół, identyfikacja urządzeń, aktualność żądań, potwierdzenia, timeouty, obciążenie magistrali i powrót po awarii; zgodność wersji. |
| HMI i licznik | SYS-008, SYS-016, SYS-017, SYS-018, SYS-023, SYS-055, SYS-062, SYS-064, SYS-066 | Ekran i przyciski, źródło prędkości i przebiegu, odczyt w warunkach enduro, priorytety ostrzeżeń, brak danych, ograniczenia edytora ekranów i prezentacja stanu po wybudzeniu. |
| Diagnostyka i trwałość danych | SYS-009, SYS-018, SYS-019, SYS-020, SYS-021, SYS-022, SYS-023, SYS-024, SYS-025, SYS-028, SYS-047 | Katalog DTC, detekcja i potwierdzenie ustąpienia; zawartość freeze frame, RTC, pełna pamięć, trwałość i spójność zapisów po zaniku zasilania; zachowanie przebiegu i map. |
| Windows, połączenie i narzędzia | SYS-006, SYS-007, SYS-008, SYS-009, SYS-010, SYS-011, SYS-025, SYS-026, SYS-027, SYS-057, SYS-058 | Interfejs i topologia, formaty danych, zapis/eksport, zgodność wersji, tryby pracy oraz warunki dopuszczenia i przerwania testów wyjść i wysyłania ramek CAN. |
| Aktualizacja i odzyskiwanie | SYS-010, SYS-027, SYS-056, SYS-057, SYS-058 | Bootloadery, identyfikacja obrazu, kolejność aktualizacji i zgodność ECU/HMI; odzyskanie po przerwaniu transmisji lub zasilania i dostęp do niesprawnego urządzenia. |
| Mechanika, PCB i instalacja | SYS-035, SYS-036, SYS-045 | Przestrzeń montażowa, obudowy, złącza, nowa wiązka, szczelność i warunki środowiskowe; parametry PCB i wykonania, ciepło, drgania i EMC. |
| Zachowanie przy uszkodzeniach | SYS-013, SYS-019, SYS-037, SYS-039, SYS-046, SYS-049, SYS-050, SYS-051, SYS-052, SYS-053, SYS-064, SYS-065, SYS-066 | Utrata/nieprawidłowe dane, restart procesora, watchdog, zwarcia/przerwy, niskie napięcie i zawieszenie HMI; reakcje i możliwość powrotu do pracy dla każdego bloku. |

## Jak używamy mapy

- Dla obszaru zapisujemy funkcje przyjęte, świadomie wyłączone i otwarte. Pytania wybieramy z luk oraz zależności, w pierwszej kolejności wpływających na wspólną PCB i interfejsy.
- Przeglądamy scenariusze normalne, graniczne, uszkodzenia i serwis oraz konfiguracje gaźnik bez TPS/z TPS, 2T/4T i docelowe TPI/TBI, zgodnie z macierzą wariantów. Osobno uwzględniamy brak opcjonalnego wyposażenia.
- Uzgodnienie zapisujemy w wymaganiu lub decyzji z identyfikowalnym źródłem. Dobór realizacji i kryteriów wykonuje się dalej dla każdego bloku; pytanie do właściciela jest jedną z metod uzupełnienia danych, obok analizy dokumentacji i pomiarów.
- Przed zamknięciem architektury i wydaniem PCB sprawdzamy każdą pozycję, jej wpływ na I/O i zasoby oraz pozostałe luki. Przed testami wymagania muszą być powiązane z metodą, kryteriami i procedurami według [zasad weryfikacji](../verification/README.md).

Aktualny stan: częściowe uzgodnienia we wszystkich powyższych obszarach; żaden wiersz nie oznacza zakończonego pełnego przeglądu. Szczegółowa macierz funkcja–wymaganie–realizacja–test i przegląd stosownych norm pozostają do przygotowania. Zmiany zakresu wymagają aktualizacji mapy i oceny wpływu.
