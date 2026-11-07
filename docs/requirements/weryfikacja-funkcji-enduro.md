# Sprawdzanie funkcji w motocyklach enduro

Data: 2026-11-01. Zasada pracy przyjęta przez właściciela. Statusy funkcji zapisano przy przykładach; zgodność konkretnych czujników i napędów z DustONE wymaga analizy oraz prób.

## Podstawa pytania

Przed propozycją nowej funkcji silnika lub osprzętu przygotowujemy:

- konkretny model enduro, rocznik i wersję, do których odnosi się przykład;
- źródło producenta: instrukcję, schemat lub katalog, z numerem strony/pozycji;
- potwierdzony sposób realizacji i jawne braki danych;
- związek z zakresem DustONE, zachowaniem OEM oraz skutki dla I/O, komponentów, gabarytów i testów.

Rozróżniamy wyposażenie konkretnego modelu, docelową funkcję wskazaną przez właściciela oraz propozycję rozszerzenia. Materiały producentów uniwersalnych ECU i półprzewodników pomagają dobrać realizację; występowanie funkcji w danym enduro potwierdzamy w dokumentacji tego motocykla. Przykłady z innych kategorii pojazdów wymagają osobnego uzasadnienia. Znajomość wyposażenia nie stanowi jeszcze potwierdzenia zgodności elektrycznej.

## Przykład — regulacja biegu jałowego IAC

| Enduro / rocznik | Potwierdzone dane | Znaczenie dla projektu |
| --- | --- | --- |
| Beta RR 350/390/430/480 EFI, 2016 | Instrukcja, s. 33: bieg jałowy sterowany przez ECU; obok opisano linkę gazu. Schemat dla RR/Race 350–480 z lat 2016–2017: legenda, poz. 46 — silnik krokowy; poz. 47 — przepustnica. | Istnieje rzeczywisty przypadek enduro 4T uzasadniający rozważenie IAC z napędem krokowym przy zachowaniu osprzętu OEM. Parametry napędu i tor mocy wymagają analizy. |
| KTM 300 EXC Six Days, 2023, EU | Katalog przepustnicy 55590: poz. 5 — śruba biegu jałowego, poz. 6 — przycisk zimnego rozruchu. | Potwierdzona ręczna regulacja; nie przenosimy automatycznie rozwiązania Bety do każdego enduro lub każdej generacji wtrysku. Sam katalog nie jest specyfikacją całego sterowania silnikiem. |

Źródła:

