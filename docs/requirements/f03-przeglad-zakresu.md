# F03 — przegląd ochrony i reakcji na usterki

Stan na 2026-11-24. **F03 zamknięty w zakresie funkcji po przeglądzie inżynierskim i akceptacji właściciela.** Karta obejmuje SYS-157–235 i ich powiązania z wcześniejszymi wymaganiami. Właściciel rozstrzygnął pytanie 242 odpowiedzią A. W odpowiedzi A na pytanie 243 (2026-11-24) właściciel zaakceptował tę kartę, zamknął F03 i zezwolił na scalenie kompletnej dokumentacji przez PR #24. Aktywnym kolejnym pakietem jest F04.

Źródła: [rejestr SYS](../01-zakres-systemu.md#2-wymagania-wynikające-z-opisu), [reakcje, podstawy i plany prób F03](f03-ochrona-i-usterki.md#szybka-nawigacja), [kolejność procesu](../00-proces-i-status.md).

## Przyjęty zakres

| Obszar | Ustalenia | Podstawa |
| --- | --- | --- |
| Wał i faza 4T | Utrata synchronizacji wału odcina zapłon i wtrysk. Wznowienie wymaga zatrzymania i nowej próby. Zanik fazy po poprawnej synchronizacji dopuszcza dalszą pracę przy zachowanej wiarygodności cyklu; profil używający fazy wymaga jej do nowego rozruchu. Sprzeczność wału i fazy odcina sterowanie. | SYS-157–159, SYS-205–207 |
| START i STOP | START działa podczas przytrzymania, z limitami. STOP odcina także rozrusznik niezależnie od głównego firmware. Wykryta przerwa lub zwarcie STOP do masy powodują diagnostykę, bez blokowania pracy i nowych rozruchów z samej tej przyczyny. | SYS-048–049, SYS-160–168 |
| Nadzór i odzyskiwanie | Nadzór odcina wyjścia niezależnie od resetu. Przyjęto limity zwykłych i samodzielnych prób, trwałość ich rozliczania i tryb naprawy Windows. Po odcięciu wznowienie wymaga zatrzymania i nowej próby. | SYS-169–183 |
| Autotest i wybudzanie | Każde wybudzenie uruchamia kontrole skonfigurowanych funkcji. Przed rozruchem kończą się próby dostępne przy zgaszonym silniku; inne czekają na warunki. START trzymany przez zwykłe wybudzenie może uruchomić rozrusznik po gotowości. Reguły nowej próby po odcięciach zachowują pierwszeństwo. | SYS-194, SYS-203–204 |
| Przewrócenie | Sprawny tor wykrywania blokuje pracę przy potwierdzonym przewróceniu. Po postawieniu wymagane są właściwe warunki i świadoma próba. Potwierdzona usterka toru zwalnia blokadę wynikającą z przewrócenia, także gdy położenie jest nieznane; ECU ostrzega o niedostępności funkcji. Pozostałe blokady obowiązują. | SYS-039–040, SYS-197–202 |
| Temperatury i barometr | Przy usterkach IAT/ECT praca i rozruch wymagają odpowiednich, osobno zweryfikowanych strategii. Temperatura ECU może pomocniczo wspierać oszacowanie IAT. Przy usterce BARO używana jest stała awaryjna. Wiarygodne IAT/ECT/BARO wracają do sterowania podczas pracy po kwalifikacji przejścia. | SYS-208–213 |
| Chłodzenie | Brak pomiaru płynu wymusza wentylator podczas pracy silnika, a wymuszenie kończy się po zatrzymaniu. Chłodzenie po zgaszeniu podlega uzgodnionym limitom. Przeciążenie odłącza wentylator; powrót wymaga właściwej próby. Po każdym wybudzeniu możliwa jest jedna nowa automatyczna próba przy spełnionych warunkach. | SYS-184–196 |
| Ostrzeżenia oleju i przegrzania | Potwierdzone przegrzanie z wiarygodnego pomiaru oraz niski stan ciśnienia oleju 0/1 ostrzegają; kierowca decyduje o zatrzymaniu. Usterka toru oleju dopuszcza pracę i nowe rozruchy z informacją o niedostępnym nadzorze. Same te reakcje ostrzegawcze nie wymuszają „Standard”. | SYS-189, SYS-223–224 |
| Ciśnienie paliwa | Usterka pomiaru dopuszcza właściwą strategię zastępczą; w zgodnym układzie pozostaje normalne sterowanie pompą i nominalne parametry. Rzeczywisty niedobór ciśnienia zatrzymuje silnik. Przy nadmiarze dopuszczono tylko kwalifikowaną, ograniczoną próbę obniżenia; niepowodzenie kończy się zatrzymaniem. Kolejna próba wymaga nowego żądania. | SYS-214–222 |
| Zawór 2T i IAC | Praca i nowy rozruch po usterce wymagają właściwych, osobno zweryfikowanych strategii. Powrót zaworu 2T podczas jazdy wymaga wiarygodnego zamknięcia TPS i kwalifikacji; ponowne dodanie gazu odkłada zakończenie powrotu. Cel krótkiego przejścia wymaga budżetu i pomiarów. IAC wraca podczas pracy po kwalifikacji albo przy kolejnym rozruchu, gdy wymagane jest zgaszenie. | SYS-225–230 |
| Wtryskiwacz, zapłon i obwód pompy | Potwierdzone wykrywalne usterki kończą sterowanie zgodnie z danym wymaganiem. Rozruch wymaga sprawnego toru i pozostałych warunków. Dla zapłonu i pompy nowa świadoma próba po zatrzymaniu uruchamia automatyczne sprawdzenie, bez potwierdzenia naprawy przez użytkownika. | SYS-231–233 |
| Ogranicznik obrotów | Aktywny w uzgodnionych profilach gaźnikowych/wtryskowych 2T/4T. Po spełnieniu warunków wraca normalne sterowanie bez nowego rozruchu. Prawidłowe zadziałanie jest zwykłym stanem, bez DTC i wymuszania „Standard”. Inne odcięcia pozostają nadrzędne. | SYS-234–235 |
| Diagnostyka i zestawy map | ECU jest właścicielem stanów. Historia DTC zachowuje przyjęte pierwsze/ostatnie wystąpienie, ramki i licznik. Usterki wymagające pracy awaryjnej albo zatrzymania wymuszają „Standard”; sam brak HMI nie zatrzymuje silnika. | SYS-019–025, SYS-046, SYS-137–138, SYS-147 |

## Przegląd spójności

Sprawdzono powiązania przyjętych zasad:

| Powiązanie | Wynik przeglądu |
| --- | --- |
| Kilka aktywnych przyczyn ograniczeń | Każda zachowuje warunki zwolnienia. Powrót po jednej usterce nie zwalnia pozostałych odcięć. Dopuszczenie strategii awaryjnej wymaga jej warunków w aktualnym stanie; sprawdzenie pojedynczej usterki nie kwalifikuje pracy po utracie innego sygnału potrzebnego tej strategii. Podstawa: SYS-128–133, SYS-208–213, SYS-225–230. |
| Powrót z ograniczania obrotów | Nie zwalnia STOP, utraty synchronizacji ani innego odcięcia wymagającego nowej próby. Podstawa: SYS-157, SYS-162, SYS-169–183, SYS-234–235. |
| Autotest i późniejsze kontrole | Wykonanie dostępnych prób przed rozruchem nie oznacza, że próby wymagające obrotu wału są już wykonane. Kontrolowane pobudzenia przy nowej próbie zapłonu/pompy pozostają w granicach STOP i zabezpieczeń. Podstawa: SYS-194, SYS-203–204, SYS-232–233. |
| HMI/CAN i blokady ECU | ECU wykonuje ochronę lokalnie. Utrata lub powrót HMI nie potwierdzają sprawności toru ani nie zwalniają blokady. Pozostałe zachowania akcesoriów należą do aktywnego F04. Podstawa: SYS-046, SYS-050–053 i odpowiednie reakcje F03. |
| Ostrzeżenie a reakcja silnika | Rzeczywiste usterki zachowują własne reakcje. Ostrzegawcze przypadki SYS-189/223/224 oraz normalne ograniczanie SYS-235 nie są automatycznie zamieniane w odcięcie lub wymuszenie „Standard”. |

Przegląd nie ujawnił kolejnej decyzji produktowej potrzebnej do przyjętego zakresu F03. Uszczegółowienie stanów, metod diagnostyki i kwalifikacja konkretnych konfiguracji należą do wskazanych etapów; nowa luka ujawniona danymi lub próbą podlega ocenie wpływu zgodnie z procesem.

## Weryfikacja i przekazanie

Dla SYS-157–235 przygotowano 79 planów prób oraz powiązanie z blokami i grupami w [macierzy weryfikacji](../verification/macierz-wymagan.md). To plany do rozwinięcia w procedury; wyników prób produktu jeszcze nie ma.

| Etap lub pakiet | Dane i praca do wykonania | Odpowiedzialność |
| --- | --- | --- |
| Etap 3 — dane osprzętu | Modele czujników, cewek, wtryskiwaczy, pompy, wentylatora, zaworu i IAC; rzeczywiste sygnały, prądy, charakterystyki oraz mechanizmy usterek. | Asystent przygotowuje listę i analizę; właściciel dostarcza dostępne dane oraz pomiary. |
| Etap 4 — architektura | Pełne stany i priorytety, budżet czasu gotowości, progi/czasy/histerezy, kwalifikacja strategii pracy i rozruchu, zakres diagnostyki oraz przejścia po usterkach. | Asystent opracowuje i uzasadnia; ważne decyzje konstrukcyjne uzgadniamy z właścicielem. |
| Etap 5 — procedury | Kryteria liczbowe, wyposażenie, połączenia, scenariusze jednoczesnych warunków i warunki przerwania każdej próby. | Asystent przygotowuje procedury przed ich wykonaniem. |
| Etapy 6–8 — elektronika i PCB | Tory ochronne i pomiarowe, niezależne odcięcia, pamięć, wybudzanie i rzeczywiste pokrycie diagnostyki. Komponenty wybieramy wspólnie; właściciel wykonuje CAD w Fusion z przekazanymi wymaganiami i przeglądami asystenta. | Asystent opracowuje obwody i wymagania; właściciel uczestniczy w doborze i wykonuje projekt CAD. |
| Etap 11 — próby produktu | Stanowiska, rzeczywiste ECU/HMI/Windows i reprezentatywne silniki dla dopuszczanych konfiguracji. | Właściciel wykonuje próby; asystent przygotowuje je i analizuje wyniki. |
| F04–F07 | Pozostałe akcesoria, prezentacja w HMI, obsługa w Windows, protokół CAN, katalog DTC i szczegóły aktualizacji/naprawy. | Rozwijamy kolejno we właściwych pakietach; F03 określa ich przyjęte reakcje silnikowe. |

Beta 300 RR Racing 2015 z gaźnikiem bez TPS potwierdzi część zakresu. Zgodność innych napędów, CDI/TCI, 4T oraz TPI/TBI wymaga osobnych danych i prób. Dla TPI nadal obowiązują warunki konwersji smarowania SYS-015/033; wykonalność nie została potwierdzona.

## Kontrola właściciela

Właściciel potwierdził zgodność karty odpowiedzią A na pytanie 243 (2026-11-24): „Akceptuję kartę i zamykam F03. Publikujemy kompletną dokumentację przez scalenie PR #24.” F03 jest zamknięty w zakresie funkcji, a aktywnym następnym pakietem jest F04. Akceptacja nie potwierdza gotowości PCB, firmware ani zgodności konkretnych motocykli; te wyniki wymagają dalszego projektu i prób.
