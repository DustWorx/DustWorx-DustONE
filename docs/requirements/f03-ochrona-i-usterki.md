# F03 — ochrona i reakcje na usterki

Stan na 2026-11-11. **F03 aktywny po zamknięciu F02.** Macierz robocza łączy zdarzenie, reakcję i warunek powrotu. Zatwierdzone wymagania są w [rejestrze SYS](../01-zakres-systemu.md). Kolejność pakietów określa [status projektu](../00-proces-i-status.md).

| Zdarzenie lub temat | Przyjęta reakcja i warunek powrotu | Do rozstrzygnięcia w F03 | Plan prób |
| --- | --- | --- | --- |
| Utrata synchronizacji wału podczas pracy | ECU odcina zapłon oraz wtrysk w wyposażonych profilach. Odzyskanie sygnału podczas dalszego obrotu utrzymuje odcięcie. Powrót wymaga zatrzymania, nowej świadomej próby rozruchu i ponownej wiarygodnej synchronizacji (SYS-157). | Wymaganie przyjęte. Kryteria rozpoznania zdarzeń do projektu. | V01, V02, V04 |
| Utrata uzyskanej synchronizacji wału podczas rozruchu elektrycznego | Potwierdzona utrata przed rozpoznaniem pracy silnika kończy próbę. ECU wyłącza rozrusznik także przy przytrzymanym START. Ponowna próba wymaga zatrzymania, zwolnienia i ponownego naciśnięcia START (SYS-158). | Wymaganie przyjęte. Kryteria utraty synchronizacji i zatrzymania do projektu. | V01, V04 |
| Utrata uzyskanej synchronizacji wału podczas rozruchu kopniakiem | Potwierdzona utrata kończy próbę. Powrót sygnału przy dalszym obrocie utrzymuje odcięcie zapłonu i wtrysku. Wznowienie wymaga zatrzymania wału i nowej próby z wiarygodną synchronizacją (SYS-159). | Wymaganie przyjęte. Kryteria zatrzymania i rozpoznania nowej próby do projektu. | V01, V02, V04 |
| Utrata sygnału fazy w profilu 4T, który go używa | Przyjęto osobne wejście Hall (SYS-070). | Reakcja i warunek powrotu zależnie od profilu. | V01, V02 |
| Przewodowy STOP i START | STOP działa przy awarii HMI lub CAN. START działa podczas przytrzymania z uzgodnionymi odcięciami i wymaganiem nowej próby po odcięciu (SYS-037/048/049). Naciśnięcie START przy aktywnym STOP utrzymuje rozrusznik wyłączony. Zwolnienie STOP wymaga nowego START (SYS-160). STOP wykryty podczas kręcenia wyłącza rozrusznik i kończy próbę. Ponowienie wymaga nowego START po zwolnieniu STOP (SYS-161). Po użyciu STOP podczas pracy odcięcie trwa do zatrzymania wału i nowej próby z wiarygodną synchronizacją (SYS-162). Wybudzone ECU wykrywa przerwę w obwodzie także przy zwolnionym STOP (SYS-163). Potwierdzona przerwa wywołuje reakcję diagnostyczną. ECU kontynuuje pracę i dopuszcza nową próbę rozruchu przy spełnieniu pozostałych warunków (SYS-164). ECU rozróżnia zwarcie przewodu STOP do masy od naciśnięcia przycisku (SYS-165). Zwarcie do masy skutkuje zapisem DTC. ECU dopuszcza dalszą pracę i nową próbę rozruchu przy spełnieniu pozostałych warunków (SYS-166). Sprawny STOP odcina zapłon i wtrysk oraz odłącza rozrusznik niezależnie od głównego firmware (SYS-167–168). | Parametry i realizacja toru do projektu. | V03, V04, V10, V13 |
| Potwierdzone przewrócenie | ECU wyłącza silnik. Po postawieniu i spełnieniu warunków bezpieczeństwa rozruch wymaga świadomej próby (SYS-039/040). | Warunki zadziałania i powrotu odpowiednie dla enduro. | V04 |
| Brak HMI albo CAN | ECU działa samodzielnie, a reakcje akcesoriów są odrębne (SYS-046/050–053). | Zależności od pozostałych stanów ochronnych. | V07 |
| Usterka TPS lub pomiaru ciśnienia używanego do określenia obciążenia | Przyjęto reguły kalibracji awaryjnej, kontrolowanego zatrzymania, powrotu i wymuszenia „Standard” (SYS-121–142). | Powiązać z pozostałymi blokadami F03. [Zakres F02](f02-przeglad-zakresu.md) opisuje przyjęte przypadki. | V02, V03, V04 |
| Chłodzenie i pozostałe pomiary ochronne | Przyjęto pomiar płynu i automatykę wentylatora oraz wejścia ciśnienia paliwa i binarne oleju (SYS-029/043/044/060). | Reakcje na niedostępny pomiar i na warunki poza dopuszczalnym zakresem w wyposażonych profilach. | V02, V03, V05 |
| Zasilanie i restart ECU | Przyjęto zasilanie bez stacyjki, zasady oszczędzania i odrębne reguły odtwarzania konfiguracji oraz map (SYS-054/084–089/106/109/155). Niezależny nadzór po wykryciu zawieszenia wymusza odcięcie wyjść i osobno inicjuje reset (SYS-169). Po resecie odcięcie zapłonu i wtrysku trwa do zatrzymania wału i nowej świadomej próby z wiarygodną synchronizacją (SYS-170). | Nowe naciśnięcie START przed zatrzymaniem wału po resecie nadzoru (pytanie 181). | V01, V04, V06, V13 |

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

## Pytanie 181 — nowe naciśnięcie START przed zatrzymaniem wału po resecie nadzoru

Do ustalenia pozostaje obsługa nowego naciśnięcia START, gdy ECU już działa po resecie nadzoru, ale wał nadal się obraca. Rozpatrujemy odrzucenie żądania oraz zachowanie go do zatrzymania wału, jeśli kierowca nadal trzyma START i spełnione są pozostałe warunki.
