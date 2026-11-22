# DustONE — ścieżka projektu, status i odpowiedzialności

Stan na 2026-11-22. Zamknięcie F02 i aktualna praca w F03 są w tabeli bieżącej pracy. Ścieżka projektu i warunki postoju z PR #17/#18 są scalone. Dokument aktualizujemy przy istotnej odpowiedzi lub decyzji, wykonanej pracy, wyniku próby, zmianie zakresu i przeglądzie etapu; wraz z wymaganiami, ADR, interfejsami i weryfikacją.

Kontrola pełnego F01 została zakończona: właściciel potwierdził zgodność podsumowania i polecił dalszą pracę (2026-11-04). Źródło kontroli: [przyjęte podsumowanie F01](requirements/f01-podsumowanie-kontrolne.md). Potwierdzenie dotyczy F01. Późniejsza odpowiedź A na pytanie 108 określiła ostatnio wybrany prawidłowy zestaw po restarcie ECU (SYS-099).

## Aktualne miejsce w procesie

**Aktywny etap 2 — zakres funkcjonalny. F01 i F02 zamknięto po kontroli właściciela. Aktywny jest F03 — ochrona i reakcje na usterki.** F04–F08 i etapy 3–12 oczekują w kolejce. Wcześniejsze wymagania, decyzje i materiały robocze pozostają zachowane; nie oznaczają formalnego rozpoczęcia ani zamknięcia dalszych etapów.

| Obszar | Stan potwierdzony dokumentacją |
| --- | --- |
| Wymagania systemowe | 228 wymagań SYS-001–228; pierwszy przydział do bloków i grup weryfikacji gotowy, kryteria i procedury do rozwinięcia. |
| Decyzje | 12 zapisów ADR-001–012; ostatni ogranicza platformę do silników chłodzonych cieczą. |
| Zakres wariantów | Macierz 6 wariantów silnika; jest planem obsługi, nie potwierdzeniem zgodności modeli. |
| Pierwsza jednostka | Beta 300 RR Racing 2015; analiza dokumentów i zdjęć, bez raportów pomiarowych instalacji. |
| Architektura | Pierwszy diagram blokowy, funkcje sześciu wariantów i przydział zasobów gotowe jako wersje robocze. Modele, parametry i liczbowe bilanse pozostają otwarte. |
| Schematy, BOM, PCB i mechanika | W repozytorium brak projektu wykonawczego i zatwierdzonego kompletnego BOM ECU/HMI. |
| Kod i próby produktu | W repozytorium brak implementacji firmware/Windows i raportów prób DustONE. Istnieją plany, szablon procedury i przydział 228 wymagań do 13 grup weryfikacji. |

Podstawy: [wymagania](requirements/README.md), [decyzje](decisions/README.md), [macierz silników](architecture/macierz-wariantow-silnika.md), [I/O](interfaces/wstepna-lista-io.md) i [weryfikacja](verification/README.md). Liczba wymagań i pytań nie jest procentem wykonania produktu.

## Etapy i warunki zakończenia

Ustalenie właściciela z 2026-11-04: **prowadzimy etapy i tematy kolejno, zamykając bieżący przed rozpoczęciem następnego**. Obowiązuje kolejność etapów 1–12, a w etapie 2: F01 → F02 → F03 → F04 → F05 → F06 → F07 → F08 → G0.

- W danym momencie aktywny jest jeden pakiet. Kolejny rozpoczynamy po spełnieniu kryteriów zakończenia i zapisaniu wyniku poprzedniego.
- Wpływ bieżącej decyzji na dalszy etap zapisujemy w odpowiednim dokumencie i kolejce; nie rozpoczynamy z tego powodu jego projektowania.
- Analiza źródeł potrzebna do określenia bieżącej funkcji należy do tego pakietu. Parametry, obliczenia i wykonanie rozwijamy na przypisanym późniejszym etapie.
- Zamknięcie zapisujemy z datą, rezultatem, podstawą decyzji i jawnymi danymi przekazanymi dalej. Nierozstrzygnięta decyzja o zakresie nie staje się zamknięta przez przeniesienie do kolejki.
- Gdy późniejsze ustalenie wymaga korekty zamkniętego wyniku, zapisujemy przyczynę i jawnie wracamy do tego miejsca, bez równoległego prowadzenia obu tematów.

