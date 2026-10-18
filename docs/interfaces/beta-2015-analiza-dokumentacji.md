# Beta RR 300 Racing 2015 - analiza dokumentacji

Data: 2026-10-18. Status: analiza dokumentów i deklaracji właściciela; bez oględzin i pomiarów motocykla. Powiązania: [lista I/O](wstepna-lista-io.md), [plan inwentaryzacji](../verification/beta-2015-plan-inwentaryzacji.md).

## 1. Źródła i zgodność

| ID | Plik dostarczony przez właściciela | Rozpoznana zawartość | Zastosowanie |
| --- | --- | --- | --- |
| A | `2015 RR 2 stroke Owners Manual.pdf` | 70 stron, RR 250-300 2T, kod 026440130 000 na s. 1. Instrukcja użytkownika, nie pełna instrukcja serwisowa. | Schemat s. 24, legenda s. 25, dane silnika s. 22-23, licznik s. 14. Przypisanie do MY2015 wynika z przekazanego pliku; zgodność z egzemplarzem wymaga sprawdzenia. |
| B | `2015 racing addition supplement-2 stroke.pdf` | 6 stron; w treści powtarza się oznaczenie RR2T Racing my'14. Schemat s. 4, legenda s. 5-6. | Materiał porównawczy MY2014. Nazwa pliku nie potwierdza zastosowania do Racing 2015. |

Numery stron poniżej liczymy od 1; dla cytowanych stron odpowiadają numeracji drukowanej. Identyfikacja kopii SHA-256:

- A: `c74b37d55d99069e30297f70ac73523f63430914c8d5da688d1dec898f788abe`.
- B: `98c985b8513f472f2c41f62b146af1e0b5a754fff9ef4ed04bb59d634d25884e`.

**Deklaracja właściciela z 2026-10-18: gaźnik w jego motocyklu nie ma TPS.** Pierwszy wariant testowy traktujemy jako gaźnikowy bez TPS. Dokument B przedstawia TPS i przełącznik dwóch map; jego zgodność z egzemplarzem pozostaje niepotwierdzona. Nie wymagamy dodania TPS do Bety; wspólna PCB zachowuje obsługę TPS dla innych zastosowań.

Zauważono błąd angielskiej legendy B: pozycje 21 i 24 powtarzają błędne określenie przedniego lewego kierunkowskazu. Rysunek oraz legenda włoska rozróżniają tylny lewy i tylny prawy. W tabeli użyto tego rozróżnienia; nie scalać numeracji A i B. Numery elementów nie są numerami styków złączy.

## 2. Mapa funkcjonalna obwodów

| Obwód | Połączenia i elementy pokazane w dokumentach | Znaczenie dla DustONE |
| --- | --- | --- |
| Generator i zapłon | Generator jest połączony z modułem zapłonowym; dalej cewka WN i świeca. Oddzielnie generator współpracuje z regulatorem. A: s. 24-25; B: s. 4-6. | Rozdzielić funkcje przewodów zasilania i synchronizacji. Nie wyznaczono jeszcze wejścia CKP, amplitud ani toru energii zapłonu. |
| Typ zapłonu | A s. 23 opisuje zapłon DC-CDI typu Kokusan z cyfrowo zmiennym wyprzedzeniem; B s. 6 nazywa moduł CDI. | Punkt wyjścia do analizy stopnia zapłonowego. Oznaczenia modułu, cewki i rzeczywiste połączenia muszą potwierdzić dobór interfejsu. |
| Rozrusznik | Akumulator, styki przekaźnika i silnik rozrusznika tworzą tor dużego prądu; osobno pokazano sterowanie przekaźnikiem i bezpiecznik. | Projektować oddzielnie sterowanie cewką i tor prądu silnika. Bezpiecznik 10 A z legendy nie określa prądu rozrusznika. |
| Instalacja i ładowanie | Regulator 12 V, akumulator, obwody odbiorników i masy ramy. | Zidentyfikować odcinki AC/DC, połączenia mas, obciążenie regulatora i zachowanie podczas kopania/rozruchu. Nazwa regulatora nie określa pełnego zakresu napięć. |
| Polecenia kierowcy | START, gaszenie, klakson, wybór świateł i kierunkowskazów; osobne przełączniki hamulców. | Zwykłe polecenia kierownicy w DustONE do HMI/CAN; ręczny STOP osobnym obwodem. Miejsce wejść hamulców pozostaje otwarte. |
| Prędkość | Czujnik koła jest połączony z licznikiem; A s. 14 opisuje go jako bezkontaktowy magnetyczny. | Nie rozstrzyga to typu elektrycznego czujnika ani potrzeby jego zasilania. Interfejs i kalibracja do określenia. |
| Wyposażenie Racing B | TPS do modułu zapłonowego, przełącznik dwóch map i kondensator 4700 µF. | Nie przenosimy tych elementów automatycznie na Betę właściciela ani do projektu DustONE. |

