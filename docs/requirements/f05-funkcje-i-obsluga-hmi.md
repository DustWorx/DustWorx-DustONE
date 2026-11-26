# F05 — funkcje i obsługa HMI

Stan na 2026-11-26. **Pakiet aktywny**, rozpoczęty po zatwierdzeniu [karty F04](f04-przeglad-zakresu.md) w odpowiedzi na pytanie 271. Przyjęto SYS-263 na podstawie własnej odpowiedzi właściciela na pytanie 272: kontrolka i animowany pasek z krótkim opisem. Następna decyzja 273 dotyczy zachowania paska przy nadal aktywnej usterce.

Źródłem wymagań pozostaje [rejestr SYS](../01-zakres-systemu.md); kolejność i bramki określa [proces](../00-proces-i-status.md). Dokument zbiera podstawy, decyzje i plany F05. Przyjęcie zakresu nie potwierdza działania produktu.

## Przyjęte podstawy

| Obszar | Obowiązujące ustalenie | Podstawa |
| --- | --- | --- |
| Role | HMI jest interfejsem użytkownika; ECU wykonuje sterowanie, kwalifikuje żądania i udostępnia rzeczywiste stany. Silnik działa niezależnie od HMI/CAN. | SYS-046/047 |
| Przyciski | Fizyczne przyciski HMI, bez dotyku. Obsługa akcesoriów przez HMI; START i STOP mają własne połączenia niezależne od panelu. | SYS-016/017/037/048 |
| Główny panel | HMI zastępuje licznik: prędkość, przebieg, dane silnika i stan motocykla. Zakres bieżących ekranów do domknięcia w F05. | SYS-018 |
| Liczniki | Całkowite motogodziny i ODO są prowadzone w ECU i odczytywane przez HMI; użytkownik nie może ich korygować ani kasować. ODO nalicza także przy zgaszonym silniku według obrotów przedniego koła. | SYS-074–080 |
| Opcjonalne wskazania | Przewidziano czujnik poszczególnych biegów i sygnał sprzęgła; nie są wymagane do pracy ECU i nie służą blokadom rozrusznika. Prezentację oraz niedostępność danych rozwijamy w F05; interfejs czujnika w dalszych etapach. | SYS-041 |
| Zestawy map | Maksymalnie trzy zestawy wybierane z HMI. Wykonanie, oczekiwanie, odmowy i powrót do „Standard” według zamkniętego F02. | SYS-028, F02 |
| Własne ekrany | Układ wskaźników i pól danych, kolory, czcionki, grafiki oraz gotowe szablony. Granice personalizacji do ustalenia w F05; narzędzie Windows w F06. | SYS-008 |
| Ostrzeżenia | HMI prezentuje usterki i powody odmowy zgodnie z F02–F04. Ostrzeżenie o DTC wygasa po potwierdzonym ustąpieniu według kryteriów danego DTC; historia nie jest przez to kasowana. | SYS-022/023, F02–F04 |
| Sen i wybudzanie | ECU koordynuje sen obu urządzeń; HMI nie usypia samodzielnie. W zwykłym śnie zasilanie HMI pozostaje włączone. Zachowane źródła wybudzania: START, kopniak, przyciski HMI, PC, przednie koło i nowe użycie hamulca. | SYS-054–066/079/080/256 |
| Stany odbiorników | Panel odczytuje stany ECU. Dawne żądanie, powrót komunikacji ani samo wybudzenie nie zastępują wymaganego nowego użycia. Klakson wybudzający wymaga zwolnienia i kolejnego naciśnięcia. | F04, SYS-239/262 |

Szczegóły reakcji silnika i odbiorników pozostają w [F02](f02-przeglad-zakresu.md), [F03](f03-przeglad-zakresu.md) i [F04](f04-przeglad-zakresu.md). F05 określa sposób obsługi i prezentacji tych stanów.

## Kolejność pracy

| Kolejność | Temat | Status / wynik do uzgodnienia |
| --- | --- | --- |
| 1 | Ważne ostrzeżenia | Aktywny temat. Przyjęto formę prezentacji SYS-263. Kolejna decyzja 273: chowanie paska; potem priorytety i obsługa kilku ostrzeżeń. |
| 2 | Dane i ekrany | W kolejce: wymagane dane, ekrany jazdy/postoju i dane opcjonalne. |
| 3 | Przyciski i menu | W kolejce: nawigacja, wybór map i obsługa akcesoriów według reguł ECU. |
| 4 | Personalizacja | W kolejce: elementy obowiązkowe, granice własnych ekranów i szablonów. |
| 5 | Stany panelu | W kolejce: uruchamianie, brak lub nieaktualność danych, utrata/powrót CAN i prezentacja przed snem. |
| 6 | Przegląd F05 | W kolejce: kontrola spójności, plany weryfikacji, przekazanie i akceptacja karty przez właściciela. |

Nie rozpoczynamy F06–F08 przed zamknięciem F05. Temat późniejszego pakietu zapisujemy w jego kolejce, gdy wynika z bieżącej decyzji.

## Kontrolka i animowany pasek ostrzeżenia