Statusy: **aktywny**, **w kolejce**, **zamknięty**. Istniejący szkic oznaczamy osobno jako materiał wstępny; nie nadaje on statusu zamknięcia etapu. Zatwierdzenie wymagania i potwierdzenie działania produktu pozostają odrębnymi stanami.

| Etap | Główny rezultat | Bieżący status | Warunek zakończenia / przejścia |
| --- | --- | --- | --- |
| 1. Organizacja | Repozytorium, struktura, zasady zmian i decyzji. | Zamknięty: 2026-11-04. Dokumentację utrzymujemy. | Uzgodnienia i źródła mają miejsce w repozytorium, zmiany są wersjonowane. |
| 2. Zakres funkcjonalny | Funkcje, wyłączenia, warianty i reguły użytkowania ECU/HMI/Windows. | F01 i F02 zamknięte. F03 aktywny, F04–F08 w kolejce. | G0: przyjęta baza zakresu, rozstrzygnięte decyzje produktowe i jawne otwarte parametry techniczne. |
| 3. Inwentaryzacja i dane | Osprzęt, sygnały, obciążenia, zasilanie i przestrzeń montażowa. | W kolejce po G0; istnieją dokumenty/zdjęcia i plan INV, bez wyników pomiarów. | Dane wystarczają do projektowania odpowiedniego bloku; braki innych wariantów mają plan pozyskania. |
| 4. Architektura | Diagramy blokowe, I/O dla wariantów, zasoby, zasilanie, interfejsy i stany awaryjne. | W kolejce po etapie 3; zachowane wstępne szkice diagramu i zasobów. | G1: uzasadniony podział bloków, bilanse, granice interfejsów i zamknięte niewiadome wpływające na projektowane bloki. |
| 5. Plan weryfikacji | Powiązanie wymaganie → blok → metoda → kryterium → próba → dowód. | W kolejce po etapie 4; zachowane szablon i wstępny przydział wymagań. | Wymagania mają przydzieloną metodę i etap; procedura wykonawcza jest gotowa przed daną próbą. |
| 6. Komponenty i schematy | Wspólny wybór ważnych części, obliczenia, biblioteki, schematy i BOM. | W kolejce; brak projektu wykonawczego. | Przyjęte części, zweryfikowane symbole/footprinty, obliczenia i przegląd schematów/ERC. |
| 7. Mechanika i instalacja | Obudowy, mocowania, uszczelnienia, złącza i nowa wiązka. | W kolejce; zapisane wstępne potrzeby. | Zgodność z miejscem montażu, dostępem, złączami, ciepłem i wymaganiami środowiskowymi. |
| 8. PCB w Fusion | Warstwy, rozmieszczenie, routing, zasilanie/masy i eksporty produkcyjne. | W kolejce; CAD wykona właściciel przy wsparciu asystenta. | G2: przegląd schematu/BOM/bibliotek, ERC/DRC, mechaniki i planu uruchomienia; gotowy komplet do wykonania. |
| 9. Firmware i Windows | Sterowanie, CAN, HMI, mapy, diagnostyka, aktualizacja i narzędzia. | W kolejce; brak kodu w repozytorium. | Funkcje i interfejsy zaimplementowane oraz sprawdzone na właściwym poziomie. |
| 10. Prototypy i uruchomienie | PCB, montaż, kontrola wykonania i uruchamianie blokami. | W kolejce; nie rozpoczęto. | G3: podstawowe zasilanie, komunikacja i I/O sprawdzone według procedur; gotowość do prób systemowych. |
| 11. Weryfikacja i walidacja | Testy bloków i systemu, stanowiska, motocykle oraz dobrane próby środowiskowe/EMC. | W kolejce; brak wyników produktu. | Dowody dla przyjętego zakresu i konfiguracji, zarejestrowane niezgodności oraz ograniczenia. |
| 12. Korekty i wydanie prototypu | Poprawki, regresja, instrukcje i wersjonowany zakres działania. | W kolejce; nie rozpoczęto. | G4: przegląd wyników, potwierdzone konfiguracje, komplet wersji i jawne ograniczenia wydania. |

