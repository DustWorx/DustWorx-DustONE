# ADR-003 — wybudzanie bez osobnego włącznika

Data: 2026-10-25. Status: zatwierdzone wymagania użytkowe; realizacja sprzętowa i parametry do projektu oraz weryfikacji.

## Problem i opcje

Rozważono osobny włącznik/stacyjkę albo obsługę bez niego z wybudzaniem urządzeń. Trzeba zapewnić rozruch START/kopniakiem bez HMI, obsługę przyciskami HMI oraz dostęp serwisowy z komputera.

## Decyzja i podstawa zatwierdzenia

W odpowiedzi na pytanie 64 z 2026-10-25 właściciel wybrał brak osobnego włącznika. Wskazał wybudzanie ECU przez START i kopniak, wybudzanie HMI oraz ECU przyciskami HMI, a także wybudzenie i blokadę usypiania obu urządzeń po podłączeniu komputera, w tym podczas aktualizacji. Po porównaniu wariantów w pytaniu 65 zatwierdził wymagane zasilanie serwisowe z akumulatora lub zasilacza 12 V; kabel PC służy do komunikacji i wybudzenia. W pytaniu 66 potwierdził, że START i kopniak wybudzają również HMI, z priorytetem gotowości ECU do rozruchu. W pytaniu 67 wybrał automatyczne usypianie obu urządzeń po konfigurowalnym czasie bezczynności, odnawianym używaniem przycisków, przy zgaszonym silniku, odłączonym PC i zakończonych zadaniach wymagających pracy. Wymagania: [SYS-054–059](../01-zakres-systemu.md).

W pytaniu 68 z 2026-10-25 właściciel zatwierdził konfigurowalną pracę wentylatora po zgaszeniu silnika, z limitem czasu i odcięciem przy niskim napięciu. Obsługa funkcji wstrzymuje uśpienie ECU ([SYS-060](../01-zakres-systemu.md)); przydatność dla danego układu chłodzenia wymaga weryfikacji. W pytaniu 69 tego samego dnia potwierdził wspólne ograniczenia dla automatyki oraz ręcznego wymuszenia przy zgaszonym silniku, bez możliwości ominięcia ich żądaniem HMI (SYS-061).

W pytaniu 70 z 2026-10-25 właściciel wskazał ECU jako koordynatora całego usypiania. HMI pozostaje aktywne do polecenia ECU; potwierdza przyjęcie polecenia ramką CAN, kończy nadawanie i zasypia, następnie zasypia ECU. Bezczynność odnawiają próby rozruchu i aktywność użytkownika w HMI. Ustalenie: SYS-059 oraz SYS-062/063. [Normalna sekwencja i otwarte wyjątki](../architecture/usypianie-ecu-hmi.md).

| Zdarzenie | Wymagane wybudzenie | Uwagi |
| --- | --- | --- |
| Naciśnięcie przewodowego START | ECU i HMI | Priorytet gotowości ECU; rozruch niezależny od HMI, dalsza obsługa według SYS-048/049. |
| Rozruch kopniakiem | ECU i HMI | Priorytet gotowości ECU; detekcja, sekwencja i czasy wymagają projektu. Obowiązuje założenie podłączonego akumulatora z SYS-013 i zakresu systemu. |
| Użycie przycisków obsługi HMI | HMI i ECU | Przyciski pozostają w HMI. |
| Podłączenie komputera | ECU i HMI | Przy dostępnym zasilaniu 12 V według SYS-058; utrzymana blokada usypiania obu urządzeń przez czas połączenia. |

## Konsekwencje dla projektu

