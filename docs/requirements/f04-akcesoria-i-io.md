# F04 — akcesoria i dodatkowe I/O

Stan na 2026-11-24. **F04 aktywny po zamknięciu F03 w pytaniu 243.** Aktualny temat: klakson. Źródłem wymagań jest [rejestr SYS](../01-zakres-systemu.md); kolejność i warunki zamknięcia określa [proces](../00-proces-i-status.md).

## Zakres i kolejność

| Temat | Stan |
| --- | --- |
| Klakson po utracie HMI/CAN | Przyjęty SYS-236, odpowiedź A na pytanie 244. |
| Klakson po odzyskaniu łączności | Otwarty, pytanie 245. |
| Pozostałe stany akcesoriów | W kolejce w F04: start/restart ECU, powrót łączności i brakujące reguły wyjść. Zachowujemy przyjęte SYS-050–053 oraz SYS-081–091. |
| Dodatkowe I/O | W kolejce: konkretne zastosowania, potrzebne funkcje i liczba wejść/wyjść. Parametry elektryczne i stopnie mocy dobieramy w dalszych etapach. |

Klakson należy do przyjętego zakresu SYS-004. Obecność klaksonu 12 V w dokumentacji Bety jest potwierdzona w [analizie instrukcji i suplementu](../interfaces/beta-2015-analiza-dokumentacji.md). ECU steruje odbiornikiem, a HMI przekazuje polecenia kierowcy. Nie ustalono tu jeszcze pełnej obsługi przycisku ani wszystkich stanów po restarcie.

## Klakson po utracie HMI lub CAN

Brak łączności może uniemożliwić przekazanie polecenia wyłączenia. W odpowiedzi **A na pytanie 244** (2026-11-24) właściciel przyjął SYS-236: po potwierdzeniu utraty HMI/CAN ECU wyłącza aktywny klakson, lokalnie i bez komputera.

Zasada nie zmienia samodzielnej pracy silnika według SYS-046. Nie ustala nowego DTC ani reguły ponownego załączenia po powrocie łączności. Czas wykrycia utraty, kryteria ważności komunikacji i czas wyłączenia wymagają określenia w etapie 4 i procedury z etapu 5.

### Plan próby SYS-236

1. Na stanowisku rzeczywistego ECU i sprawnego toru klaksonu odtworzyć prawidłową komunikację HMI. Załączyć klakson zaakceptowanym poleceniem. Rejestrować komunikację, stan ECU i rzeczywiste napięcie/prąd wyjścia.
2. Osobno odtworzyć wyłączenie HMI, przerwę komunikacji CAN oraz zatrzymanie wymaganych komunikatów HMI przy pozostającym zasilaniu. Dla każdego przypadku potwierdzić lokalne rozpoznanie utraty i wyłączenie klaksonu według kryteriów projektu. Zmierzyć czas od potwierdzenia utraty do wyłączenia; granice liczbowe ustalić przed wykonaniem.
3. Powtórzyć bez sesji Windows oraz z symulowaną pracą i zatrzymaniem silnika. Wyłączenie klaksonu ma nie wymagać nowego polecenia z HMI lub PC; sama utrata HMI nie wyłącza sterowania silnikiem według SYS-046.
4. Sprawdzić utratę łączności przy już wyłączonym klaksonie i niezależne działanie istniejących zabezpieczeń wyjścia. Próba nie potwierdza zachowania po odzyskaniu łączności — to osobny przypadek z pytania 245. Wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

Plan wymaga procedury wykonawczej, stanowiska i kryteriów liczbowych. Nie ma wyników prób produktu.

## Następna decyzja

**Pytanie 245:** co zrobić po odzyskaniu HMI/CAN, jeśli klakson wyłączono według SYS-236, a przycisk pozostaje trzymany? Do decyzji właściciela nie zakładamy samoczynnego wznowienia ani obowiązkowego nowego naciśnięcia. Pozostajemy przy klaksonie przed kolejnym tematem F04.