## 3. Tabela osprzętu i odniesień do schematów

| Element / funkcja | Numer A, s. 24-25 | Numer B, s. 4-6 | Dane dokumentowe / brakujące |
| --- | --- | --- | --- |
| Akumulator | 26; zaciski 25/32 | 29; zaciski 28/33 | W obu legendach 12 V, 4 Ah; aktualny model i chemia do sprawdzenia. |
| Generator / regulator | 27 / 18 | 30 / 18 | Oznaczenia, uzwojenia, prostowanie i przebiegi do identyfikacji. |
| Moduł zapłonowy / cewka / świeca | 33 / 34 / 35 | 35 / 36 / 37 | Potrzebne oznaczenia OEM, złącza, parametry energii i sterowania. |
| Przekaźnik / silnik rozrusznika | 31 / 30 | 31 / 32 | Prąd cewki, tłumienie przepięć i tor dużego prądu do ustalenia. |
| Bezpiecznik / masy | 28 / 29, 37 | 27 / 26, 38 | Bezpiecznik opisany 10 A; podział zabezpieczeń do odtworzenia na egzemplarzu. |
| START / gaszenie silnika | 3 / 12 | 3 / 11 | Stan styków, odniesienie elektryczne i reakcje na uszkodzenia do potwierdzenia. |
| Czujnik koła / licznik | 4 / 7 | 4 / 7 | Typ sygnału i parametry wejścia licznika niepodane. |
| Przełączniki hamulca przód / tył | 2 / 36 | 2 / 25 | Parametry i wspólne przewody do ustalenia. |
| Światło główne / pozycyjne przód | 10 / 38 | 40 / 39 | Odpowiednio 12 V 35/35 W i 12 V 5 W; podział włókien oraz równoczesność do potwierdzenia. |
| Kierunkowskazy przód P/L, tył L/P | 1/17, 21/23 | 1/17, 21/24 | 12 V 10 W na lampę według legend; prądy załączania do pomiaru. |
| Tył LED / oświetlenie tablicy | 22 / 24 | 22 / 23 | Funkcje pozycyjne/STOP i rzeczywiste prądy do potwierdzenia. |
| Klakson / jego przycisk | 11 / 13 | 41 / 12 | Klakson opisany 12 V; prąd niepodany. |
| Wentylator / przerywacz | 19 / 20 | 19 / 20 | Obecny sterownik wentylatora jest własnym projektem właściciela, działa automatycznie bez ręcznego włącznika i wykorzystuje [NTC B57301K0103A001](beta-czujnik-temperatury-b57301k0103a001.md), według właściciela z końcówką w płynie w przewodzie łączącym obie chłodnice. Schemat modułu, wentylator, prądy, kierunek przepływu i połączenia do ustalenia. Numery dotyczą dokumentów, nie potwierdzają zgodności z zestawem OEM. |
| TPS / przełącznik map / kondensator | Brak osobnych pozycji w legendzie | 34 / 10 / 16 | Według B kondensator 4700 µF, przełącznik wybiera dwie mapy (s. 3). Właściciel potwierdza brak TPS w swojej Becie. |

