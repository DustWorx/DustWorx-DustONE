# Oszczędzanie energii po zgaszeniu silnika

Data: 2026-11-01. Podstawa: odpowiedź właściciela na pytanie 87, [SYS-083/084](../01-zakres-systemu.md), [ADR-009](../decisions/adr-009-oszczedzanie-energii.md). Zakres funkcjonalny wskazany przez właściciela; parametry i reguły szczegółowe do projektu.

## Przyjęty zakres

- Po potwierdzonym zatrzymaniu silnika włączone mijania/drogowe przechodzą w przednie i tylne pozycyjne. Przy zgaszonym silniku można ponownie włączyć mijania/drogowe z HMI.
- ECU nadzoruje napięcie podczas pracy. Przy zgaszonym silniku, jeszcze przed snem, niskie napięcie uruchamia oszczędzanie i wyłącza pozycyjne oraz zbędne odbiorniki załączone z HMI. Wykaz odbiorników wymaga uzgodnienia.
- Nadal obowiązują: automatyczne pozycyjne po uruchomieniu (SYS-082), wyłączenie oświetlenia przed prawidłowym snem (SYS-081) oraz niezależność ECU od HMI. To osobny stan pracy przed snem, nie zastępstwo koordynowanego usypiania.

## Rekomendacje i decyzje otwarte

1. Potwierdzać spadek przez ustalony czas i zastosować histerezę. Wzrost napięcia po odłączeniu obciążeń nie powinien wywoływać cyklicznego przywracania i odcinania. [Analog Devices](https://www.analog.com/en/resources/analog-dialogue/articles/adding-hysteresis-for-smooth-undervoltage-and-overvoltage-lockout.html) opisuje tę zależność; nie oznacza to wyboru układu ani wartości.
2. Progi dobrać do akumulatora, obciążeń i potrzeb rozruchu oraz potwierdzić pomiarowo. [Yuasa](https://www.yuasabatteries.com/about/events-news/news/new-battery-when-to-replace/) rozróżnia napięcie spoczynkowe, zachowanie pod obciążeniem i typ akumulatora. Nie przyjęto uniwersalnego progu dla wszystkich chemii.
3. Pytanie 88: czy zwykłe polecenie HMI może ominąć aktywne oszczędzanie? Rekomendacja: odrzucać takie polecenia i pokazywać powód; odpowiedź pozostaje otwarta. Zwykłe ręczne włączenie po zgaszeniu poza oszczędzaniem jest wymaganiem SYS-083.
4. Ustalić wyjście z trybu po wzroście napięcia, potwierdzonym ładowaniu lub ponownym uruchomieniu; określić obsługę zapamiętanych żądań. Rekomendacja: nie przywracać dużych obciążeń wyłącznie wskutek chwilowego odbicia napięcia.
5. Określić listę odbiorników i priorytety: ochrona nie może przypadkowo odłączyć funkcji wymaganych do działania ECU, STOP, rozruchu, komunikacji i trwałego zapisu danych. Wentylator ma własne ograniczenia SYS-060/061; powiązać je z nową polityką. Dla PC uwzględnić zasilanie serwisowe SYS-058, blokadę snu SYS-057 i bezpieczne ukończenie lub przerwanie aktualizacji. Sposób prezentacji, ewentualna diagnostyka i postępowanie przy błędzie pomiaru są otwarte.

Tryb oszczędzania odbiorników i minimalne napięcie poprawnej pracy elektroniki wymagają osobnej analizy. Zdolność wykrywania ruchu koła oraz wybudzania przy małym poborze należy powiązać z budżetem energii; nie przyjęto odłączenia akumulatora ani automatycznego odcięcia zasilania HMI w tym trybie.

## Plan prób do uszczegółowienia

| Obszar | Oczekiwane potwierdzenie |
| --- | --- |
| Zatrzymanie silnika | Z uprzednio włączonych mijania lub drogowych przejście na oba pozycyjne; ponowne ręczne włączenie z HMI poza oszczędzaniem. |
| Spadek napięcia | Wejście przed snem i wyłączenie ustalonych odbiorników także bez sprawnego HMI; granice czasu i napięcia do ustalenia. |
| Powrót i zakłócenia | Powolne przejście przez próg, krótkie zapady i odbicie po odciążeniu: zachowanie według przyjętych reguł, bez niekontrolowanego przełączania. |
| Polecenia i priorytety | Wyniki zgodne z przyszłą odpowiedzią na pytanie 88; osobno rozruch, wentylator, PC/aktualizacja, zapis danych i uśpienie. |
| Pomiar i energia | Dokładność, uszkodzenia toru, prąd odbiorników oraz pobór ECU/HMI w stanach docelowych. |

Stanowiska, konkretne połączenia, limity i dowody zostaną przygotowane przed próbami. To plan, nie wykonane testy ani potwierdzenie ochrony akumulatora.
