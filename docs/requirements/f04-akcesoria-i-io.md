# F04 — akcesoria i dodatkowe I/O

Stan na 2026-11-24. **F04 aktywny po zamknięciu F03 w pytaniu 243.** Aktualny temat: klakson. Źródłem wymagań jest [rejestr SYS](../01-zakres-systemu.md); kolejność i warunki zamknięcia określa [proces](../00-proces-i-status.md).

## Zakres i kolejność

| Temat | Stan |
| --- | --- |
| Klakson po utracie HMI/CAN | Przyjęty SYS-236, odpowiedź A na pytanie 244. |
| Klakson po odzyskaniu łączności | Przyjęty SYS-237, odpowiedź A na pytanie 245: zwolnienie i nowe naciśnięcie. |
| Klakson po restarcie ECU | Przyjęty SYS-238, odpowiedź A na pytanie 246: zwolnienie i nowe naciśnięcie. |
| Klakson przy zwykłym wybudzeniu ze snu | Otwarty, pytanie 247. |
| Pozostałe stany akcesoriów | W kolejce w F04: start/restart ECU, powrót łączności i brakujące reguły wyjść. Zachowujemy przyjęte SYS-050–053 oraz SYS-081–091. |
| Dodatkowe I/O | W kolejce: konkretne zastosowania, potrzebne funkcje i liczba wejść/wyjść. Parametry elektryczne i stopnie mocy dobieramy w dalszych etapach. |

Klakson należy do przyjętego zakresu SYS-004. Obecność klaksonu 12 V w dokumentacji Bety jest potwierdzona w [analizie instrukcji i suplementu](../interfaces/beta-2015-analiza-dokumentacji.md). ECU steruje odbiornikiem, a HMI przekazuje polecenia kierowcy. Nie ustalono tu jeszcze pełnej obsługi przycisku ani wszystkich stanów po restarcie.

## Klakson po utracie HMI lub CAN

Brak łączności może uniemożliwić przekazanie polecenia wyłączenia. W odpowiedzi **A na pytanie 244** (2026-11-24) właściciel przyjął SYS-236: po potwierdzeniu utraty HMI/CAN ECU wyłącza aktywny klakson, lokalnie i bez komputera.

Zasada nie zmienia samodzielnej pracy silnika według SYS-046. Nie ustanawia nowego DTC; ponowne załączenie po powrocie łączności podlega SYS-237. Czas wykrycia utraty, kryteria ważności komunikacji i czas wyłączenia wymagają określenia w etapie 4 i procedury z etapu 5.

### Plan próby SYS-236

1. Na stanowisku rzeczywistego ECU i sprawnego toru klaksonu odtworzyć prawidłową komunikację HMI. Załączyć klakson zaakceptowanym poleceniem. Rejestrować komunikację, stan ECU i rzeczywiste napięcie/prąd wyjścia.
2. Osobno odtworzyć wyłączenie HMI, przerwę komunikacji CAN oraz zatrzymanie wymaganych komunikatów HMI przy pozostającym zasilaniu. Dla każdego przypadku potwierdzić lokalne rozpoznanie utraty i wyłączenie klaksonu według kryteriów projektu. Zmierzyć czas od potwierdzenia utraty do wyłączenia; granice liczbowe ustalić przed wykonaniem.
3. Powtórzyć bez sesji Windows oraz z symulowaną pracą i zatrzymaniem silnika. Wyłączenie klaksonu ma nie wymagać nowego polecenia z HMI lub PC; sama utrata HMI nie wyłącza sterowania silnikiem według SYS-046.
4. Sprawdzić utratę łączności przy już wyłączonym klaksonie i niezależne działanie istniejących zabezpieczeń wyjścia. Zachowanie po odzyskaniu łączności sprawdzić odrębnie według planu SYS-237. Wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

Plan wymaga procedury wykonawczej, stanowiska i kryteriów liczbowych. Nie ma wyników prób produktu.

## Klakson po odzyskaniu łączności

W odpowiedzi **A na pytanie 245** (2026-11-24) właściciel przyjął SYS-237: powrót HMI/CAN nie wznawia klaksonu wyłączonego po utracie łączności. Przy trzymanym przycisku klakson pozostaje wyłączony; ponowne użycie wymaga zwolnienia i nowego naciśnięcia.

