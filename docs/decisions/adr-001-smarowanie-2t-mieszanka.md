# ADR-001 — smarowanie silników 2T mieszanką

Data: 2026-10-18  
Status: zatwierdzona decyzja właściciela dotycząca zakresu ECU i warunku montażu; konwersja TPI pozostaje niezweryfikowana.

## Decyzja

ECU nie steruje pompą dozującą olej 2T. Silnik 2T ma pracować na mieszance przygotowanej w zbiorniku. W motocyklach z oddzielnym dozowaniem właściciel wymaga sprzętowego usunięcia pompy i przejścia na mieszankę.

Podstawa: odpowiedź właściciela na pytanie 28 i jej doprecyzowanie w rozmowie projektowej z 2026-10-18. Wymagania: [SYS-032 i SYS-033](../01-zakres-systemu.md).

## Konsekwencje techniczne

- Nie przewidujemy dedykowanej funkcji sprzętowej ani programowej dozowania oleju 2T.
- Warunek montażu obejmuje poprawne przystosowanie układu paliwowego i smarowania do mieszanki; sprawdzenie dotyczy konkretnego modelu i konwersji.
- Samo usunięcie pompy nie stanowi zatwierdzonej konwersji TPI. Wcześniejszy cel obsługi wtrysku TPI pozostaje warunkowy w zakresie montażu; nie deklarujemy zgodności niezweryfikowanej przeróbki.
- Sposób konwersji, kryteria i plan jej walidacji pozostają do opracowania. Ta decyzja nie zatwierdza konkretnej procedury usunięcia dozownika ani uruchomienia tak przerobionego silnika.

## Podstawa oceny TPI

[Instrukcja KTM 250/300 EXC TPI MY2022, rozdziały 9.8–9.9, s. 49](https://en.enduro.team/images/9/9a/2022_KTM_250-300_EXC_TPI_OM_eng.pdf) wymaga oddzielnego oleju i wyklucza tankowanie mieszanki w konfiguracji fabrycznej. [Opis KTM](https://www.ktm.com/en-ph/models/enduro/2-stroke/ktm-300-exc-tpi-sixdays2022.html) wskazuje podawanie oleju do przepustnicy, m.in. dla smarowania wału korbowego, oraz wtrysk paliwa do kanałów przepłukujących. Wniosek projektowy: zdolność do poprawnej pracy na mieszance wymaga osobnego wykazania po zmianie konfiguracji.
