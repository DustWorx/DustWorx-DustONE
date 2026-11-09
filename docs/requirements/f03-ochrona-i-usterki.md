# F03 — ochrona i reakcje na usterki

Stan na 2026-11-09. **F03 aktywny po zamknięciu F02.** Macierz robocza łączy zdarzenie, reakcję i warunek powrotu. Zatwierdzone wymagania są w [rejestrze SYS](../01-zakres-systemu.md). Kolejność pakietów określa [status projektu](../00-proces-i-status.md).

| Zdarzenie lub temat | Przyjęta reakcja i warunek powrotu | Do rozstrzygnięcia w F03 | Plan prób |
| --- | --- | --- | --- |
| Utrata synchronizacji wału podczas pracy | ECU odcina zapłon oraz wtrysk w wyposażonych profilach. Odzyskanie sygnału podczas dalszego obrotu utrzymuje odcięcie. Powrót wymaga zatrzymania, nowej świadomej próby rozruchu i ponownej wiarygodnej synchronizacji (SYS-157). | Wymaganie przyjęte. Kryteria rozpoznania zdarzeń do projektu. | V01, V02, V04 |
| Utrata uzyskanej synchronizacji wału podczas rozruchu elektrycznego | Obowiązują warunki START i limity rozrusznika według SYS-048/049. | Czy zakończyć bieżącą próbę po utracie synchronizacji przed potwierdzeniem pracy silnika (pytanie 168). | V01, V04 |
| Utrata sygnału fazy w profilu 4T, który go używa | Przyjęto osobne wejście Hall (SYS-070). | Reakcja i warunek powrotu zależnie od profilu. | V01, V02 |
| Przewodowy STOP i START | STOP działa przy awarii HMI lub CAN. START działa podczas przytrzymania z uzgodnionymi odcięciami i wymaganiem nowej próby po odcięciu (SYS-037/048/049). | Reakcje na usterki torów, zbieg poleceń i warunki odblokowania. | V04 |
| Potwierdzone przewrócenie | ECU wyłącza silnik. Po postawieniu i spełnieniu warunków bezpieczeństwa rozruch wymaga świadomej próby (SYS-039/040). | Warunki zadziałania i powrotu odpowiednie dla enduro. | V04 |
| Brak HMI albo CAN | ECU działa samodzielnie, a reakcje akcesoriów są odrębne (SYS-046/050–053). | Zależności od pozostałych stanów ochronnych. | V07 |
| Usterka TPS lub pomiaru ciśnienia używanego do określenia obciążenia | Przyjęto reguły kalibracji awaryjnej, kontrolowanego zatrzymania, powrotu i wymuszenia „Standard” (SYS-121–142). | Powiązać z pozostałymi blokadami F03. [Zakres F02](f02-przeglad-zakresu.md) opisuje przyjęte przypadki. | V02, V03, V04 |
| Chłodzenie i pozostałe pomiary ochronne | Przyjęto pomiar płynu i automatykę wentylatora oraz wejścia ciśnienia paliwa i binarne oleju (SYS-029/043/044/060). | Reakcje na niedostępny pomiar i na warunki poza dopuszczalnym zakresem w wyposażonych profilach. | V02, V03, V05 |
| Zasilanie i restart ECU | Przyjęto zasilanie bez stacyjki, zasady oszczędzania i odrębne reguły odtwarzania konfiguracji oraz map (SYS-054/084–089/106/109/155). | Reakcje ochronne podczas pracy silnika i warunki ponownego dopuszczenia po restarcie. | V04, V06 |

## Utrata synchronizacji wału podczas pracy

Instrukcja serwisowa Beta 250/300 RR MY2020 opisuje czujnik pick-up przy układzie zapłonu. Katalog części Beta RR 390–480 EFI MY2016 pokazuje pick-up w zespole koła magnesowego. Źródła potwierdzają zastosowanie w enduro 2T oraz 4T. [Beta 250/300 RR MY2020, rozdz. 3.11](https://betausa.com/content/SUPPORT_PDF%27s/2020%20Beta%20250%20RR%20%26%20300%20RR%20Service%20Manual.pdf), [Beta RR 390–480 EFI MY2016, katalog części](https://betausa.com/content/SUPPORT_PDF%27s/2016%20390-480%20RR%204-stroke%20and%20Race%20Edition.pdf).

W odpowiedzi A na pytanie 167 (2026-11-09) właściciel przyjął odcięcie zapłonu i wtrysku po potwierdzonej utracie synchronizacji. ECU utrzymuje odcięcie, gdy sygnał wróci przed zatrzymaniem. Po zatrzymaniu wznowienie jest możliwe w nowej świadomej próbie START lub kopniakiem, odpowiednio do wyposażenia, z wiarygodną synchronizacją i przy spełnieniu pozostałych warunków rozruchu (SYS-157). Zapis usterki i wymuszenie „Standard” podlegają SYS-019 i SYS-137. Kryteria rozpoznania zatrzymania, nowej próby i wiarygodności synchronizacji określimy w projekcie.

### Plan próby SYS-157

1. Na stanowisku odwzorować pracę silnika z poprawnym sygnałem wału. Potwierdzić utratę synchronizacji i obserwować wyjścia zapłonu oraz wtrysku odpowiednio do profilu. Przywrócić prawidłowy sygnał przed zatrzymaniem wału. Oczekiwane jest utrzymanie odcięcia.
2. Odwzorować zatrzymanie. Sprawdzić utrzymanie odcięcia bez nowej próby, w tym z przytrzymanym wcześniej START. W oddzielnych próbach zainicjować nowy rozruch przez START i kopniak zgodnie z wyposażeniem. Sprawdzić dopuszczenie sterowania po wiarygodnej synchronizacji oraz utrzymanie odcięcia przy braku wiarygodnej synchronizacji i osobno przy aktywnym STOP.
3. Powtórzyć na reprezentatywnych profilach gaźnikowych i wtryskowych oraz dla przewidzianych wejść wału. Metody wymuszenia i czasy reakcji dobrać do profilu. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Pytanie 168 — utrata synchronizacji podczas rozruchu elektrycznego

Bieżący przypadek obejmuje potwierdzoną utratę już uzyskanej synchronizacji, gdy START jest nadal wciśnięty, a ECU jeszcze nie potwierdziło pracy silnika. Wybór dotyczy odcięcia rozrusznika albo kontynuacji tej próby do uzgodnionego limitu. Rozrusznik i pick-up są udokumentowane w enduro Beta 250/300 RR MY2020. [Instrukcja serwisowa Betamotor, rozdz. 2.4.4 i 2.5](https://betausa.com/content/SUPPORT_PDF%27s/2020%20Beta%20250%20RR%20%26%20300%20RR%20Service%20Manual.pdf).