Projekt wspólnej PCB obejmuje docelowy uzgodniony zakres 2T/4T bez zmian obsady. Uruchamianie i firmware rozwijamy etapami od Bety; pozostałe warianty wymagają własnych analiz, stanowisk i prób.

## Co pozostało w funkcjonalności

**F01 i F02 zamknięte. Pozostaje sześć pakietów F03–F08** oraz przegląd zamykający G0. Ich treść i wynik wymagany do zamknięcia opisuje [rejestr domknięcia zakresu](requirements/domkniecie-zakresu-funkcjonalnego.md). Pakiet może zawierać kilka decyzji; część jego funkcji jest już uzgodniona. Jest to roboczy plan domknięcia obecnego zakresu, aktualizowany przy ujawnieniu nowych luk.

Parametry wyliczane z osprzętu, charakterystyki czujników, wartości elementów, konkretne procesory i układy, formaty CAN oraz layout rozwijamy w odpowiednich etapach architektury i projektu wykonawczego. Ważne komponenty nadal wybieramy wspólnie.

## Bieżąca praca i kolejka

| Zadanie | Status | Materiał / warunek podjęcia |
| --- | --- | --- |
| W04 — Zakres funkcjonalny: F01 | Zamknięty po kontroli właściciela: 2026-11-04. | [Pomiary](requirements/f01-pomiary-silnika.md), [przegląd sterowania i wynik zamknięcia](requirements/f01-sterowanie-silnikiem.md); dane techniczne przekazane do kolejki etapów 3–6. |
| F02 — Mapy, konfiguracja i strojenie ECU | Zamknięty po akceptacji właściciela 2026-11-09. | Odpowiedź A na pytanie 166. [Karta F02](requirements/f02-przeglad-zakresu.md) zawiera przyjęty zakres, plan weryfikacji i przekazanie. |
| F03 — Ochrona i reakcje na usterki | Aktywny po zamknięciu F02. | Uzgodniono reakcje na utratę synchronizacji wału (SYS-157–159), przewodowe START i STOP (SYS-160–168), odcięcie, restart i diagnostykę po zawieszeniu (SYS-169–172) oraz limity i odzyskiwanie (SYS-173–180). Przyjęto reakcje na zanik zasilania podczas pracy silnika oraz rozruchu elektrycznego i kopniakiem (SYS-181–183). Przy usterce pomiaru temperatury płynu ECU zapisuje DTC, wymusza włączenie wentylatora podczas pracy silnika i kończy to wymuszenie po potwierdzeniu zatrzymania (SYS-184–185). Przy zgaszonym silniku i potwierdzonej usterce ECU dopuszcza ręczne włączenie z HMI z limitami i zabezpieczeniami (SYS-186). Jeżeli usterka zostanie potwierdzona w trakcie automatycznego chłodzenia po zgaszeniu, ECU kończy to chłodzenie (SYS-187). Po odzyskaniu wiarygodnego pomiaru chłodzenie może wrócić przy odpowiedniej temperaturze i napięciu, w granicach pierwotnego limitu (SYS-188). Przy potwierdzonym przegrzaniu z wiarygodnego pomiaru HMI ostrzega kierowcę, który decyduje o zatrzymaniu silnika (SYS-189). Potwierdzone przeciążenie skutkujące odłączeniem wentylatora powoduje zapis DTC z zamrożoną ramką i ostrzeżenie na HMI także przed przegrzaniem (SYS-190). Próba na potwierdzenie z HMI obejmuje pomiar prądu i odblokowuje zwykłe sterowanie dopiero po potwierdzeniu sprawności (SYS-191–192). ECU zachowuje usterkę i blokadę przez sen. Po każdym wybudzeniu automatycznie sprawdza wyposażony wentylator i przywraca sterowanie po pozytywnej próbie (SYS-193). Autotest obejmuje funkcje skonfigurowane w danym motocyklu (SYS-194). Odłożoną próbę wentylatora ECU wykonuje automatycznie po powrocie warunków w tym samym okresie wybudzenia (SYS-195). Po nieudanej próbie wentylatora każde następne wybudzenie dopuszcza jedną nową próbę automatyczną przy właściwych warunkach (SYS-196). Po postawieniu przewróconego motocykla rozruch elektryczny wymaga nowego naciśnięcia START, jeśli wcześniejsze naciśnięcie nastąpiło przed potwierdzeniem postawienia (SYS-197). Usterka toru wykrywania przewrócenia podczas pracy silnika bez aktywnej blokady skutkuje dalszą pracą, zapisem DTC z zamrożoną ramką i ostrzeżeniem na HMI (SYS-198). Przy nieaktywnej blokadzie po upadku usterka toru wykrywania przewrócenia dopuszcza świadomy rozruch przy pozostałych spełnionych warunkach i wywołuje ostrzeżenie na HMI (SYS-199). Potwierdzona usterka toru zwalnia aktywną blokadę po przewróceniu i wywołuje ostrzeżenie. Rozruch wymaga nowej świadomej próby i spełnienia pozostałych warunków (SYS-200). Po odzyskaniu wiarygodnego pomiaru ECU przywraca wykrywanie przewrócenia jeszcze podczas bieżącej pracy silnika (SYS-201). Po wybudzeniu ECU ustala blokadę na podstawie aktualnej oceny położenia. Przy sprawnym torze i poprawnym położeniu ocena mieści się w czasie przygotowania ECU do rozruchu (SYS-202). Przed rozruchem ECU kończy wszystkie próby autotestu wykonalne w aktualnych warunkach przy zgaszonym silniku; pozostałe czekają na właściwe warunki (SYS-203). [Macierz reakcji F03](requirements/f03-ochrona-i-usterki.md). Przy zwykłym wybudzeniu trzymany START uruchamia rozrusznik po zakończeniu wymaganych prób i spełnieniu warunków, z zachowaniem nadrzędnych reguł nowej próby po odcięciach (SYS-204). W 4T o stałych fazach zanik impulsów czujnika fazy po synchronizacji pozwala kontynuować pracę z DTC przy wiarygodnym cyklu 720° i sygnale wału (SYS-205). Nowe uruchomienie profilu wykorzystującego czujnik fazy wymaga prawidłowego sygnału fazy i rozpoznania cyklu 720°; rozrusznik umożliwia sprawdzenie sygnału podczas obrotu w ramach istniejących limitów (SYS-206). Potwierdzona niezgodność fazy z wałem podczas pracy powoduje odcięcie zapłonu i wtrysku; wznowienie wymaga zatrzymania wału, nowej świadomej próby i prawidłowej synchronizacji (SYS-207). Reakcje dla opisanych przypadków wału i fazy są uzgodnione; parametry i kryteria dekoderów pozostają do projektu. Przy usterce IAT dopuszczono dalszą pracę i nowy rozruch na osobno zweryfikowanych strategiach zastępczych, z możliwością pomocniczego użycia temperatury ECU, trybem „Standard” i DTC (SYS-208). Po odzyskaniu wiarygodnego IAT ECU automatycznie wraca do pomiaru w bieżącej pracy, z przejściem zweryfikowanym dla profilu (SYS-209). Przy usterce barometru ECU dopuszcza dalszą pracę i rozruchy, wyłącza kompensację opartą na bieżącym pomiarze i używa stałej awaryjnej wartości ciśnienia określonej w oprogramowaniu (SYS-210). Po potwierdzeniu odzyskanej wiarygodności barometru ECU automatycznie wraca do pomiaru i kompensacji podczas bieżącej pracy, z przejściem zweryfikowanym dla profilu (SYS-211). Przy usterce ECT wtrysk dopuszcza dalszą pracę i rozruch na osobno zweryfikowanych strategiach profilu; bez właściwej strategii obowiązuje kontrolowane zatrzymanie albo blokada rozruchu (SYS-212). Po odzyskaniu wiarygodnego ECT korekty dawkowania automatycznie wracają do pomiaru w bieżącej pracy, z przejściem zweryfikowanym dla profilu (SYS-213). Przy usterce pomiaru ciśnienia paliwa przyjęto dalszą pracę i rozruchy na zweryfikowanej strategii profilu (SYS-214). Przyjęto zasadę normalnego sterowania pompą i nominalnych parametrów ciśnienia dla zgodnych układów; pozostałe profile wymagają osobnej strategii (SYS-215). Po odzyskaniu wiarygodnego pomiaru ciśnienia paliwa i warunków normalnej pracy ECU automatycznie kończy strategię zastępczą podczas pracy, z przejściem zweryfikowanym dla profilu (SYS-216). Potwierdzony rzeczywisty niedobór ciśnienia paliwa powoduje kontrolowane zatrzymanie; nowy rozruch wymaga potwierdzenia prawidłowego zasilania (SYS-217). Po ochronnym zatrzymaniu pompa jest wyłączona; ograniczoną próbę odbudowy ciśnienia uruchamia nowe żądanie START/kopniakiem, bez automatycznych ponowień (SYS-218). Przy zbyt wysokim ciśnieniu przyjęto ograniczoną próbę obniżenia pompą tylko na zweryfikowanej strategii i w granicach osprzętu; brak warunków lub niepowodzenie oznaczają zatrzymanie i wyłączenie pompy (SYS-219). Po udanym obniżeniu ciśnienia przyjęto monitorowaną strategię zastępczą do końca pracy silnika; normalne sterowanie dopiero przy kolejnym rozruchu po kwalifikacji profilu (SYS-220). Nowy rozruch na strategii zastępczej dopuszczono po osobnej walidacji rozruchu, potwierdzeniu prawidłowego ciśnienia i pozostałych warunków (SYS-221). Po ochronnym zatrzymaniu przy wysokim ciśnieniu przygotowanie pompy rozpoczyna dopiero nowa próba START/kopniakiem, bez automatycznych ponowień (SYS-222). Przy potwierdzonym stanie niskiego ciśnienia oleju z wejścia 0/1 podczas pracy 4T ECU zapisuje DTC i ostrzega, pozostawiając decyzję o zatrzymaniu kierowcy (SYS-223). Przy wykrywalnej usterce toru ciśnienia oleju dopuszczono dalszą pracę i nowe rozruchy, z DTC i informacją o niedostępnym nadzorze (SYS-224). Po usterce pozycjonowania elektronicznego zaworu wydechowego 2T dopuszczono pracę i rozruch na odpowiednich, osobno zweryfikowanych strategiach; brak właściwej strategii oznacza zatrzymanie albo blokadę rozruchu (SYS-225). Po odzyskaniu pozycjonowania zaworu przyjęto powrót podczas pracy po potwierdzonym zamknięciu przepustnicy i spełnieniu zweryfikowanych warunków profilu; gdy przejście jest niedopuszczone, powrót wymaga kolejnego rozruchu i kwalifikacji (SYS-226). Ponowne otwarcie przepustnicy podczas przejścia odkłada zakończenie powrotu do kolejnego potwierdzonego zamknięcia (SYS-227). Przyjęto cel możliwie krótkiego przejścia; budżet czasu zostanie określony z danymi napędu i pomiarami (SYS-228). |
| W05 — Inwentaryzacja Bety | W kolejce, etap 3. | Zachowany [plan INV](verification/beta-2015-plan-inwentaryzacji.md); brak wyników pomiarowych. |
| W01/W02 — Architektura i zasoby | W kolejce, etap 4. | Zachowane [diagram](architecture/blokowa-systemu.md) i [macierz wariantów](architecture/macierz-wariantow-silnika.md); bez zamkniętych bilansów. |
| W03 — Weryfikacja wymagań | W kolejce, etap 5. | Zachowany [przydział 202 SYS do grup](verification/macierz-wymagan.md); kryteria, procedury i dowody do rozwinięcia. |
| W06 — Bilanse i wybór komponentów | W kolejce, etapy 4 i 6. | Wymagane wejściowe parametry; ważne komponenty wybierzemy wspólnie. |

