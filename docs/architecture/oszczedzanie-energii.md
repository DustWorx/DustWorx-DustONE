# Oszczędzanie energii po zgaszeniu silnika

Data opracowania: 2026-11-01. Aktualizacja: 2026-11-03. Podstawa: odpowiedzi właściciela na pytania 87 i 90, A na pytania 88, 89 i 91 oraz B na pytanie 92, [SYS-083–091](../01-zakres-systemu.md), [ADR-009](../decisions/adr-009-oszczedzanie-energii.md). Zakres funkcjonalny wskazany przez właściciela; parametry i reguły szczegółowe do projektu.

## Przyjęty zakres

- Po potwierdzonym zatrzymaniu silnika włączone mijania/drogowe przechodzą w przednie i tylne pozycyjne. Przy zgaszonym silniku można ponownie włączyć mijania/drogowe z HMI.
- ECU nadzoruje napięcie podczas pracy. Przy zgaszonym silniku, jeszcze przed snem, niskie napięcie uruchamia oszczędzanie i wyłącza pozycyjne oraz zbędne odbiorniki załączone z HMI. Wykaz odbiorników wymaga uzgodnienia.
- Podczas aktywnego odcięcia ECU odrzuca zwykłe żądania ponownego załączenia objętych nim odbiorników. Przy próbie z HMI przy zgaszonym silniku panel informuje: „Wymagane uruchomienie silnika” (SYS-085/086, odpowiedź A na pytanie 88). Kontrola działa w ECU także dla bezpośrednich zwykłych poleceń; restart HMI nie znosi blokady.
- W normalnym użytkowaniu wyjście wymaga jednocześnie potwierdzonej pracy silnika i napięcia powyżej progu powrotu przez ustalony czas (SYS-087, odpowiedź A na pytanie 89). Do tego momentu odcięcie obejmuje również automatyczne żądania załączenia objętych nim odbiorników. Wartości parametrów pozostają otwarte.
- Po zwolnieniu odcięcia mijania/drogowe i dodatkowe odbiorniki użytkownika czekają na nowe polecenie HMI (SYS-088). Pozycyjne wracają według automatyki. Funkcje ochrony silnika, w tym wentylator, kierują się aktualnym zapotrzebowaniem i własnymi zabezpieczeniami (SYS-089, odpowiedź właściciela na pytanie 90). Poprzednie ręczne wymuszenie wentylatora nie wraca automatycznie.
- Jawnie włączony tryb serwisowy pozwala zwolnić odcięcie bez pracy silnika przy potwierdzonym stabilnym zasilaniu warsztatowym (SYS-090, odpowiedź A na pytanie 91). Sam kabel PC nie wystarcza, a zabezpieczenia wyjść pozostają aktywne. Zwolnienie odcięcia dopuszcza wykonanie testów; samo nie załącza wyjść.
- Nadal obowiązują: automatyczne pozycyjne po uruchomieniu z uwzględnieniem aktywnego odcięcia (SYS-082/087), wyłączenie oświetlenia przed prawidłowym snem (SYS-081) oraz niezależność ECU od HMI. To osobny stan pracy przed snem, nie zastępstwo koordynowanego usypiania.

