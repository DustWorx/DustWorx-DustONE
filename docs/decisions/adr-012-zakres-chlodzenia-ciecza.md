# ADR-012 — zakres silników chłodzonych cieczą

Data: 2026-11-04. Status: **zatwierdzona**.

## Decyzja i źródło

Docelowa platforma ECU obejmuje wyłącznie jednocylindrowe silniki 2T/4T chłodzone cieczą, z wymaganym pomiarem temperatury płynu. Wariant obejmujący także chłodzenie powietrzem został wyłączony.

Źródło: odpowiedź właściciela **B na pytanie 107**: „Tylko silniki chłodzone cieczą — wymagamy pomiaru temperatury płynu”.

Decyzję zapisano w SYS-098; pomiar temperatury płynu pozostaje w SYS-044. Pozostałe przyjęte warianty zasilania paliwem i wspólna PCB pozostają określone przez dotychczasowe wymagania.

## Skutki

Macierz wariantów i kwalifikacja modeli podlegają ograniczeniu chłodzenia cieczą. Dla tej platformy nie projektujemy funkcji temperatury silnika chłodzonego powietrzem. Miejsce pomiaru płynu, czujniki, zakres, dokładność i realizację określimy w etapach 3–6; ważne części wybierzemy wspólnie.

Przegląd pomiarów F01 został zakończony. Weryfikacja obejmie kontrolę zadeklarowanego zakresu i wymagany pomiar płynu w odpowiednich konfiguracjach, według grup V03/V13. Parametry i procedury wykonawcze oraz dowody produktu pozostają do opracowania.

## Uzupełnienie F03 z 2026-11-12

W odpowiedzi **A na pytanie 194** właściciel zatwierdził automatyczne włączenie sprawnego wentylatora podczas pracy silnika, gdy ECU potwierdzi usterkę pomiaru temperatury płynu. ECU zapisuje DTC z zamrożoną ramką (SYS-184). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-184).

W odpowiedzi **A na pytanie 195** właściciel zatwierdził zakończenie tego wymuszenia po potwierdzeniu zatrzymania silnika przy utrzymującej się usterce, także w profilu z włączonym chłodzeniem po zgaszeniu (SYS-185). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-185).

W odpowiedzi A na pytanie 196 (2026-11-12) właściciel dopuścił ręczne włączenie sprawnego wentylatora z HMI przy zgaszonym silniku, wybudzonym ECU i nadal potwierdzonej usterce pomiaru temperatury płynu. Obowiązują limit czasu, odcięcie przy niskim napięciu (SYS-061) oraz zabezpieczenia wyjścia (SYS-186). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-186).

W odpowiedzi A na pytanie 197 (2026-11-12) właściciel zatwierdził zakończenie trwającego chłodzenia automatycznego po zgaszeniu silnika, gdy ECU potwierdzi usterkę pomiaru temperatury płynu (SYS-187). Aktywne ręczne żądanie może nadal podtrzymywać pracę wentylatora zgodnie z SYS-186. [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-187).