- Tory wykrywania wymaganych zdarzeń muszą działać również podczas uśpienia. Wybudzanie START/kopniakiem pozostaje niezależne od HMI.
- Zaprojektować automatyczne wybudzenie HMI od START/kopniaka z priorytetem gotowości ECU. Opóźnione uruchomienie lub awaria HMI nie może blokować rozruchu ECU.
- Określić sposób przekazania wybudzenia HMI–ECU, np. przez odpowiedni tor CAN lub osobny sygnał. Nie wybrano jeszcze interfejsu wybudzania ani komponentów.
- Zaprojektować detekcję podłączenia komputera i utrzymanie blokady usypiania w obu urządzeniach, także przy bezczynności transmisji. Uwzględnić aplikację urządzeń i bootloadery. Kontrolowany restart wymagany przez aktualizację jest odrębną operacją od uśpienia.
- Rozdzielić przyczynę wybudzenia od żądania rozruchu. Użycie przycisków HMI i podłączenie komputera służą także do obsługi przy zgaszonym silniku.
- ECU inicjuje usypianie HMI poleceniem i w normalnym przebiegu oczekuje na jego aplikacyjne potwierdzenie, przed własnym uśpieniem. HMI nie zasypia autonomicznie po bezczynności.
- Odnawiać czas bezczynności po użyciu przycisków, próbach rozruchu i rzeczywistej aktywności użytkownika w HMI. Zwykły cykliczny odczyt danych i ruch CAN nie stanowią same w sobie aktywności użytkownika; podłączenie PC blokuje sen niezależnie od ruchu danych.
- Przed planowanym uśpieniem zakończyć zadania wymagające pracy, np. obsługę rozruchu i wymagane zapisy pamięci nieulotnej. Obsługa wentylatora po zgaszeniu według SYS-060/061 wstrzymuje uśpienie; HMI czeka na polecenie ECU. Limity czasu i napięcia mają pierwszeństwo przed ręcznym żądaniem HMI. Pozostałe blokady wymagają doprecyzowania.

## Do określenia

Budżet prądu czuwania, napięcia pracy i wymagania wobec zasilacza warsztatowego, detekcja kopania i zakłóceń, sekwencja zasilania i czasy gotowości ECU/zapłonu/wtrysku/HMI, zakres i wartość domyślna czasu bezczynności, początek odliczania, pozostałe zadania wstrzymujące sen i stany wyjść. Dla sekwencji usypiania ustalić formaty ramek, czasy, powiązanie potwierdzenia z bieżącą próbą, obsługę nowej aktywności i braków potwierdzenia. Dla wentylatora po zgaszeniu: wspólny limit czasu i próg napięcia, detekcja napięcia, filtracja/histereza, warunki zakończenia i ponowienia oraz przejście przy ponownym rozruchu. Dla komputera ustalić definicję wykrywanego połączenia, sposób podtrzymania blokady i bezpieczne jej zwolnienie po rozłączeniu lub przerwaniu aktualizacji.

Zasilanie serwisowe: [porównanie wariantów A/B i uzasadnienie wyboru A](../architecture/zasilanie-serwisowe-porownanie.md). Wybrano wymagane zewnętrzne zasilanie 12 V (SYS-058).

## Proponowana weryfikacja

Z uśpienia sprawdzić osobno każde zdarzenie z tabeli; potwierdzić automatyczne wybudzanie obu urządzeń. Dla START i kopniaka sprawdzić także rozruch przy niedostępnym HMI oraz opóźnionym jego uruchomieniu. Zmierzyć sekwencję zasilania, czasy wybudzenia i gotowości do rozruchu oraz prąd czuwania. Sprawdzić, że HMI i komputer mogą wybudzić urządzenia do obsługi przy zgaszonym silniku.

Przy zgaszonym silniku, odłączonym PC i braku zadań blokujących sprawdzić rozpoczęcie sekwencji po skonfigurowanym czasie. Przyciski, próby rozruchu i aktywność użytkownika w HMI mają odnowić odliczanie; sam cykliczny odczyt danych go nie odnawia. Zweryfikować kolejność polecenia, aplikacyjnego potwierdzenia, zakończenia nadawania HMI i przejść w sen; rzeczywisty stan niskiego poboru sprawdzić pomiarowo. Praca silnika, aktywne zadanie wymagające pracy i podłączony PC mają wstrzymywać sekwencję. Dodatkowe przypadki wskazano w opisie sekwencji.

Dla pracy wentylatora po zgaszeniu sprawdzić blokowanie uśpienia ECU, odcięcie po limicie czasu lub niskim napięciu także przy ręcznym żądaniu HMI i późniejsze dopuszczenie uśpienia według SYS-059 przy braku innych blokad. Szczegółowe próby funkcji są wskazane przy SYS-060/061 w zakresie systemu.

Przy zasilaniu 12 V z akumulatora i osobno z odpowiedniego zasilacza warsztatowego sprawdzić wybudzenie po podłączeniu PC oraz utrzymanie gotowości ECU/HMI mimo bezczynności, podczas diagnostyki i aktualizacji. Po rozłączeniu sprawdzić zwolnienie blokady według przyszłej specyfikacji z uwzględnieniem stanu aktualizacji. Warunki i mierzalne limity ustalić przed próbami; testów sprzętu ani firmware nie wykonano.
