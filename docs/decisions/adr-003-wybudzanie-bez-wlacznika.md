# ADR-003 — wybudzanie bez osobnego włącznika

Data: 2026-10-25. Status: zatwierdzone wymagania użytkowe; realizacja sprzętowa i parametry do projektu oraz weryfikacji.

## Problem i opcje

Rozważono osobny włącznik/stacyjkę albo obsługę bez niego z wybudzaniem urządzeń. Trzeba zapewnić rozruch START/kopniakiem bez HMI, obsługę przyciskami HMI oraz dostęp serwisowy z komputera.

## Decyzja i podstawa zatwierdzenia

W odpowiedzi na pytanie 64 z 2026-10-25 właściciel wybrał brak osobnego włącznika. Wskazał wybudzanie ECU przez START i kopniak, wybudzanie HMI oraz ECU przyciskami HMI, a także wybudzenie i blokadę usypiania obu urządzeń po podłączeniu komputera, w tym podczas aktualizacji. Po porównaniu wariantów w pytaniu 65 zatwierdził wymagane zasilanie serwisowe z akumulatora lub zasilacza 12 V; kabel PC służy do komunikacji i wybudzenia. Wymagania: [SYS-054–058](../01-zakres-systemu.md).

| Zdarzenie | Wymagane wybudzenie | Uwagi |
| --- | --- | --- |
| Naciśnięcie przewodowego START | ECU | Niezależnie od HMI; dalsza obsługa rozruchu według SYS-048/049. |
| Rozruch kopniakiem | ECU | Detekcja i czas gotowości wymagają projektu; obowiązuje założenie podłączonego akumulatora z SYS-013 i zakresu systemu. |
| Użycie przycisków obsługi HMI | HMI i ECU | Przyciski pozostają w HMI. |
| Podłączenie komputera | ECU i HMI | Przy dostępnym zasilaniu 12 V według SYS-058; utrzymana blokada usypiania obu urządzeń przez czas połączenia. |

## Konsekwencje dla projektu

- Tory wykrywania wymaganych zdarzeń muszą działać również podczas uśpienia. Wybudzanie START/kopniakiem pozostaje niezależne od HMI.
- Określić sposób przekazania wybudzenia HMI–ECU, np. przez odpowiedni tor CAN lub osobny sygnał. Nie wybrano jeszcze interfejsu wybudzania ani komponentów.
- Zaprojektować detekcję podłączenia komputera i utrzymanie blokady usypiania w obu urządzeniach, także przy bezczynności transmisji. Uwzględnić aplikację urządzeń i bootloadery. Kontrolowany restart wymagany przez aktualizację jest odrębną operacją od uśpienia.
- Rozdzielić przyczynę wybudzenia od żądania rozruchu. Użycie przycisków HMI i podłączenie komputera służą także do obsługi przy zgaszonym silniku.

## Do określenia

Budżet prądu czuwania, napięcia pracy i wymagania wobec zasilacza warsztatowego, detekcja kopania i zakłóceń, czasy gotowości ECU/zapłonu/wtrysku, wybudzanie HMI od START/kopniaka, zasady zasypiania bez komputera i stany wyjść. Dla komputera ustalić definicję wykrywanego połączenia, sposób podtrzymania blokady i bezpieczne jej zwolnienie po rozłączeniu lub przerwaniu aktualizacji.

Zasilanie serwisowe: [porównanie wariantów A/B i uzasadnienie wyboru A](../architecture/zasilanie-serwisowe-porownanie.md). Wybrano wymagane zewnętrzne zasilanie 12 V (SYS-058).

## Proponowana weryfikacja

Z uśpienia sprawdzić osobno każde zdarzenie z tabeli; START i kopniak także przy niedostępnym HMI. Zmierzyć czasy wybudzenia i gotowości do rozruchu oraz prąd czuwania. Sprawdzić, że HMI i komputer mogą wybudzić urządzenia do obsługi przy zgaszonym silniku.

Przy zasilaniu 12 V z akumulatora i osobno z odpowiedniego zasilacza warsztatowego sprawdzić wybudzenie po podłączeniu PC oraz utrzymanie gotowości ECU/HMI mimo bezczynności, podczas diagnostyki i aktualizacji. Po rozłączeniu sprawdzić zwolnienie blokady według przyszłej specyfikacji z uwzględnieniem stanu aktualizacji. Warunki i mierzalne limity ustalić przed próbami; testów sprzętu ani firmware nie wykonano.
