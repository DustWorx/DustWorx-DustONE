# F04 — przegląd akcesoriów i dodatkowych I/O

Stan na 2026-11-26. **Karta gotowa do kontroli właściciela; F04 pozostaje aktywny.** Obejmuje SYS-236–262 i powiązane wcześniejsze funkcje. Ostatnią decyzję, A na pytanie 270, zapisano w SYS-262. Zamknięcie wymaga osobnej odpowiedzi na pytanie 271.

Źródła: [rejestr SYS](../01-zakres-systemu.md#2-wymagania-wynikające-z-opisu), [ustalenia i plany F04](f04-akcesoria-i-io.md), [proces](../00-proces-i-status.md). Karta podsumowuje te źródła; nie tworzy drugiego rejestru wymagań.

## Przyjęty zakres

| Obszar | Ustalenia | Podstawa |
| --- | --- | --- |
| Role i sterowanie | ECU wykonuje sterowanie lokalnie i jest właścicielem stanów; HMI przekazuje żądania i pokazuje rzeczywisty wynik. START i STOP pozostają niezależne od HMI. | SYS-016/037/046–048 |
| Światła podstawowe | Po uruchomieniu automatyczne przednie i tylne pozycyjne; mijania/drogowe z HMI. Po zatrzymaniu silnika włączone mijania/drogowe przechodzą na pozycyjne, z możliwością ponownego ręcznego włączenia. Przy ciągłej pracy utrata HMI zachowuje stan według SYS-050 z priorytetem automatyki i ochrony. Po restarcie przy zgaszonym silniku OFF do nowego polecenia. Zwykły sen wyłącza światła; po wybudzeniu wymagają nowego polecenia przy zgaszonym silniku. | SYS-050/081–088/250/262 |
| Światło hamowania | Osobne bezpośrednie wejścia obu hamulców; światło reaguje na ich bieżące stany bez HMI/CAN. Nowe użycie wybudza ECU i HMI, a działanie światła nie czeka na HMI. Przy braku innych blokad po bezczynności światło gaśnie przed snem także przy trzymanym hamulcu. Nowe użycie odnawia bezczynność; samo trzymanie nie odnawia jej stale ani nie wybudza ponownie. | SYS-051/256/262 |
| Pojedyncze kierunkowskazy | Miganie realizuje ECU. Utrata HMI/CAN wyłącza kierunek; powrót komunikacji, restart i wybudzenie nie odtwarzają dawnej strony. Przed snem wyłączenie, później nowy świadomy wybór. W oszczędzaniu pojedyncza strona jest niedostępna. | SYS-052/251–253/257 |
| Klakson | Utrata HMI/CAN wyłącza sygnał. Po powrocie łączności, restarcie oraz zwykłym wybudzeniu wymagane zwolnienie i nowe naciśnięcie. Pierwsze naciśnięcie wybudzające nie uruchamia dźwięku. Autotest bez samoczynnego dźwięku; próba dźwiękowa świadomie. Normalne puszczenie przycisku kończy sygnał. Oszczędzanie oraz zwykły sen odłączają klakson, także przy trzymaniu. | SYS-236–240/257/262 |
| Dodatkowe kanały | Trzy niezależnie sterowane kanały mocy do lamp i zasilania akcesoriów. ON/OFF i opcjonalny PWM zgodnych lamp; GPS/ładowarki w ON/OFF. Przy ciągłej pracy utrata HMI/CAN zachowuje stany. Restart oraz prawidłowy sen/wybudzenie: OFF do nowego polecenia. Lokalna usterka odcina tylko dany kanał przy prawidłowych warunkach pozostałych; wspólne zagrożenia pozostają nadrzędne. | SYS-241–246/249 |
| Próby po zwarciu/przeciążeniu | Dodatkowe kanały, podstawowe światła, kierunkowskazy i klakson bez automatycznych ponowień. Jedna świadoma ograniczona próba; po niepowodzeniu blokada kanału do pełnego cyklu prawidłowego snu i wybudzenia albo pełnego zaniku i powrotu zasilania. Reset programu i powrót CAN nie odnawiają limitu. Odnowienie nie włącza odbiornika ani nie kasuje historii DTC. | SYS-247/248/253 |
| Próba światła hamowania | Przy dostępnym wspólnym limicie, po zwolnieniu obu hamulców, nowe użycie któregokolwiek może zlecić próbę bez HMI. Trzymany hamulec, powrót CAN i samo odnowienie limitu nie zlecają próby. HMI/serwis nie omijają tego samego limitu. | SYS-254 |
| Oszczędzanie energii | Odcięte pozycyjne, mijania/drogowe, trzy dodatkowe kanały, pojedynczy kierunek i klakson. Światło hamowania i świadome awaryjne dostępne podczas pracy ECU w granicach ochrony. Zwykłe ON objętego odbiornika odrzucone; HMI pokazuje powód. Wyjście w normalnym użytkowaniu wymaga pracy silnika i napięcia powrotu przez przyjęty później czas. Ręczne odbiorniki nie wracają samoczynnie. | SYS-084–089/257 |
| Serwis i wentylator | Jawny wyjątek serwisowy wymaga stabilnego zasilania warsztatowego; samo PC nie zwalnia odcięcia. Po utracie sesji rozpoczęty test może dokończyć do pierwotnego limitu, bez nowych testów. Wentylator zachowuje własne reguły i zabezpieczenia z zamkniętego F03. Zasilanie HMI pozostaje według SYS-064–066. | SYS-060/061/064–066/089–091, F03 |
| Awaryjne | Świadome wspólne miganie obu stron, dostępne także w oszczędzaniu. Utrata HMI/CAN przy ciągłej pracy nie przerywa migania. Aktywny tryb blokuje skoordynowany sen ECU/HMI do wyłączenia lub właściwego ochronnego zakończenia. Po restarcie programu i powrocie zasilania OFF do nowego polecenia. Awaryjne mają pierwszeństwo: wybór strony odrzucony do ich świadomego wyłączenia i nowego wyboru. Dawna strona nie wraca. | SYS-257–261 |
| Zwykłe odbiorniki a sen | Przy zgaszonym silniku, braku PC i innych blokad ręczne mijania/drogowe oraz trzymany hamulec lub klakson nie blokują snu; ECU wyłącza je przed snem. Samo utrzymane wejście nie wybudza ponownie, wymagane zwolnienie i nowe użycie. Po wybudzeniu mijania/drogowe OFF do nowego polecenia; hamowanie według bieżących wejść po gotowości, klakson według zasady nowego naciśnięcia. | SYS-059/081/239/245/252/262 |
| Zewnętrzne porty | Każdy ma uzgodnione zastosowanie, bez dodatkowych portów/magistral do nieokreślonych urządzeń. Zachowane czujniki, osprzęt, trzy kanały mocy, CAN, PC oraz programowanie/debugowanie według ról. Wewnętrzne zasoby i punkty testowe do architektury. | SYS-255 |

## Przegląd spójności

| Powiązanie | Wynik |
| --- | --- |
| Oszczędzanie a sen | Dostępność hamowania w oszczędzaniu nie blokuje zwykłego snu; po bezczynności działa SYS-262. Awaryjne mają odrębną blokadę SYS-259. Wentylator, PC i inne zadania zachowują własne warunki. |
| Utrzymany sygnał a nowa aktywność | Nowe użycie hamulca odnawia bezczynność. Samo trzymanie nie odnawia jej stale i nie powoduje pętli ponownego wybudzania. Po wybudzeniu innym źródłem hamowanie znów odpowiada aktualnym wejściom po gotowości. |
| Nowe polecenie a stare dane HMI | Dawny ON, dawna strona, trzymany przycisk i ponowione wcześniejsze żądanie nie zastępują wymaganej nowej czynności. ECU jest źródłem stanu po odzyskaniu łączności. Dokładna kwalifikacja do protokołu. |
| Sen/restart a limit prób | Pełny prawidłowy cykl snu i wybudzenia lub pełny zanik/powrót zasilania odnawiają wyłącznie prawo opisane w SYS-248/253. Nie dowodzą naprawy i nie uruchamiają próby bez właściwego żądania. Reset programu nie odnawia limitu. |
| Autotest a wyjścia OFF | Autotest SYS-194 nie omija stanów OFF, ochrony i zakazu samoczynnych ponowień. Klakson nie wydaje samoczynnego dźwięku. Wentylator zachowuje odrębne zaakceptowane próby F03; reguły dodatkowych kanałów i podstawowych świateł są odrębne. |
| START a klakson | START przy zwykłym wybudzeniu może działać na tym samym przytrzymaniu według SYS-204. Klakson wymaga kolejnego naciśnięcia według SYS-239. Przenoszenie reguły jednego przycisku na drugi byłoby błędem. |

Po rozstrzygnięciu 270 przegląd przyjętego zakresu nie wskazał kolejnej decyzji funkcjonalnej blokującej kartę F04. Nowa potrzeba ujawniona danymi lub próbą podlega kontroli zmian. Parametry, fizyczna realizacja i kwalifikacja osprzętu pozostają w dalszych etapach.

## Weryfikacja i przekazanie

Dla SYS-236–262 przygotowano **27 planów prób/przeglądu** i przypisanie do bloków oraz grup w [macierzy weryfikacji](../verification/macierz-wymagan.md). Uzupełniają je wcześniejsze plany oświetlenia, snu i energii. Wszystkie wymagania pozostają niezweryfikowane na produkcie; brak wyników DustONE.

| Etap lub pakiet | Praca do wykonania |
| --- | --- |
| Etap 3 — dane osprzętu | Odbiorniki i dopuszczalne kombinacje lamp, prądy ciągłe/załączania/zablokowania, napięcia, wejścia hamulców, wymiary i jednoczesne obciążenia. Dane Bety oraz stanowisk dla pozostałego zakresu. |
| Etap 4 — architektura | Podział fizycznych kanałów, zasoby PWM, topologia i ochrona, izolacja usterek, bilans zasilania/ciepła, detekcja nowych zdarzeń przy utrzymanych wejściach, czasy/filtracja, kwalifikacja poleceń i sekwencje snu/resetu. Pobór aktywnych awaryjnych ocenić oddzielnie od 28 dni postoju w śnie. |
| Etap 5 — procedury | Liczbowe kryteria, wyposażenie i połączenia, warianty/rewizje, scenariusze stanów jednoczesnych, bezpieczne wymuszanie usterek oraz warunki przerwania. Procedura musi być gotowa przed daną próbą. |
| Etapy 6–8 — komponenty, schematy i PCB | Ważne układy wybieramy wspólnie. Asystent przygotowuje obwody, obliczenia, biblioteki i wymagania dla warstw/layoutu; właściciel wykonuje CAD w Fusion z przeglądami asystenta. Preferencja SmartFET nie jest wyborem konkretnego układu ani potwierdzeniem prądów lub topologii. |
| F05–F07 | Przypisanie i obsługa przycisków, stany/odmowy HMI, testy z Windows, protokół, katalog DTC i sesje serwisowe. Rozwijamy kolejno, zachowując przyjęte reguły ECU. |
| Etap 11 — produkt | Właściciel wykonuje przygotowane próby fizyczne; asystent opracowuje procedury, analizuje wyniki, wskazuje poprawki i regresję. Beta potwierdzi swoją konfigurację; pozostałe funkcje wymagają stanowisk i odpowiednich urządzeń. |

## Kontrola właściciela

**Oczekiwana odpowiedź na pytanie 271.** Akceptacja zamknie F04 wyłącznie w zakresie funkcji i pozwoli rozpocząć F05 — funkcje i obsługę HMI. Etap 2 i bramka G0 pozostają otwarte do zakończenia F05–F08. Schematy, BOM, PCB, implementacja i próby produktu wymagają dalszej pracy zgodnie z procesem.
