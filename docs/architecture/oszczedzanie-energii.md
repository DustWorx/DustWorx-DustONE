# Oszczędzanie energii po zgaszeniu silnika

Data: 2026-11-01. Podstawa: odpowiedzi właściciela na pytanie 87 i A na pytanie 88, [SYS-083–086](../01-zakres-systemu.md), [ADR-009](../decisions/adr-009-oszczedzanie-energii.md). Zakres funkcjonalny wskazany przez właściciela; parametry i reguły szczegółowe do projektu.

## Przyjęty zakres

- Po potwierdzonym zatrzymaniu silnika włączone mijania/drogowe przechodzą w przednie i tylne pozycyjne. Przy zgaszonym silniku można ponownie włączyć mijania/drogowe z HMI.
- ECU nadzoruje napięcie podczas pracy. Przy zgaszonym silniku, jeszcze przed snem, niskie napięcie uruchamia oszczędzanie i wyłącza pozycyjne oraz zbędne odbiorniki załączone z HMI. Wykaz odbiorników wymaga uzgodnienia.
- Podczas aktywnego odcięcia ECU odrzuca zwykłe żądania ponownego załączenia objętych nim odbiorników. Przy próbie z HMI przy zgaszonym silniku panel informuje: „Wymagane uruchomienie silnika” (SYS-085/086, odpowiedź A na pytanie 88). Kontrola działa w ECU także dla bezpośrednich zwykłych poleceń; restart HMI nie znosi blokady.
- Nadal obowiązują: automatyczne pozycyjne po uruchomieniu (SYS-082), wyłączenie oświetlenia przed prawidłowym snem (SYS-081) oraz niezależność ECU od HMI. To osobny stan pracy przed snem, nie zastępstwo koordynowanego usypiania.

## Rekomendacje i decyzje otwarte

1. Potwierdzać spadek przez ustalony czas i zastosować histerezę. Wzrost napięcia po odłączeniu obciążeń nie powinien wywoływać cyklicznego przywracania i odcinania. [Analog Devices](https://www.analog.com/en/resources/analog-dialogue/articles/adding-hysteresis-for-smooth-undervoltage-and-overvoltage-lockout.html) opisuje tę zależność; nie oznacza to wyboru układu ani wartości.
2. Progi dobrać do akumulatora, obciążeń i potrzeb rozruchu oraz potwierdzić pomiarowo. [Yuasa](https://www.yuasabatteries.com/about/events-news/news/new-battery-when-to-replace/) rozróżnia napięcie spoczynkowe, zachowanie pod obciążeniem i typ akumulatora. Nie przyjęto uniwersalnego progu dla wszystkich chemii.
3. Zwykłe ręczne włączenie po zgaszeniu poza oszczędzaniem pozostaje wymaganiem SYS-083. W aktywnym odcięciu działa SYS-085/086. Określić status i powód odmowy przekazywany do HMI oraz jego aktualność po przywróceniu CAN. Komunikat o uruchomieniu silnika nie jest automatyczną zgodą na odblokowanie po samym naciśnięciu START.
4. Ustalić wyjście z trybu po wzroście napięcia, potwierdzonym ładowaniu lub ponownym uruchomieniu; określić obsługę zapamiętanych żądań. Rekomendacja: nie przywracać dużych obciążeń wyłącznie wskutek chwilowego odbicia napięcia.
5. Określić listę odbiorników i priorytety: ochrona nie może przypadkowo odłączyć funkcji wymaganych do działania ECU, STOP, rozruchu, komunikacji i trwałego zapisu danych. Wentylator ma własne ograniczenia SYS-060/061; powiązać je z nową polityką. Dla PC uwzględnić zasilanie serwisowe SYS-058, blokadę snu SYS-057 i bezpieczne ukończenie lub przerwanie aktualizacji. Sposób prezentacji, ewentualna diagnostyka i postępowanie przy błędzie pomiaru są otwarte.

Tryb oszczędzania odbiorników i minimalne napięcie poprawnej pracy elektroniki wymagają osobnej analizy. Zdolność wykrywania ruchu koła oraz wybudzania przy małym poborze należy powiązać z budżetem energii; nie przyjęto odłączenia akumulatora ani automatycznego odcięcia zasilania HMI w tym trybie.

## Plan prób do uszczegółowienia

| Obszar | Oczekiwane potwierdzenie |
| --- | --- |
| Zatrzymanie silnika | Z uprzednio włączonych mijania lub drogowych przejście na oba pozycyjne; ponowne ręczne włączenie z HMI poza oszczędzaniem. |
| Spadek napięcia | Wejście przed snem i wyłączenie ustalonych odbiorników także bez sprawnego HMI; granice czasu i napięcia do ustalenia. |
| Powrót i zakłócenia | Powolne przejście przez próg, krótkie zapady i odbicie po odciążeniu: zachowanie według przyjętych reguł, bez niekontrolowanego przełączania. |
| Blokada i HMI | Próby ON z HMI, bezpośrednich standardowych interfejsów i ponawiane polecenia: wyjście pozostaje odłączone. Przy zgaszonym silniku HMI pokazuje odmowę i wymagane uruchomienie silnika. Powtórzyć po restarcie HMI i odtworzeniu CAN, gdy oszczędzanie w ECU nadal jest aktywne. |
| Priorytety i powrót | Rozruch, wentylator, PC/aktualizacja, zapis danych i uśpienie według przyszłych reguł. Warunki wyjścia z oszczędzania oraz ponownych załączeń pozostają do specyfikacji. |
| Pomiar i energia | Dokładność, uszkodzenia toru, prąd odbiorników oraz pobór ECU/HMI w stanach docelowych. |

Stanowiska, konkretne połączenia, limity i dowody zostaną przygotowane przed próbami. To plan, nie wykonane testy ani potwierdzenie ochrony akumulatora.