A s. 22 wskazuje gaźnik PWK 36S AG; A s. 23 opisuje odśrodkowy zawór wydechowy ze sprężynami. Są to dane instrukcji, nie wyniki oględzin Racing 2015. Mechaniczny zawór w wariancie zgodnym z A nie pozwoli zweryfikować wymaganego elektronicznego power valve na tym motocyklu.

Moce lamp są danymi nominalnymi, nie parametrami kanałów SmartFET. Do wstępnego bilansu: 35 W / 12 V = ok. 2,92 A dla jednego włókna, 10 W / 12 V = ok. 0,83 A dla lampy kierunkowskazu. Rzeczywiste napięcie, prąd załączania, temperatura i równoczesność wymagają danych z egzemplarza.

## 4. Brakujące dane i proponowane punkty pomiarowe

To lista obiektów do przygotowania procedur, bez instrukcji podłączenia sond do niezweryfikowanych styków.

| ID | Obiekt / punkt odniesienia | Co trzeba ustalić / zarejestrować |
| --- | --- | --- |
| BETA-P01 | Akumulator, zasilanie modułu zapłonowego i wybrane punkty masy | Model akumulatora, minimalne napięcie przy rozruszniku/kopniaku, spadki przewodów i czas odzyskiwania. Najpierw rozpoznać faktyczne wejście zasilania modułu. |
| BETA-P02 | Generator, regulator i wiązka modułu zapłonowego | Funkcje uzwojeń/przewodów, źródło i energia zapłonu, sygnał synchronizacji; nie wyprowadzamy ich z samych kolorów. |
| BETA-P03 | Zidentyfikowany sygnał synchronizacji | Typ czujnika, amplituda i polaryzacja podczas kopania/rozruchu, układ znaczników i odniesienie do GMP; sama częstotliwość nie wyznacza kąta zapłonu. |
| BETA-P04 | Cewka i moduł zapłonowy | Oznaczenia, schemat, parametry pierwotne i energia; pomiary przebiegów dopiero po doborze sondy i potwierdzeniu punktów. Wtórny obwód WN poza pierwszą serią pomiarów. |
| BETA-P05 | Przełączniki START, STOP, hamulców i świateł | Stany styków i ciągłość przy wyłączonym, odpowiednio odłączonym obwodzie; typ sygnału po odtworzeniu schematu egzemplarza. |
| BETA-P06 | Czujnik koła i jego wtyczka | Typ czujnika, zasilanie lub styk, przebieg, liczba impulsów na obrót i obwód koła. |
| BETA-P07 | Lampy, klakson, wentylator i cewka przekaźnika rozrusznika | Faktyczna obecność, oznaczenia, prądy ustalone/załączania, równoczesność i zabezpieczenia. Przyrządy do pomiaru prądu do określenia. |

Kolejność: oznaczenia i fotografie osprzętu, porównanie z dokumentami, mapa rzeczywistych złączy, pomiary nieaktywnej instalacji, następnie uzgodnione procedury przebiegów. Plan i wyposażenie: [inwentaryzacja](../verification/beta-2015-plan-inwentaryzacji.md). Wciąż brakuje m.in. parametrów CKP, odniesienia do GMP, energii zapłonu, maksymalnych obrotów i prądów obciążeń; nie wybieramy jeszcze stopni zapłonowych ani SmartFET-ów.

## 5. Stan weryfikacji

Przeczytano dane i legendy oraz obejrzano schemat A s. 24 i B s. 4. Schemat A ma ograniczoną czytelność drobnych oznaczeń w dostarczonym PDF. Nie ustalono zweryfikowanego pinoutu, numerów części ani zgodności z instalacją motocykla. Nie wykonano pomiarów i prób. Brak elementu w legendzie nie jest dowodem jego braku w egzemplarzu. Opracowanie przechowujemy w repozytorium; źródła PDF identyfikujemy nazwą, stronami i sumą kontrolną.
