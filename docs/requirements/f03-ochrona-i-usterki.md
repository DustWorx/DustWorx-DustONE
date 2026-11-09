# F03 — ochrona i reakcje na usterki

Stan na 2026-11-09. **F03 aktywny po zamknięciu F02.** Macierz robocza łączy zdarzenie, reakcję i warunek powrotu. Zatwierdzone wymagania są w [rejestrze SYS](../01-zakres-systemu.md). Kolejność pakietów określa [status projektu](../00-proces-i-status.md).

| Zdarzenie lub temat | Przyjęta reakcja i warunek powrotu | Do rozstrzygnięcia w F03 | Plan prób |
| --- | --- | --- | --- |
| Utrata synchronizacji wału podczas pracy | Przyjęto obsługę czujników VR i Hall (SYS-069). | Pierwsza decyzja dotyczy wznowienia sterowania po odzyskaniu synchronizacji (pytanie 167). | V01, V02, V04 |
| Utrata sygnału fazy w profilu 4T, który go używa | Przyjęto osobne wejście Hall (SYS-070). | Reakcja i warunek powrotu zależnie od profilu. | V01, V02 |
| Przewodowy STOP i START | STOP działa przy awarii HMI lub CAN. START działa podczas przytrzymania z uzgodnionymi odcięciami i wymaganiem nowej próby po odcięciu (SYS-037/048/049). | Reakcje na usterki torów, zbieg poleceń i warunki odblokowania. | V04 |
| Potwierdzone przewrócenie | ECU wyłącza silnik. Po postawieniu i spełnieniu warunków bezpieczeństwa rozruch wymaga świadomej próby (SYS-039/040). | Warunki zadziałania i powrotu odpowiednie dla enduro. | V04 |
| Brak HMI albo CAN | ECU działa samodzielnie, a reakcje akcesoriów są odrębne (SYS-046/050–053). | Zależności od pozostałych stanów ochronnych. | V07 |
| Usterka TPS lub pomiaru ciśnienia używanego do określenia obciążenia | Przyjęto reguły kalibracji awaryjnej, kontrolowanego zatrzymania, powrotu i wymuszenia „Standard” (SYS-121–142). | Powiązać z pozostałymi blokadami F03. [Zakres F02](f02-przeglad-zakresu.md) opisuje przyjęte przypadki. | V02, V03, V04 |
| Chłodzenie i pozostałe pomiary ochronne | Przyjęto pomiar płynu i automatykę wentylatora oraz wejścia ciśnienia paliwa i binarne oleju (SYS-029/043/044/060). | Reakcje na niedostępny pomiar i na warunki poza dopuszczalnym zakresem w wyposażonych profilach. | V02, V03, V05 |
| Zasilanie i restart ECU | Przyjęto zasilanie bez stacyjki, zasady oszczędzania i odrębne reguły odtwarzania konfiguracji oraz map (SYS-054/084–089/106/109/155). | Reakcje ochronne podczas pracy silnika i warunki ponownego dopuszczenia po restarcie. | V04, V06 |

## Pytanie 167 — powrót po utracie synchronizacji wału

Instrukcja serwisowa Beta 250/300 RR MY2020 opisuje czujnik pick-up przy układzie zapłonu. Katalog części Beta RR 390–480 EFI MY2016 pokazuje pick-up w zespole koła magnesowego. Źródła potwierdzają zastosowanie w enduro 2T oraz 4T. [Beta 250/300 RR MY2020, rozdz. 3.11](https://betausa.com/content/SUPPORT_PDF%27s/2020%20Beta%20250%20RR%20%26%20300%20RR%20Service%20Manual.pdf), [Beta RR 390–480 EFI MY2016, katalog części](https://betausa.com/content/SUPPORT_PDF%27s/2016%20390-480%20RR%204-stroke%20and%20Race%20Edition.pdf).

W obu proponowanych wariantach po potwierdzonej utracie synchronizacji ECU wyłącza zapłon i wtrysk tam, gdzie występuje. Wariant A utrzymuje odcięcie do zatrzymania silnika i świadomej nowej próby rozruchu ze sprawną synchronizacją. Wariant B pozwala wznowić sterowanie po wiarygodnej ponownej synchronizacji podczas dalszego obrotu silnika, jeśli pozostałe warunki bezpieczeństwa są spełnione. Po zatrzymaniu również w wariancie B potrzebna jest nowa próba. Warunki rozpoznania utraty, odzyskania oraz zatrzymania określimy dla przyjętej strategii.

Do zaplanowania na stanowisku są potwierdzona utrata i powrót synchronizacji podczas obrotu oraz po zatrzymaniu, obserwacja wyjść i sprawdzenie zachowania przy aktywnym STOP. Po decyzji ustalimy kryteria i przypadki dla właściwych profili. [Macierz weryfikacji](../verification/macierz-wymagan.md).
