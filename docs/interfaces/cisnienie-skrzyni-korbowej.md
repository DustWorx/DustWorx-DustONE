# Ciśnienie skrzyni korbowej 2T — przegląd F01

Stan na: 2026-11-04. **Propozycja zakresu, przed decyzją właściciela.** Bieżący temat F01 po zamknięciu zakresu MAP. Nie dodano wymagania SYS ani nie wybrano czujnika lub elektroniki.

## Potwierdzony przykład enduro

KTM 300 EXC TPI MY2020: fabryczny katalog silnika 084688TEN, strona oznaczona ENGINE 17 (strona PDF 19), grupa LUBRICATING SYSTEM, poz. 8 — czujnik nazwany „Crankcase Presure Sensor CCP”, numer OEM 55641075000. [Dokument KTM udostępniony przez dealera KTMshop](https://www.ktmshop.se/bike-manuals/084688T_EN.pdf).

To źródło producenta w kopii dystrybutora. Numer jest identyfikatorem referencji OEM; nie jest wyborem komponentu DustONE. Katalog potwierdza obecność czujnika, bez pełnej specyfikacji elektrycznej, przypisania wszystkich zastosowań ani strategii sterowania.

## Propozycja do rozstrzygnięcia

Włączyć możliwość odczytu ciśnienia gazów w skrzyni korbowej silnika 2T z kompatybilnego czujnika OEM lub dodatkowego. Konfiguracje niewymagające tego pomiaru mogłyby działać bez czujnika.

Pomiar dotyczy ciśnienia gazów w skrzyni korbowej. Binarne wejście ciśnienia oleju ma własny zakres SYS-029, a wyłączenie sterowania dozownikiem oleju 2T nadal określają SYS-032/033. Wykonalność konwersji smarowania TPI pozostaje osobnym, zapisanym warunkiem zgodności.

## Dane na późniejsze etapy

Jeśli zakres zostanie przyjęty, w etapach 3–4 określimy źródło i pobór ciśnienia, czujniki, sygnały/zasilanie, zakres i dynamikę, diagnostykę oraz użycie w strategii. Współdzielenie torów z MAP lub potrzeba odrębnych wejść wymagają analizy wariantów i jednoczesności; liczby kanałów jeszcze nie wybrano. Dobór ważnych części pozostaje wspólny.

Do rozwinięcia w etapie 5: wzorcowanie toru i próby usterek (V03) oraz użycie w przyjętej konfiguracji silnika (V02). Brak procedur wykonawczych i wyników produktu.
