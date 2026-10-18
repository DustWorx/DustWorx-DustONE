# Beta - moduł zapłonowy Kokusan CU7542

Data: 2026-10-18. Status: odczyt zdjęć egzemplarza właściciela i porównanie z katalogiem; parametry elektryczne niezweryfikowane. Powiązania: [analiza dokumentacji Bety](beta-2015-analiza-dokumentacji.md), [cewka IG5128](beta-cewka-zaplonowa-ig5128.md), [plan inwentaryzacji](../verification/beta-2015-plan-inwentaryzacji.md).

## Identyfikacja fotograficzna

Źródła: zdjęcia właściciela `IMG_3020.JPG` i `IMG_3021.JPG`, przekazane 2026-10-18.

| Miejsce oznaczenia | Odczyt | Stan interpretacji |
| --- | --- | --- |
| Napis na obudowie | KOKUSAN DENKI, MADE IN JAPAN | Producent rozpoznany na zdjęciach. |
| Główna etykieta | 026400001-000 | Dosłowny odczyt; znaczenie tego numeru względem numeru katalogowego do ustalenia. |
| Główna etykieta | CU7542 | Oznaczenie modułu; brak potwierdzonej dokumentacji interfejsu dla tego kodu. |
| Główna etykieta | 4D 21 | Dodatkowy kod; znaczenie nieustalone. |
| Boczna etykieta Beta | 026400038 300; RR 2T 300cc | Numer porównany z katalogiem; pozostałych części uszkodzonej etykiety nie odtwarzamy domysłem. |

Właściciel podał **8 przewodów we wtyczce**. To informacja o istniejącym module, bez potwierdzenia funkcji styków. DustONE otrzyma nową wiązkę i nowe złącze ECU (SYS-045); odtworzenie całego pinoutu starego CDI nie jest warunkiem rozpoczęcia projektu. Potrzebne są interfejsy zachowywanych czujników i osprzętu.

Identyfikacja źródeł SHA-256:

- `IMG_3020.JPG`: `2f7395735aadceee1c6a18f766ce1a37027c9b7fbc0eadbbaa6dbe347eb4839e`.
- `IMG_3021.JPG`: `eeafab9229d751e475c4530899d802528b939cc85aea3307655dce90955fb8be`.

## Powiązanie z katalogiem Beta

[Katalog producenta RR 2T Enduro 2015, 250/300cc, s. 49, Tav.40, poz. 9](https://www.beta-motoren.nl/media/download_gallery/Onderdelen_rr_2t_enduro_250-300_2015.compressed.pdf) wymienia `026400038 300` jako moduł CDI dla wersji 300cc. Jest to dokument producenta udostępniony przez dystrybutora. [Katalog Beta Motorcycles Australia](https://www.betamotor.com.au/40-wiring-harness-from-chassis-700001-to-700789~946617) używa zapisu `026.40.003.83.00` i opisu CDI RR TS MY13, 300CC. Zapisy odpowiadają temu samemu ciągowi cyfr co boczna etykieta.

Rozpoznano numer rzeczywiście sfotografowanego modułu. Zgodność fabrycznej obsady dla konkretnego egzemplarza Racing 2015 i wariant oprogramowania/map pozostają niepotwierdzone. Katalog części identyfikuje zespół, ale nie określa jego pinoutu, napięć ani energii wyjścia.

Opis DC-CDI typu Kokusan z instrukcji użytkownika A s. 23 jest wskazówką dokumentową (zob. analizę instrukcji), a nie wynikiem pomiaru tego egzemplarza. Zdjęcia potwierdzają producenta i oznaczenia, bez rozstrzygnięcia toru zasilania/ładowania energii zapłonu.

## Dane do dalszej analizy

| Obszar | Potrzebne dane |
| --- | --- |
| Cewka zapłonowa | Oznaczenia odczytane ze zdjęcia; parametry i plan charakterystyki w [karcie cewki](beta-cewka-zaplonowa-ig5128.md). |
| Zasilanie i generator | Parametry dostępnego zasilania, regulatora i mas potrzebne do nowego ECU oraz rozruchu kopniakiem. |
| Synchronizacja | Źródło sygnału, typ czujnika i amplitudy podczas kopania/rozruchu, układ znaczników oraz odniesienie do GMP. |
| Stopień zapłonowy | Tor energii i parametry cewki/sterowania; dopiero potem granica integracji oraz dobór układów DustONE. |

Odczyt etykiet stanowi część INV-01; nie wykonano pomiarów. Wykorzystanie seryjnego CDI do pomiarów porównawczych może wymagać rozpoznania konkretnych punktów, ale nie narzuca złącza ani układu nowej wiązki. Procedury oscyloskopowe przygotujemy po potwierdzeniu punktów oraz odniesienia pomiaru zgodnie z planem inwentaryzacji.
