# ADR-009 — oświetlenie i oszczędzanie energii po zgaszeniu

Data: 2026-11-01; uzupełnienie: 2026-11-26. Status: zakres funkcjonalny wskazany przez właściciela; parametry i szczegółowe reguły otwarte.

## Decyzja i źródło

W odpowiedzi na pytanie 87 właściciel wybrał przejście z włączonych mijania/drogowych na przednie i tylne pozycyjne po zgaszeniu silnika. Przy zgaszonym silniku użytkownik może ponownie włączyć mijania lub drogowe z HMI. ECU ma na bieżąco nadzorować napięcie i przed uśpieniem wyłączać pozycyjne oraz zbędne odbiorniki włączone z HMI, gdy napięcie spadnie poniżej progu. Wymagania: [SYS-083–091](../01-zakres-systemu.md).

Uzasadnienie właściciela: ograniczyć rozładowanie akumulatora, zachowując możliwość świadomego użycia oświetlenia po zatrzymaniu silnika.

## Konsekwencje

Rozszerza to nadzór napięcia wymagany już dla wentylatora. Ustalić parametry profilu akumulatora, tor pomiarowy, próg, potwierdzenie spadku, priorytety i wartości powrotu. Listę odbiorników doprecyzowano w SYS-257. W odpowiedzi A na pytanie 88 właściciel zatwierdził odrzucanie żądań ponownego włączenia przez ECU i dodał komunikat HMI o wymaganym uruchomieniu silnika (SYS-085/086). W odpowiedzi A na pytanie 89 właściciel zatwierdził wyjście w normalnym użytkowaniu po potwierdzeniu pracy silnika i utrzymaniu napięcia powyżej progu powrotu przez ustalony czas; do tego momentu odcięcie pozostaje aktywne (SYS-087). Samo naciśnięcie START nie potwierdza pracy silnika.

W odpowiedzi na pytanie 90 właściciel wybrał powrót zależny od funkcji: mijania/drogowe i dodatkowe odbiorniki użytkownika pozostają wyłączone do nowego polecenia, a uzgodnione funkcje ochrony silnika, np. wentylator, działają automatycznie według bieżącej potrzeby i własnych zabezpieczeń (SYS-088/089). Ręczne wymuszenie wentylatora nie jest samo odtwarzane.

W odpowiedzi A na pytanie 91 właściciel dopuścił jawne wejście w tryb serwisowy, umożliwiający zwolnienie odcięcia bez pracy silnika przy stabilnym zasilaniu warsztatowym, do testów z Windows. Samo podłączenie PC nie zwalnia odcięcia, a zabezpieczenia wyjść pozostają aktywne (SYS-090). W odpowiedzi B na pytanie 92 właściciel dopuścił po potwierdzonej utracie sesji dokończenie rozpoczętego testu do wcześniejszego limitu, bez przyjmowania nowych testów; po zakończeniu wyjątek jest wycofywany (SYS-091). Zabezpieczenia pozostają nadrzędne. Uprawnienia, kwalifikacja zasilania, detekcja utraty i stany końcowe wyjść są otwarte.

[Analiza i plan weryfikacji](../architecture/oszczedzanie-energii.md) oddzielają ten zakres od rekomendacji histerezy, filtracji i nieustalonych parametrów i szczegółów trybu serwisowego. Lista odbiorników jest przyjęta w SYS-257. Parametrów liczbowych, mechanizmów i komponentów nie wybrano; działania na produkcie jeszcze nie potwierdzono.

## Doprecyzowanie listy odbiorników — F04

W odpowiedzi na pytanie 265 (2026-11-26) właściciel pozostawił światło hamowania i możliwość włączenia awaryjnych, wyłączając pojedynczy kierunek. Odpowiedź A na doprecyzowanie potwierdziła odcięcie klaksonu. SYS-257 zapisuje listę wraz z odcięciem świateł stałych i wszystkich trzech dodatkowych kanałów. Awaryjne są świadomym żądaniem wspólnego migania obu stron, nie automatycznym skutkiem oszczędzania. Zabezpieczenia oraz własne reguły wentylatora/HMI nadal obowiązują. [Lista i plan prób F04](../requirements/f04-akcesoria-i-io.md#odbiorniki-w-oszczędzaniu-energii). Podtrzymanie po utracie HMI/CAN przy ciągłej pracy przyjęto później w SYS-258; blokadę snu przyjęto w SYS-259, a OFF po restarcie przyjęto w SYS-260.

Odpowiedź A na pytanie 266 (2026-11-26) przyjmuje SYS-258: ECU podtrzymuje włączone awaryjne po utracie HMI/CAN przy nieprzerwanej pracy, także w oszczędzaniu. Zabezpieczenia i dopuszczone zasilanie pozostają nadrzędne. Decyzja nie rozstrzyga snu ani restartu. [Ustalenie i plan próby F04](../requirements/f04-akcesoria-i-io.md#awaryjne-po-utracie-hmican).

Odpowiedź A na pytanie 267 (2026-11-26) przyjmuje SYS-259: dostępne w oszczędzaniu awaryjne wstrzymują skoordynowany sen obu urządzeń na czas aktywnej obsługi, z zachowaniem ochrony. Po jej zakończeniu pozostają zwykłe warunki snu. [Ustalenie i plan próby](../requirements/f04-akcesoria-i-io.md#awaryjne-a-usypianie).

Odpowiedź B na pytanie 268 (2026-11-26) przyjmuje SYS-260: awaryjne pozostają OFF po restarcie programu i powrocie zasilania do nowego świadomego polecenia. Dawny ON i dane HMI nie odtwarzają ich ani blokady snu. Pozostałe warunki snu oraz ochrony nadal obowiązują. [Ustalenie i plan próby F04](../requirements/f04-akcesoria-i-io.md#awaryjne-po-restarcie-i-powrocie-zasilania).

Odpowiedź A na pytanie 270 (2026-11-26) przyjmuje SYS-262: przy braku innych blokad zwykłe mijania/drogowe, hamowanie i klakson gasną przed snem także przy utrzymanym wejściu. Dostępność światła hamowania w oszczędzaniu nie blokuje zwykłego snu; awaryjne zachowują osobną blokadę SYS-259. Po wybudzeniu obowiązują przyjęte reakcje i nowe polecenia. [Plan próby F04](../requirements/f04-akcesoria-i-io.md#plan-próby-sys-262).
