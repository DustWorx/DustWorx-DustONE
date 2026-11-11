# ADR-002 — samodzielność ECU i HMI jako klient

Data decyzji 2026-10-25. Uzupełnienie 2026-11-11 obejmuje nadzór obwodu STOP oraz odcięcie przez STOP i niezależny nadzór przy zawieszeniu głównego firmware ECU. Szczegóły realizacji są do określenia.

## Problem i opcje

Utrata HMI lub CAN może oznaczać wyłączenie silnika albo pozostawienie sterowania w samodzielnym ECU. Należy ustalić właściciela danych i odpowiedzialność za wykonywanie żądań.

## Decyzja i podstawa zatwierdzenia

Właściciel projektu w odpowiedzi na pytanie 55 z 2026-10-25 wskazał, że ECU ma działać niezależnie od komunikacji z HMI, jest właścicielem danych, a HMI wysyła żądania odczytu lub polecenia, np. zmiany map. W odpowiedzi na pytanie 56 i późniejszym doprecyzowaniu tego samego dnia potwierdził, że przyciski obsługi HMI pozostają podłączone do HMI, natomiast START i STOP są od niego niezależne.

ECU samodzielnie steruje silnikiem i jego zabezpieczeniami, zarządza konfiguracją, mapami, diagnostyką oraz danymi eksploatacyjnymi motocykla. HMI jest klientem: prezentuje dane i przekazuje żądania użytkownika. ECU rozstrzyga wykonanie żądania i podaje rzeczywisty stan. Obecność HMI nie jest warunkiem pracy ECU; sama utrata HMI/CAN nie gasi silnika. Powiązania: [SYS-046 i SYS-047](../01-zakres-systemu.md).

W odpowiedzi **A na pytanie 170** (2026-11-11) właściciel zatwierdził utrzymanie wyłączonego rozrusznika przy naciśnięciu START na zgaszonym silniku z aktywnym przewodowym STOP. Po zwolnieniu STOP wymagane jest nowe naciśnięcie START (SYS-160). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md).

W odpowiedzi **A na pytanie 171** (2026-11-11) właściciel zatwierdził odłączenie rozrusznika po wykryciu przewodowego STOP podczas kręcenia. ECU kończy próbę. Po zwolnieniu STOP potrzebne jest nowe naciśnięcie START (SYS-161). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md).

W odpowiedzi **A na pytanie 172** (2026-11-11) właściciel zatwierdził utrzymanie odcięcia po zwolnieniu STOP podczas obrotu wału. Powrót sterowania wymaga zatrzymania wału i nowej świadomej próby rozruchu z wiarygodną synchronizacją (SYS-162). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md).

W odpowiedzi **A na pytanie 173** (2026-11-11) właściciel zatwierdził nadzór przewodowego STOP w wybudzonym ECU. ECU rozpoznaje przerwę w obwodzie także przy zwolnionym przycisku, niezależnie od HMI i CAN (SYS-163). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md).

W odpowiedzi na **pytanie 174** (2026-11-11) właściciel ustalił reakcję diagnostyczną na przerwę w obwodzie STOP. ECU zgłasza DTC, kontynuuje sterowanie silnikiem i dopuszcza nową próbę rozruchu przy spełnieniu pozostałych warunków (SYS-164). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-164).

W odpowiedzi **A na pytanie 175** (2026-11-11) właściciel zatwierdził odrębne rozpoznawanie zwarcia przewodu sygnałowego STOP do masy. Wybudzone ECU odróżnia je od naciśnięcia sprawnego przycisku niezależnie od HMI i CAN (SYS-165). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-165).

W odpowiedzi **A na pytanie 176** (2026-11-11) właściciel zatwierdził zapis DTC z zamrożoną ramką po potwierdzonym zwarciu STOP do masy. ECU kontynuuje sterowanie i dopuszcza nowy rozruch przy spełnieniu pozostałych warunków (SYS-166). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-166).

W odpowiedzi **A na pytanie 177** (2026-11-11) właściciel zatwierdził działanie sprawnego przewodowego STOP przy zawieszeniu głównego firmware ECU. Naciśnięcie STOP wymusza odcięcie zapłonu oraz wtrysku w wyposażonych profilach (SYS-167). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-167).