**Najbliższy krok to ustalenie dalszej pracy i rozruchu przy potwierdzonej wykrywalnej usterce IAC w wyposażonym profilu 4T (pytanie 236). Reakcje zaworu wydechowego, warunki powrotu i zachowanie po ponownym dodaniu gazu przyjęto w SYS-225–227. Cel krótkiego czasu przejścia zapisano w SYS-228; liczbowe limity, dane napędu i przebieg wymagają projektu oraz prób.** Przyjęte reakcje i plan prób są w [macierzy F03](requirements/f03-ochrona-i-usterki.md). Konkrety osprzętu, w tym wykonalność konwersji TPI, mają właścicieli i etapy w [przekazaniu F01](requirements/f01-sterowanie-silnikiem.md). Parametry elektryczne, bilanse i procedury wykonawcze pozostają w kolejce właściwych etapów.

## Warunki przechodzenia dalej

| Bramka | Co musi być gotowe |
| --- | --- |
| G0 — baza funkcjonalna | Przeglądy F01–F08 zakończone decyzją lub jawnym wyłączeniem; spójny rejestr wymagań; pozostałe niewiadome mają właściciela zadania i etap rozstrzygnięcia. |
| G1 — architektura do projektowania | I/O i zasoby dla wariantów, bilanse zasilania i ciepła, interfejsy oraz ocena istotnych niewykonalności; dane wystarczające dla projektowanego bloku. |
| G2 — wykonanie PCB | Przyjęte schematy/BOM/biblioteki, ważne części wybrane wspólnie, przegląd PCB, ERC/DRC i mechaniki oraz plan uruchomienia z punktami pomiarowymi. |
| G3 — próby systemowe | Kontrolowane uruchomienie zasilania i bloków, gotowe stanowiska/procedury, znane limity oraz zapisane wyniki dopuszczające kolejne próby. |
| G4 — wydanie prototypu | Potwierdzony zakres działania dla właściwych rewizji i konfiguracji, regresja, dokumentacja oraz lista ograniczeń i prac pozostałych. |

