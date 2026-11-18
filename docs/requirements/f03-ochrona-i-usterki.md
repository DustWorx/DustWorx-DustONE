# F03 — ochrona i reakcje na usterki

Stan na 2026-11-18. **F03 aktywny po zamknięciu F02.** Macierz robocza łączy zdarzenie, reakcję i warunek powrotu. Zatwierdzone wymagania są w [rejestrze SYS](../01-zakres-systemu.md). Kolejność pakietów określa [status projektu](../00-proces-i-status.md).

| Zdarzenie lub temat | Przyjęta reakcja i warunek powrotu | Do rozstrzygnięcia w F03 | Plan prób |
| --- | --- | --- | --- |
| Utrata synchronizacji wału podczas pracy | ECU odcina zapłon oraz wtrysk w wyposażonych profilach. Odzyskanie sygnału podczas dalszego obrotu utrzymuje odcięcie. Powrót wymaga zatrzymania, nowej świadomej próby rozruchu i ponownej wiarygodnej synchronizacji (SYS-157). | Wymaganie przyjęte. Kryteria rozpoznania zdarzeń do projektu. | V01, V02, V04 |
| Utrata uzyskanej synchronizacji wału podczas rozruchu elektrycznego | Potwierdzona utrata przed rozpoznaniem pracy silnika kończy próbę. ECU wyłącza rozrusznik także przy przytrzymanym START. Ponowna próba wymaga zatrzymania, zwolnienia i ponownego naciśnięcia START (SYS-158). | Wymaganie przyjęte. Kryteria utraty synchronizacji i zatrzymania do projektu. | V01, V04 |
| Utrata uzyskanej synchronizacji wału podczas rozruchu kopniakiem | Potwierdzona utrata kończy próbę. Powrót sygnału przy dalszym obrocie utrzymuje odcięcie zapłonu i wtrysku. Wznowienie wymaga zatrzymania wału i nowej próby z wiarygodną synchronizacją (SYS-159). | Wymaganie przyjęte. Kryteria zatrzymania i rozpoznania nowej próby do projektu. | V01, V02, V04 |
| Utrata sygnału fazy w profilu 4T, który go używa | Wejście Hall według SYS-070. W 4T o stałych fazach brak impulsów po synchronizacji przy wiarygodnym cyklu i wale pozwala kontynuować sterowanie z DTC (SYS-205). Nowe uruchomienie wymaga prawidłowego sygnału fazy i cyklu 720° (SYS-206). Potwierdzona niezgodność obecnych sygnałów fazy i wału odcina zapłon i wtrysk do zatrzymania oraz nowej świadomej próby z prawidłową synchronizacją (SYS-207). | Wymagania dla opisanych przypadków przyjęte. Kryteria zgodności i diagnostyki, tolerancje, filtracja, czasy oraz pokrycie dekoderów do projektu i prób. | V01, V02, V03, V04, V07, V10 |
| Przewodowy STOP i START | STOP działa przy awarii HMI lub CAN. START działa podczas przytrzymania z uzgodnionymi odcięciami i wymaganiem nowej próby po odcięciu (SYS-037/048/049). Naciśnięcie START przy aktywnym STOP utrzymuje rozrusznik wyłączony. Zwolnienie STOP wymaga nowego START (SYS-160). STOP wykryty podczas kręcenia wyłącza rozrusznik i kończy próbę. Ponowienie wymaga nowego START po zwolnieniu STOP (SYS-161). Po użyciu STOP podczas pracy odcięcie trwa do zatrzymania wału i nowej próby z wiarygodną synchronizacją (SYS-162). Wybudzone ECU wykrywa przerwę w obwodzie także przy zwolnionym STOP (SYS-163). Potwierdzona przerwa wywołuje reakcję diagnostyczną. ECU kontynuuje pracę i dopuszcza nową próbę rozruchu przy spełnieniu pozostałych warunków (SYS-164). ECU rozróżnia zwarcie przewodu STOP do masy od naciśnięcia przycisku (SYS-165). Zwarcie do masy skutkuje zapisem DTC. ECU dopuszcza dalszą pracę i nową próbę rozruchu przy spełnieniu pozostałych warunków (SYS-166). Sprawny STOP odcina zapłon i wtrysk oraz odłącza rozrusznik niezależnie od głównego firmware (SYS-167–168). Przy zwykłym wybudzeniu obsługę START przytrzymanego podczas autotestu określa SYS-204. | Parametry i realizacja toru do projektu. | V03, V04, V10, V13 |
| Potwierdzone przewrócenie | ECU wyłącza silnik. Po postawieniu i spełnieniu warunków bezpieczeństwa rozruch wymaga świadomej próby (SYS-039/040). Przy sprawnym torze i START naciśniętym przed postawieniem rozrusznik czeka na zwolnienie i nowe naciśnięcie (SYS-197). Zwolnienie blokady przy potwierdzonej usterce podlega SYS-200. Po wybudzeniu ECU ustala blokadę rozruchu na podstawie aktualnego, wiarygodnego pomiaru położenia (SYS-202). | Kryteria położenia, czasy potwierdzenia i budżet czasu gotowości do projektu. | V03, V04, V06, V07 |
| Usterka toru wykrywania przewrócenia | Usterka toru wykrywania przewrócenia podczas pracy silnika bez aktywnej blokady skutkuje dalszą pracą, zapisem DTC z zamrożoną ramką i ostrzeżeniem na HMI (SYS-198). Przy nieaktywnej blokadzie ECU dopuszcza świadomą próbę rozruchu, jeśli spełniono pozostałe warunki. HMI ostrzega o niedostępności wykrywania (SYS-199). Potwierdzona usterka toru zwalnia aktywną blokadę po przewróceniu i wywołuje ostrzeżenie. Rozruch wymaga nowej świadomej próby i spełnienia pozostałych warunków (SYS-200). Po odzyskaniu wiarygodnego pomiaru ECU przywraca wykrywanie przewrócenia jeszcze podczas bieżącej pracy silnika (SYS-201). | Kryteria potwierdzenia usterki i odzyskania wiarygodności do projektu. | V02, V03, V04, V07, V08, V10 |
| Brak HMI albo CAN | ECU działa samodzielnie, a reakcje akcesoriów są odrębne (SYS-046/050–053). | Zależności od pozostałych stanów ochronnych. | V07 |
| Usterka TPS lub pomiaru ciśnienia używanego do określenia obciążenia | Przyjęto reguły kalibracji awaryjnej, kontrolowanego zatrzymania, powrotu i wymuszenia „Standard” (SYS-121–142). | Powiązać z pozostałymi blokadami F03. [Zakres F02](f02-przeglad-zakresu.md) opisuje przyjęte przypadki. | V02, V03, V04 |
| Usterka pomiaru IAT w profilu wtryskowym | Przyjęto dalszą pracę i nowy rozruch na osobno zweryfikowanych strategiach zastępczych dla profilu, przy wiarygodnych pozostałych wymaganych sygnałach. Pomocnicza temperatura ECU może służyć oszacowaniu IAT. Obowiązują „Standard”, DTC i oznaczenie danych zastępczych (SYS-208). | Powrót na prawidłowy IAT podczas pracy (pytanie 218). Model, warunki przydatności i zakres kalibracji do projektu i prób. | V02, V03, V04, V06, V07, V08, V09, V10, V13 |
| Chłodzenie i pozostałe pomiary ochronne | Przyjęto pomiar płynu i automatykę wentylatora oraz wejścia ciśnienia paliwa i binarne oleju (SYS-029/043/044/060). Przy usterce pomiaru temperatury płynu ECU automatycznie włącza wentylator podczas pracy silnika i zapisuje DTC (SYS-184). Po potwierdzeniu zatrzymania kończy to wymuszenie przy nadal aktywnej usterce (SYS-185). Przy zgaszonym silniku i potwierdzonej usterce ECU dopuszcza ręczne włączenie z HMI z limitami i zabezpieczeniami (SYS-186). Jeżeli usterka zostanie potwierdzona w trakcie automatycznego chłodzenia po zgaszeniu, ECU kończy to chłodzenie (SYS-187). Po odzyskaniu wiarygodnego pomiaru chłodzenie może wrócić przy odpowiedniej temperaturze i napięciu, w granicach pierwotnego limitu (SYS-188). Przy potwierdzonym przegrzaniu z wiarygodnego pomiaru HMI ostrzega kierowcę, który decyduje o zatrzymaniu silnika (SYS-189). Potwierdzone przeciążenie skutkujące odłączeniem wentylatora powoduje zapis DTC z zamrożoną ramką i ostrzeżenie na HMI także przed przegrzaniem (SYS-190). Próba na potwierdzenie z HMI obejmuje pomiar prądu i odblokowuje zwykłe sterowanie dopiero po potwierdzeniu sprawności (SYS-191–192). ECU zachowuje usterkę i blokadę przez sen. Wentylator wyposażonej konfiguracji podlega automatycznej próbie przy wybudzeniu według SYS-193. Odłożoną próbę wentylatora ECU wykonuje automatycznie po powrocie warunków w tym samym okresie wybudzenia (SYS-195). Po nieudanej próbie wentylatora każde następne wybudzenie dopuszcza jedną nową próbę automatyczną przy właściwych warunkach (SYS-196). | Parametry prób wentylatora do projektu. Reakcje na pozostałe niedostępne pomiary i warunki poza dopuszczalnym zakresem. | V02, V03, V05, V06, V07, V08, V10 |
| Zasilanie i restart ECU | Zasilanie bez stacyjki, zasady oszczędzania i odtwarzania danych (SYS-054/084–089/106/109/155). Odcięcie, restart i zapis DTC po zawieszeniu określają SYS-169–172. Limity, odzyskiwanie i powrót po przerwaniu prób określają SYS-173–180. Przyjęto reakcje na zanik zasilania podczas pracy silnika oraz rozruchu elektrycznego i kopniakiem (SYS-181–183). | Kryteria wykrywania zdarzeń, czasy i realizacja do projektu. | V01, V04, V06, V10, V12, V13 |
| Autotest po wybudzeniu ze snu | ECU obejmuje autotestem funkcje skonfigurowane w danym motocyklu. Przed dopuszczeniem rozruchu kończy wszystkie próby możliwe w aktualnych warunkach przy zgaszonym silniku. Próby wymagające innych warunków zachowują status oczekiwania. O dopuszczeniu decydują wyniki i właściwe reakcje na usterki (SYS-194/203). Przy zwykłym wybudzeniu trzymany START uruchamia rozrusznik po spełnieniu warunków według SYS-204. | Wymagania przyjęte. Metody, kryteria zakończenia i budżet czasu do projektu. | V03, V04, V05, V06, V07, V10 |

## Utrata synchronizacji wału podczas pracy