- [Beta USA — instrukcja RR 4T EFI 2016, s. 33](https://betausa.com/content/SUPPORT_PDF%27s/2016%20RR%204%20stroke%20owners%20manual_0.pdf), wskazana w [indeksie producenta](https://betausa.com/off-road-support/).
- [Beta USA — schematy RR/Race 4T 2005–2024](https://betausa.com/content/WIRING%20DIAGRAM%204T%202%2024%20new.pdf), strony PDF 8–9: model 2015 350 / 2016–2017 350–480 oraz legenda poz. 46/47. To odniesienie do opublikowanego dokumentu, bez kopiowania oryginału do repozytorium.
- [KTM — katalog przepustnicy 300 EXC Six Days 2023, pozycje 5/6](https://sparepartsfinder.ktm.com/ComponentGroupTemplate/PrintComponentGroupTemplate/55590?culture=en&modelidentifier=1002337401&tenantId=1).

Po sprawdzeniu przykładów właściciel w odpowiedzi na poprawione pytanie 77 z 2026-11-01 przyjął IAC z napędem krokowym dla potwierdzonych modeli enduro. Zakres zapisuje SYS-071 w [PR #11](https://github.com/DustWorx/DustWorx-DustONE/pull/11). Przed wyborem elektroniki potrzebne są parametry uzwojeń/sterowania, kalibracja, wymagane zasoby, zachowanie przy usterce i plan prób. Nie przyjęto obsługi wszystkich zaworów IAC ani napędów krokowych.

## Potwierdzony przykład, funkcja wyłączona — kontrola trakcji

KTM potwierdza opcjonalną kontrolę trakcji w rodzinie EXC-F MY2024: 250, 350, 450 i 500. Funkcja jest obsługiwana opcjonalnym przełącznikiem wyboru map. [Komunikat producenta z 2023-05-24 o MY2024](https://press.ktm.com/news-challenge-accepted-the-2024-ktm-exc-range-is-here-to-redefine-limits?id=179901&l=uk&menueid=5904).

W odpowiedzi na pytanie 78 z 2026-11-01 właściciel wyłączył kontrolę trakcji z zakresu DustONE. Wyłączenie zapisuje SYS-072 w [PR #11](https://github.com/DustWorx/DustWorx-DustONE/pull/11). Potwierdzone wyposażenie OEM nie oznacza automatycznego włączenia funkcji do projektu. Quickshifter pozostaje poza zakresem zgodnie z SYS-042; pozostałe uzgodnione pomiary zachowują swoje wymagania.

## Potwierdzony przykład, funkcja przyjęta — sygnalizacja rezerwy paliwa

Beta RR 350/390/430/480 EFI 2016 ma kontrolkę rezerwy paliwa: [instrukcja, s. 20 oraz s. 25, punkt 7.3](https://betausa.com/content/SUPPORT_PDF%27s/2016%20RR%204%20stroke%20owners%20manual_0.pdf). [Schemat Beta USA, strony PDF 8–9](https://betausa.com/content/WIRING%20DIAGRAM%204T%202%2024%20new.pdf) wskazuje czujnik rezerwy w poz. 31 i kontrolkę w poz. 17.

W odpowiedzi na pytanie 79 z 2026-11-01 właściciel przyjął opcjonalny odczyt czujnika rezerwy przez ECU i ostrzeżenie na HMI. Konfiguracje bez czujnika działają bez tej funkcji. Wymaganie SYS-073 zapisano w [PR #11](https://github.com/DustWorx/DustWorx-DustONE/pull/11). Interfejs elektryczny czujnika, ewentualne pobudzenie, tor pomiarowy, filtracja i diagnostyka wymagają sprawdzenia; z samej binarnej informacji użytkowej o rezerwie nie wynika typ wejścia sprzętowego.

## Przyjęte liczniki całkowite — motogodziny i ODO

Instrukcja Beta RR 125/200/250/300 2T Standard/Race MY2020 wymienia łączny licznik godzin oraz dwa dodatkowe, kasowalne liczniki A/B: [dokument producenta, s. 25 oraz 28–29](https://betausa.com/content/SUPPORT_PDF%27s/2020%20Beta%20RR%202-Stroke%20Owners%20Manual.pdf).

W odpowiedzi na pytanie 80 i doprecyzowaniu z 2026-11-01 właściciel wybrał całkowite motogodziny oraz ODO, oba odporne na manipulację i bez ustawiania, korekty lub kasowania przez użytkownika końcowego. Zakres zapisują SYS-074–076 i ADR-007 w [PR #11](https://github.com/DustWorx/DustWorx-DustONE/pull/11). Liczniki pomocnicze A/B nie wchodzą do ustalenia. To również jawne wymaganie właściciela, niezależne od sposobu działania fabrycznego wyświetlacza. W odpowiedzi A na pytanie 81 tego samego dnia właściciel zatwierdził chronioną procedurę producenta/serwisu do inicjalizacji nowego ECU i przenoszenia udokumentowanych wartości, z rejestrem każdej operacji. SYS-077 i doprecyzowanie ADR-007 zapisano w [PR #12](https://github.com/DustWorx/DustWorx-DustONE/pull/12). Kryteria naliczania, dokładność, trwałość, mechanizmy ochrony oraz szczegóły tej procedury wymagają projektu.

## Przykład — mapy elektronicznego zaworu wydechowego 2T

KTM opisuje zastosowanie TBI i elektronicznego zaworu wydechowego w gamie EXC 2T MY2024, obejmującej 300 EXC HARDENDURO. [Materiał KTM o gamie EXC MY2024](https://www.ktm.com/en-ca/ktm-world/stories/the-2024-ktm-exc-roars-through-lesotho.html).

W dokumentacji narzędzia strojenia TSP ERM dla KTM 2T TBI opisano osobne korekty położenia zaworu dla białego i zielonego trybu. W DustONE sterowanie zaworem jest przyjęte w SYS-034. W odpowiedzi A na pytanie 128 (2026-11-07) właściciel przyjął odrębną mapę zaworu dla każdego zestawu wyposażonej konfiguracji 2T (SYS-119). [Instrukcja TSP ERM, sekcja 6.4, s. 25](https://www.tsp-erm.com/wp-content/uploads/user_guide/ERM-User-Guide-KTM-2T.pdf#page=25).

## Przykład — TPS w mapie zapłonu gaźnikowego enduro

W instrukcji Yamaha WR450F MY2003 opisano zapłon CDI, który wyznacza kąt zapłonu z prędkości obrotowej silnika oraz otwarcia przepustnicy mierzonego przez TPS. W odpowiedzi A na pytanie 129 (2026-11-07) właściciel przyjął dla gaźnika krzywą obrotową bez TPS albo mapę od obrotów i położenia przepustnicy z TPS (SYS-120). Brak TPS w referencyjnej Becie potwierdził właściciel w odpowiedzi na pytanie 45. [Instrukcja serwisowa Yamaha WR450F MY2003, rozdział Map-Controlled CDI Unit](https://www.manualslib.mx/manual/564547/Yamaha-Wr450F-2003.html?page=644).

## Przykład — praca po wykryciu usterki TPS

Instrukcja wtryskowej Yamaha WR450FB MY2012 przewiduje rozruch i jazdę w trybie awaryjnym po wykryciu przerwy lub zwarcia obwodu TPS. To przykład zachowania motocykla enduro po utracie sygnału. Reakcja w gaźnikowym wariancie DustONE korzystającym z TPS jest otwartą decyzją F02. [Instrukcja serwisowa Yamaha WR450FB, nr 1DX-28199-10, kod 15, s. 9-37](https://www.motopetersburg.ru/docs/yamaha-wr450FB-2012-2015-owners-service-manual.pdf).
