# F01 — przegląd pomiarów silnika

Stan na: 2026-11-04, po odpowiedzi A na pytanie 106. **F01 aktywny; zakres pomiarów w końcowym przeglądzie.** Uzgodnienie funkcji jest odrębne od późniejszego doboru czujników i potwierdzenia działania produktu.

## Przyjęte funkcje

| Funkcja | Podstawa | Status zakresu / dalsza praca |
| --- | --- | --- |
| Wał VR lub cyfrowy Hall | SYS-069 | Przyjęte; czujniki i dekodery w etapach 3–4. |
| Dodatkowa faza 4T, cyfrowy Hall | SYS-070 | Przyjęte, opcjonalne zależnie od konfiguracji. |
| TPS oraz wariant gaźnika bez TPS | SYS-014/038 | Przyjęte; parametry i wykorzystanie według konfiguracji. |
| Temperatura dolotu IAT | SYS-031 | Przyjęte; temperatura ECU jest osobnym pomiarem. |
| Temperatura płynu chłodzącego | SYS-044 | Przyjęte dla silników chłodzonych cieczą; zakres innych sposobów chłodzenia poniżej. |
| Ciśnienie atmosferyczne i temperatura ECU na PCB | SYS-030 | Przyjęte; ważne sensory wybierzemy wspólnie później. |
| MAP | SYS-096 | Zakres funkcji zamknięty po pytaniu 105. |
| Ciśnienie gazów w skrzyni korbowej 2T, CCPS | SYS-097 | Zakres funkcji zamknięty po pytaniu 106. |
| Wartość ciśnienia paliwa i binarne ciśnienie oleju | SYS-029 | Przyjęte; interfejsy według osprzętu. |
| Napięcie akumulatora | SYS-084/092 | Przyjęty nadzór i profile; wartości parametrów później. |

Pozostałe uzgodnione sygnały motocykla — m.in. koło, hamulce, sprzęgło, biegi, rezerwa i wykrywanie przewrócenia — zachowują swoje wymagania. Ich pozostałe reguły są przypisane do odpowiednich pakietów, bez rozpoczynania ich teraz. Zintegrowane tory lambda i EGT pozostają poza przyjętym zakresem.

## Ostatnia zidentyfikowana kwestia zakresu pomiarów

SYS-044 określa temperaturę płynu w silnikach chłodzonych cieczą. Nie ustalono, czy platforma obejmuje również silniki chłodzone powietrzem oraz odpowiedni dla nich pomiar temperatury silnika.

Potwierdzony przykład: **Honda XR400R MY2000**, jednocylindrowy 4T chłodzony powietrzem. [Dane producenta](https://global.honda/jp/news/2000/c000117d.html), tabela „2000 PRODUCTION RACE MACHINES — MAIN SPECIFICATIONS 2”, kolumna XR400R. Źródło potwierdza sposób chłodzenia; nie potwierdza fabrycznego czujnika temperatury głowicy.

Do decyzji właściciela: zakres ciecz + powietrze z odpowiednim pomiarem temperatury silnika, albo ograniczenie platformy do chłodzenia cieczą. Przy przyjęciu powietrza miejsce pomiaru, czujnik, zakres, charakterystyka, tor wejściowy i wykorzystanie ustalimy w późniejszych etapach. Nie zakładamy zgodności toru z każdym typem czujnika ani identycznych progów temperatury.

Po rozstrzygnięciu i sprawdzeniu spójności zapisujemy wynik przeglądu pomiarów, a następnie przechodzimy do przeglądu sterowania w tym samym F01. F02 i dalsze etapy pozostają w kolejce.