ECU egzekwuje tę regułę na podstawie wiarygodnych danych HMI. Stany przycisku, rozpoznanie nowego naciśnięcia i odrzucanie wcześniejszych poleceń rozwiniemy w etapie 4. Ustalenie dotyczy odzyskania komunikacji po SYS-236; obsługę nadal trzymanego przycisku po restarcie ECU określa SYS-238.

### Plan próby SYS-237

1. Na stanowisku ECU–HMI załączyć klakson, przerwać łączność i potwierdzić wyłączenie według SYS-236. Trzymając przycisk, przywrócić prawidłową komunikację. Potwierdzić, że rzeczywiste wyjście pozostaje wyłączone mimo informacji o nadal naciśniętym przycisku.
2. Zwolnić przycisk, potwierdzić odebranie prawidłowego stanu zwolnienia i ponownie go nacisnąć. Przy spełnionych pozostałych warunkach potwierdzić załączenie klaksonu. Osobno odtworzyć powrót łączności z przyciskiem już zwolnionym.
3. Odtworzyć wcześniejsze polecenia załączenia oraz ponowną utratę i powrót łączności przed nowym naciśnięciem. Sprawdzić brak samoczynnego wznowienia i brak uznania powtarzanego stanu „naciśnięty” za nowe naciśnięcie. Szczegóły danych i kryteria ważności ustalić z protokołem przed wykonaniem.
4. Powtórzyć po utracie zasilania samego HMI oraz bez sesji Windows, przy aktywnych zabezpieczeniach wyjścia. Rejestrować CAN, stan kwalifikacji w ECU i rzeczywiste napięcie/prąd klaksonu. Wyniki powiązać z HW/FW i konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Klakson po restarcie ECU

W odpowiedzi **A na pytanie 246** (2026-11-24) właściciel przyjął SYS-238: po odzyskaniu gotowości ECU nie wznawia klaksonu na podstawie przycisku trzymanego od czasu sprzed restartu. Ponowne użycie wymaga zwolnienia i nowego naciśnięcia.

Reguła dotyczy obsługi poleceń użytkownika po restarcie. Nie rozstrzyga zwykłego wybudzenia ze snu ani pobudzeń diagnostycznych autotestu. Kwalifikację stanów przycisku i moment dopuszczenia poleceń opracujemy w etapie 4.

### Plan próby SYS-238

1. Na stanowisku ECU–HMI załączyć klakson i wywołać kontrolowany restart ECU, pozostawiając HMI działające oraz przycisk trzymany. Po odzyskaniu gotowości ECU i prawidłowej komunikacji potwierdzić brak zwykłego załączenia klaksonu ze starego stanu przycisku. Rejestrować komunikację, gotowość ECU i rzeczywiste napięcie/prąd wyjścia.
2. Zwolnić przycisk i nacisnąć go ponownie. Przy potwierdzonych stanach i spełnionych pozostałych warunkach potwierdzić dopuszczenie nowego użycia klaksonu. Osobno rozpocząć od zwolnionego przycisku i sprawdzić pierwsze nowe naciśnięcie po gotowości.
3. Powtórzyć dla reprezentatywnych przyczyn restartu objętych projektem oraz wcześniejszych poleceń załączenia odtwarzanych przez HMI. Po każdym restarcie potwierdzić tę samą kwalifikację; nie traktować ponownego komunikatu o nadal trzymanym przycisku jako nowego naciśnięcia.
4. Powtórzyć bez sesji Windows i z aktywną odrębną ochroną wyjścia. Zabezpieczenia nadal obowiązują. Próba nie zatwierdza pobudzeń diagnostycznych podczas uruchamiania ani zachowania przy zwykłym wybudzeniu. Przed wykonaniem ustalić kryteria, połączenia i sposób restartu; wyniki powiązać z HW/FW oraz konfiguracją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

To plan do rozwinięcia w procedurę; prób produktu jeszcze nie wykonano.

## Następna decyzja

**Pytanie 247:** system śpi prawidłowo, bez wcześniejszej blokady wymagającej nowego naciśnięcia. Kierowca naciska i trzyma klakson, wybudzając HMI/ECU według SYS-055. Czy po uzyskaniu gotowości dopuścić sygnał na tym samym przytrzymaniu, czy wymagać nowego naciśnięcia? Zwykłe wybudzenie odróżniamy od restartu SYS-238 i odzyskania łączności SYS-237.
