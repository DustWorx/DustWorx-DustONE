# F05 — funkcje i obsługa HMI

Stan na 2026-11-26. **Pakiet aktywny**, rozpoczęty po zatwierdzeniu [karty F04](f04-przeglad-zakresu.md) w odpowiedzi na pytanie 271. Nowe ustalenia F05 nie zostały jeszcze przyjęte. Pierwsza propozycja: pytanie 272.

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
| 1 | Ważne ostrzeżenia | Aktywny temat: sposób prezentacji na każdym ekranie, priorytety i obsługa kilku ostrzeżeń. Pierwsza decyzja 272. |
| 2 | Dane i ekrany | W kolejce: wymagane dane, ekrany jazdy/postoju i dane opcjonalne. |
| 3 | Przyciski i menu | W kolejce: nawigacja, wybór map i obsługa akcesoriów według reguł ECU. |
| 4 | Personalizacja | W kolejce: elementy obowiązkowe, granice własnych ekranów i szablonów. |
| 5 | Stany panelu | W kolejce: uruchamianie, brak lub nieaktualność danych, utrata/powrót CAN i prezentacja przed snem. |
| 6 | Przegląd F05 | W kolejce: kontrola spójności, plany weryfikacji, przekazanie i akceptacja karty przez właściciela. |

Nie rozpoczynamy F06–F08 przed zamknięciem F05. Temat późniejszego pakietu zapisujemy w jego kolejce, gdy wynika z bieżącej decyzji.

## Pierwsza decyzja — pytanie 272

**Propozycja, bez decyzji właściciela.** ECU zgłasza ważne ostrzeżenie, np. przegrzanie lub usterkę wentylatora. Kierowca może w tym czasie używać własnego ekranu HMI. Jak przedstawić problem na każdym ekranie, także niestandardowym?

- **A — rekomendowana:** widoczny krótki tekst opisujący problem; własny układ nie może go usunąć ani ukryć. Szczegóły po otwarciu listy ostrzeżeń.
- **B:** widoczny symbol ostrzeżenia; pełny opis dopiero po otwarciu listy.

A przekazuje przyczynę bez dodatkowej obsługi. B zajmuje mniej miejsca, ale wymaga otwarcia opisu. Oba warianty zachowują ostrzeganie wymagane w F03. Czas prezentacji, potwierdzanie, priorytety i przypadki wielu ostrzeżeń rozstrzygniemy kolejno w tym temacie. Nie wybrano jeszcze układu graficznego ani komponentu wyświetlacza.

## Weryfikacja i przekazanie

Po przyjęciu każdej nowej reguły dopisujemy identyfikator SYS, źródło decyzji, przypisanie do bloku/grupy weryfikacji oraz plan próby lub przeglądu. F05 nie ma jeszcze nowych wymagań ani nowych planów; wcześniejsze wymagania i ich weryfikacja pozostają zachowane. Właściciel wykona przygotowane próby na odpowiednim etapie produktu, a asystent opracuje procedury i przeanalizuje wyniki.

| Miejsce dalszej pracy | Co należy tam rozwinąć |
| --- | --- |
| Etap 4 — architektura | Rozdzielczość, czytelność, zasoby grafiki/pamięci, czasy gotowości i reakcji, ważność danych i protokół. Parametry wynikają z przyjętych funkcji i danych osprzętu. |
| Etap 5 — procedury | Mierzalne kryteria prezentacji, obsługa w rękawicach i warunkach enduro, stany jednoczesne, utrata/odzyskanie danych i powiązanie z zachowaniem ECU. |
| Etapy 6–8 — sprzęt i PCB | Wspólny wybór ważnych komponentów HMI; schematy, zasilanie, przyciski, obudowa, warstwy i layout do wykonania CAD przez właściciela w Fusion z przeglądami asystenta. |
| F06/F07 | Edytor i przesyłanie ekranów w Windows, operacje serwisowe, katalog diagnostyki oraz aktualizacje. Rozwijamy w ich kolejności. |

Zamknięcie wymaga przyjęcia powyższego zakresu, kontroli powiązań z F01–F04, planów weryfikacji i wyraźnej akceptacji karty F05 przez właściciela. Etap 2 i G0 pozostają otwarte.
