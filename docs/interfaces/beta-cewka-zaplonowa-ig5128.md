# Beta — cewka zapłonowa IG5128

Data: 2026-10-18. Status: identyfikacja ze zdjęcia; bez pomiarów i potwierdzonej specyfikacji elektrycznej. Powiązania: [moduł Kokusan CU7542](beta-modul-zaplonowy-kokusan-cu7542.md), [lista I/O](wstepna-lista-io.md).

## Obserwacje i źródła

Zdjęcie właściciela `IMG_3019.JPG` przedstawia cewkę zamontowaną w Becie 300 RR Racing 2015. Odczytane oznaczenia: **RC01**, **IG5128**, **140822**. Znaczenie kodów RC01 i 140822 nie zostało potwierdzone; nie interpretujemy ostatniego jako daty produkcji. Na widocznym fragmencie nie ma czytelnej nazwy producenta.

Widać przewód wysokiego napięcia i mocowanie z końcówką oczkową przewodu. Zdjęcie nie ustala kompletnego schematu połączeń uzwojeń ani funkcji pobliskiego białego złącza. Sposób połączenia uzwojeń z zaciskami i masą pozostaje do potwierdzenia.

SHA-256 zdjęcia: `819009f107b2d2396dbe20721da07fcdb3dd2ebdc8b9644f4b4d802a721a84ec`. Oryginał pozostaje plikiem właściciela; karta przechowuje odczyt i identyfikację źródła.

[Katalog KTM 250 XC-W 2014, układ zapłonowy, poz. 16](https://sparepartsfinder.ktm.com/ComponentGroupTemplate/PrintComponentGroupTemplate/13084?culture=en&modelidentifier=1000057303&tenantId=1) wymienia `59039006000`, „IGNITIONCOIL IG5128”, z dopiskiem „ONLY FOR SIX DAYS”. Potwierdza to występowanie oznaczenia w dokumentacji producenta. Nie potwierdza parametrów elektrycznych ani zamienności cewki KTM z egzemplarzem Bety.

[Katalog Beta RR 2T Enduro 2015, s. 49, Tav.40, poz. 10](https://www.beta-motoren.nl/media/download_gallery/Onderdelen_rr_2t_enduro_250-300_2015.compressed.pdf) podaje numer zespołu cewki `006400108 000`. Na zdjęciu nie odczytano tego numeru; powiązanie konkretnego egzemplarza z numerem katalogowym pozostaje niepotwierdzone.

## Dane potrzebne do projektu stopnia zapłonowego

| Dane | Cel / sposób pozyskania |
| --- | --- |
| Zaciski i połączenia z masą | Potwierdzić interfejs samej cewki do nowej wiązki. Rozpoznanie starego złącza ECU nie jest wymaganiem SYS-045. |
| Rezystancja uzwojeń i wpływ fajki | Dokumentacja producenta lub pomiar odpowiednio odłączonego zespołu; zapisać temperaturę oraz uwzględnić rezystancję przewodów pomiarowych. Fajkę rozpatrzyć osobno. |
| Indukcyjność i warunki jej określenia | Dokumentacja lub pomiar właściwym przyrządem; sam multimetr nie potwierdza indukcyjności ani nasycenia. |
| Sposób wzbudzania i dopuszczalne obciążenie | Potwierdzona specyfikacja lub opracowane próby: przebieg napięcia/prądu, energia impulsu, częstotliwość i temperatura. Odtworzony przebieg seryjnego układu jest punktem odniesienia, a nie dowodem granicznych parametrów cewki. |

Opis DC-CDI w instrukcji Bety jest wskazówką dla analizy, nie gotową specyfikacją tej cewki. Nie wybrano napięcia ładowania, pojemności magazynującej energię, tranzystora/tyrystora ani czasu ładowania uzwojenia. Nie należy traktować cewki jako obciążenia do bezpośredniego zasilania 12 V na podstawie zdjęcia.

Najbliższy rezultat: karta interfejsu cewki oraz źródła synchronizacji wału, następnie wybór architektury zapłonu. Obsługa tej Bety nie zamyka wymagań dla pozostałych silników 2T/4T. Instrukcję pomiarów opracujemy po rozpoznaniu zacisków i toru pomiarowego; obecna karta nie jest procedurą podłączenia sond do zapłonu.
