# Weryfikacja

Miejsce na plan weryfikacji wymagań, opisy stanowisk, procedury oraz raporty z prób.

## Odpowiedzialność i pokrycie wymagań

Asystent prowadzący inżynierię przygotowuje plan, stanowiska, dobór przyrządów, procedury z konkretnymi połączeniami i ustawieniami, oczekiwane wyniki, tolerancje oraz warunki przerwania. Właściciel wykonuje próby fizyczne i przekazuje dane. Asystent analizuje wyniki, aktualizuje status wymagań, proponuje korekty i potrzebną regresję. Procedury przygotowujemy przed odpowiadającym im etapem prób.

Każde wymaganie otrzymuje metodę potwierdzenia i dowód. Metoda może obejmować test/pomiar, analizę lub inspekcję/przegląd. Funkcje i parametry użytkowe sprawdzamy na rzeczywistym ECU/HMI/aplikacji i odpowiednich konfiguracjach silnika. Analizy konstrukcji i symulacje uzupełniają te próby.

Macierz weryfikacji ma wiązać: ID wymagania i wariant, metodę, procedurę/etap, kryterium akceptacji, rewizję badanego produktu, wynik oraz dowód. Jedno wymaganie może wymagać wielu prób; jedna próba może pokrywać kilka wymagań. Uzgodnienie wymagania, obliczenie lub odczyt danych komponentu nie zastępują wymaganej próby systemu.

## Przygotowanie i wykonanie

Stosujemy [szablon procedury i zapisu wyniku](szablon-procedury-testowej.md). Procedura gotowa do wykonania zawiera potwierdzone punkty i warunki podłączenia, właściwe przyrządy, kroki, mierzalne granice zaliczenia i przerwania oraz sposób zapisu dowodów. Brakujące dane lub kryteria pozostawiają ją w statusie projektu.

Próby prowadzimy zgodnie z gotowością: analiza i przeglądy, uruchomienie bloków, testy stanowiskowe wejść/wyjść i usterek, integracja ECU–HMI–Windows, odpowiednie silniki/motocykle oraz potrzebne próby środowiskowe i EMC. Zakres tych ostatnich określimy z wymaganiami, bez deklarowania niepotwierdzonej zgodności.

Dla próby zapisujemy co najmniej: powiązane wymagania, badaną rewizję sprzętu i oprogramowania, warunki, kryterium zaliczenia, wynik i odsyłacze do dowodów. Przy zmianie projektu określamy wpływ na wymagania i dobieramy powtórzenia/regresję. Wymagania bez dowodów pozostają niezweryfikowane.

Beta 300 RR Racing 2015 jest pierwszą konfiguracją testową. Macierz wariantów musi także objąć gaźnik z TPS, 4T i docelowe TPI/TBI; potrzebują one osobnych stanowisk i jednostek. Brak dostępnej konfiguracji zapisujemy jako ograniczenie weryfikacji.

## Bieżący stan

Etap 5 oczekuje w kolejce zgodnie z [procesem](../00-proces-i-status.md). Poniższe plany i powiązania są zachowanymi materiałami wstępnymi; zapis wpływu bieżących decyzji nie rozpoczyna tego etapu.

Przygotowano [wstępny plan inwentaryzacji Bety Racing 2015](beta-2015-plan-inwentaryzacji.md) z listą dostępnych przyrządów: multimetr, Rigol DHO804, 4 sondy PVP3150 i 3 sondy P4100. Model multimetru i dokumentacja P4100 pozostają do określenia. Przy części wymagań są propozycje prób, a powyżej określono zasady i szablon. Przygotowano [pierwszy przydział 245 wymagań do bloków i 13 grup weryfikacji](macierz-wymagan.md). Kryteria liczbowe, konfiguracje, procedury wykonawcze i dowody wymagają rozwinięcia; nie ma raportów pomiarów ani prób produktu. Kod testów i dane wejściowe obejmujące wiele komponentów należą do `tests/`.

Przeanalizowano instrukcję i suplement dostarczone przez właściciela: [wyniki i braki danych](../interfaces/beta-2015-analiza-dokumentacji.md). Rozbieżność oznaczenia rocznika suplementu i wyposażenia TPS wymaga porównania z motocyklem; schemat nie jest jeszcze zweryfikowaną mapą jego złączy.