W odpowiedzi **A na pytanie 178** (2026-11-11) właściciel zatwierdził odłączenie rozrusznika przez sprawny przewodowy STOP również przy zawieszeniu głównego firmware i przytrzymanym START (SYS-168). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-168).

W odpowiedzi **A na pytanie 179** (2026-11-11) właściciel zatwierdził samoczynne odcięcie zapłonu, wtrysku i rozrusznika po wykryciu zawieszenia głównego firmware. Nadzór wymusza odcięcie niezależnie od resetu i osobno inicjuje reset (SYS-169). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-169).

W odpowiedzi **A na pytanie 180** (2026-11-11) właściciel zatwierdził wznowienie zapłonu i wtrysku po resecie nadzoru dopiero po zatrzymaniu wału, w nowej świadomej próbie rozruchu z wiarygodną synchronizacją (SYS-170). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-170).

W odpowiedzi **A na pytanie 181** (2026-11-11) właściciel zatwierdził odrzucenie START przed potwierdzeniem zatrzymania wału po resecie nadzoru. Rozrusznik można załączyć po nowym naciśnięciu START wykonanym po zatrzymaniu (SYS-171). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-171).

W odpowiedzi na **pytanie 182** (2026-11-11) właściciel ustalił zapis przyczyny i dostępnych danych zdarzenia w zamrożonej ramce po potwierdzonym resecie nadzoru (SYS-172). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-172).

W odpowiedzi **A na pytanie 183** (2026-11-11) właściciel zatwierdził limit automatycznych prób uruchomienia po powtarzających się resetach nadzoru i utrzymanie odcięcia po osiągnięciu limitu (SYS-173). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-173).

W odpowiedzi na **pytanie 184** (2026-11-11) właściciel wskazał automatyczne odzyskiwanie ECU. Po limicie standardowych prób ECU samoczynnie rozpoczyna odzyskiwanie przy utrzymanym odcięciu (SYS-174). [Plan próby F03](../requirements/f03-ochrona-i-usterki.md#plan-próby-sys-174).

## Konsekwencje

- Dane i pomiary wymagane do autonomicznego sterowania silnikiem oraz jego zabezpieczeń muszą być dostępne ECU bez udziału HMI. Uwzględnić to przy wyborze miejsca podłączenia czujników.
- Pracujące ECU korzysta z własnej konfiguracji i aktywnych map. Odczyt lub odświeżanie ekranu nie steruje cyklem pracy silnika.
- Przyciski obsługi HMI i zwykłe przełączniki akcesoriów pozostają podłączane do HMI według SYS-016. START ma osobne przewodowe wejście ECU (SYS-048), a STOP osobny obwód gaszenia (SYS-037). Oba działają bez HMI i komunikacji CAN ECU–HMI.
- Szczegóły trwałości poszczególnych danych, rozmieszczenia zasobów graficznych i pamięci podręcznej HMI pozostają do specyfikacji; ECU musi posiadać dane wymagane do samodzielnej pracy.

## Do określenia

Ważność i potwierdzanie żądań, wykrywanie utraty komunikacji, stany akcesoriów i rozrusznika, zachowanie przy ponownym połączeniu oraz ewentualne DTC komunikacyjne. Model odczytu/publikacji danych, czasy, formaty i szybkość CAN nie zostały wybrane.

## Proponowana weryfikacja

Próby stanowiskowe: ECU z HMI nieobecnym od włączenia zasilania; utrata połączenia i restart HMI podczas symulowanej pracy silnika; odczyt konfiguracji i aktywnej mapy po przywróceniu komunikacji. Kryterium SYS-046: sam brak HMI/CAN nie wyłącza sterowania ani lokalnych zabezpieczeń. Dla SYS-047 sprawdzić, że HMI odczytuje rzeczywisty stan ECU, a wykonanie żądania jest rozstrzygane w ECU. Sprawdzić obsługę START i STOP przy odłączonym lub wyłączonym HMI oraz przerwanej komunikacji ECU–HMI; zachować warunki rozruchu wynikające z konfiguracji ECU. Szczegółowe warunki i limity ustalić przed próbami. Nie wykonano jeszcze testów sprzętu ani firmware.
