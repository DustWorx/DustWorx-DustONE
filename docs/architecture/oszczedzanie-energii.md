# Oszczędzanie energii po zgaszeniu silnika

Data: 2026-11-01. Podstawa: odpowiedzi właściciela na pytanie 87 oraz A na pytania 88 i 89, [SYS-083–087](../01-zakres-systemu.md), [ADR-009](../decisions/adr-009-oszczedzanie-energii.md). Zakres funkcjonalny wskazany przez właściciela; parametry i reguły szczegółowe do projektu.

## Przyjęty zakres

- Po potwierdzonym zatrzymaniu silnika włączone mijania/drogowe przechodzą w przednie i tylne pozycyjne. Przy zgaszonym silniku można ponownie włączyć mijania/drogowe z HMI.
- ECU nadzoruje napięcie podczas pracy. Przy zgaszonym silniku, jeszcze przed snem, niskie napięcie uruchamia oszczędzanie i wyłącza pozycyjne oraz zbędne odbiorniki załączone z HMI. Wykaz odbiorników wymaga uzgodnienia.
- Podczas aktywnego odcięcia ECU odrzuca zwykłe żądania ponownego załączenia objętych nim odbiorników. Przy próbie z HMI przy zgaszonym silniku panel informuje: „Wymagane uruchomienie silnika” (SYS-085/086, odpowiedź A na pytanie 88). Kontrola działa w ECU także dla bezpośrednich zwykłych poleceń; restart HMI nie znosi blokady.
- W normalnym użytkowaniu wyjście wymaga jednocześnie potwierdzonej pracy silnika i napięcia powyżej progu powrotu przez ustalony czas (SYS-087, odpowiedź A na pytanie 89). Do tego momentu odcięcie obejmuje również automatyczne żądania załączenia objętych nim odbiorników. Wartości parametrów pozostają otwarte.
- Nadal obowiązują: automatyczne pozycyjne po uruchomieniu z uwzględnieniem aktywnego odcięcia (SYS-082/087), wyłączenie oświetlenia przed prawidłowym snem (SYS-081) oraz niezależność ECU od HMI. To osobny stan pracy przed snem, nie zastępstwo koordynowanego usypiania.

## Rekomendacje i decyzje otwarte

1. Potwierdzać spadek przez ustalony czas i zastosować histerezę. Wzrost napięcia po odłączeniu obciążeń nie powinien wywoływać cyklicznego przywracania i odcinania. [Analog Devices](https://www.analog.com/en/resources/analog-dialogue/articles/adding-hysteresis-for-smooth-undervoltage-and-overvoltage-lockout.html) opisuje tę zależność; nie oznacza to wyboru układu ani wartości.
2. Progi dobrać do akumulatora, obciążeń i potrzeb rozruchu oraz potwierdzić pomiarowo. [Yuasa](https://www.yuasabatteries.com/about/events-news/news/new-battery-when-to-replace/) rozróżnia napięcie spoczynkowe, zachowanie pod obciążeniem i typ akumulatora. Nie przyjęto uniwersalnego progu dla wszystkich chemii.
3. Zwykłe ręczne włączenie po zgaszeniu poza oszczędzaniem pozostaje wymaganiem SYS-083. HMI powinno odróżnić odmowę przy zgaszonym silniku („Wymagane uruchomienie silnika”) od trwającej blokady po jego uruchomieniu; proponowany wtedy opis to „Oczekiwanie na stabilne zasilanie”. Dokładny komunikat tej drugiej sytuacji jest propozycją interfejsu, a stan i powód pochodzą z ECU. W aktywnym odcięciu działa SYS-085/086. Określić status i powód odmowy przekazywany do HMI oraz jego aktualność po przywróceniu CAN. Komunikat o uruchomieniu silnika nie jest automatyczną zgodą na odblokowanie po samym naciśnięciu START.
4. Wyjście w normalnym użytkowaniu określa SYS-087. Ustalić wartości progu i czasu, szczegóły kwalifikacji i obsługę zapamiętanych żądań po zwolnieniu odcięcia. Zasady zasilania warsztatowego i testów pozostają do określenia. Sam wzrost napięcia przy zgaszonym silniku ani sama praca silnika bez spełnienia warunku napięcia nie zwalniają odcięcia w normalnym użytkowaniu.
5. Określić listę odbiorników i priorytety: ochrona nie może przypadkowo odłączyć funkcji wymaganych do działania ECU, STOP, rozruchu, komunikacji i trwałego zapisu danych. Wentylator ma własne ograniczenia SYS-060/061; powiązać je z nową polityką. Dla PC uwzględnić zasilanie serwisowe SYS-058, blokadę snu SYS-057 i bezpieczne ukończenie lub przerwanie aktualizacji. Sposób prezentacji, ewentualna diagnostyka i postępowanie przy błędzie pomiaru są otwarte.

Tryb oszczędzania odbiorników i minimalne napięcie poprawnej pracy elektroniki wymagają osobnej analizy. Zdolność wykrywania ruchu koła oraz wybudzania przy małym poborze należy powiązać z budżetem energii; nie przyjęto odłączenia akumulatora ani automatycznego odcięcia zasilania HMI w tym trybie.

## Plan prób do uszczegółowienia

| Obszar | Oczekiwane potwierdzenie |
| --- | --- |
| Zatrzymanie silnika | Z uprzednio włączonych mijania lub drogowych przejście na oba pozycyjne; ponowne ręczne włączenie z HMI poza oszczędzaniem. |
| Spadek napięcia | Wejście przed snem i wyłączenie ustalonych odbiorników także bez sprawnego HMI; granice czasu i napięcia do ustalenia. |
| Powrót i zakłócenia | Powolne przejście przez próg, krótkie zapady i odbicie po odciążeniu: zachowanie według przyjętych reguł, bez niekontrolowanego przełączania. |
| Blokada i HMI | Próby ON z HMI, bezpośrednich standardowych interfejsów i ponawiane polecenia: wyjście pozostaje odłączone. Przy zgaszonym silniku HMI pokazuje odmowę i wymagane uruchomienie silnika. Powtórzyć po restarcie HMI i odtworzeniu CAN, gdy oszczędzanie w ECU nadal jest aktywne. |
| Wyjście w normalnym użytkowaniu | Sprawdzić osobno: wzrost napięcia bez pracy silnika, pracę silnika bez wymaganego napięcia oraz zbyt krótkie spełnienie warunku. Odcięcie pozostaje aktywne; zwolnienie następuje dopiero po spełnieniu obu warunków przez ustalony czas. Uwzględnić przerwanie warunku napięcia lub pracy silnika przed końcem kwalifikacji. |
| Priorytety i ponowne załączenia | Potwierdzić, że automatyka pozycyjnych nie omija aktywnego odcięcia. Rozruch, wentylator, PC/aktualizacja, zapis danych, sen i przywracanie ręcznych stanów po zwolnieniu według dalszej specyfikacji. |
| Pomiar i energia | Dokładność, uszkodzenia toru, prąd odbiorników oraz pobór ECU/HMI w stanach docelowych. |

Stanowiska, konkretne połączenia, limity i dowody zostaną przygotowane przed próbami. To plan, nie wykonane testy ani potwierdzenie ochrony akumulatora.
