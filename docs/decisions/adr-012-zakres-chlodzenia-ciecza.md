# ADR-012 — zakres silników chłodzonych cieczą

Data: 2026-11-04. Status: **zatwierdzona**.

## Decyzja i źródło

Docelowa platforma ECU obejmuje wyłącznie jednocylindrowe silniki 2T/4T chłodzone cieczą, z wymaganym pomiarem temperatury płynu. Wariant obejmujący także chłodzenie powietrzem został wyłączony.

Źródło: odpowiedź właściciela **B na pytanie 107**: „Tylko silniki chłodzone cieczą — wymagamy pomiaru temperatury płynu”.

Decyzję zapisano w SYS-098; pomiar temperatury płynu pozostaje w SYS-044. Pozostałe przyjęte warianty zasilania paliwem i wspólna PCB pozostają określone przez dotychczasowe wymagania.

## Skutki

Macierz wariantów i kwalifikacja modeli podlegają ograniczeniu chłodzenia cieczą. Dla tej platformy nie projektujemy funkcji temperatury silnika chłodzonego powietrzem. Miejsce pomiaru płynu, czujniki, zakres, dokładność i realizację określimy w etapach 3–6; ważne części wybierzemy wspólnie.

Przegląd pomiarów F01 został zakończony. Weryfikacja obejmie kontrolę zadeklarowanego zakresu i wymagany pomiar płynu w odpowiednich konfiguracjach, według grup V03/V13. Parametry i procedury wykonawcze oraz dowody produktu pozostają do opracowania.