Projekt wykonawczy bloków rozpoczynamy w etapie 6 po zakończeniu wcześniejszych etapów i uzyskaniu danych wejściowych. Zamrożenie PCB wymaga rozstrzygnięcia kwestii wpływających na wspólny sprzęt. Status uzgodnionego wymagania i status zweryfikowanego produktu prowadzimy oddzielnie.

## Najważniejsze niewiadome do następnego etapu

| Temat | Działanie i miejsce rozstrzygnięcia |
| --- | --- |
| TPI i smarowanie mieszanką | Ocena wykonalności dla konkretnych jednostek zgodnie z macierzą wariantów; warunek przed deklaracją zgodności. |
| Wspólny sprzęt i kompaktowość | Parametry CDI/TCI, czujników i napędów, jednoczesność I/O, prądy oraz ciepło — etapy 3–6. |
| Wybudzanie i rezerwa energii | Bazowa instalacja enduro bez stacyjki ma stałe zasilanie ECU z akumulatora i [automatyczne usypianie ECU/HMI](architecture/usypianie-ecu-hmi.md) (SYS-054/059). W architekturze zasilania uwzględnić kopniak, ruch koła, HMI, zasilanie HMI w śnie i rezerwę po 4 tygodniach postoju przy −10°C…+40°C dla minimum 3 Ah AGM / 2 Ah LiFePO4. |
| Pokrycie poza Betą | Zaplanować reprezentatywne stanowiska i jednostki 4T/TPI/TBI; wyniki Bety potwierdzają jej konfigurację. |