Dane motocykla testowego: [referencja akumulatora — AGM 12 V, 4 Ah](../interfaces/beta-2015-analiza-dokumentacji.md#akumulator), na podstawie odpowiedzi właściciela na pytania 93/94 i dokumentacji katalogowej. To punkt wyjścia do pierwszej analizy i prób; zakres obsługiwanych typów akumulatorów dla całej platformy pozostaje otwarty. Progi odcięcia i powrotu nie są jeszcze dobrane. [Porównanie AGM i LiFePO4](akumulatory-agm-lifepo4-porownanie.md) przygotowano na życzenie właściciela w odpowiedzi C na pytanie 95; zakres obsługiwanych typów pozostaje do wyboru.

## Rekomendacje i decyzje otwarte

1. Potwierdzać spadek przez ustalony czas i zastosować histerezę. Wzrost napięcia po odłączeniu obciążeń nie powinien wywoływać cyklicznego przywracania i odcinania. [Analog Devices](https://www.analog.com/en/resources/analog-dialogue/articles/adding-hysteresis-for-smooth-undervoltage-and-overvoltage-lockout.html) opisuje tę zależność; nie oznacza to wyboru układu ani wartości.
2. Progi dobrać do akumulatora, obciążeń i potrzeb rozruchu oraz potwierdzić pomiarowo. [Yuasa](https://www.yuasabatteries.com/about/events-news/news/new-battery-when-to-replace/) rozróżnia napięcie spoczynkowe, zachowanie pod obciążeniem i typ akumulatora. Nie przyjęto uniwersalnego progu dla wszystkich chemii.
3. Zwykłe ręczne włączenie po zgaszeniu poza oszczędzaniem pozostaje wymaganiem SYS-083. HMI powinno odróżnić odmowę przy zgaszonym silniku („Wymagane uruchomienie silnika”) od trwającej blokady po jego uruchomieniu; proponowany wtedy opis to „Oczekiwanie na stabilne zasilanie”. Dokładny komunikat tej drugiej sytuacji jest propozycją interfejsu, a stan i powód pochodzą z ECU. W aktywnym odcięciu działa SYS-085/086. Określić status i powód odmowy przekazywany do HMI oraz jego aktualność po przywróceniu CAN. Komunikat o uruchomieniu silnika nie jest automatyczną zgodą na odblokowanie po samym naciśnięciu START.
4. Wyjście w normalnym użytkowaniu określa SYS-087. Ustalić wartości progu i czasu oraz szczegóły kwalifikacji. Powrót ręcznych odbiorników i automatyki określają SYS-088/089; odrzucone lub dawne żądanie ON nie zastępuje nowego polecenia użytkownika dla odbiornika ręcznego. Zakres wyjątku serwisowego określa SYS-090; jego kwalifikacja, uprawnienia, przerwanie i powrót do zwykłego sterowania wymagają specyfikacji. Sam wzrost napięcia przy zgaszonym silniku ani sama praca silnika bez spełnienia warunku napięcia nie zwalniają odcięcia w normalnym użytkowaniu.
5. Określić listę odbiorników i priorytety: ochrona nie może przypadkowo odłączyć funkcji wymaganych do działania ECU, STOP, rozruchu, komunikacji i trwałego zapisu danych. Wentylator ma własne ograniczenia SYS-060/061; powiązać je z nową polityką. Dla PC uwzględnić zasilanie serwisowe SYS-058, blokadę snu SYS-057 i bezpieczne ukończenie lub przerwanie aktualizacji. Sposób prezentacji, ewentualna diagnostyka i postępowanie przy błędzie pomiaru są otwarte.

Tryb oszczędzania odbiorników i minimalne napięcie poprawnej pracy elektroniki wymagają osobnej analizy. Zdolność wykrywania ruchu koła oraz wybudzania przy małym poborze należy powiązać z budżetem energii; nie przyjęto odłączenia akumulatora ani automatycznego odcięcia zasilania HMI w tym trybie.

## Tryb serwisowy — szczegóły do projektu

Określić jawne wejście z aplikacji Windows i potwierdzenie przez ECU, sposób potwierdzenia źródła/wydajności zasilania oraz próg i czas kwalifikacji napięcia. Rozdzielić blokadę snu przy PC (SYS-057) od zezwolenia na testy: obecność połączenia nie jest zezwoleniem. Zaprojektować odrębne polecenie wykonania testu, statusy i właściwe warunki przerwania przy spadku napięcia, STOP, rozruchu lub pracy silnika. Utratę sesji obsłużyć według SYS-091: bez nowych testów, rozpoczęty do wcześniej ustalonego limitu przy nadal spełnionych warunkach. Dokładne reakcje poszczególnych wyjść i czasy pozostają do uzgodnienia.

Wyjątek dotyczy warunku pracy silnika przy zwalnianiu odcięcia do testów, przy zachowaniu zabezpieczeń wyjść. Nie przyznaje sam w sobie uprawnień do inicjalizacji/przenoszenia chronionych liczników ani dowolnego programowania firmware; obowiązują odrębne zasady SYS-076–078. Sterowanie testami i rozstrzyganie warunków muszą być po stronie ECU, także wobec bezpośrednich poleceń.

## Utrata sesji podczas testu

Właściciel wybrał w pytaniu 92 wariant B (SYS-091). Po potwierdzeniu utraty sesji ECU blokuje nowe testy. Rozpoczęty test może zakończyć się w swoim normalnym przebiegu, najpóźniej z wcześniej ustalonym limitem, o ile nie zadziała zabezpieczenie lub inny właściwy warunek przerwania. Następnie wyjątek serwisowy jest wycofywany i stosuje się normalne sterowanie, z uwzględnieniem automatyki ochrony silnika.

Limit musi być nadzorowany lokalnie w ECU i przyjęty przed startem. Utrata lub ponowne nawiązanie połączenia nie rozpoczyna go od nowa; ponowienie lub zakolejkowanie polecenia nie może tworzyć nowego testu w fazie dokańczania. Sam powrót połączenia nie zastępuje jawnego wejścia w tryb według SYS-090. Dopuszczenie nowego testu i kwalifikacja sesji wymagają specyfikacji.

Konsekwencja dla projektu: brak aktywnego testu nie uzasadnia podtrzymania wyjątku po potwierdzonej utracie sesji. Sposób rozpoznania sesji i jej utraty, obsługę polecenia przerwania, stany końcowe kanałów oraz arbitraż z automatyką określić przed implementacją. Zasada dotyczy testów wyjść; aktualizacja firmware ma odrębny przebieg i procedurę odzyskiwania.

## Plan prób do uszczegółowienia

| Obszar | Oczekiwane potwierdzenie |
| --- | --- |
| Zatrzymanie silnika | Z uprzednio włączonych mijania lub drogowych przejście na oba pozycyjne; ponowne ręczne włączenie z HMI poza oszczędzaniem. |
| Spadek napięcia | Wejście przed snem i wyłączenie ustalonych odbiorników także bez sprawnego HMI; granice czasu i napięcia do ustalenia. |
| Powrót i zakłócenia | Powolne przejście przez próg, krótkie zapady i odbicie po odciążeniu: zachowanie według przyjętych reguł, bez niekontrolowanego przełączania. |
| Blokada i HMI | Próby ON z HMI, bezpośrednich standardowych interfejsów i ponawiane polecenia: wyjście pozostaje odłączone. Przy zgaszonym silniku HMI pokazuje odmowę i wymagane uruchomienie silnika. Powtórzyć po restarcie HMI i odtworzeniu CAN, gdy oszczędzanie w ECU nadal jest aktywne. |
| Wyjście w normalnym użytkowaniu | Sprawdzić osobno: wzrost napięcia bez pracy silnika, pracę silnika bez wymaganego napięcia oraz zbyt krótkie spełnienie warunku. Odcięcie pozostaje aktywne; zwolnienie następuje dopiero po spełnieniu obu warunków przez ustalony czas. Uwzględnić przerwanie warunku napięcia lub pracy silnika przed końcem kwalifikacji. |
| Powrót odbiorników użytkownika | Mijania/drogowe i dodatkowy odbiornik uprzednio włączone z HMI pozostają wyłączone po zwolnieniu odcięcia; nowe polecenie włącza je przy spełnionych pozostałych warunkach. Pozycyjne wracają według automatyki. |
| Powrót automatyki | Po wyjściu przy żądaniu chłodzenia wentylator działa bez nowego polecenia HMI; bez żądania chłodzenia nie odtwarza dawnego ręcznego ON. Po ponownym zgaszeniu sprawdzić nadal obowiązujące limity SYS-060/061. Pozostałe uzgodnione funkcje ochronne zweryfikować według ich warunków i zabezpieczeń. |
| Tryb serwisowy | Przy zgaszonym silniku porównać samo podłączenie PC z jawnym wejściem przy stabilnym zasilaniu. Bez jawnego wejścia odcięcie nie jest zwalniane; dopuszczony tryb umożliwia test po osobnym poleceniu. Nieprawidłowe zasilanie nie spełnia warunków. Potwierdzić aktywność zabezpieczeń wyjść według ich procedur. |
| Utrata sesji w teście | Przerwać sesję w różnych fazach: brak nowych testów, aktualny kończy się nie później niż z pierwotnym limitem. Sprawdzić normalne zakończenie przed limitem, osiągnięcie limitu oraz powrót normalnego sterowania i cofnięcie wyjątku. |
| Limit i nadrzędne warunki | Ponowienie poleceń i przywrócenie łączności nie przesuwają limitu ani nie uruchamiają następnego testu w fazie dokańczania. Zadziałanie zabezpieczenia przerywa test zgodnie z procedurą wyjścia, także przed limitem. Osobno ocenić brak aktywnego testu przy utracie sesji. |
| Priorytety i przejścia | Potwierdzić, że automatyka pozycyjnych nie omija aktywnego odcięcia. Szczegóły rozruchu, PC/aktualizacji, zapisów danych, snu i lista odbiorników według dalszej specyfikacji. |
| Pomiar i energia | Dokładność, uszkodzenia toru, prąd odbiorników oraz pobór ECU/HMI w stanach docelowych. |

Stanowiska, konkretne połączenia, limity i dowody zostaną przygotowane przed próbami. To plan, nie wykonane testy ani potwierdzenie ochrony akumulatora.