SYS-092 obejmuje osobne testy zgodności AGM i LiFePO4. [Plan prób zasilania](../architecture/akumulatory-agm-lifepo4-porownanie.md) wskazuje zakres do uszczegółowienia dla obu typów; próby Bety z AGM nie potwierdzają zgodności LiFePO4. Procedury wykonawcze i kryteria powstaną po ustaleniu modeli, granic i stanowisk.

SYS-093 wymaga potwierdzenia rezerwy na rozruch po minimum 4 tygodniach postoju bez doładowania. [Plan weryfikacji postoju](../architecture/budzet-energii-postoju.md) obejmuje pomiar całego poboru, bilans i próbę zestawu ECU/HMI z reprezentatywnymi akumulatorami AGM/LiFePO4. Dla Bety i konfiguracji z obiema metodami oceniamy rozruch kopniakiem, z zasilaniem ECU/osprzętu z akumulatora (odpowiedź B na pytanie 97). W motocyklach wyłącznie z rozrusznikiem elektrycznym po tym samym czasie wymagany jest rozruch elektryczny (odpowiedź A na pytanie 98). Otoczenie dla celu postoju/rozruchu wynosi od −10°C do +40°C (odpowiedź A na pytanie 99). Minimalne pojemności znamionowe wynoszą 3 Ah AGM i 2 Ah LiFePO4 (C10, odpowiedź A na pytanie 100). Stan początkowy, użyteczna pojemność, liczba/czas prób, stabilizacja cieplna i tolerancje pozostają do ustalenia; nie ma wyników prób.

Dla F03 przygotowano 79 planów prób SYS-157–235. [Karta przeglądu](../requirements/f03-przeglad-zakresu.md) podaje zakres, wynik kontroli spójności i odpowiedzialność za dalsze procedury oraz próby. Akceptacja funkcji nie zastępuje wyników produktu.

Dla SYS-236 w [F04](../requirements/f04-akcesoria-i-io.md#plan-próby-sys-236) przygotowano plan lokalnego wyłączenia klaksonu po utracie HMI/CAN. F03 zachowuje 79 planów; F04 zawiera obecnie 10 planów: SYS-236–245. To materiały do procedur, bez wyników produktu.

[Plan SYS-237](../requirements/f04-akcesoria-i-io.md#plan-próby-sys-237) obejmuje odzyskanie łączności przy trzymanym i zwolnionym przycisku klaksonu, wcześniejsze polecenia oraz dopuszczenie nowego naciśnięcia.

[Plan SYS-238](../requirements/f04-akcesoria-i-io.md#plan-próby-sys-238) obejmuje restart ECU z działającym HMI i trzymanym przyciskiem klaksonu oraz dopuszczenie użycia dopiero po zwolnieniu i nowym naciśnięciu.

[Plan SYS-239](../requirements/f04-akcesoria-i-io.md#plan-próby-sys-239) obejmuje naciśnięcie klaksonu wybudzające system i wymagane nowe użycie po zwolnieniu, bez odłożonego sygnału z pierwszego naciśnięcia.

[Plan SYS-240](../requirements/f04-akcesoria-i-io.md#plan-próby-sys-240) obejmuje brak samoczynnego dźwięku w autoteście, zakres dostępnych sprawdzeń bez dźwięku i świadome wywołanie próby dźwiękowej z zachowaniem zabezpieczeń.

[Plan SYS-241](../requirements/f04-akcesoria-i-io.md#plan-próby-sys-241) obejmuje zakres dodatkowych wyjść mocy: reprezentatywne oświetlenie i zewnętrzne akcesoria, po ustaleniu kanałów, parametrów i kryteriów.

[Plan SYS-242](../requirements/f04-akcesoria-i-io.md#plan-próby-sys-242) obejmuje trzy dodatkowe kanały, niezależność ich zwykłego sterowania i dopuszczone kombinacje obciążeń.

[Plan SYS-243](../requirements/f04-akcesoria-i-io.md#plan-próby-sys-243) obejmuje zachowanie stanów trzech dodatkowych kanałów po utracie HMI/CAN i nadrzędność zabezpieczeń oraz ochrony energii.

[Plan SYS-244](../requirements/f04-akcesoria-i-io.md#plan-próby-sys-244) obejmuje wyłączone dodatkowe kanały po nieplanowanym restarcie lub powrocie zasilania oraz nowe dopuszczone polecenie ich załączenia.

[Plan SYS-245](../requirements/f04-akcesoria-i-io.md#plan-próby-sys-245) obejmuje wyłączenie dodatkowych kanałów przed prawidłowym snem i pozostawienie ich wyłączonych po zwykłym wybudzeniu do nowego polecenia.