## Zakres prowadzenia inżynierii

Asystent prowadzący inżynierię odpowiada za przygotowanie i uzasadnienie wymagań, architektury, interfejsów, obliczeń, doboru komponentów, schematów, bibliotek i footprintów, opracowanie i przeglądy rozmieszczenia elementów oraz prowadzenia połączeń PCB, integrację mechaniczną i dokumentację wykonawczą. Decyzje podejmujemy z właścicielem projektu i zapisujemy ich podstawę.

Dobór elementów obejmuje potrzebne parametry, wartości i tolerancje, zapasy, obudowę, symbol/footprint, numer producenta i powiązanie z BOM. Głębokość analizy dopasowujemy do roli elementu; kluczowe układy wymagają porównania i weryfikacji dokumentacji producenta. Schemat i PCB obejmują też zasilanie, zabezpieczenia, masy, prądy, ciepło, prowadzenie sygnałów, montaż i wykonalność produkcji.

### Wspólny dobór ważnych komponentów

Ustalenie właściciela: wybór każdego ważnego komponentu konsultujemy i podejmujemy wspólnie przed przyjęciem go do projektu. Obejmuje to procesory ECU/HMI, czujniki na PCB (w tym akcelerometr/IMU i czujnik ciśnienia atmosferycznego), transceivery, układy zasilania, sterowniki wyjść, pamięci i inne elementy istotne dla funkcji, interfejsów, dokładności, gabarytów lub niezawodności. Zasada obejmuje także elementy pasywne, jeśli ich wybór ma takie znaczenie, oraz istotne zmiany wcześniej przyjętych części.