Instrukcja serwisowa Beta 250/300 RR MY2020 opisuje czujnik pick-up przy układzie zapłonu. Katalog części Beta RR 390–480 EFI MY2016 pokazuje pick-up w zespole koła magnesowego. Źródła potwierdzają zastosowanie w enduro 2T oraz 4T. [Beta 250/300 RR MY2020, rozdz. 3.11](https://betausa.com/content/SUPPORT_PDF%27s/2020%20Beta%20250%20RR%20%26%20300%20RR%20Service%20Manual.pdf), [Beta RR 390–480 EFI MY2016, katalog części](https://betausa.com/content/SUPPORT_PDF%27s/2016%20390-480%20RR%204-stroke%20and%20Race%20Edition.pdf).

W odpowiedzi A na pytanie 167 (2026-11-09) właściciel przyjął odcięcie zapłonu i wtrysku po potwierdzonej utracie synchronizacji. ECU utrzymuje odcięcie, gdy sygnał wróci przed zatrzymaniem. Po zatrzymaniu wznowienie jest możliwe w nowej świadomej próbie START lub kopniakiem, odpowiednio do wyposażenia, z wiarygodną synchronizacją i przy spełnieniu pozostałych warunków rozruchu (SYS-157). Zapis usterki i wymuszenie „Standard” podlegają SYS-019 i SYS-137. Kryteria rozpoznania zatrzymania, nowej próby i wiarygodności synchronizacji określimy w projekcie.

### Plan próby SYS-157

1. Na stanowisku odwzorować pracę silnika z poprawnym sygnałem wału. Potwierdzić utratę synchronizacji i obserwować wyjścia zapłonu oraz wtrysku odpowiednio do profilu. Przywrócić prawidłowy sygnał przed zatrzymaniem wału. Oczekiwane jest utrzymanie odcięcia.
2. Odwzorować zatrzymanie. Sprawdzić utrzymanie odcięcia bez nowej próby, w tym z przytrzymanym wcześniej START. W oddzielnych próbach zainicjować nowy rozruch przez START i kopniak zgodnie z wyposażeniem. Sprawdzić dopuszczenie sterowania po wiarygodnej synchronizacji oraz utrzymanie odcięcia przy braku wiarygodnej synchronizacji i osobno przy aktywnym STOP.
3. Powtórzyć na reprezentatywnych profilach gaźnikowych i wtryskowych oraz dla przewidzianych wejść wału. Metody wymuszenia i czasy reakcji dobrać do profilu. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Utrata synchronizacji podczas rozruchu elektrycznego

Rozrusznik i pick-up są udokumentowane w enduro Beta 250/300 RR MY2020. [Instrukcja serwisowa Betamotor, rozdz. 2.4.4 i 2.5](https://betausa.com/content/SUPPORT_PDF%27s/2020%20Beta%20250%20RR%20%26%20300%20RR%20Service%20Manual.pdf).

W odpowiedzi A na pytanie 168 (2026-11-09) właściciel przyjął wyłączenie rozrusznika po potwierdzonej utracie wcześniej uzyskanej synchronizacji, zanim ECU rozpozna pracę silnika. Dalsze przytrzymanie START i odzyskanie sygnału pozostawiają bieżącą próbę zakończoną. Kolejna próba elektryczna jest możliwa po potwierdzonym zatrzymaniu, zwolnieniu i ponownym naciśnięciu START po zatrzymaniu. Zapłon i wtrysk w nowej próbie wymagają wiarygodnej synchronizacji. Obowiązują również SYS-048/049 i pozostałe warunki rozruchu (SYS-158).

### Plan próby SYS-158

1. Zlecić rozruch przewodowym START. Odwzorować uzyskanie synchronizacji, a następnie jej potwierdzoną utratę przed rozpoznaniem pracy silnika. Przytrzymać START i sprawdzić odłączenie rozrusznika oraz odcięcie zapłonu i wtrysku odpowiednio do profilu.
2. Przywrócić sygnał przed zatrzymaniem. Zwolnić i ponownie nacisnąć START podczas obrotu. Sprawdzić utrzymanie odcięcia, także gdy naciśnięcie trwa przez zatrzymanie. Osobno sprawdzić stan po zatrzymaniu bez zwolnienia pierwotnego START.
3. Po potwierdzonym zatrzymaniu zwolnić i ponownie nacisnąć START. Sprawdzić dopuszczenie nowej próby przy spełnionych pozostałych warunkach oraz dopuszczenie zapłonu i wtrysku po uzyskaniu wiarygodnej synchronizacji. Powtórzyć bez wiarygodnej synchronizacji i potwierdzić utrzymanie odcięcia wyjść silnikowych. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Utrata synchronizacji podczas rozruchu kopniakiem

Betamotor dokumentuje opcjonalny kopniak w Beta 250/300 RR MY2020. [Instrukcja serwisowa Betamotor, rozdz. 3.7](https://betausa.com/content/SUPPORT_PDF%27s/2020%20Beta%20250%20RR%20%26%20300%20RR%20Service%20Manual.pdf).

W odpowiedzi A na pytanie 169 właściciel przyjął przerwanie próby kopniakiem po potwierdzonej utracie wcześniej uzyskanej synchronizacji przed rozpoznaniem pracy silnika. Powrót sygnału, gdy wał jeszcze się obraca, utrzymuje odcięcie zapłonu i wtrysku w profilach wtryskowych. ECU dopuszcza je ponownie po potwierdzonym zatrzymaniu wału w nowej świadomej próbie z wiarygodną synchronizacją i przy spełnionych pozostałych warunkach rozruchu (SYS-159, zapis z 2026-11-11).

### Plan próby SYS-159

1. Na stanowisku odwzorować obrót wału wywołany kopnięciem. Doprowadzić do uzyskania synchronizacji, a następnie wymusić potwierdzoną utratę przed rozpoznaniem pracy silnika. Przywrócić poprawny przebieg podczas dalszego obrotu i sprawdzić utrzymanie odcięcia zapłonu oraz wtrysku odpowiednio do profilu.
2. Odwzorować zatrzymanie wału, a następnie nową świadomą próbę kopniakiem. Sprawdzić, czy ECU dopuszcza sterowanie po wiarygodnej synchronizacji. W osobnych przebiegach sprawdzić utrzymanie odcięcia przy sygnale niewiarygodnym oraz przy aktywnym STOP.
3. Użyć reprezentatywnych profili z kopniakiem i właściwych sygnałów czujnika wału. Kryteria potwierdzenia zatrzymania, rozpoznania nowej próby i czasy reakcji określić przed wykonaniem prób. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Naciśnięcie START przy aktywnym STOP

Schemat elektryczny Beta RR 250/300 Race 2T MY2025 pokazuje przyciski STOP i START oraz rozrusznik. [Instrukcja Betamotor, schemat elektryczny RR 250–300](https://betausa.com/content/2025-Owner%20manual-RR-RACE-2T.rev.pdf#page=17).

W odpowiedzi A na pytanie 170 (2026-11-11) właściciel zatwierdził blokadę rozrusznika przy naciśnięciu START na zgaszonym silniku z aktywnym przewodowym STOP. Po zwolnieniu STOP do rozruchu potrzebne jest nowe naciśnięcie START. Przytrzymanie wcześniej naciśniętego START utrzymuje rozrusznik wyłączony (SYS-160).

### Plan próby SYS-160

1. Na stanowisku odwzorować zgaszony silnik i spełnić pozostałe warunki rozruchu. Nacisnąć przewodowy STOP, następnie nacisnąć i przytrzymać START. Potwierdzić wyłączone wyjście rozrusznika oraz blokadę zapłonu i wtrysku odpowiednio do profilu.
2. Zwolnić STOP przy nadal przytrzymanym START. Sprawdzić utrzymanie wyłączonego rozrusznika. Zwolnić i ponownie nacisnąć START. Potwierdzić dopuszczenie rozruchu zgodnie z pozostałymi warunkami.
3. Powtórzyć przy nieobecnym HMI oraz przy przerwanej komunikacji CAN z HMI. Czasy reakcji i wyposażenie stanowiska określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Naciśnięcie STOP podczas kręcenia

W odpowiedzi A na pytanie 171 (2026-11-11) właściciel zatwierdził wyłączenie rozrusznika po wykryciu przewodowego STOP podczas kręcenia przed potwierdzeniem pracy silnika. ECU kończy próbę i odcina zapłon, a w profilach wtryskowych również wtrysk. Po zwolnieniu STOP przytrzymany START utrzymuje rozrusznik wyłączony. Kierowca musi ponownie nacisnąć START po zwolnieniu obu przycisków i spełnieniu pozostałych warunków rozruchu (SYS-161).

### Plan próby SYS-161

1. Na stanowisku przy spełnionych warunkach rozruchu nacisnąć i przytrzymać START. Potwierdzić wysterowanie rozrusznika. Przed rozpoznaniem pracy silnika i przed upływem limitu kręcenia nacisnąć przewodowy STOP. Sprawdzić wyłączenie rozrusznika oraz odcięcie zapłonu i wtrysku odpowiednio do profilu.
2. Zwolnić STOP przy nadal wciśniętym START. Potwierdzić utrzymanie wyłączonego rozrusznika. Zwolnić i nacisnąć START ponownie przy spełnionych warunkach rozruchu. Sprawdzić dopuszczenie nowej próby.
3. Powtórzyć przy nieobecnym HMI oraz przy przerwanej komunikacji CAN z HMI. Kryterium czasowe odcięcia i sposób obserwacji wyjść określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Zwolnienie STOP podczas obrotu wału

W odpowiedzi A na pytanie 172 (2026-11-11) właściciel zatwierdził utrzymanie odcięcia po zwolnieniu STOP podczas dalszego obrotu wału. ECU może ponownie dopuścić zapłon i wtrysk po zwolnieniu STOP i potwierdzonym zatrzymaniu wału, w ramach nowej świadomej próby rozruchu z wiarygodną synchronizacją. Obowiązują pozostałe warunki rozruchu (SYS-162).

### Plan próby SYS-162

1. Na stanowisku odwzorować potwierdzoną pracę silnika z poprawną synchronizacją. Nacisnąć przewodowy STOP i potwierdzić odcięcie zapłonu oraz wtrysku odpowiednio do profilu. Zwolnić STOP przy nadal obracającym się wale i wiarygodnym sygnale. Sprawdzić utrzymanie odcięcia.
2. Odwzorować zatrzymanie wału. Sprawdzić utrzymanie odcięcia do nowej próby. Rozpocząć nową próbę przewodowym START albo kopniakiem, odpowiednio do wyposażenia. Potwierdzić wznowienie sterowania przy wiarygodnej synchronizacji i spełnionych warunkach rozruchu. W osobnym przebiegu sprawdzić utrzymanie odcięcia przy niewiarygodnej synchronizacji.
3. Powtórzyć na reprezentatywnych profilach gaźnikowych i wtryskowych, także przy nieobecnym HMI albo przerwanej komunikacji CAN z HMI. Metody wykrycia zatrzymania i nowej próby oraz kryteria czasowe określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Wykrywanie przerwy obwodu STOP

Schemat Beta RR 250/300 Race 2T MY2025 potwierdza przewodowy przycisk gaszenia. [Instrukcja Betamotor, schemat elektryczny RR 250–300](https://betausa.com/content/2025-Owner%20manual-RR-RACE-2T.rev.pdf#page=17).

W odpowiedzi A na pytanie 173 (2026-11-11) właściciel zatwierdził nadzór obwodu STOP w wybudzonym ECU. ECU odróżnia stan zwolnionego przycisku od przerwy oraz rozpoznaje naciśnięcie sprawnego przycisku. Nadzór działa niezależnie od HMI i komunikacji CAN (SYS-163). Sposób pomiaru, potwierdzania stanu i dopasowania do osprzętu OEM określimy w projekcie.

### Plan próby SYS-163

1. Przy wybudzonym ECU sprawdzić kolejno zwolniony i naciśnięty przycisk w sprawnym obwodzie. Potwierdzić rozpoznanie obu stanów i działanie STOP zgodnie z SYS-037.
2. Przy zwolnionym przycisku wymusić przerwę w obwodzie na stanowisku. Potwierdzić rozpoznanie przerwy przez ECU. Przywrócić ciągłość i sprawdzić ponowne rozpoznanie sprawnego obwodu przy zwolnionym przycisku. Powtórzyć dla reprezentatywnych miejsc przerwy określonych po wyborze toru.
3. Powtórzyć wykrywanie przed rozruchem oraz przy symulowanej pracy silnika, także bez HMI lub przy przerwanej komunikacji CAN. Przed próbą określić warunki elektryczne i kryteria czasowe potwierdzenia przerwy. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Reakcja na przerwę obwodu STOP

W odpowiedzi na pytanie 174 (2026-11-11) właściciel ustalił, że potwierdzona przerwa skutkuje DTC z zamrożoną ramką (SYS-019). Sama przerwa oznacza reakcję diagnostyczną (SYS-164). ECU kontynuuje pracę nominalną na wybranym zestawie map, jeżeli spełnione są warunki pracy nominalnej. Nowa świadoma próba rozruchu jest możliwa także przy utrzymującej się przerwie, gdy pozostałe warunki rozruchu są spełnione.

### Plan próby SYS-164

1. Na stanowisku odwzorować nominalną pracę silnika na poprawnym zestawie innym niż „Standard”. Wymusić przerwę w obwodzie STOP przy zwolnionym przycisku. Potwierdzić zgłoszenie DTC, zapis zamrożonej ramki, dalsze sterowanie zapłonem i wtryskiem odpowiednio do profilu oraz utrzymanie wybranego zestawu map.
2. Odwzorować zatrzymanie silnika na stanowisku przy utrzymującej się przerwie. Wykonać nową świadomą próbę rozruchu i potwierdzić dopuszczenie przy spełnionych pozostałych warunkach. Powtórzyć z przerwą obecną już przy wybudzeniu, odpowiednio dla START i kopniaka.
3. W osobnym przebiegu wymusić brak wiarygodnej synchronizacji przy utrzymującej się przerwie. Potwierdzić, że zapłon i wtrysk czekają na warunki dopuszczenia. Próby wykonać dla reprezentatywnych profili gaźnikowych i wtryskowych, także bez HMI. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Wykrywanie zwarcia do masy w obwodzie STOP

W odpowiedzi A na pytanie 175 (2026-11-11) właściciel zatwierdził odrębne rozpoznawanie zwarcia przewodu sygnałowego STOP do masy. Wybudzone ECU odróżnia zwarcie od naciśnięcia sprawnego przycisku, zwolnionego przycisku i przerwy w obwodzie. Nadzór działa niezależnie od HMI i CAN (SYS-163 i SYS-165).

### Plan próby SYS-165

1. Na stanowisku przy wybudzonym ECU zweryfikować klasyfikację zwolnionego i naciśniętego sprawnego przycisku oraz przerwy w obwodzie według SYS-163.
2. Przy zwolnionym przycisku wymusić zwarcie przewodu sygnałowego STOP do masy. Potwierdzić klasyfikację jako odrębny stan usterki. Usunąć zwarcie i sprawdzić rozpoznawanie sprawnego przycisku w obu położeniach.
3. Powtórzyć rozpoznawanie zwarcia przed rozruchem i przy symulowanej pracy silnika, także bez HMI lub po przerwaniu komunikacji CAN. Punkty wymuszania, warunki elektryczne i kryteria potwierdzenia określić przed próbą dla wybranego toru. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Reakcja na zwarcie STOP do masy

W odpowiedzi A na pytanie 176 (2026-11-11) właściciel zatwierdził reakcję diagnostyczną na potwierdzone zwarcie do masy. ECU zapisuje DTC z zamrożoną ramką i kontynuuje bieżące sterowanie silnikiem. ECU dopuszcza nową świadomą próbę rozruchu przy utrzymującym się zwarciu, jeżeli pozostałe warunki rozruchu są spełnione (SYS-166).

### Plan próby SYS-166

1. Powtórzyć próbę pracy silnika z [planu SYS-164](#plan-próby-sys-164), wymuszając zwarcie przewodu STOP do masy rozpoznawane według SYS-165. Sprawdzić DTC właściwy dla zwarcia, zamrożoną ramkę i dalsze sterowanie na wybranym zestawie map.
2. Powtórzyć przypadki rozruchu z planu SYS-164 z utrzymującym się zwarciem. Potwierdzić dopuszczenie nowej próby przez START lub kopniak, odpowiednio do wyposażenia. Objąć zwarcie obecne przy wybudzeniu oraz próbę kontrolną z niewiarygodną synchronizacją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Działanie STOP przy zawieszeniu głównego firmware ECU

W odpowiedzi A na pytanie 177 (2026-11-11) właściciel zatwierdził odcięcie zapłonu i wtrysku po naciśnięciu sprawnego przewodowego STOP również przy zawieszeniu głównego firmware ECU (SYS-167). Wznowienie po użyciu STOP podczas pracy silnika podlega SYS-162.

### Plan próby SYS-167

1. Na stanowisku z obciążeniami zastępczymi odwzorować pracę silnika i wymusić zawieszenie głównego firmware przy aktywnym poleceniu sterowania. Nacisnąć STOP. Zarejestrować sygnał przycisku, stan resetu ECU i przebieg na obciążeniu. Potwierdzić odcięcie po naciśnięciu STOP przy nadal zawieszonym firmware.
2. Powtórzyć próbę dla zapłonu CDI i TCI/IDI oraz dla wyjścia wtrysku w wyposażonym profilu, także przy odłączonym HMI. Metoda wymuszania zawieszenia ma umożliwić odróżnienie skutku STOP od automatycznej reakcji nadzoru. Kryterium czasu odcięcia i punkty pomiarowe określić przed próbą.
3. Zwolnić STOP, zasymulować dalszy obrót wału i przywrócić działanie firmware. Zweryfikować wznowienie sterowania według SYS-162, po zatrzymaniu i przy nowej świadomej próbie z wiarygodną synchronizacją. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Odłączenie rozrusznika przez STOP przy zawieszeniu głównego firmware

W odpowiedzi A na pytanie 178 (2026-11-11) właściciel zatwierdził odłączenie rozrusznika po naciśnięciu sprawnego przewodowego STOP przy zawieszonym głównym firmware, także przy przytrzymanym START. STOP kończy próbę. Dopuszczenie nowej próby podlega SYS-161 (SYS-168).

### Plan próby SYS-168

1. Na stanowisku odwzorować rozruch elektryczny na obciążeniu zastępczym toru wykonawczego. Utrzymać START i wymusić zawieszenie głównego firmware przy aktywnym sterowaniu rozrusznikiem. Nacisnąć STOP. Zarejestrować sygnały START i STOP, stan resetu i stan obciążenia. Potwierdzić odłączenie rozrusznika po naciśnięciu STOP przy nadal zawieszonym firmware.
2. Zwolnić STOP i przywrócić działanie ECU przy nadal wciśniętym START. Potwierdzić utrzymanie wyłączenia oraz dopuszczenie nowej próby po puszczeniu i ponownym naciśnięciu START przy spełnieniu pozostałych warunków. Podczas próby zweryfikować również odcięcie zapłonu i wtrysku według SYS-167.
3. Powtórzyć bez HMI. Metodę wymuszania zawieszenia dobrać tak, aby odróżnić zadziałanie STOP od reakcji nadzoru. Punkty pomiarowe i dopuszczalny czas odłączenia określić przed próbą dla wybranego toru. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Samoczynne odcięcie po wykryciu zawieszenia głównego firmware ECU

W odpowiedzi A na pytanie 179 (2026-11-11) właściciel zatwierdził samoczynne odcięcie zapłonu, wtrysku i rozrusznika przez niezależny nadzór ECU. Po wykryciu zawieszenia odcięcie działa bez naciśnięcia STOP i niezależnie od skuteczności resetu. Nadzór osobno inicjuje reset (SYS-169).

### Plan próby SYS-169

1. Na stanowisku z obciążeniami zastępczymi odwzorować pracę silnika i rozruch elektryczny w osobnych przebiegach. Pozostawić STOP zwolniony. Wymusić zawieszenie przy aktywnym poleceniu sterowania. Potwierdzić samoczynne odcięcie właściwych wyjść i zainicjowanie resetu przez nadzór. Zarejestrować wykrycie zawieszenia, sygnał resetu i stan obciążeń.
2. Powtórzyć próbę z wymuszoną nieskutecznością resetu na stanowisku, tak aby polecenie sterowania z zawieszonego firmware pozostało aktywne. Sprawdzić, czy nadzór sygnalizuje reset, a obciążenia pozostają wyłączone przez czas zawieszenia.
3. Objąć zapłon CDI i TCI/IDI, wyjście wtrysku w wyposażonym profilu oraz tor rozrusznika przy przytrzymanym START. Przed próbą określić metodę wymuszania zawieszenia, punkty pomiarowe i dopuszczalny czas odcięcia. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Wznowienie sterowania po resecie zainicjowanym przez nadzór

W odpowiedzi A na pytanie 180 (2026-11-11) właściciel zatwierdził utrzymanie odcięcia zapłonu i wtrysku po resecie nadzoru także wtedy, gdy ECU odzyskało wiarygodną synchronizację przy nadal obracającym się wale. Po potwierdzonym zatrzymaniu wału ECU dopuszcza sterowanie w nowej świadomej próbie rozruchu z wiarygodną synchronizacją i przy spełnieniu pozostałych warunków (SYS-170).

### Plan próby SYS-170

1. Na stanowisku z obciążeniami zastępczymi odwzorować pracę silnika, zainicjować reset według SYS-169 i przez cały reset podawać wiarygodne sygnały obracającego się wału oraz fazy, jeśli profil jej wymaga. Potwierdzić utrzymanie odcięcia zapłonu i wtrysku po odzyskaniu działania ECU i synchronizacji.
2. Odwzorować potwierdzone zatrzymanie wału. Sprawdzić utrzymanie odcięcia do nowej świadomej próby. Wykonać nową próbę przez START albo kopniak, odpowiednio do wyposażenia. Potwierdzić dopuszczenie zapłonu i wtrysku przy wiarygodnej synchronizacji i spełnionych pozostałych warunkach.
3. Powtórzyć nową próbę bez wiarygodnej synchronizacji i sprawdzić utrzymanie odcięcia. Przed próbami ustalić kryteria zatrzymania wału i rozpoznania nowej próby. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## START przed zatrzymaniem wału po resecie nadzoru

W odpowiedzi A na pytanie 181 (2026-11-11) właściciel zatwierdził odrzucenie START naciśniętego przed potwierdzeniem zatrzymania wału po resecie nadzoru. ECU dopuszcza załączenie rozrusznika po nowym naciśnięciu START wykonanym po potwierdzonym zatrzymaniu i przy spełnieniu pozostałych warunków. Wciśnięty START trzeba najpierw puścić (SYS-171).

### Plan próby SYS-171

1. Na stanowisku z obciążeniem zastępczym toru rozrusznika odwzorować obrót wału i reset według SYS-169. Po przywróceniu działania ECU nacisnąć START przy nadal obracającym się wale. Potwierdzić wyłączenie rozrusznika. Utrzymać START przez zatrzymanie wału i sprawdzić, czy rozrusznik pozostaje wyłączony po potwierdzeniu zatrzymania.
2. Puścić START i nacisnąć ponownie po potwierdzonym zatrzymaniu wału. Przy spełnionych pozostałych warunkach potwierdzić załączenie rozrusznika oraz dopuszczenie zapłonu i wtrysku zgodnie z SYS-170 po odzyskaniu wiarygodnej synchronizacji.
3. Powtórzyć próbę z START przytrzymanym od chwili poprzedzającej reset. Sprawdzić wymóg nowego naciśnięcia po potwierdzeniu zatrzymania. Przed próbą określić kryterium zatrzymania i punkty pomiarowe. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Zamrożona ramka po potwierdzonym resecie nadzoru

W odpowiedzi na pytanie 182 (2026-11-11) właściciel ustalił zapis przyczyny resetu i dostępnych danych związanych ze zdarzeniem. Po potwierdzeniu resetu nadzoru według SYS-169 ECU zapisuje DTC i zamrożoną ramkę. Przy braku wiarygodnych danych dodatkowych ramka zawiera przyczynę resetu i oznaczenie niedostępności danych. Informację o czasie i jego ważności stosujemy według SYS-021 (SYS-172).

### Plan próby SYS-172

1. Na stanowisku wymusić reset nadzoru według SYS-169 z dostępnymi, znanymi danymi związanymi ze zdarzeniem. Po ponownym uruchomieniu odczytać DTC i zamrożoną ramkę. Sprawdzić zgodność przyczyny, wartości danych i informacji o czasie z przebiegiem próby.
2. Powtórzyć z potwierdzoną przyczyną resetu oraz częściowo dostępnymi danymi, a następnie z samą przyczyną. Sprawdzić zapis DTC i ramki oraz oznaczenie niedostępności. Objąć także przypadek niewiarygodnego czasu rzeczywistego zgodnie z SYS-021.
3. W przebiegu kontrolnym wywołać ponowne uruchomienie z innej przyczyny. Sprawdzić, czy zapis DTC zawieszenia powstaje wyłącznie po potwierdzeniu zadziałania nadzoru. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Powtarzające się resety nadzoru podczas uruchamiania ECU

W odpowiedzi A na pytanie 183 (2026-11-11) właściciel zatwierdził limit automatycznych prób standardowego uruchomienia głównego firmware, gdy nadzór ponownie resetuje ECU przed zakończeniem uruchamiania. Zapłon, rozrusznik i wtrysk w wyposażonych profilach pozostają odcięte w trakcie prób. Po osiągnięciu limitu nadzór przerywa standardowe próby i utrzymuje odcięcie także przy niezakończonym uruchomieniu głównego firmware (SYS-173). ECU rozpoczyna odzyskiwanie według SYS-174.

### Plan próby SYS-173

1. Na stanowisku z obciążeniami zastępczymi wymusić reset nadzoru i ponawiać zawieszenie przed potwierdzeniem zakończenia uruchamiania. Zarejestrować liczbę automatycznych prób i stan wyjść. Potwierdzić odcięcie zapłonu, rozrusznika i wtrysku w wyposażonym profilu przez całą sekwencję.
2. Po osiągnięciu ustalonego limitu utrzymać usterkę i stabilne zasilanie. Sprawdzić zakończenie standardowych prób i utrzymanie odcięcia przy przejściu do odzyskiwania, również przy wciśniętym START. Przed próbą określić kryterium zakończenia uruchamiania, liczbę prób i czas obserwacji po osiągnięciu limitu.
3. W przebiegu kontrolnym potwierdzić gotowość i stabilną pracę według SYS-180 przed wyczerpaniem limitu. Sprawdzić zakończenie sekwencji i dopuszczenie wyjść zgodnie z SYS-170 i SYS-171. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Automatyczne odzyskiwanie ECU po osiągnięciu limitu

W odpowiedzi na pytanie 184 (2026-11-11) właściciel wskazał potrzebę automatycznego odzyskiwania ECU. Po osiągnięciu limitu standardowych prób ECU samoczynnie rozpoczyna odzyskiwanie przy odciętym zapłonie, rozruszniku i wtrysku w wyposażonych profilach (SYS-174). Powrót do rozruchu po pomyślnym odzyskaniu podlega SYS-170 i SYS-171. Zasady dopuszczania firmware określa SYS-078.

### Plan próby SYS-174

1. Na stanowisku z obciążeniami zastępczymi doprowadzić do osiągnięcia limitu według [planu SYS-173](#plan-próby-sys-173), przy odłączonym HMI i komputerze oraz zwolnionych przyciskach. Potwierdzić samoczynne rozpoczęcie odzyskiwania przy niezakończonym uruchomieniu głównego firmware.
2. Zarejestrować stan wyjść od ostatniej standardowej próby przez cały przebieg odzyskiwania. Powtórzyć z naciśnięciem START w czasie odzyskiwania i sprawdzić utrzymanie odcięcia. Po pomyślnym odzyskaniu zweryfikować warunki nowego rozruchu według SYS-170 i SYS-171. Szczegóły przebiegów określić po wyborze działań odzyskiwania. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Samodzielne odzyskiwanie ECU i naprawa z Windows

W odpowiedzi A na pytanie 185 (2026-11-11) właściciel zatwierdził samodzielne odzyskiwanie gotowości ECU jako pierwszy krok po wejściu według SYS-174. Po wyczerpaniu limitu samodzielnych prób bez odzyskania gotowości ECU udostępnia przewodową naprawę z Windows także przy nieuruchomionym głównym firmware (SYS-176). Odcięcie i warunki nowego rozruchu obowiązują według SYS-174 (SYS-175). Reguły naprawy i kryteria gotowości firmware są wejściem do F07.

### Plan próby SYS-175

1. Doprowadzić do wejścia w odzyskiwanie według [planu SYS-174](#plan-próby-sys-174). Przy odłączonym HMI i komputerze umożliwić skuteczne samodzielne odzyskanie. Potwierdzić powrót ECU do gotowości i warunki nowej próby rozruchu według SYS-174.
2. Powtórzyć z wyczerpaniem limitu samodzielnych prób według SYS-176 i nieuruchomionym głównym firmware. Podłączyć przewodowo komputer z aplikacją Windows, potwierdzić rozpoznanie trybu naprawy oraz wykonać reprezentatywną operację naprawy określoną w F07. Na obciążeniach zastępczych sprawdzić utrzymanie odcięcia do potwierdzonego odzyskania. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Limit samodzielnych prób odzyskania ECU

W odpowiedzi B na pytanie 186 (2026-11-11) właściciel zatwierdził osobny limit kilku samodzielnych prób odzyskania. ECU ponawia odzyskiwanie do zakończenia serii powodzeniem według SYS-180 albo do wyczerpania limitu. Po wyczerpaniu limitu bez odzyskania gotowości ECU kończy automatyczne próby i udostępnia naprawę z Windows według SYS-175. Odcięcie wyjść podlega SYS-174 (SYS-176).

### Plan próby SYS-176

1. Na stanowisku wymusić wejście do odzyskiwania według SYS-174 i niepowodzenie pierwszej samodzielnej próby. Potwierdzić, że ECU rozpoczyna kolejną samodzielną próbę w granicach osobnego limitu i utrzymuje odcięcie. Zarejestrować próby standardowego uruchomienia i próby odzyskiwania, aby sprawdzić oba limity.
2. Wymusić niepowodzenie kolejnych prób aż do wyczerpania limitu. Potwierdzić zakończenie automatycznych prób, utrzymanie odcięcia i dostęp do naprawy przez Windows według [planu SYS-175](#plan-próby-sys-175).
3. W przebiegu kontrolnym umożliwić potwierdzenie gotowości i stabilnej pracy według SYS-180 w kolejnej próbie, w tym przy ostatniej dozwolonej. Sprawdzić zakończenie sekwencji i warunki nowego rozruchu według SYS-174. Wartość limitu i kryteria powodzenia oraz niepowodzenia określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Powrót zasilania przed rozpoczęciem naprawy z Windows

W odpowiedzi A na pytanie 187 (2026-11-11) właściciel zatwierdził zachowanie stanu oczekiwania na naprawę przy zaniku zasilania. Po powrocie zasilania ECU bezpośrednio udostępnia tryb naprawy z Windows. Odcięcie według SYS-174 obowiązuje od chwili przywrócenia zasilania (SYS-177).

### Plan próby SYS-177

1. Na stanowisku wyczerpać limit według [planu SYS-176](#plan-próby-sys-176) i potwierdzić dostępność trybu naprawy. Przed wykonaniem operacji naprawy odłączyć komputer i HMI oraz wymusić całkowity zanik zasilania ECU.
2. Przywrócić zasilanie i rejestrować sekwencję uruchamiania oraz stan wyjść na obciążeniach zastępczych od chwili powrotu zasilania. Potwierdzić bezpośredni powrót do trybu naprawy i utrzymanie odcięcia. Powtórzyć z przytrzymanym START.
3. Podłączyć przewodowo komputer i potwierdzić dostępność trybu naprawy. Przed rozpoczęciem naprawy odłączyć komputer, powtórzyć cykl zasilania i sprawdzić ponowne odtworzenie stanu. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Limit prób po zaniku zasilania w trakcie samodzielnego odzyskiwania

W odpowiedzi A na pytanie 188 (2026-11-11) właściciel zatwierdził zachowanie wykorzystania limitu oraz zaliczenie przerwanej próby. Po powrocie zasilania ECU odtwarza wykorzystanie limitu w tej sekwencji i zalicza przerwaną próbę jeden raz. Jeżeli limit dopuszcza kolejną próbę, ECU kontynuuje odzyskiwanie. Jeżeli limit został wyczerpany, udostępnia naprawę z Windows. Od chwili powrotu zasilania utrzymuje odcięcie według SYS-174 (SYS-178).

### Plan próby SYS-178

1. Na stanowisku rozpocząć sekwencję według [planu SYS-176](#plan-próby-sys-176) i przerwać zasilanie podczas próby, po której pozostaje co najmniej jedna dozwolona próba. Po powrocie zasilania potwierdzić odtworzenie wcześniej wykorzystanych prób, jednokrotne zaliczenie przerwanej próby i kontynuację w ramach pozostałego limitu.
2. Powtórzyć z zanikiem zasilania podczas ostatniej dozwolonej próby. Sprawdzić dostępność trybu naprawy z Windows po powrocie zasilania i zakończenie automatycznych prób. Przez oba przebiegi obserwować stan wyjść na obciążeniach zastępczych od chwili powrotu zasilania.
3. Powtórzyć z zanikami zasilania w kolejnych rozpoczętych próbach. Porównać wykorzystanie limitu z liczbą faktycznie rozpoczętych prób, w tym prób przerwanych. Przed próbą określić punkty wymuszania zaniku i sposób obserwacji wykorzystania limitu. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Limit standardowych prób nadzoru po zaniku zasilania

W odpowiedzi B na pytanie 189 (2026-11-11) właściciel zatwierdził zachowanie liczby zakończonych standardowych prób po zaniku zasilania. Przerwaną próbę ECU ponawia w ramach tego samego miejsca w limicie i zalicza ją po zakończeniu. Po wyczerpaniu limitu bez potwierdzenia gotowości ECU rozpoczyna odzyskiwanie według SYS-174. Odcięcie obowiązuje od chwili powrotu zasilania (SYS-179).

### Plan próby SYS-179

1. Na stanowisku rozpocząć serię według [planu SYS-173](#plan-próby-sys-173). Zakończyć część prób niepowodzeniem i przerwać zasilanie podczas kolejnej próby przed potwierdzeniem jej zakończenia. Po przywróceniu zasilania sprawdzić zachowanie liczby zakończonych prób i ponowienie przerwanej próby w tym samym miejscu limitu.
2. Powtórzyć z jednym lub kilkoma zanikami zasilania podczas ostatniej dozwolonej próby. Po każdym powrocie sprawdzić ponowienie tej próby oraz stan wyjść na obciążeniach zastępczych od chwili zasilenia.
3. Umożliwić zakończenie ponawianej ostatniej próby niepowodzeniem przy stabilnym zasilaniu. Potwierdzić jej zaliczenie i samoczynne rozpoczęcie odzyskiwania według SYS-174. Przed próbami ustalić kryterium zakończenia standardowej próby i sposób obserwacji limitu. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Zakończenie serii po potwierdzeniu gotowości i stabilnej pracy ECU

W odpowiedzi A na pytanie 190 (2026-11-11) właściciel zatwierdził wymaganie potwierdzenia gotowości i ustalonego okresu stabilnej pracy przed zamknięciem serii standardowych prób lub samodzielnego odzyskiwania. Zawieszenie w tym okresie jest niepowodzeniem próby w bieżącej serii. Po wyczerpaniu limitu standardowych prób bez powodzenia ECU uruchamia odzyskiwanie według SYS-174. Po wyczerpaniu limitu odzyskiwania bez powodzenia udostępnia naprawę z Windows według SYS-175 i SYS-176 (SYS-180).

### Plan próby SYS-180

1. Powtórzyć dla standardowego uruchamiania według [planu SYS-173](#plan-próby-sys-173) i samodzielnego odzyskiwania według [planu SYS-176](#plan-próby-sys-176). Po potwierdzeniu gotowości zapewnić stabilną pracę. Sprawdzić utrzymanie bieżącej serii i odcięcia w czasie potwierdzania stabilności oraz zakończenie serii po upływie ustalonego okresu.
2. Wymusić kolejne zawieszenie tuż przed upływem okresu stabilności. Potwierdzić zaliczenie niepowodzenia do bieżącej serii oraz zastosowanie pozostałego limitu. Powtórzyć dla ostatniej dozwolonej próby i potwierdzić przejście do odzyskiwania po standardowych próbach albo do naprawy z Windows po próbach odzyskania.
3. Po potwierdzonym zakończeniu serii wymusić kolejne zawieszenie i sprawdzić rozpoczęcie nowej serii. Przed próbami określić okres stabilności, obserwowane stany i kryteria ich potwierdzenia. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Wznowienie sterowania po zaniku zasilania podczas pracy silnika

W odpowiedzi A na pytanie 191 (2026-11-12) właściciel zatwierdził utrzymanie odcięcia zapłonu i wtrysku, gdy zanik zasilania przerwie działanie ECU podczas pracy silnika, a zasilanie wróci przed zatrzymaniem wału. ECU weryfikuje konfigurację i synchronizację podczas dalszego obrotu przy odciętych wyjściach. ECU może dopuścić sterowanie w nowej świadomej próbie rozruchu po potwierdzonym zatrzymaniu wału, z wiarygodną synchronizacją i przy spełnionych pozostałych warunkach (SYS-181).

### Plan próby SYS-181

1. Na stanowisku z obciążeniami zastępczymi odwzorować pracę silnika z poprawną konfiguracją. Wywołać całkowity zanik zasilania powodujący ponowne uruchomienie ECU. Po powrocie zasilania nadal odwzorowywać obrót wału oraz fazę, jeśli profil jej wymaga. Zarejestrować zasilanie i stan wyjść od chwili powrotu zasilania. Potwierdzić odcięcie zapłonu i wtrysku również po odzyskaniu wiarygodnej synchronizacji.
2. Odwzorować zatrzymanie wału i sprawdzić utrzymanie odcięcia do nowej świadomej próby. Wykonać nową próbę przewodowym START albo kopniakiem, odpowiednio do wyposażenia. Potwierdzić dopuszczenie zapłonu i wtrysku po uzyskaniu wiarygodnej synchronizacji przy spełnionych pozostałych warunkach. W przebiegu kontrolnym wymusić niewiarygodną synchronizację i sprawdzić utrzymanie odcięcia.
3. Uwzględnić zapłon CDI i TCI/IDI oraz wtrysk w wyposażonych profilach. Powtórzyć próbę bez HMI. Przed próbą określić sposób wymuszenia zaniku, kryterium ponownego uruchomienia i zatrzymania wału oraz punkty pomiarowe. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Rozrusznik po zaniku zasilania ECU podczas rozruchu

W odpowiedzi A na pytanie 192 (2026-11-12) właściciel zatwierdził zakończenie próby rozruchu elektrycznego, jeśli zanik zasilania przerwie działanie ECU. Od powrotu zasilania rozrusznik pozostaje wyłączony także przy przytrzymanym START. Kolejna próba wymaga potwierdzonego zatrzymania wału oraz nowego naciśnięcia START po zatrzymaniu, przy spełnieniu pozostałych warunków. Wciśnięty START trzeba najpierw puścić (SYS-182).

### Plan próby SYS-182

1. Na stanowisku z obciążeniem zastępczym toru rozrusznika odwzorować rozruch elektryczny przy przytrzymanym START. Wymusić całkowity zanik zasilania powodujący ponowne uruchomienie ECU. Przywrócić zasilanie przy nadal przytrzymanym START i symulowanym obrocie wału. Zarejestrować zasilanie, START, stan obciążenia i potwierdzić wyłączony rozrusznik od chwili powrotu zasilania.
2. Przy nadal przytrzymanym START odwzorować zatrzymanie wału. Potwierdzić utrzymanie wyłączenia. Puścić START i nacisnąć go ponownie po potwierdzonym zatrzymaniu. Przy spełnionych pozostałych warunkach sprawdzić załączenie rozrusznika w nowej próbie.
3. Powtórzyć bez HMI. W przebiegu kontrolnym wykonać nowe naciśnięcie START podczas obrotu wału po powrocie zasilania. Sprawdzić, że rozrusznik oczekuje na naciśnięcie po potwierdzonym zatrzymaniu. Kryteria zatrzymania i sposób pomiaru stanu toru określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Zanik zasilania podczas próby rozruchu kopniakiem

W odpowiedzi A na pytanie 193 (2026-11-12) właściciel zatwierdził zakończenie rozpoczętej próby kopniakiem po zaniku zasilania ECU, gdy zasilanie wraca przy nadal obracającym się wale. ECU utrzymuje odcięcie zapłonu i wtrysku także po odzyskaniu synchronizacji w czasie dalszego obrotu. Dopuszcza zapłon i wtrysk w nowej próbie kopniakiem po potwierdzeniu zatrzymania wału, przy wiarygodnej synchronizacji i spełnionych pozostałych warunkach (SYS-183).

### Plan próby SYS-183

1. Na stanowisku z obciążeniami zastępczymi przy aktywnym ECU odwzorować rozpoczętą próbę kopniakiem. Przed potwierdzeniem pracy silnika wywołać zanik zasilania powodujący ponowne uruchomienie ECU. Po powrocie zasilania odwzorować dalszy obrót wału. Sprawdzić odcięcie zapłonu i wtrysku w wyposażonym profilu od chwili powrotu zasilania, także po odzyskaniu wiarygodnej synchronizacji.
2. Odwzorować zatrzymanie wału, potwierdzić utrzymanie odcięcia, a następnie rozpocząć nową próbę kopniakiem. Sprawdzić dopuszczenie zapłonu i wtrysku przy wiarygodnej synchronizacji i spełnionych pozostałych warunkach. Powtórzyć bez HMI.
3. W przebiegu kontrolnym wybudzić ECU kopniakiem przy dostępnym zasilaniu i sprawdzić zwykły rozruch według SYS-054. Przed próbą określić kryteria zatrzymania wału i rozpoznania nowej próby oraz punkty pomiarowe. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Wentylator podczas pracy silnika przy usterce pomiaru temperatury płynu

Właściciel potwierdził wentylator i pomiar temperatury płynu w egzemplarzu referencyjnym Beta 300 RR Racing 2015. Schemat Beta RR 250–300 Race 2T MY2025 również pokazuje opcjonalny wentylator. [Instrukcja Betamotor, schemat elektryczny RR 250–300](https://betausa.com/content/2025-Owner%20manual-RR-RACE-2T.rev.pdf#page=17).

W odpowiedzi A na pytanie 194 (2026-11-12) właściciel zatwierdził automatyczne włączenie sprawnego wentylatora podczas potwierdzonej pracy silnika, gdy ECU potwierdzi usterkę pomiaru temperatury płynu. ECU utrzymuje wymuszenie przez czas pracy z potwierdzoną usterką oraz zapisuje DTC z zamrożoną ramką. Wymuszenie działa lokalnie, niezależnie od HMI i CAN (SYS-184).

### Plan próby SYS-184

1. Na stanowisku odwzorować pracę silnika w profilu ze sprawnym wentylatorem i wiarygodną temperaturą poniżej progu załączenia. Potwierdzić wyłączony wentylator. Wymusić reprezentatywną usterkę wejścia temperatury i po jej potwierdzeniu sprawdzić automatyczne załączenie i utrzymanie pracy wentylatora przy potwierdzonej usterce. Odczytać DTC i zamrożoną ramkę według SYS-019.
2. Powtórzyć z wentylatorem włączonym przez normalną automatykę przed usterką. Sprawdzić utrzymanie włączenia podczas przejścia na wymuszenie po usterce.
3. Powtórzyć z odłączonym HMI oraz w osobnym przebiegu przerwać CAN po załączeniu. Sprawdzić załączenie i utrzymanie pracy wentylatora. Kryteria potwierdzenia usterki, rodzaje wymuszanych usterek i punkty pomiarowe określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Zakończenie wymuszenia wentylatora po zatrzymaniu silnika

W odpowiedzi A na pytanie 195 (2026-11-12) właściciel zatwierdził zakończenie automatycznego wymuszenia z SYS-184 po potwierdzeniu zatrzymania silnika przy utrzymującej się usterce pomiaru. Reguła obowiązuje także przy włączonej funkcji chłodzenia po zgaszeniu (SYS-060, SYS-185).

### Plan próby SYS-185

1. Na stanowisku odwzorować pracę silnika ze sprawnym wentylatorem i potwierdzoną usterką pomiaru temperatury płynu. Sprawdzić aktywne wymuszenie według SYS-184. Utrzymać usterkę i zasilanie ECU. W próbie jedynym żądaniem włączenia ma być wymuszenie awaryjne.
2. Odwzorować zatrzymanie silnika. Po jego potwierdzeniu sprawdzić wycofanie wymuszenia awaryjnego i wyłączenie wyjścia wentylatora.
3. Wykonać próbę z wyłączoną i włączoną funkcją chłodzenia po zgaszeniu. W wariancie z włączoną funkcją zapewnić napięcie powyżej progu odcięcia i dostępny limit czasu, aby zweryfikować, że samo zatrzymanie kończy wymuszenie. Powtórzyć bez łączności z HMI. Kryterium potwierdzenia zatrzymania i dopuszczalny czas reakcji określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Ręczne włączenie wentylatora przy zgaszonym silniku i usterce pomiaru

W odpowiedzi A na pytanie 196 (2026-11-12) właściciel dopuścił ręczne włączenie sprawnego wentylatora z HMI przy zgaszonym silniku, wybudzonym ECU i nadal potwierdzonej usterce pomiaru temperatury płynu. Obowiązują limit czasu, odcięcie przy niskim napięciu (SYS-061) oraz zabezpieczenia wyjścia (SYS-186).

### Plan próby SYS-186

1. Na stanowisku użyć ECU i HMI ze sprawnym torem wentylatora. Odwzorować zgaszony silnik, wybudzone ECU, potwierdzoną usterkę pomiaru i warunki zasilania dopuszczające włączenie. Przy braku żądania automatyki zlecić włączenie z HMI i potwierdzić pracę wentylatora.
2. Przy utrzymanej usterce sprawdzić osobno wyłączenie po upływie limitu czasu i odcięcie po wystąpieniu warunku niskiego napięcia. Dodatkowo wysłać ręczne żądanie przy aktywnym odcięciu napięciowym i sprawdzić, że wyjście pozostaje wyłączone.
3. Przy aktywnym ręcznym żądaniu sprawdzić działanie zabezpieczeń wyjścia przez kontrolowane wymuszenie według projektu kanału. W osobnym przebiegu przerwać komunikację z HMI i po potwierdzeniu jej utraty sprawdzić anulowanie ręcznego żądania według SYS-053. Progi, czasy i sposób wymuszenia określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Usterka pomiaru podczas automatycznego chłodzenia po zgaszeniu

W odpowiedzi A na pytanie 197 (2026-11-12) właściciel zatwierdził zakończenie trwającego chłodzenia automatycznego po zgaszeniu silnika, gdy ECU potwierdzi usterkę pomiaru temperatury płynu (SYS-187). Aktywne ręczne żądanie może nadal podtrzymywać pracę wentylatora zgodnie z SYS-186.

### Plan próby SYS-187

1. Na stanowisku odwzorować zatrzymanie silnika z wiarygodnym pomiarem temperatury wymagającym chłodzenia. Potwierdzić załączenie wentylatora przez automatykę po zgaszeniu według SYS-060. Zapewnić prawidłowe napięcie, zapas czasu i brak ręcznego żądania.
2. Wymusić reprezentatywną usterkę pomiaru i utrzymać warunki czasu oraz zasilania pozwalające na chłodzenie. Po potwierdzeniu usterki sprawdzić wycofanie żądania automatyki i wyłączenie wyjścia wentylatora.
3. Powtórzyć przy jednocześnie aktywnym żądaniu ręcznym z HMI. Po potwierdzeniu usterki wentylator ma działać, dopóki ręczne żądanie jest dopuszczone według SYS-186. Wycofać żądanie ręczne przy utrzymanej usterce i sprawdzić wyłączenie wyjścia przed upływem limitu czasu. Metodę wymuszenia usterki i kryterium czasu reakcji określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Powrót wiarygodnego pomiaru po przerwaniu chłodzenia

W odpowiedzi A na pytanie 198 (2026-11-12) właściciel dopuścił ponowne uruchomienie automatycznego chłodzenia w tym samym postoju po odzyskaniu wiarygodnego pomiaru, gdy aktualna temperatura wymaga chłodzenia, napięcie dopuszcza pracę, a pierwotny limit czasu pozostaje ważny. Wznowienie wykorzystuje pozostały czas pierwotnego limitu (SYS-188).

### Plan próby SYS-188

1. Na stanowisku uruchomić automatyczne chłodzenie po zgaszeniu według SYS-060 i ustalić pierwotny termin jego zakończenia. Wymusić potwierdzoną usterkę pomiaru i sprawdzić zakończenie chłodzenia według SYS-187. ECU pozostaje wybudzone podczas próby, a ręczne żądanie jest nieaktywne.
2. Przed upływem pierwotnego limitu przywrócić wiarygodny pomiar wskazujący zapotrzebowanie na chłodzenie przy napięciu dopuszczającym pracę. Przy utrzymanym zapotrzebowaniu i prawidłowym napięciu sprawdzić wznowienie, pracę do pierwotnego terminu i wyłączenie z upływem tego terminu.
3. W osobnych przebiegach przywrócić wiarygodny pomiar z temperaturą niewymagającą chłodzenia, przy napięciu objętym odcięciem i po upływie pierwotnego limitu. W każdym przebiegu sprawdzić, że wentylator pozostaje wyłączony. Kryteria wiarygodności, progi, tolerancje czasu i metodę pomiaru określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Ostrzeżenie przy potwierdzonym przegrzaniu

Instrukcja Betamotor RR 125 LC opisuje kontrolkę przegrzania. KTM 690 Enduro R MY2026 stosuje ostrzeżenie o wysokiej temperaturze płynu i ogranicza maksymalne obroty w przypadku przegrzania. [Instrukcja Betamotor RR 125 LC](https://betamotor.com/wp-content/uploads/2019/02/Manual_RR_LC_2019-4.pdf), [Instrukcja KTM 690 Enduro R MY2026, rozdział 7.15](https://manualzz.com/doc/87646720/ktm-690-enduro-r-bike-2026-owner-manual).

W odpowiedzi A na pytanie 199 (2026-11-12) właściciel wybrał ostrzeżenie na HMI po potwierdzeniu przegrzania przy wiarygodnym pomiarze podczas pracy silnika. Decyzję o zatrzymaniu z powodu przegrzania podejmuje kierowca (SYS-189).

### Plan próby SYS-189

1. Na stanowisku z ECU i HMI odwzorować pracę silnika oraz wiarygodny pomiar temperatury płynu poniżej kryterium przegrzania. Podnieść symulowaną temperaturę do warunków potwierdzenia przegrzania. Sprawdzić przekazanie stanu przez ECU i pojawienie się ostrzeżenia na HMI po potwierdzeniu.
2. Przy aktywnym ostrzeżeniu sprawdzić pracę wyjść silnikowych zgodnie z bieżącym profilem, w tym dotychczasowe granice obrotów i korekty zależne od temperatury. Następnie użyć przewodowego STOP i sprawdzić zatrzymanie według SYS-037 i SYS-162.
3. Powtórzyć na reprezentatywnym profilu gaźnikowym i wtryskowym. W osobnym przebiegu zadać stan niesprawnego wejścia temperatury przy braku aktywnego przegrzania. Sprawdzić reakcję na usterkę pomiaru według SYS-184 oraz brak nowego potwierdzenia przegrzania na podstawie tego sygnału. Progi, czasy potwierdzenia i kryteria obserwacji wyjść ustalić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Ostrzeżenie po odłączeniu przeciążonego wentylatora

Instrukcja KTM 450 EXC-F MY2025 wskazuje wentylator jako nadzorowane wyjście OCU. Moduł odłącza przeciążone wyjście i sygnalizuje jego stan diodą. [Instrukcja KTM 450 EXC-F MY2025, s. 131](https://manualzz.com/doc/81264919/ktm-450-exc-f-six-days-bike-2025-owner-manual), [Materiały KTM o OCU](https://www.ktm.com/en-us/2024-enduro-range-press-kit.html#offroad-control-unit).

W odpowiedzi A na pytanie 200 (2026-11-13) właściciel zatwierdził zapis DTC z zamrożoną ramką i odrębne ostrzeżenie kierowcy na HMI po odłączeniu wentylatora przez zabezpieczenie z powodu potwierdzonego przeciążenia. Ostrzeżenie pojawia się również przy temperaturze poniżej progu przegrzania (SYS-190).

### Plan próby SYS-190

1. Na stanowisku z ECU i HMI odwzorować pracę silnika z wiarygodnym odczytem temperatury powodującym załączenie wentylatora, poniżej progu przegrzania. Potwierdzić prawidłowe załączenie bez ostrzeżenia o usterce obwodu wentylatora.
2. Wymusić przeciążenie za pomocą kontrolowanego obciążenia stanowiska według ograniczeń zaprojektowanego kanału. Sprawdzić odcięcie wyjścia, potwierdzenie usterki i ostrzeżenie o obwodzie wentylatora na HMI, nadal poniżej progu przegrzania. Zmierzyć czas od potwierdzenia usterki do ostrzeżenia. Odczytać DTC z powiązaną zamrożoną ramką w Windows według SYS-019–024.
3. Powtórzyć potwierdzenie usterki przy odłączonym HMI i sprawdzić odcięcie wyjścia oraz zapis diagnostyczny w ECU. W osobnym przebiegu sprawdzić wygaszenie ostrzeżenia po potwierdzeniu ustąpienia usterki i zachowanie historii DTC według SYS-023. Sposób potwierdzenia ustąpienia usterki, kryteria przeciążenia i dopuszczalny czas reakcji określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Utrzymanie odcięcia wentylatora po przeciążeniu

Dokumentacja sterownika samochodowego Texas Instruments pokazuje działanie zabezpieczenia nadprądowego w trybie automatycznego ponawiania i w trybie utrzymania odcięcia. [Texas Instruments TPS1211-Q1, rysunki 9-8 i 9-9](https://www.ti.com/lit/ds/symlink/tps1211-q1.pdf#page=35).

W odpowiedzi A na pytanie 201 (2026-11-13) właściciel zatwierdził utrzymanie odcięcia wentylatora po potwierdzonym przeciążeniu do sprawdzenia obwodu i świadomego odblokowania. Reguła obowiązuje również przy dalszym zapotrzebowaniu na chłodzenie (SYS-191).

### Plan próby SYS-191

1. Na stanowisku uruchomić wentylator zgodnie z zapotrzebowaniem na chłodzenie. Wymusić kontrolowane przeciążenie i potwierdzić odcięcie według SYS-190. Przywrócić sprawne obciążenie bez zgody na próbę. Sprawdzić, że wyjście pozostaje odłączone przy żądaniu automatyki, przy zwykłym ręcznym żądaniu z HMI i przy odrębnym wymuszeniu awaryjnym według SYS-184.
2. Przy utrzymanej usterce zasymulować zgaszenie silnika bez uśpienia ECU. Sprawdzić utrzymanie odcięcia i ostrzeżenia oraz brak załączenia przez chłodzenie po zgaszeniu. Powtórzyć przy zgaszeniu i użyciu zwykłego polecenia włączenia wentylatora z HMI.
3. Przyjąć świadome potwierdzenie z HMI. Sprawdzić, że przed potwierdzeniem sprawności załączenie jest możliwe wyłącznie w kontrolowanej próbie SYS-192. Po udanej próbie wywołać nowe przeciążenie i sprawdzić ponowne odcięcie. Parametry obciążenia i kryteria czasowe określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Kontrolowana próba wentylatora po potwierdzeniu na HMI

Instrukcja KTM 450 EXC-F MY2025 wskazuje sprawdzenie wentylatora i instalacji elektrycznej w razie usterki obwodu sygnalizowanej przez OCU. [Instrukcja KTM 450 EXC-F MY2025, rozdział 21](https://manualzz.com/doc/81264919/ktm-450-exc-f-six-days-bike-2025-owner-manual).

W odpowiedzi na pytanie 202 (2026-11-13) właściciel wybrał potwierdzenie na HMI po usunięciu blokady lub sprawdzeniu wentylatora. ECU wykonuje próbę z pomiarem prądu zarówno przy pracującym, jak i przy zgaszonym silniku, jeśli pozostaje wybudzone. Pozytywny wynik przywraca normalne sterowanie. Nieudana próba pozostawia odcięcie oraz informację o niesprawnym wentylatorze (SYS-191–192).

Dla wentylatora szczotkowego trzeba rozróżnić prąd rozruchowy od prądu utrzymującego się przy zablokowanym wirniku. Progi i czas rozruchu należy potwierdzić dla danego wentylatora w jego zakresie napięcia i temperatury. Zabezpieczenie przed zwarciem pozostaje aktywne również w czasie rozruchu próby. [Texas Instruments, detekcja zablokowania silnika szczotkowego](https://www.ti.com/lit/ab/slvafq3/slvafq3.pdf#page=1).

Sterownik wentylatora bezszczotkowego może wykrywać blokadę wewnętrznie i odłączać silnik lub sam ponawiać próbę. Dla zgodnych modeli trzeba sprawdzić, czy przebieg prądu pozwala wiarygodnie ocenić rozruch i pracę. Gdy wynik jest niejednoznaczny, do rozważenia pozostaje wykorzystanie dostępnego sygnału obrotów lub statusu napędu. [Texas Instruments DRV10970, rozdział 8.3.3](https://www.ti.com/lit/ds/symlink/drv10970.pdf#page=15).

### Plan próby SYS-192

1. Po odcięciu według SYS-190 przywrócić sprawne obciążenie. Potwierdzić na HMI zakończenie czynności przy wentylatorze. Zarejestrować jedną ograniczoną próbę, przebieg prądu i moment potwierdzenia sprawności. Sprawdzić rozpoznanie poprawnego prądu rozruchowego i powrót automatyki dopiero po pozytywnym wyniku. Powtórzyć przy pracującym silniku i po jego zgaszeniu przy wybudzonym ECU oraz z aktualnym żądaniem chłodzenia i bez niego.
2. Na kontrolowanym stanowisku wykonać osobne przebiegi z utrzymującą się blokadą, przerwą obwodu i niejednoznacznym wynikiem pomiaru. Sprawdzić zakończenie próby, utrzymanie odcięcia, informację o wyniku na HMI i brak samoczynnego ponowienia w tym samym okresie wybudzenia.
3. Przy próbie z potwierdzonym przeciążeniem lub zwarciem sprawdzić działanie zabezpieczenia także podczas rozruchu próbnego. W osobnym przebiegu z udaną próbą sprawdzić wygaszenie ostrzeżenia i zachowanie historii według SYS-022/023. Metodę wymuszania, bezpieczne limity i kryteria sprawności ustalić przed próbą dla wybranego wentylatora. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Automatyczna próba wentylatora po wybudzeniu

W odpowiedzi na pytanie 203 (2026-11-13) właściciel wskazał próbę wentylatora w autoteście przy każdym wybudzeniu ze snu, również po zapamiętanej usterce. Próba jest automatyczna, bez polecenia z HMI, gdy pozwalają na to warunki zasilania i zabezpieczenia wyjścia (SYS-193). Aktywna usterka z poprzedniego okresu pracy jest zachowana do potwierdzenia sprawności.

Instrukcja KTM 350 EXC-F MY2026 wymienia przerwę i zwarcie w obwodzie wentylatora w wykazie usterek. Diagnostyka wyjścia bez zasilania roboczego jest możliwa w niektórych układach kluczujących. Ocena rozruchu i pracy wentylatora podlega kryteriom dobranym do jego konstrukcji. [Instrukcja KTM 350 EXC-F MY2026, kod błyskowy 43](https://manualzz.com/doc/86852189/ktm-350-exc-f-bike-2026-owner-manual). [Texas Instruments TPS1H000-Q1, rozdział 6.3.5.2](https://www.ti.com/lit/ds/symlink/tps1h000-q1.pdf#page=15).

### Plan próby SYS-193

1. Doprowadzić do potwierdzonej usterki i odcięcia. Zgasić silnik i uśpić ECU. Wybudzić je ruchem przedniego koła lub przyciskiem HMI przy napięciu i stanie układu dopuszczającym próbę. Sprawdzić odtworzenie blokady i samodzielne rozpoczęcie kontrolowanej próby. Osobno powtórzyć z wentylatorem nadal zablokowanym i z naprawionym podczas snu. Oczekiwane wyniki to odpowiednio utrzymanie odcięcia z ostrzeżeniem albo powrót do sterowania według aktualnego zapotrzebowania, wygaszenie ostrzeżenia i zachowanie historii.
2. Uśpić ECU ze sprawnym wentylatorem. Podczas snu na stanowisku zasymulować odłączenie wentylatora. Wybudzić ECU i sprawdzić wykrycie nowej usterki, zapis DTC z zamrożoną ramką i przekazanie stanu do HMI. Powtórzyć z pozostawionym sprawnym wentylatorem oraz z profilem bez wentylatora, w którym ta próba nie ma zastosowania.
3. Wybudzić ECU przy napięciu uniemożliwiającym próbę. W osobnym przebiegu dopuścić rozruch przy braku warunków próby według SYS-203, a warunki próby wentylatora przywrócić dopiero podczas trwającego rozruchu. Sprawdzić odłożenie załączenia, odnotowanie braku wyniku i zachowanie istniejącego odcięcia. Podczas dopuszczonej próby powtórzyć sprawdzenie ochrony wyjścia. Kryteria prądu, zasilania i czasu ustalić dla danego wentylatora przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Autotest funkcji ECU i osprzętu po wybudzeniu

Właściciel rozszerzył autotest na funkcje ECU i wyposażenie danej konfiguracji. Autotest ma wykrywać także usterki lub odłączenia powstałe podczas postoju (SYS-194).

Dla każdego profilu określimy pokrycie autotestu. Kontrole dostępne przy nieruchomym silniku obejmują stan ECU i tory, które można ocenić bez uruchamiania osprzętu silnikowego. Sprawdzenia wymagające ruchu, obciążenia lub innego stanu pracy czekają na właściwe warunki. Przykładowo poprawna kontrola elektryczna wejścia czujnika wału nie potwierdza jakości jego impulsów podczas obrotu.

### Plan próby SYS-194

1. Dla profilu z poprawną konfiguracją przejść przez cykl snu i wybudzenia od START, kopniaka, przycisku HMI, podłączenia PC oraz ruchu przedniego koła, zgodnie z wyposażeniem. Sprawdzić inicjację autotestu i dostępne kontrole w każdym wariancie.
2. Na stanowisku podczas snu wymusić reprezentatywną usterkę wejścia lub odłączenie wyposażonego odbiornika. Po wybudzeniu sprawdzić rozpoznanie i zapis DTC. W osobnych przebiegach sprawdzić stan sprawny, brak opcjonalnego wyposażenia według konfiguracji oraz próbę oczekującą na warunki. Dla czujnika wału bez ruchu sprawdzić, że ECU nie przedstawia funkcjonalnej próby dekodera jako wykonanej.
3. Przy wybudzeniu bez żądania rozruchu obserwować wyjścia rozrusznika, zapłonu i wtrysku. Powtórzyć podczas rozpoczęcia rozruchu elektrycznego i kopniakiem. Sprawdzić wstrzymanie wyjść rozruchowych do zakończenia dostępnych prób według SYS-203, dalsze zachowanie według reguł rozruchu oraz działanie bez HMI zgodnie z SYS-046 i SYS-054. Kryteria zakończenia kontroli i czasy reakcji określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Wykonanie odłożonej próby wentylatora

W odpowiedzi A na pytanie 204 (2026-11-13) właściciel wybrał automatyczne wykonanie odłożonej próby wentylatora w tym samym okresie wybudzenia po powrocie właściwych warunków. Do potwierdzenia sprawności ECU utrzymuje istniejące odcięcie i stan usterki (SYS-195).

### Plan próby SYS-195

1. Wybudzić ECU przy zasilaniu pozwalającym na pracę ECU i uniemożliwiającym aktywną próbę wentylatora. Sprawdzić brak zasilenia wentylatora, stan oczekiwania i utrzymanie zapamiętanej blokady. Przywrócić warunki próby w tym samym okresie wybudzenia, bez polecenia z HMI. Sprawdzić samoczynne załączenie próbne oraz reakcję na pozytywny wynik według SYS-193.
2. Dopuścić rozruch według SYS-203 przy niespełnionych warunkach próby wentylatora. Podczas trwającego rozruchu elektrycznego przywrócić warunki zasilania próby i sprawdzić dalsze odłożenie do zakończenia rozruchu. Powtórzyć na stanowisku dla rozruchu kopniakiem. Wykonanie próby następuje po spełnieniu wszystkich jej warunków. W osobnym przebiegu, gdy próba wentylatora jest dostępna już po wybudzeniu przed rozruchem, sprawdzić jej wykonanie przed dopuszczeniem rozruchu zgodnie z SYS-203.
3. Wykonać odłożoną próbę z nadal uszkodzonym wentylatorem. Sprawdzić aktywność zabezpieczeń, odcięcie i aktualizację stanu diagnostycznego według SYS-193. Progi zasilania, czasy i kryteria gotowości ustalić w projekcie przed próbami. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Kolejne wybudzenia po nieudanej próbie wentylatora

KTM opisuje niezależne odłączanie uszkodzonych obwodów w motocyklach enduro. Dokumentacja TI pokazuje dwa sposoby reakcji stopnia mocy na przeciążenie: samoczynne ponowienie i utrzymanie odcięcia. [Materiały KTM o OCU](https://www.ktm.com/en-us/2024-enduro-range-press-kit.html#offroad-control-unit). [Texas Instruments TPS1211-Q1, rysunki 9-8 i 9-9](https://www.ti.com/lit/ds/symlink/tps1211-q1.pdf#page=35).

W odpowiedzi B na pytanie 205 (2026-11-13) właściciel ustalił jedną próbę automatyczną przy każdym kolejnym wybudzeniu po nieudanym autoteście wentylatora, o ile pozwalają na to warunki i zabezpieczenia. Negatywny wynik utrzymuje odcięcie i kończy próby automatyczne w bieżącym okresie wybudzenia (SYS-196).

### Plan próby SYS-196

1. Na stanowisku utrzymać potwierdzoną blokadę wentylatora i dopuszczalne warunki zasilania. Wykonać kilka osobnych cykli snu i wybudzenia, w tym od ruchu przedniego koła. W każdym okresie wybudzenia potwierdzić dokładnie jedną automatyczną próbę. Po negatywnym wyniku obserwować wyjście przy utrzymanym zapotrzebowaniu na chłodzenie i sprawdzić, że zwykłe sterowanie pozostaje zablokowane, a automatyka nie uruchamia drugiej próby.
2. Wybudzić ECU przy niedopuszczalnym napięciu. Sprawdzić stan oczekiwania i brak załączenia do powrotu warunków. Po ich powrocie sprawdzić jedną próbę automatyczną według SYS-195. W osobnym przebiegu pozwolić ECU zasnąć bez możliwości wykonania próby i sprawdzić jedną próbę po kolejnym wybudzeniu przy dopuszczalnym napięciu.
3. Po uśpieniu zastąpić niesprawny wentylator sprawnym i sprawdzić przywrócenie zwykłego sterowania dopiero po udanej próbie z aktywnymi zabezpieczeniami. Po serii z utrzymującą się usterką sprawdzić, że osobne potwierdzenie z HMI może zlecić kontrolowaną próbę według SYS-192. Kryteria czasowe, warunki zasilania i metodę wymuszania ustalić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Przytrzymany START podczas podnoszenia motocykla

KTM potwierdza zastosowanie automatycznego wyłączenia silnika po wykryciu upadku w rodzinie enduro MY2024. [KTM, opis czujnika przewrócenia](https://www.ktm.com/en-us/2024-enduro-range-press-kit.html#roll-over-sensor).

W odpowiedzi A na pytanie 206 (2026-11-13) właściciel zatwierdził utrzymanie rozrusznika wyłączonego po postawieniu motocykla, jeżeli kierowca nacisnął START jeszcze podczas aktywnej blokady i nadal go trzyma. ECU dopuszcza kolejną próbę po zwolnieniu i nowym naciśnięciu START przy spełnieniu pozostałych warunków (SYS-197).

### Plan próby SYS-197

1. Na stanowisku odwzorować potwierdzone przewrócenie, zgaszenie silnika i zatrzymanie wału. Nacisnąć przewodowy START, gdy motocykl nadal leży. Przytrzymując START, odwzorować postawienie i potwierdzenie prawidłowego położenia. Sprawdzić, że rozrusznik pozostaje wyłączony podczas całej sekwencji.
2. Puścić START i potwierdzić utrzymanie wyłączonego wyjścia. Nacisnąć START ponownie po potwierdzonym postawieniu. Przy spełnionych warunkach rozruchu sprawdzić załączenie. W odrębnych przebiegach zwolnić i ponownie nacisnąć START przed potwierdzeniem postawienia oraz ponowić po postawieniu z aktywnym STOP. Sprawdzić utrzymanie odcięcia w obu przypadkach.
3. Powtórzyć sekwencję z odłączonym HMI. Kryteria potwierdzenia położenia, tolerancje czasowe i pomiar stanu wyjścia dobrać przed wykonaniem próby. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Usterka toru wykrywania przewrócenia podczas jazdy

W instrukcji KTM 350 EXC-F MY2026 kod błyskowy 15 obejmuje usterki obwodu czujnika pochylenia, w tym przerwę lub zbyt wysoki sygnał. [Instrukcja KTM 350 EXC-F MY2026, rozdział 22](https://manualzz.com/doc/86852189/ktm-350-exc-f-bike-2026-owner-manual).

W odpowiedzi A na pytanie 207 (2026-11-13) właściciel zatwierdził kontynuowanie pracy silnika przy utracie wiarygodnej informacji o położeniu z powodu usterki toru i nieaktywnej blokadzie po upadku. ECU zapisuje DTC z zamrożoną ramką i zgłasza na HMI niedostępność wykrywania przewrócenia (SYS-198).

### Plan próby SYS-198

1. Na stanowisku odwzorować pracujący silnik przy prawidłowym pomiarze położenia i nieaktywnej blokadzie po przewróceniu. Wymusić reprezentatywną usterkę toru powodującą utratę wiarygodności pomiaru. Po potwierdzeniu usterki sprawdzić ciągłość sterowania silnikiem według bieżącego profilu, zapis DTC z zamrożoną ramką i ostrzeżenie na HMI o niedostępności wykrywania przewrócenia.
2. Powtórzyć przy odłączonym HMI oraz w osobnym przebiegu po przerwaniu CAN. Sprawdzić ciągłość pracy silnika i lokalny zapis diagnostyczny. Przy utrzymującej się usterce użyć przewodowego STOP i sprawdzić zgaszenie silnika według SYS-037 i SYS-162. Uwzględnić reprezentatywny profil gaźnikowy i wtryskowy.
3. W kontrolnym przebiegu podać wiarygodny sygnał rzeczywistego przewrócenia zgodny z kryteriami SYS-039 i sprawdzić wyłączenie silnika. W osobnym przebiegu usterki potwierdzić ustąpienie według kryteriów danego toru oraz wygaszenie ostrzeżenia z zachowaniem historii DTC według SYS-022/023. Przed próbą określić reprezentatywne uszkodzenia, kryteria potwierdzenia oraz warunki ponownej oceny wiarygodności. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Rozruch przy usterce toru wykrywania przewrócenia

W odpowiedzi A na pytanie 208 (2026-11-13) właściciel zatwierdził dopuszczenie świadomego rozruchu przez START lub kopniak przy potwierdzonej usterce toru wykrywania przewrócenia, gdy blokada po upadku jest nieaktywna i spełniono pozostałe warunki rozruchu. HMI ostrzega o niedostępności wykrywania przewrócenia (SYS-199).

### Plan próby SYS-199

1. Na stanowisku odwzorować zgaszony silnik, nieaktywną blokadę po przewróceniu i potwierdzoną usterkę toru położenia, np. przerwę lub niewiarygodny odczyt odpowiedni dla użytego czujnika. Sprawdzić ostrzeżenie na HMI i dostępność DTC z zamrożoną ramką według SYS-019. Przed żądaniem rozruchu sprawdzić stan wyjść rozrusznika, zapłonu i wtrysku.
2. Przy spełnionych pozostałych warunkach wykonać osobne próby przewodowym START i kopniakiem zgodnie z wyposażeniem profilu. Sprawdzić dopuszczenie odpowiedniej metody, w tym sterowanie zapłonem i wtryskiem po uzyskaniu wymaganej synchronizacji. Powtórzyć przy odłączonym HMI i przy utraconej komunikacji CAN. Przy braku HMI odczytać zapis diagnostyczny z ECU.
3. Powtórzyć obie metody z aktywnym przewodowym STOP i sprawdzić utrzymanie odcięcia zgodnie z SYS-037 i SYS-160–162. Metodę wymuszenia usterki, warunki synchronizacji i kryteria obserwacji wyjść określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Zwolnienie blokady po przewróceniu przy potwierdzonej usterce

KTM opisuje automatyczne zgaszenie silnika po wykryciu upadku w rodzinie enduro MY2024. [KTM, opis czujnika przewrócenia](https://www.ktm.com/en-us/2024-enduro-range-press-kit.html#roll-over-sensor).

W odpowiedzi na pytanie 209 (2026-11-14) właściciel ustalił, że po potwierdzeniu usterki toru wykrywania przewrócenia ECU zwalnia blokadę po upadku niezależnie od aktualnego stanu motocykla. HMI ostrzega o niedostępności wykrywania przewrócenia. Do ponownego rozruchu potrzebna jest nowa świadoma próba, a pozostałe warunki rozruchu nadal obowiązują (SYS-200).

### Plan próby SYS-200

1. Na stanowisku odwzorować potwierdzone przewrócenie, zgaszenie silnika i aktywną blokadę. Utrzymać odwzorowane położenie motocykla po upadku. Wymusić usterkę toru i sprawdzić utrzymanie blokady przed potwierdzeniem usterki. Po potwierdzeniu sprawdzić zwolnienie blokady, oznaczenie funkcji jako niedostępnej, DTC z zamrożoną ramką oraz ostrzeżenie na HMI. Powtórzyć dla usterki wykrytej podczas podnoszenia motocykla przed potwierdzeniem prawidłowego położenia.
2. Zasymulować START przytrzymany przy aktywnej blokadzie. Po potwierdzeniu usterki sprawdzić, że rozrusznik, zapłon i wtrysk pozostają wyłączone do nowej próby. Sprawdzić dopuszczenie po puszczeniu i nowym naciśnięciu START oraz w osobnym przebiegu po nowej próbie kopniakiem, przy spełnieniu pozostałych warunków. Powtórzyć z aktywnym przewodowym STOP. Sprawdzić zwolnienie blokady po upadku oraz utrzymanie odcięcia wyjść przez STOP.
3. Powtórzyć z odłączonym HMI. Sprawdzić lokalne zwolnienie blokady i zapis diagnostyczny, a po powrocie komunikacji sprawdzić ostrzeżenie o aktywnej niedostępności. Przed próbami określić kryteria potwierdzenia usterki, metodę odwzorowania stanów i czasy reakcji. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Powrót wykrywania przewrócenia po odzyskaniu pomiaru

W odpowiedzi A na pytanie 210 (2026-11-14) właściciel zatwierdził automatyczny powrót wykrywania przewrócenia w trakcie bieżącej pracy silnika po potwierdzeniu wiarygodności pomiaru (SYS-201).

### Plan próby SYS-201

1. Na stanowisku odwzorować pracujący silnik, aktywną usterkę toru i niedostępne wykrywanie przewrócenia według SYS-198. Podać przejściowy prawidłowy odczyt, który nie spełnia kryterium odzyskania wiarygodności. Sprawdzić utrzymanie niedostępności i ostrzeżenia. Następnie podać wiarygodny pomiar prawidłowego położenia i spełnić kryterium odzyskania wiarygodności bez zatrzymywania silnika.
2. Po potwierdzeniu odzyskania wiarygodności sprawdzić powrót wykrywania i dalszą pracę silnika przy prawidłowym położeniu. Sprawdzić wygaszenie ostrzeżenia po potwierdzeniu ustąpienia usterki oraz zachowanie DTC i zamrożonych ramek w historii według SYS-022/023.
3. W tym samym cyklu pracy podać sygnał spełniający kryteria przewrócenia z SYS-039. Sprawdzić automatyczne zgaszenie silnika. Powtórzyć z odłączonym HMI. Kryteria wiarygodności, sposób odwzorowania położenia i czasy reakcji określić przed próbą. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Ocena położenia po wybudzeniu ECU

Honda CRF250L MY2015 wymaga cyklu stacyjki przed ponownym uruchomieniem po zadziałaniu czujnika przewrócenia. [Instrukcja Hondy CRF250L MY2015](https://cdn.powersports.honda.com/documentum/MWOM/ml.remawmom.2015_31kzza20_crf25l.pdf#page=101).

W odpowiedzi na pytanie 211 (2026-11-15) właściciel ustalił ponowną ocenę położenia przy wybudzeniu. Potwierdzenie, że motocykl nadal leży, utrzymuje blokadę. Po potwierdzeniu prawidłowego położenia świadoma próba rozruchu jest możliwa przy spełnieniu pozostałych warunków (SYS-202).

W doprecyzowaniu pytania 212 z 2026-11-15 właściciel określił cel czasowy oceny położenia. Przy sprawnym czujniku i stojącym motocyklu ocena ma się zakończyć w czasie przygotowania ECU do próby rozruchu. Właściciel zaproponował wykonanie oceny podczas autotestu (SYS-202).

### Plan próby SYS-202

1. Odwzorować potwierdzone przewrócenie, zatrzymanie wału, aktywną blokadę i przejście w uśpienie. Pozostawić motocykl w położeniu odpowiadającym przewróceniu. Wybudzić ECU i sprawdzić wstrzymanie rozruchu podczas oczekiwania na wiarygodny wynik. Po potwierdzeniu położenia odpowiadającego przewróceniu sprawdzić aktywną blokadę. W obu stanach sprawdzić w odrębnych przebiegach, że próby START i kopniakiem utrzymują rozrusznik, zapłon i wtrysk wyłączone odpowiednio do wyposażenia. W odrębnym przebiegu odwzorować przewrócenie podczas snu bez aktywnej blokady przed uśpieniem.
2. Powtórzyć cykl z aktywną blokadą przed snem i postawieniem motocykla podczas snu. Po wybudzeniu podać prawidłowy pomiar spełniający kryteria wiarygodności. Sprawdzić, że ECU dopuszcza nową próbę START lub kopniakiem po potwierdzeniu położenia i spełnieniu pozostałych warunków. Powtórzyć z odłączonym HMI. Osobno sprawdzić, że samo potwierdzenie położenia nie uruchamia silnika.
3. Wybudzić ECU w warunkach, w których tor pomiarowy początkowo nie dostarcza wiarygodnego wyniku i sprawdzić wstrzymanie rozruchu do czasu uzyskania wyniku albo potwierdzenia usterki. W próbie z usterką potwierdzić reakcję według SYS-199 i SYS-200. Kryteria położenia i wiarygodności określić przed próbą.
4. Przy prawidłowym położeniu i sprawnym czujniku zarejestrować od tego samego zdarzenia wybudzenia czas do potwierdzenia położenia oraz czas do zakończenia pozostałych czynności przygotowujących ECU do próby rozruchu. Sprawdzić, czy ocena położenia kończy się w tym czasie. Uwzględnić wybudzenie przez START i kopniak stosownie do wyposażenia oraz dopuszczone warunki napięcia i temperatury. Przed próbą określić punkty pomiarowe oraz budżet czasu gotowości. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Próby autotestu przed dopuszczeniem rozruchu

W odpowiedzi **B na pytanie 212** (2026-11-17) właściciel zatwierdził zakończenie wszystkich prób autotestu wykonalnych w aktualnych warunkach przy zgaszonym silniku przed dopuszczeniem rozruchu (SYS-203). Dotyczy to także próby wentylatora, jeżeli warunki pozwalają ją wykonać. Ten warunek doprecyzowuje wcześniejsze pierwszeństwo rozruchu: dostępne próby przed rozruchem trzeba najpierw zakończyć, a rozruch nadal pozostaje niezależny od gotowości HMI.

Próby wymagające obrotu wału, pracy silnika albo innych niespełnionych warunków pozostają oczekujące. Odłożoną próbę wentylatora ECU wykonuje według SYS-195. O dopuszczeniu rozruchu po zakończeniu prób decydują ich wyniki i właściwe reakcje na usterki. Potwierdzona usterka wentylatora utrzymuje odcięcie jego obwodu według SYS-191–196; potwierdzone położenie motocykla na boku przy sprawnym torze utrzymuje blokadę rozruchu według SYS-202.

### Plan próby SYS-203

1. Na stanowisku z poprawnym profilem, sprawnym torem położenia i prawidłowym położeniem motocykla wybudzić ECU w warunkach umożliwiających wszystkie przewidziane próby przy zgaszonym silniku, w tym próbę wyposażonego wentylatora. Podczas ich trwania zgłosić START, a w osobnym przebiegu zasymulować obroty wału odpowiadające kopniakowi. Sprawdzić brak sterowania rozrusznikiem, zapłonem i wtryskiem w celu rozruchu do zakończenia dostępnych prób oraz wykonanie dopuszczonej próby wentylatora. Po zakończeniu prób sprawdzić gotowość i świadomy rozruch przy spełnieniu pozostałych warunków. Obsługę przytrzymanego START przy zwykłym wybudzeniu określa SYS-204.
2. Zasymulować usterkę wentylatora podczas próby. Sprawdzić zakończenie próby, DTC i utrzymanie odcięcia wentylatora zgodnie z SYS-191–196 oraz dopuszczenie rozruchu, gdy pozostałe warunki są spełnione. W odrębnym przebiegu podać wiarygodny pomiar położenia na boku i sprawdzić utrzymanie blokady rozruchu mimo zakończenia prób. Powtórzyć z aktywnym przewodowym STOP.
3. Wybudzić ECU przy zasilaniu wystarczającym do właściwego rozruchu, ale uniemożliwiającym próbę wentylatora. Sprawdzić, że ta próba zachowuje status oczekiwania, a po zakończeniu pozostałych dostępnych kontroli ECU może dopuścić świadomy rozruch. Po powrocie warunków sprawdzić wykonanie według SYS-195. W profilu bez wentylatora sprawdzić zgodność zakresu z konfiguracją.
4. Dla prób wymagających obrotu wału lub pracy silnika sprawdzić status oczekiwania przed rozruchem oraz wykonanie dopiero we właściwym stanie; brak obrotu nie może powodować oznaczenia dekodera jako sprawdzonego. Sprawdzić, że samo wybudzenie i zakończenie autotestu bez żądania rozruchu nie uruchamiają silnika.
5. Powtórzyć właściwe przebiegi bez HMI oraz przy opóźnionym uruchomieniu HMI. Zmierzyć czas od wybudzenia do zakończenia poszczególnych prób i gotowości do rozruchu, osobno dla START i kopniaka. Przed próbami określić wyposażenie profilu, warunki wykonalności, kryteria zakończenia, punkty pomiaru oraz budżet czasu. Próby produktu pozostają do wykonania na właściwym etapie. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## START przytrzymany podczas autotestu

W odpowiedzi **A na pytanie 213** (2026-11-17) właściciel zatwierdził rozpoczęcie pracy rozrusznika na tym samym przytrzymaniu START po zakończeniu prób wymaganych przed rozruchem podczas zwykłego wybudzenia (SYS-204). Prawidłowe położenie i pozostałe warunki muszą być spełnione. Reguły nowej próby po STOP, przewróceniu, resecie oraz innych odcięciach pozostają nadrzędne. Żądanie trwa tylko podczas trzymania START według SYS-048.

### Plan próby SYS-204

1. Na stanowisku uśpić ECU w zwykłym stanie, bez blokady po przewróceniu lub odcięcia wymagającego nowej próby. Utrzymać prawidłowy pomiar położenia i pozostałe warunki rozruchu. Nacisnąć START i trzymać go przez dostępne próby autotestu, w tym próbę wyposażonego wentylatora według SYS-203. Sprawdzić wyłączony rozrusznik do zakończenia wymaganych prób oraz jego załączenie po uzyskaniu gotowości bez ponownego naciśnięcia. Zarejestrować START, zakończenie prób i sterowanie rozrusznikiem; kryteria i budżet czasu określić przed próbą.
2. W odrębnym przebiegu puścić START przed zakończeniem prób. Po uzyskaniu gotowości sprawdzić brak samoczynnego kręcenia oraz dopuszczenie nowego żądania START. Przy prawidłowym rozruchu sprawdzić wyłączenie po puszczeniu przycisku według SYS-048. Osobno sprawdzić automatyczne odcięcia i brak ponawiania przy dalszym trzymaniu według SYS-049.
3. Powtórzyć właściwe przebiegi po zdarzeniach wymagających nowej próby: aktywny STOP według SYS-160–161, utrata synchronizacji podczas rozruchu według SYS-158, reset nadzoru według SYS-171, przerwanie zasilania podczas kręcenia według SYS-182 i podnoszenie motocykla według SYS-197. Sprawdzić, że SYS-204 zachowuje wymaganie nowego naciśnięcia wynikające z tych reakcji. Uwzględnić zwolnienie blokady po usterce toru według SYS-200.
4. Powtórzyć zwykłe wybudzenie z odłączonym HMI i w odrębnym przebiegu z opóźnionym jego uruchomieniem. Dla sprawnego toru położenia utrzymującego wiarygodny stan przewrócenia sprawdzić dalszą blokadę mimo zakończenia prób i trzymanego START. Kryteria poszczególnych usterek i połączenia stanowiska ustalić przed próbami. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Utrata impulsów fazy po prawidłowej synchronizacji 4T

W odpowiedzi na **pytanie 214** (2026-11-18) właściciel przyjął dalszą pracę silnika 4T o stałych fazach rozrządu po usterce czujnika fazy, z rejestracją DTC, gdy ECU zachowuje wiarygodną informację o cyklu i sygnale wału (SYS-205). ECU utrzymuje bieżące sterowanie i zestaw map; pozostałe reakcje ochronne pozostają aktywne. Rozpatrywany przypadek dotyczy braku kolejnych impulsów po wcześniejszym poprawnym rozpoznaniu cyklu.

[Haltech — Trigger System, Synchronization Mode](https://support.haltech.com/portal/en/kb/articles/trigger) potwierdza możliwość utrzymywania rozpoznanego cyklu z wału w odpowiedniej strategii oraz wymóg prawidłowego sygnału wału. Kryteria wiarygodności i diagnostykę określimy dla dekodera DustONE.

### Plan próby SYS-205

1. Na stanowisku z symulatorem wału i fazy uruchomić profil 4T o stałych fazach rozrządu, który wykorzystuje wejście fazy. Po prawidłowym rozpoznaniu cyklu zasymulować brak kolejnych impulsów fazy przy prawidłowym wale. Sprawdzić dalsze sterowanie zapłonem i wtryskiem według dotychczasowego cyklu i zestawu map oraz brak przesunięcia harmonogramu o 360°. Powtórzyć przy reprezentatywnych obrotach i obciążeniach profilu. Późniejsze dopuszczenie profilu wymaga prób zgodnego silnika 4T.
2. Sprawdzić zapis DTC i zamrożonej ramki według SYS-019/024 oraz udostępnienie stanu HMI. Powtórzyć z odłączonym HMI i CAN, potwierdzając lokalne sterowanie i zapis. W odrębnym przebiegu użyć profilu niewykorzystującego wejścia fazy i potwierdzić zgodność diagnostyki z konfiguracją.
3. Po zaniku impulsów fazy wprowadzić utratę synchronizacji wału. Sprawdzić odcięcie według SYS-157 oraz utrzymanie jego reguł ponowienia. W osobnym przebiegu sprawdzić działanie przewodowego STOP. SYS-205 dopuszcza dalszą pracę przy zachowanej wiarygodności cyklu i wału.
4. Przed próbami określić wzorce wejść, kryteria rozpoznania i utraty wiarygodności, czas potwierdzenia usterki, punkty obserwacji harmonogramu oraz połączenia stanowiska. Rozruch z usterką podlega SYS-206, a potwierdzona niezgodność sygnałów SYS-207. Kryteria zaniku i powrotu sygnału oraz diagnostyka wymagają specyfikacji według SYS-019–025; odcięcie według SYS-207 ma własne warunki wznowienia. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Rozruch profilu 4T wykorzystującego czujnik fazy

W odpowiedzi **B na pytanie 215** (2026-11-18) właściciel wymaga prawidłowego czujnika fazy przy nowym uruchomieniu silnika, jeżeli profil go wykorzystuje (SYS-206). Wymagany sygnał fazy i rozpoznanie cyklu 720° muszą zostać potwierdzone przed dopuszczeniem zapłonu i wtrysku. Dalsza praca po zaniku impulsów po wcześniejszej synchronizacji pozostaje dopuszczona według SYS-205.

Rozrusznik może obracać wałem w celu sprawdzenia sygnału przy spełnieniu pozostałych warunków, podczas przytrzymywania START i w granicach SYS-049. Próby wymagające obrotu są wykonywane we właściwym stanie zgodnie z SYS-203. Obecność historii DTC nie zastępuje bieżącej oceny sprawności; ręczne kasowanie historii nie jest warunkiem potwierdzenia naprawy.

Rozważono rozruch 360° i zapasowe rozpoznanie fazy z MAP. Wariant B wymaga sygnału czujnika zadeklarowanego w profilu. Profile niewykorzystujące czujnika fazy według SYS-070 nadal mają własną nominalną strategię.

### Plan próby SYS-206

1. Na stanowisku z symulatorem wału i fazy uruchomić profil wymagający czujnika fazy, następnie zasymulować zanik impulsów przy zachowanym wale i cyklu według SYS-205. Zatrzymać silnik przewodowym STOP. Przy trwającej usterce podjąć nową próbę START i osobno kopniakiem. Sprawdzić wstrzymanie zapłonu i wtrysku przy braku prawidłowej fazy, także przy prawidłowym MAP. Przy rozruchu elektrycznym sprawdzić dopuszczone kręcenie, zakończenie po puszczeniu START lub limicie oraz reguły ponowienia z SYS-048/049. Sprawdzić brak zastąpienia wymaganej fazy trybem 360° lub MAP.
2. Bez ręcznego kasowania DTC przywrócić prawidłowy sygnał fazy i podjąć nową próbę. Sprawdzić dopuszczenie sterowania silnikiem po prawidłowym rozpoznaniu wału i fazy oraz spełnieniu pozostałych warunków. Potwierdzić zachowanie historii i aktualizację stanu usterki zgodnie z SYS-019–025. Powtórzyć po śnie ECU i po restarcie przy nieruchomym silniku, sprawdzając bieżącą ocenę fazy. Kryteria oceny sygnałów i limity rozruchu ustalić przed próbami.
3. Sprawdzić profil niewykorzystujący czujnika fazy z odłączonym wejściem: zachowanie ma wynikać z jego nominalnej konfiguracji według SYS-070. W profilu wykorzystującym czujnik podać impulsy niezgodne ze wzorcem i sprawdzić brak dopuszczenia przed prawidłowym rozpoznaniem cyklu.
4. Powtórzyć właściwe przebiegi z odłączonym HMI oraz CAN. Osobno sprawdzić aktywny STOP i pozostałe nadrzędne blokady. Po próbach stanowiskowych wykonać procedurę właściwego, zgodnego silnika 4T na odpowiednim etapie. Wzorce, punkty obserwacji, połączenia i mierzalne kryteria określić przed wykonaniem. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Potwierdzona niezgodność sygnałów fazy i wału podczas pracy

W odpowiedzi **A na pytanie 216** (2026-11-18) właściciel zatwierdził odcięcie zapłonu i wtrysku oraz zapis DTC po potwierdzonej niezgodności sygnałów fazy i wału w pracującym 4T (SYS-207). Wznowienie wymaga zatrzymania wału, nowej świadomej próby i prawidłowej synchronizacji. Obecność impulsów nie stanowi potwierdzenia ich poprawnej relacji.

Rozróżnienie reakcji jest uzgodnione: brak impulsów po wcześniejszej synchronizacji przy zachowanej wiarygodności cyklu podlega SYS-205, nowe uruchomienie profilu wykorzystującego czujnik fazy podlega SYS-206, a potwierdzona niezgodność podczas pracy podlega SYS-207. Kryteria, tolerancje, filtracja i czasy będą określone dla dekodera.

### Plan próby SYS-207

1. Na stanowisku z symulatorem wału i fazy doprowadzić profil 4T do prawidłowej pracy. Podać obecne sygnały o relacji niespełniającej zdefiniowanych kryteriów zgodności. Po potwierdzeniu usterki sprawdzić odcięcie zapłonu i wtrysku oraz zapis DTC i zamrożonej ramki. Zarejestrować odchyłkę wejść, potwierdzenie usterki i odcięcie wyjść. Sprawdzić czas diagnostyki oraz całkowity czas reakcji względem budżetów ustalonych przed próbą.
2. Przywrócić zgodne sygnały, utrzymując obrót wału. Sprawdzić zachowanie odcięcia. Nacisnąć START przed zatrzymaniem i utrzymać przez zatrzymanie; rozrusznik ma pozostać wyłączony. Po zatrzymaniu zwolnić START i wykonać nową próbę, potwierdzając dopuszczenie sterowania po wymaganej synchronizacji według SYS-206. Osobno sprawdzić nową próbę kopniakiem po zatrzymaniu i działanie aktywnego STOP.
3. W odrębnym przebiegu podać przejściową odchyłkę, która nie spełnia kryteriów potwierdzenia tej usterki. Sprawdzić reakcję zgodną ze specyfikacją diagnostyczną. Osobno zasymulować sam zanik impulsów fazy przy zachowanym wiarygodnym cyklu i wale, potwierdzając dalszą pracę według SYS-205. Nowy rozruch ze sprzecznymi sygnałami podlega SYS-206.
4. Powtórzyć właściwe przebiegi bez HMI i CAN. Sprawdzić wymagany wybór „Standard” i anulowanie oczekującej zmiany zestawu według SYS-137/147 oraz zachowanie historii DTC. Wzorce sygnałów, progi, czasy i punkty obserwacji ustalić przed wykonaniem. Późniejszą procedurę zgodnego silnika 4T przygotować po weryfikacji stanowiskowej. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Usterka temperatury powietrza dolotowego IAT — praca i rozruch

Pomiar IAT jest przyjętym zakresem według SYS-031. Potwierdzony przykład enduro: Beta RR 350 EFI MY2016 wykorzystuje T-MAP, łączący temperaturę i ciśnienie dolotu. [Schemat producenta, strony PDF 8–9, legenda poz. 30](https://betausa.com/content/WIRING%20DIAGRAM%204T%202%2024%20new.pdf#page=9).

IAT dostarcza temperaturę powietrza potrzebną do kompensacji dawki paliwa. Przy tym samym ciśnieniu zimniejsze powietrze ma większą gęstość i dla zachowania składu mieszanki wymaga większej ilości paliwa. Dokładny udział pomiaru zależy od strategii profilu. [Haltech — rola IAT](https://support.haltech.com/portal/en/kb/articles/inlet-air-temperature-sensor-7-4-2020).

Przykład ilustracyjny z równania gazu doskonałego: przy tym samym ciśnieniu powietrze o temperaturze 0°C ma około 15% większą gęstość niż przy 40°C (stosunek 313,15/273,15 ≈ 1,146). To porównanie samej gęstości; rzeczywista kompensacja paliwa wymaga kalibracji profilu. [NASA — równanie stanu gazu](https://www1.grc.nasa.gov/beginners-guide-to-aeronautics/equation-of-state/).

Przy typowej kompensacji gęstości zaniżona temperatura przyjęta przez ECU może prowadzić do nadmiaru paliwa, a zawyżona do niedoboru. Błędna dawka może pogorszyć rozruch, równomierność pracy i osiągi. Zbyt uboga mieszanka przy dużym obciążeniu stanowi ryzyko uszkodzenia silnika. [Haltech — praca pod obciążeniem](https://support.haltech.com/portal/en/kb/articles/applying-load-to-the-engine).

IAT jest ważny dla dawkowania. Po jego utracie ECU może nadal znać położenie silnika z wału i fazy, a strategia zastępcza może umożliwić pracę w zweryfikowanym zakresie. Prawidłowość takiej strategii podczas pracy i rozruchu wymaga osobnych prób. Ewentualne ograniczenia oraz zastępczą temperaturę dobierzemy dla konkretnego profilu.

W odpowiedzi na **pytanie 217 i jego doprecyzowanie** (2026-11-18) właściciel objął strategią awaryjną także nowy rozruch przy trwającym nieprawidłowym pomiarze lub uszkodzonym IAT (SYS-208). Dotyczy to profilu wtryskowego z wiarygodnymi pozostałymi wymaganymi sygnałami i odpowiednią, osobno zweryfikowaną strategią dla pracy oraz rozruchu. Obowiązują DTC, „Standard” według SYS-137 i pozostałe zabezpieczenia. Celem jest możliwie normalna jazda w zakresie potwierdzonym próbami.

Przyjęty kierunek obejmuje oszacowanie zastępczej IAT w granicach zweryfikowanej kalibracji profilu, z oceną przydatności pomocniczej temperatury ECU. Praca i rozruch wymagają osobnej walidacji. Temperatura PCB pozostaje osobną wielkością według SYS-031.

### Pomocnicza temperatura ECU — wejście do projektu

Przy projektowaniu strategii ocenimy przydatność temperatury ECU jako pomocniczych danych do oszacowania zastępczej IAT przy usterce. Podstawowy pomiar dolotu nadal pochodzi z IAT według SYS-031. Dobór konkretnego barometru i sposobu pomiaru temperatury pozostaje do wspólnej decyzji na właściwym etapie.

[Bosch BME280, opis na s. 3 i uwaga 7 na s. 12](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme280-ds002.pdf#page=12) dopuszcza szacowanie temperatury otoczenia z kanału temperatury i wskazuje wpływ PCB oraz samonagrzewania na jego wskazanie. Jest to przykład własności pomiaru, a nie wybór komponentu do DustONE.

Wniosek projektowy: po dostatecznym wyrównaniu temperatur taki odczyt może dać użyteczne odniesienie. W trakcie pracy i po gorącym postoju trzeba uwzględnić zmienny błąd i opóźnienie cieplne, zależne od obudowy, montażu i obciążeń ECU. Dokładność sensora nie opisuje całego błędu oszacowania dolotu. Warunek wyrównania ciśnienia dla barometru jest już przekazany do projektu obudowy w zakresie systemu.

Przykład ilustracyjny: przy rzeczywistej IAT 20°C i zastąpieniu jej odczytem PCB 60°C prosty model gęstości przy tym samym ciśnieniu zaniży oszacowaną masę powietrza o około 12% (293,15/333,15 − 1). Rzeczywisty wpływ na dawkę zależy od strategii i kalibracji profilu. [Podstawa obliczenia — równanie stanu gazu](https://www1.grc.nasa.gov/beginners-guide-to-aeronautics/equation-of-state/).

Założenia realizacji do zweryfikowania dla profilu:

1. Zapamiętać ostatnią wiarygodną IAT wraz z wiekiem próbki i stanem jej ważności.
2. Szacować temperaturę na podstawie wiarygodnych dostępnych danych. Kandydatami są temperatura ECU, stan cieplny silnika z ECT i czas od wybudzenia lub zmiany stanu. Skład danych, model i zakres jego wiarygodności wynikną z pomiarów; warunki zimnego postoju oraz gorącego ponownego rozruchu wymagają odrębnej oceny.
3. Strategię zastępczą powiązać z wymuszonym „Standard” według SYS-137. Celem jest zachowanie możliwie normalnej jazdy w zweryfikowanym zakresie. Ewentualne ograniczenia wynikają z prób i dopuszczalnej niepewności dawki. Stan IAT i dane oszacowane mają być rozróżnialne w diagnostyce; zamrożona ramka powinna pozwolić ocenić źródło oszacowania.

### Plan próby SYS-208

1. Dla przygotowanego profilu i modelu porównać oszacowanie IAT z działającym, skalibrowanym referencyjnym pomiarem, przed użyciem oszacowania do sterowania dawką. Rejestrować IAT, temperaturę ECU, ECT, stan odbiorników i wiek danych. Objąć oceną wyrównanie temperatur po postoju, zimne wybudzenie, nagrzewanie elektroniki, wolną i szybszą jazdę, gorący postój, wpływ montażu/obudowy i obciążenia wyjść. Przed próbą określić dopuszczalny błąd i warunki wiarygodności modelu.
2. Przy sprawnym referencyjnym pomiarze i potwierdzonej kalibracji zasymulować usterkę używanego IAT podczas pracy wtrysku. Sprawdzić dalszą pracę w dopuszczonym zakresie, przejście na „Standard”, odmowę zmiany zestawu według SYS-137 i poprawne oznaczenie użycia wartości zastępczej. Dopiero po ocenie stanowiskowej i błędu estymacji wykonać próby dawki z zewnętrznym pomiarem lambda, zgodnie z zakresem strojenia.
3. Osobno zweryfikować nowy rozruch przy trwającej usterce: zimny i ciepły silnik, gorący postój oraz sen/wybudzenie ECU. Uwzględnić brak lub stary ostatni IAT i niesprawny pomocniczy pomiar temperatury ECU. Sprawdzić wyłącznie użycie danych i strategii dopuszczonych dla danego przypadku; pozostałe warunki rozruchu, START, STOP i faza nadal obowiązują.
4. Sprawdzić warunki graniczne kalibracji, egzekwowanie przewidzianych ograniczeń oraz reakcję przy braku odpowiedniej zweryfikowanej strategii: kontrolowane zatrzymanie podczas pracy albo blokadę uruchomienia. Kryteria zakresu i przejść określić przed próbą.
5. Sprawdzić DTC, zamrożone ramki pierwszego/ostatniego wystąpienia, licznik wystąpień oraz dostępne dane o źródle oszacowania i wieku użytego IAT. Odczyt w HMI i Windows ma rozróżniać stan pomiaru oraz użycie danych zastępczych.
6. Powtórzyć odpowiednie przypadki bez HMI i CAN, sprawdzając lokalną decyzję ECU, zapis i wymagane zabezpieczenia. Do dopuszczenia profilu potrzebne są próby właściwego silnika wtryskowego, z oddzielnymi kryteriami dla pracy i rozruchu. Model, komponenty, połączenia oraz mierzalne kryteria ustalić przed wykonaniem. [Macierz weryfikacji](../verification/macierz-wymagan.md).

## Pytanie 218 — powrót na prawidłowy pomiar IAT

Silnik pracuje na zastępczej IAT według SYS-208, a ECU potwierdza, że pomiar znów jest wiarygodny. Rzeczywista temperatura może różnić się od oszacowanej, więc zmiana źródła wpływa na korektę dawki. Wniosek projektowy: powrót podczas pracy wymaga potwierdzenia wiarygodności i sprawdzenia sposobu przejścia dla profilu.

Do ustalenia pozostaje automatyczny powrót podczas bieżącej pracy, po potwierdzeniu pomiaru i z przejściem zweryfikowanym dla profilu, albo utrzymanie strategii zastępczej do następnego uruchomienia silnika z prawidłowym IAT. Pierwszy wariant umożliwia wcześniejsze korzystanie z rzeczywistego pomiaru; drugi zachowuje tryb do końca bieżącej pracy, podobnie do przyjętej reguły dla pomiarów obciążenia w F02. Parametry potwierdzenia i przejścia należą do późniejszej specyfikacji.

Pytanie dotyczy źródła IAT i zakończenia strategii zastępczej. Historia DTC oraz wybór zestawu „Standard” podlegają już przyjętym regułom SYS-019–025 i SYS-137–138.