**Przyjęto 2026-11-26, pytanie 272, własna odpowiedź właściciela — SYS-263.** HMI pokazuje kontrolkę oraz animowany pasek wysuwający się z góry albo dołu ekranu, z krótkim opisem tego, co jest nie tak. Dotyczy to także własnych ekranów użytkownika.

Źródło: „kontrolka na ekranie oraz pasek animowany wyjezdzajacy z dołu lub góry który krótkim opisem mówi co jest nie tak”. Nie wybrano jeszcze konkretnej krawędzi, koloru, ikony, czasu ani parametrów animacji. Wygaszanie ostrzeżenia o DTC po potwierdzonym ustąpieniu usterki pozostaje według SYS-023; historia w ECU podlega SYS-022. Chowanie samego paska nie jest potwierdzeniem naprawy ani poleceniem kasowania DTC.

### Plan próby SYS-263

Status: **plan do rozwinięcia, bez wyników produktu**. Blok: HMI-UI; grupa: V08. Powiązania: SYS-008/018/022/023 oraz ostrzeżenia przyjęte w F03.

1. Na stanowisku ECU–HMI lub z kontrolowanym źródłem stanów ECU zgłosić przykładowe ważne ostrzeżenie, np. przegrzanie albo usterkę wentylatora. Zapisać wejściowy stan/identyfikator ostrzeżenia i rewizje urządzeń.
2. Na każdym uzgodnionym ekranie gotowym i własnym potwierdzić kontrolkę oraz wysunięcie paska z wybranej w projekcie górnej albo dolnej krawędzi. Krótki opis ma odpowiadać zgłoszonemu problemowi.
3. Sprawdzić szablony i własne układy z dużą liczbą pól, grafik i różnymi dopuszczonymi ustawieniami. Treść ekranu nie może zasłonić kontrolki ani prezentowanego paska. Nawigacja nie może pozbawić kolejnego ekranu wymaganej prezentacji ostrzeżenia.
4. Zarejestrować obraz i czasy prezentacji; ocenić czytelność na docelowym HMI. Kryteria liczbowe, parametry animacji oraz scenariusze chowania, potwierdzania i wielu ostrzeżeń uzupełnić po ich uzgodnieniu. Nie uznawać tych otwartych przypadków za zaliczone.

Przed wykonaniem: zamknąć właściwe reguły F05, wybrać wspólnie ekran i platformę, opracować format danych, mierzalne kryteria oraz procedurę stanowiskową. Plan prezentacji nie wymaga wywoływania rzeczywistego przegrzania silnika.

## Następna decyzja — pytanie 273

**Propozycja, bez decyzji właściciela.** Usterka nadal jest aktywna, HMI pokazało kontrolkę i opis na pasku. Czy pasek powinien sam się schować, czy czekać na potwierdzenie kierowcy?

- **A:** pasek pozostaje do potwierdzenia przyciskiem.
- **B — rekomendowana:** pasek chowa się po ustalonym czasie; wartość dobierzemy później.

W obu propozycjach kontrolka pozostaje przy aktywnej usterce. Potwierdzenie oznacza przeczytanie komunikatu, bez kasowania DTC lub zmiany reakcji ECU. B ogranicza obsługę przycisków w enduro i czas zajmowania ekranu; A daje kierowcy czas na przeczytanie kosztem potrzeby potwierdzenia. Priorytety ostrzeżeń i wyjątki dla szczególnie ważnych komunikatów rozstrzygniemy następnie w tym samym temacie.

## Weryfikacja i przekazanie

Po przyjęciu każdej nowej reguły dopisujemy identyfikator SYS, źródło decyzji, przypisanie do bloku/grupy weryfikacji oraz plan próby lub przeglądu. F05 obejmuje obecnie jedno nowe wymaganie SYS-263 i jeden plan próby; wcześniejsze wymagania i ich weryfikacja pozostają zachowane. Właściciel wykona przygotowane próby na odpowiednim etapie produktu, a asystent opracuje procedury i przeanalizuje wyniki.

| Miejsce dalszej pracy | Co należy tam rozwinąć |
| --- | --- |
| Etap 4 — architektura | Rozdzielczość, czytelność, zasoby grafiki/pamięci, czasy gotowości i reakcji, ważność danych i protokół. Parametry wynikają z przyjętych funkcji i danych osprzętu. |
| Etap 5 — procedury | Mierzalne kryteria prezentacji, obsługa w rękawicach i warunkach enduro, stany jednoczesne, utrata/odzyskanie danych i powiązanie z zachowaniem ECU. |
| Etapy 6–8 — sprzęt i PCB | Wspólny wybór ważnych komponentów HMI; schematy, zasilanie, przyciski, obudowa, warstwy i layout do wykonania CAD przez właściciela w Fusion z przeglądami asystenta. |
| F06/F07 | Edytor i przesyłanie ekranów w Windows, operacje serwisowe, katalog diagnostyki oraz aktualizacje. Rozwijamy w ich kolejności. |

Zamknięcie wymaga przyjęcia powyższego zakresu, kontroli powiązań z F01–F04, planów weryfikacji i wyraźnej akceptacji karty F05 przez właściciela. Etap 2 i G0 pozostają otwarte.