Asystent przygotowuje wymagania dla elementu, weryfikuje dokumentację i przedstawia zwykle 2–3 odpowiednich kandydatów: konkretne numery producenta, parametry, obudowy, interfejsy, pobór mocy, ograniczenia, dostępność i orientacyjny koszt z datą sprawdzenia. Porównanie zawiera rekomendację z uzasadnieniem i skutki dla pozostałych bloków, firmware oraz PCB. Jeżeli brak sensownych alternatyw, przedstawia przyczynę. Właściciel może zaproponować własny komponent do oceny.

Wybór omawiamy z właścicielem; propozycje pozostają propozycjami do czasu jego potwierdzenia. Przyjętą część, uzasadnienie i źródło decyzji zapisujemy przy danym bloku/BOM, a decyzje architektoniczne także w ADR. Asystent następnie opracowuje potrzebne obwody, wartości elementów towarzyszących, połączenia, wymagania dla bibliotek i layoutu oraz kryteria weryfikacji. Projekt w Autodesk Fusion wykonuje właściciel, otrzymując od asystenta informacje, dane i wymagania potrzebne do jego realizacji oraz przeglądy wyników.

Firmware przygotowuje właściciel z Codexem zgodnie z ustalonym sposobem współpracy. Praca inżynierska obejmuje wymagania, przydział zasobów, interfejsy, kryteria i testy potrzebne również do firmware oraz aplikacji Windows.

## Współpraca przy schematach i PCB

Ustalenie właściciela: projekt CAD wykonuje w Autodesk Fusion Electronics, korzystając z przygotowanych przez asystenta rozwiązań. Asystent dostarcza schematy bloków z wartościami i połączeniami, uzasadnienie doboru elementów, propozycje rozmieszczenia komponentów oraz liczby i funkcji warstw. Określa zasady prowadzenia sygnałów, zasilania i mas, wymagane odstępy, szerokości i przelotki oraz potrzebne kontrole elektryczne, cieplne i produkcyjne. Parametry ustalamy z obliczeń, danych producentów i warunków wykonania PCB.

Pracujemy blokami: dane wejściowe → rozwiązanie i obliczenia → odwzorowanie w Fusion → przegląd schematu, bibliotek i PCB → korekty. Archiwizujemy pliki edytowalne oraz powiązane eksporty dla konkretnej rewizji. Zrzuty ekranu pomagają w przeglądzie, ale nie zastępują kontroli połączeń, reguł i footprintów.

Bezpośrednia obsługa Fusion przez asystenta pozostaje opcjonalnym sposobem pracy. W sesji z 2026-10-25 narzędzie Windows wykryło zainstalowany Fusion, bez uruchomionego okna; brak dedykowanego narzędzia Fusion w tej sesji. Obsługa edytora schematów i PCB nie została jeszcze sprawdzona w praktyce. Przed wykorzystaniem jej do projektu należy przeprowadzić próbę na małym obwodzie, obejmującą zapis, ponowne otwarcie i kontrolę wyniku.

## Podstawa pytań i kontrola kompletności

Pytania wynikają z celów właściciela i wcześniejszych odpowiedzi, scenariuszy użycia i stanów urządzeń, macierzy wariantów silnika, dokumentacji zachowywanego osprzętu oraz analizy zależności i możliwych uszkodzeń. Dokumenty referencyjne dostarczają danych; potwierdzenie zgodności danego osprzętu wymaga analizy i pomiarów.

