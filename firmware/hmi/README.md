# Oprogramowanie HMI

Miejsce na kod prezentacji danych, obsługi kierowcy, komunikacji CAN, diagnostyki i aktualizacji HMI.

Stan: brak implementacji. Platforma i technologia interfejsu pozostają do ustalenia. Personalizacja ekranu z aplikacji Windows jest wymaganiem; jej zakres wymaga doprecyzowania.

Po wykryciu obrotów przedniego koła ECU wybudza również HMI (SYS-080). Naliczanie ODO w ECU nie czeka na gotowość HMI i działa przy jego awarii. Sposób przekazania wybudzenia i czasy reakcji są otwarte. Weryfikacja obejmie wybudzenie obu urządzeń i odrębne próby ODO z opóźnionym oraz niedostępnym HMI: [ADR-003](../../docs/decisions/adr-003-wybudzanie-bez-wlacznika.md).

SYS-086: przy próbie włączenia odbiornika objętego aktywnym odcięciem oszczędzania, przy zgaszonym silniku HMI wyświetla odmowę i informację „Wymagane uruchomienie silnika”. Źródłem decyzji jest ECU (SYS-085); panel nie znosi blokady lokalną zmianą stanu. Gdy silnik już pracuje, a warunek napięcia/czasu z SYS-087 nadal nie jest spełniony, HMI powinno przedstawiać aktualny powód dalszej blokady. Proponowany opis: „Oczekiwanie na stabilne zasilanie”. Aktualność statusów, kodowanie przyczyny i dokładny opis tego stanu wymagają specyfikacji: [analiza i plan prób](../../docs/architecture/oszczedzanie-energii.md).

HMI wyświetla przyczynę odrzucenia zmiany zestawu map otrzymaną z ECU po usterce wymagającej pracy awaryjnej lub zatrzymania silnika (SYS-135 i SYS-137). Szczegóły scenariusza i próby zawiera [specyfikacja F02](../../docs/interfaces/mapy-i-konfiguracja.md).

Gdy ECU zgłasza aktywny stan przegrzania według SYS-189, HMI ostrzega kierowcę. Układ i pierwszeństwo komunikatu określimy w wymaganiach HMI.

Gdy ECU zgłasza potwierdzone przeciążenie skutkujące odłączeniem wentylatora, HMI ostrzega o usterce jego obwodu według SYS-190. Wygaszenie ostrzeżenia podlega SYS-023.

HMI udostępnia osobne potwierdzenie zakończenia czynności przy wentylatorze, które zleca próbę w ECU. HMI informuje o nieudanej próbie według SYS-192 i przedstawia aktywną usterkę przekazaną z ECU po wybudzeniu według SYS-193.

Gdy ECU zgłasza niedostępność wykrywania przewrócenia, HMI ostrzega kierowcę także przy zgaszonym silniku oraz po zwolnieniu blokady po upadku (SYS-198–200). Po potwierdzonym ustąpieniu usterki HMI wygasza ostrzeżenie według SYS-023 i SYS-201.

Przy odłożonym przełączeniu zestawu w czasie jazdy HMI pokazuje oczekiwanie i wskazuje faktycznie aktywny zestaw według stanu otrzymanego z ECU (SYS-143).

Po otrzymaniu statusu wygaśnięcia żądania HMI informuje kierowcę o konieczności ponownego wyboru zestawu (SYS-144).

Po zastąpieniu oczekującego żądania HMI wskazuje aktualny oczekujący zestaw według statusu ECU (SYS-145).

Po potwierdzeniu przez ECU HMI informuje o anulowaniu zmiany i pokazuje aktywny zestaw (SYS-146).

HMI aktualizuje status oczekującego wyboru na podstawie informacji z ECU o anulowaniu przy wymuszeniu „Standard” po usterce (SYS-147).

Po odzyskaniu łączności HMI odczytuje z ECU aktywny zestaw i bieżący stan oczekiwania na przełączenie (SYS-148).

Na postoju przy zgaszonym silniku HMI przekazuje wybór do zasilanego ECU i pokazuje faktycznie zastosowany zestaw (SYS-149).

Po restarcie ECU HMI odczytuje faktycznie aktywny zestaw i bieżący stan oczekiwania z ECU (SYS-150).

Po ponownym wyborze tego samego oczekującego zestawu HMI nadal pokazuje oczekiwanie według danych ECU. Termin wygaśnięcia pozostaje pierwotny (SYS-151).

Do specyfikacji HMI: dla SYS-208 panel przedstawia zgłoszoną przez ECU usterkę IAT i rozróżnia wartość mierzoną od zastępczej według udostępnionego statusu. Wymuszenie „Standard” i odmowa zmiany zestawu podlegają SYS-137. Sposób prezentacji ustalimy we właściwym pakiecie; HMI nie wyznacza oszacowania IAT. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-208).

Po powrocie na rzeczywisty IAT według SYS-209 HMI aktualizuje źródło temperatury oraz bieżące ostrzeżenie według statusu ECU i SYS-023. Historia usterki pozostaje zachowana. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-209).

Do specyfikacji HMI: przy SYS-210 panel prezentuje otrzymaną z ECU usterkę barometru i stan użycia stałej wartości zastępczej. Odmowa zmiany zestawu podlega SYS-137. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-210).

Po powrocie do pomiaru barometru według SYS-211 HMI aktualizuje źródło ciśnienia i bieżące ostrzeżenie według statusu ECU oraz SYS-023. Historia pozostaje zachowana. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-211).

Do specyfikacji HMI: dla SYS-212 rozróżnić brak wiarygodnego pomiaru temperatury płynu i dane zastępcze używane przez ECU do dawkowania. Prezentacja wynika ze statusu ECU; układ ekranu ustalimy we właściwym pakiecie. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-212).

Po odzyskaniu ECT według SYS-213 HMI aktualizuje źródło temperatury i bieżące ostrzeżenie zgodnie ze statusem ECU i SYS-023. Historia pozostaje zachowana. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-213).

Do specyfikacji HMI: SYS-214 wymaga informacji o niedostępnym pomiarze ciśnienia paliwa i stanie strategii zastępczej według danych ECU. Dane zastępcze pozostają odróżnialne od pomiaru. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-214).

Dla SYS-215 HMI odróżnia dane nominalne używane przez ECU od wiarygodnego pomiaru ciśnienia, zgodnie z otrzymanym statusem. Sposób prezentacji ustalimy we właściwym pakiecie. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-215).

Po zakończeniu strategii zastępczej według SYS-216 HMI aktualizuje źródło ciśnienia paliwa, stan strategii i bieżące ostrzeżenie według statusu ECU. Historia DTC pozostaje zachowana. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-216).

Do specyfikacji HMI: SYS-217 wymaga ostrzeżenia o rzeczywistym niedoborze ciśnienia paliwa i przedstawienia przyczyny blokady uruchomienia według statusu ECU. Panel nie zwalnia blokady lokalną zmianą danych. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-217).

Dla SYS-218 HMI przedstawia stan przygotowania ciśnienia i powód utrzymanej blokady według ECU. Ograniczona próba START/kopniakiem działa niezależnie od HMI; jego wybudzenie samo nie inicjuje pompy przy stanie po SYS-217. [Plan próby](../../docs/requirements/f03-ochrona-i-usterki.md#plan-próby-sys-218).
