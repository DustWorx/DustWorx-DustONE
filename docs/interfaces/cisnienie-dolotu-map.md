# Ciśnienie dolotu MAP — przegląd F01

Stan na: 2026-11-04. **Potwierdzony przykład OEM; obsługa MAP w DustONE jest propozycją przed decyzją.** Powiązanie: F01, [macierz wariantów](../architecture/macierz-wariantow-silnika.md) i [lista I/O](wstepna-lista-io.md). Nie dodano nowego wymagania SYS ani nie wybrano komponentu.

## Podstawa

Beta RR 350 EFI MY2016: [schemat producenta](https://betausa.com/content/WIRING%20DIAGRAM%204T%202%2024%20new.pdf), strony PDF 8–9, opis rodziny 2015 350 / 2016–2017 350–480 RR/Race. Legenda poz. 30 wskazuje T-MAP, łączący temperaturę i ciśnienie bezwzględne w kolektorze dolotowym.

To dowód występowania pomiaru w enduro; parametry i pinout czujnika wymagają dalszej analizy. Ten przykład nie zatwierdza listy kompatybilnych modeli.

## Znaczenie dla wspólnej PCB

IAT jest już wymagane przez SYS-031. MAP jest odrębnym pomiarem ciśnienia dolotu; barometr na PCB według SYS-030 służy do pomiaru ciśnienia atmosferycznego. Tor wartości ciśnienia paliwa według SYS-029 także ma odrębną funkcję.

**Propozycja do uzgodnienia:** umożliwić odczyt MAP z kompatybilnego czujnika OEM lub dodatkowego. Konfiguracje niewykorzystujące MAP działałyby bez podłączonego czujnika. W modelu z T-MAP należy rozpoznać oba sygnały i ich zasilanie, zachowując wymagany odczyt IAT.

Przed doborem elektroniki określamy model i charakterystykę czujnika, zakres ciśnień, zasilanie/sygnał, dokładność, częstotliwość, zabezpieczenia i diagnostykę. Liczbę wejść bilansujemy z równoczesnymi pomiarami, w tym ciśnieniem paliwa. Strategie wtrysku i wymagania pomiarów innych ciśnień rozwijamy dla konkretnych jednostek; nie wynikają automatycznie z samego dodania wejścia MAP.

## Weryfikacja po ewentualnym przyjęciu

Grupa V03: wzorcowe ciśnienie i rzeczywisty czujnik, błąd toru w przyjętym zakresie, próby przerwy/zwarcia i konfiguracji bez MAP. Grupa V02: wykorzystanie danych w przyjętej strategii na właściwym silniku. Kryteria liczbowe i procedury przed wykonaniem prób.

Następna decyzja produktowa: czy włączyć obsługę MAP do zakresu wspólnej PCB. Dopiero po odpowiedzi aktualizujemy SYS, listę I/O, warianty i przydział weryfikacji.
