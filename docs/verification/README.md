# Weryfikacja

Miejsce na plan weryfikacji wymagań, opisy stanowisk, procedury oraz raporty z prób.

## Odpowiedzialność i pokrycie wymagań

Asystent prowadzący inżynierię przygotowuje plan, stanowiska, dobór przyrządów, procedury z konkretnymi połączeniami i ustawieniami, oczekiwane wyniki, tolerancje oraz warunki przerwania. Właściciel wykonuje próby fizyczne i przekazuje dane. Asystent analizuje wyniki, aktualizuje status wymagań, proponuje korekty i potrzebną regresję. Procedury przygotowujemy przed odpowiadającym im etapem prób.

Każde wymaganie otrzymuje metodę potwierdzenia i dowód. Metoda może obejmować test/pomiar, analizę lub inspekcję/przegląd. Funkcje i parametry użytkowe sprawdzamy na rzeczywistym ECU/HMI/aplikacji i odpowiednich konfiguracjach silnika. Analizy konstrukcji i symulacje uzupełniają te próby.

Macierz weryfikacji ma wiązać: ID wymagania i wariant, metodę, procedurę/etap, kryterium akceptacji, rewizję badanego produktu, wynik oraz dowód. Jedno wymaganie może wymagać wielu prób; jedna próba może pokrywać kilka wymagań. Uzgodnienie wymagania, obliczenie lub odczyt danych komponentu nie zastępują wymaganej próby systemu.

## Przygotowanie i wykonanie

Stosujemy [szablon procedury i zapisu wyniku](szablon-procedury-testowej.md). Procedura gotowa do wykonania zawiera potwierdzone punkty i warunki podłączenia, właściwe przyrządy, kroki, mierzalne granice zaliczenia i przerwania oraz sposób zapisu dowodów. Brakujące dane lub kryteria pozostawiają ją w statusie projektu.

Próby prowadzimy zgodnie z gotowością: analiza i przeglądy, uruchomienie bloków, testy stanowiskowe wejść/wyjść i usterek, integracja ECU–HMI–Windows, odpowiednie silniki/motocykle oraz potrzebne próby środowiskowe i EMC. Zakres tych ostatnich określimy z wymaganiami, bez deklarowania niepotwierdzonej zgodności.

Dla próby zapisujemy co najmniej: powiązane wymagania, badaną rewizję sprzętu i oprogramowania, warunki, kryterium zaliczenia, wynik i odsyłacze do dowodów. Przy zmianie projektu określamy wpływ na wymagania i dobieramy powtórzenia/regresję. Wymagania bez dowodów pozostają niezweryfikowane.

Beta 300 RR Racing 2015 jest pierwszą konfiguracją testową. Macierz wariantów musi także objąć gaźnik z TPS, 4T i docelowe TPI/TBI; potrzebują one osobnych stanowisk i jednostek. Brak dostępnej konfiguracji zapisujemy jako ograniczenie weryfikacji.

## Bieżący stan

Przygotowano [wstępny plan inwentaryzacji Bety Racing 2015](beta-2015-plan-inwentaryzacji.md) z listą dostępnych przyrządów: multimetr, Rigol DHO804, 4 sondy PVP3150 i 3 sondy P4100. Model multimetru i dokumentacja P4100 pozostają do określenia. Przy części wymagań są propozycje prób, a powyżej określono zasady i szablon. Pełna macierz weryfikacji i kompletne procedury wykonawcze pozostają do opracowania; nie ma raportów pomiarów ani prób produktu. Kod testów i dane wejściowe obejmujące wiele komponentów należą do `tests/`.

Przeanalizowano instrukcję i suplement dostarczone przez właściciela: [wyniki i braki danych](../interfaces/beta-2015-analiza-dokumentacji.md). Rozbieżność oznaczenia rocznika suplementu i wyposażenia TPS wymaga porównania z motocyklem; schemat nie jest jeszcze zweryfikowaną mapą jego złączy.