Ustalenie właściciela z 2026-11-01: przed pytaniem o nową funkcję silnika lub osprzętu sprawdzamy jej występowanie w motocyklach enduro odpowiadających celowi DustONE. Przedstawiamy konkretny model, rocznik, źródło producenta i potwierdzony sposób realizacji oraz znaczenie dla wspólnej PCB. Funkcje wynikające bezpośrednio z celów właściciela oznaczamy jako takie. [Zasada weryfikacji i przykład IAC](requirements/weryfikacja-funkcji-enduro.md) określa sposób dokumentowania podstaw pytania. Brak potwierdzenia pozostaje jawną luką; sam opis funkcji w uniwersalnym ECU nie potwierdza wyposażenia enduro.

Przed pytaniem wskazujemy aktywny pakiet i cel. Przechodzimy do następnego pakietu dopiero po zapisanym zamknięciu poprzedniego; wpływ na późniejsze tematy odkładamy do ich kolejki. Najpierw określamy decyzje wpływające na sprzęt i wspólną PCB. Szczegóły niezależne od sprzętu można rozwijać później. Pytania pojedyncze z propozycjami służą ustalaniu preferencji, zakresu, brakujących informacji oraz wspólnemu wyborowi ważnych komponentów po przedstawieniu porównania. Obliczenia i propozycje rozwiązań technicznych przygotowuje asystent z uzasadnieniem; właściciel aktywnie uczestniczy w doborze części według powyższej zasady.

### Sposób przedstawiania pytań

Ustalenie właściciela z 2026-11-18: przed pytaniem z propozycjami krótko wyjaśniamy problem i podstawę decyzji:

1. Rolę sygnału lub funkcji w ECU oraz jego znaczenie dla sterowania.
2. Rozpatrywany przypadek, zakładane sprawne elementy i skutki utraty lub błędu sygnału.
3. Wpływ na rozruch, pracę silnika, osprzęt i kierowcę — odpowiednio do tematu.
4. Możliwe reakcje, ich korzyści i ograniczenia oraz uzasadnienie rekomendacji.
5. Dane i próby potrzebne do potwierdzenia rozwiązania; przykłady liczbowe oznaczamy jako ilustracyjne.

Następnie pokazujemy jedno pytanie w oknie wyboru z 2–3 zrozumiałymi propozycjami. Zakres wyjaśnienia dopasowujemy do problemu. Prośba o wyjaśnienie pozostawia pytanie otwarte i nie stanowi wyboru wariantu.

### Kontrola kompletności

Kompletność sprawdzamy według [mapy obszarów i otwartych tematów](requirements/pokrycie-funkcjonalne.md), a nie liczby zadanych pytań. Dla każdego obszaru przeglądamy normalną pracę, rozruch/wyłączenie, granice, brak opcjonalnego wyposażenia, usterki oraz serwis i aktualizację, odpowiednio do jego roli. Zapisujemy wymagania przyjęte, wyłączenia i kwestie otwarte. Każda istotna decyzja otrzymuje źródło; wymagania łączymy dalej z blokiem realizującym i weryfikacją.

Przed zamknięciem architektury, wydaniem PCB i rozpoczęciem prób wykonujemy odpowiedni przegląd pokrycia. Późniejsza zmiana wymaga oceny wpływu na pozostałe urządzenia, I/O, zasoby, dokumentację i testy. Pełny przegląd kompletności oraz szczegółowa macierz realizacji i weryfikacji pozostają do opracowania; sama mapa obszarów ich nie zastępuje.

## Odpowiedzialność za testy

Asystent przygotowuje plan, powiązanie testów z wymaganiami, stanowiska, wyposażenie, procedury, oczekiwane wyniki i kryteria przerwania. Właściciel wykonuje próby fizyczne i przekazuje dane. Asystent analizuje wyniki, wskazuje niezgodności, proponuje poprawki oraz określa potrzebną regresję. [Zasady weryfikacji i szablon procedury](verification/README.md) są miejscem źródłowym dla tego procesu.

Każde wymaganie musi mieć właściwą metodę i dowód potwierdzenia. Funkcje i parametry działania obejmujemy próbami rzeczywistego ECU/HMI/aplikacji; obliczenia i przeglądy uzupełniają weryfikację konstrukcji. Status uzgodnionego wymagania jest odrębny od statusu zweryfikowanego wykonania.
