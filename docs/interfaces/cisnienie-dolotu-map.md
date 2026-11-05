# Ciśnienie dolotu MAP — przegląd F01

Stan na: 2026-11-04. **Zakres funkcji MAP zatwierdzony; temat funkcjonalny zamknięty 2026-11-04.** Powiązanie: F01, [macierz wariantów](../architecture/macierz-wariantow-silnika.md) i [lista I/O](wstepna-lista-io.md). Źródło: odpowiedź właściciela A na pytanie 105; dodano SYS-096. Czujnika i komponentów toru nie wybrano.

## Podstawa

Beta RR 350 EFI MY2016: [schemat producenta](https://betausa.com/content/WIRING%20DIAGRAM%204T%202%2024%20new.pdf), strony PDF 8–9, opis rodziny 2015 350 / 2016–2017 350–480 RR/Race. Legenda poz. 30 wskazuje T-MAP, łączący temperaturę i ciśnienie bezwzględne w kolektorze dolotowym.

To dowód występowania pomiaru w enduro; parametry i pinout czujnika wymagają dalszej analizy. Ten przykład nie zatwierdza listy kompatybilnych modeli.

## Znaczenie dla wspólnej PCB

IAT jest już wymagane przez SYS-031. MAP jest odrębnym pomiarem ciśnienia dolotu; barometr na PCB według SYS-030 służy do pomiaru ciśnienia atmosferycznego. Tor wartości ciśnienia paliwa według SYS-029 także ma odrębną funkcję.

**Przyjęty zakres:** odczyt MAP z kompatybilnego czujnika OEM lub dodatkowego. Konfiguracje niewymagające MAP mogą działać bez podłączonego czujnika. W modelu z T-MAP należy rozpoznać oba sygnały i ich zasilanie, zachowując wymagany odczyt IAT.

Przed doborem elektroniki określamy model i charakterystykę czujnika, zakres ciśnień, zasilanie/sygnał, dokładność, częstotliwość, zabezpieczenia i diagnostykę. Liczbę wejść bilansujemy z równoczesnymi pomiarami, w tym ciśnieniem paliwa. Strategie wtrysku i wymagania pomiarów innych ciśnień rozwijamy dla konkretnych jednostek; nie wynikają automatycznie z samego dodania wejścia MAP.

## Weryfikacja do rozwinięcia w etapie 5

Grupa V03: wzorcowe ciśnienie i rzeczywisty czujnik, błąd toru w przyjętym zakresie, próby przerwy/zwarcia i konfiguracji bez MAP. Grupa V02: wykorzystanie danych w przyjętej strategii na właściwym silniku. Kryteria liczbowe i procedury przed wykonaniem prób.

Zamknięcie dotyczy zakresu funkcji. Parametry osprzętu, rozwiązanie toru i potwierdzenie zgodności czujników pozostają w kolejce etapów 3–6 i późniejszych prób. SYS-096, lista I/O, warianty i przydział weryfikacji zostały powiązane z decyzją.
