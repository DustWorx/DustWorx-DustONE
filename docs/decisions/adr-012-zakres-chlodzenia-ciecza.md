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

W odpowiedzi A na pytanie 198 (2026-11-12) właściciel dopuścił ponowne uruchomienie automatycznego chłodzenia w tym samym postoju po odzyskaniu wiarygodnego pomiaru, gdy aktualna temperatura wymaga chłodzenia, napięcie dopuszcza pracę, a pierwotny limit czasu pozostaje ważny. Wznowienie wykorzystuje pozostały czas pierwotnego limitu (SYS-188). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-188).

W odpowiedzi A na pytanie 199 (2026-11-12) właściciel wybrał ostrzeżenie na HMI po potwierdzeniu przegrzania przy wiarygodnym pomiarze podczas pracy silnika. Decyzję o zatrzymaniu z powodu przegrzania podejmuje kierowca (SYS-189). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-189).

## Uzupełnienie F03 z 2026-11-13

W odpowiedzi A na pytanie 200 (2026-11-13) właściciel zatwierdził zapis DTC z zamrożoną ramką i odrębne ostrzeżenie kierowcy na HMI po odłączeniu wentylatora przez zabezpieczenie z powodu potwierdzonego przeciążenia. Ostrzeżenie pojawia się również przy temperaturze poniżej progu przegrzania (SYS-190). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-190).

W odpowiedzi A na pytanie 201 (2026-11-13) właściciel zatwierdził utrzymanie odcięcia wentylatora po potwierdzonym przeciążeniu do sprawdzenia obwodu i świadomego odblokowania. Reguła obowiązuje również przy dalszym zapotrzebowaniu na chłodzenie (SYS-191). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-191).

W odpowiedzi na pytanie 202 (2026-11-13) właściciel wybrał potwierdzenie na HMI po usunięciu blokady lub sprawdzeniu wentylatora. ECU wykonuje próbę z pomiarem prądu zarówno przy pracującym, jak i przy zgaszonym silniku, jeśli pozostaje wybudzone. Pozytywny wynik przywraca normalne sterowanie. Nieudana próba pozostawia odcięcie oraz informację o niesprawnym wentylatorze (SYS-191–192). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-192).

Właściciel doprecyzował również zachowanie po uśpieniu. ECU przechowuje stan usterki i odcięcia, odtwarza go po wybudzeniu i sprawdza wentylator w ramach autotestu (SYS-193). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-193).
