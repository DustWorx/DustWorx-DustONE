# Akumulatory AGM i LiFePO4 — porównanie zakresu

Data: 2026-11-03. Status: po porównaniu właściciel w pytaniu 95 wybrał A — obsługę obu typów na wspólnej PCB, z osobnymi profilami i testami zgodności ([SYS-092 i ADR-010](../decisions/adr-010-akumulatory-agm-lifepo4.md)). Realizacja i parametry pozostają do projektu. Powiązania: [zakres systemu](../01-zakres-systemu.md), [zarządzanie energią](oszczedzanie-energii.md), [referencja Bety](../interfaces/beta-2015-analiza-dokumentacji.md#akumulator). Nie wybrano komponentów ani parametrów zasilania.

## Punkt odniesienia

Dla Bety przyjęto AGM 12 V, 4 Ah. Przykładowy [BS BTX5L-BS](https://bs-battery.com/usa/product/btx5l-bs/) ma 4 Ah przy rozładowaniu 10-godzinnym. [BSLi-02](https://bs-battery.com/product/bsli-02/) to LiFePO4 12,8 V, 2 Ah według tej samej deklarowanej miary; [Beta USA oferuje go do enduro/MX](https://betausa.com/bs-heavy-duty-lithium-battery/). To przykłady do analizy, nie zatwierdzone modele dla całej platformy. Wyższy prąd rozruchowy nie oznacza większej pojemności do zasilania odbiorników na postoju.

## Wpływ na projekt

| Obszar | Tylko AGM | AGM i LiFePO4 |
| --- | --- | --- |
| Tor zasilania ECU/HMI | Przetwornice, ochrona wejścia i pomiar napięcia dobrane do uzgodnionych warunków instalacji AGM. | Proponowany ten sam tor, dobrany do łącznego zakresu warunków obu typów. Sama różnica chemii nie wymusza drugiej przetwornicy; wykonalność jednej obsady PCB wymaga analizy i prób. |
| Ochrona wejścia | Spadki rozruchowe, zakłócenia, przepięcia i przerwy zasilania. | Te same kategorie oraz zachowanie przy odłączeniu/powrocie źródła przez zabezpieczenia wybranego akumulatora, jeżeli je ma. |
| Firmware ECU | Jeden zakres profili napięcia, czasów i kwalifikacji dla zgodnych AGM. | Wybierany profil AGM/LiFePO4 i parametry dla zakwalifikowanych modeli. Dotychczasowe zasady odcięcia i powrotu SYS-084–091 pozostają podstawą. |
| Windows i HMI | Konfiguracja parametrów, odczyt napięcia i powodów ograniczeń. | Dodatkowo jawny wybór i zapis profilu w ECU; aplikacja/HMI prezentują stan pochodzący z ECU. Sposób uprawnień do zmiany profilu do uzgodnienia. |
| Czuwanie i odbiorniki | Budżet prądu oraz czas postoju dobrane do pojemności, stanu i temperatury akumulatora. | Sprawdzić również najmniejszą dopuszczoną rzeczywistą pojemność. Przykładowe 2 Ah LiFePO4 nie zapewnia takiej samej rezerwy dla świateł i wentylatora jak 4 Ah AGM; nie uogólniać tych pojemności na wszystkie modele. |
| Dodatkowe pomiary | Potrzebny uzgodniony tor napięcia i pomiar prądu czuwania na stanowisku. | Sam wybór dwóch typów nie przesądza o dodaniu na PCB pomiaru prądu baterii lub jej temperatury. Potrzebę dodatkowych torów rozstrzygniemy z wymaganiami i dokumentacją zgodnych akumulatorów. |
| Koszt i gabaryty | Mniej wariantów do kwalifikacji. | Więcej prac nad profilami, stanowiskami i regresją. Różnica BOM/powierzchni jest nieznana przed doborem wspólnego toru i parametrów; nie deklarujemy kosztu zerowego. |

Spadki rozruchowe i przepięcia wymagają projektu niezależnie od wyboru chemii. [TI SNVA681A](https://www.ti.com/lit/an/snva681a/snva681a.pdf) opisuje te kategorie w samochodowych instalacjach. Dla DustONE jest to materiał do analizy; przebiegi, energia i granice pracy mają wynikać z docelowych motocykli oraz uzgodnionych prób, bez automatycznego przenoszenia wartości ani układów z noty.

## Ładowanie i dostępność energii

Profil ochrony ECU ogranicza odbiorniki DustONE; nie zastępuje zgodnego układu ładowania motocykla ani zabezpieczeń akumulatora. Dla wybranego LiFePO4 sprawdzić regulator i instrukcję baterii, w tym napięcie, prąd i temperaturę ładowania. [Instrukcja BS Lithium/Lithium Max, wydanie 2026-03, s. 2–4](https://bs-battery.com/wp-content/uploads/2023/01/2023-01_BS-BATTERY_Manual_Lithium.pdf) określa własne ograniczenia i opisuje płytkę wyrównującą ładowanie. Nie utożsamiamy tego opisu z potwierdzonym odcięciem rozładowania.

Zabezpieczenia zależą od modelu. Przykładowo [EarthX ETX](https://earthxbatteries.com/our-batteries/battery-charging/) odłącza obciążenie przy nadmiernym rozładowaniu; nie przypisujemy tej funkcji każdemu LiFePO4 ani BSLi-02. Gdy na zaciskach nie ma dostępnej energii, wybudzenie ECU przez START, koło, HMI lub kabel PC nie może samo zapewnić zasilania. Funkcja kopniaka dotyczy osłabionej, nadal zasilającej baterii; wariant pracy bez jej energii nie jest wymagany. Charakter powrotu zasilania oraz możliwych przepięć wymaga oceny konkretnego generatora/regulatora.

## Plan weryfikacji do uszczegółowienia

Plan obejmuje oba typy zgodnie z SYS-092. To zakres do późniejszych procedur, bez wykonanych prób. Przed testem ustalimy połączenia, temperatury, obciążenia, granice i dowody według [zasad weryfikacji](../verification/README.md).

| Próba / etap | AGM | Dodatkowo przy LiFePO4 | Powiązanie |
| --- | --- | --- | --- |
| Dokumentacja i inwentaryzacja | Identyfikacja baterii, regulatora, obciążeń i stanu. | Limity konkretnego modelu, zgodność ładowania, obecność i sposób działania zabezpieczeń. | SYS-013, BETA-P01 / INV-04 |
| Rozruch i słaba bateria — stanowisko, potem motocykl | Przebiegi zasilania przy rozruszniku i kopniaku; gotowość ECU/HMI. | Te same scenariusze dla dopuszczonych temperatur i stanów baterii, z zachowaniem jej ograniczeń. | SYS-013/048/049/054 |
| Oszczędzanie — stanowisko/system | Odcięcie, histereza/czasy, odmowy ON, kwalifikowany powrót i serwis. | Osobne parametry profilu i sprawdzenie niewłaściwego/niepoprawnego profilu. Reakcja na błędny profil wymaga uzgodnienia. | SYS-060/061, SYS-084–091 |
| Sen i wybudzanie — ECU/HMI | Rzeczywisty pobór obu urządzeń i torów czuwania; wszystkie zatwierdzone źródła wybudzenia. | Budżet dla najmniejszej dopuszczonej pojemności; dostępność energii po długim postoju. | SYS-054–059, SYS-062–066, SYS-079/080 |
| Zanik/powrót i zakłócenia — zabezpieczone stanowisko | Reset, wyjścia, DTC, liczniki i odzyskanie po przerwaniu aktualizacji. | Emulacja odłączenia/powrotu przez zabezpieczenia, jeśli dany model je ma; zgodność z regulatorem. | SYS-010/013, SYS-019–025, SYS-074–078 |
| Integracja — motocykl i serwis | Regulator pod obciążeniem, światła, wentylator i zasilanie warsztatowe. | Powtórzenie dla zatwierdzonych konfiguracji LiFePO4. | SYS-004/058/060/061, SYS-083–091 |

Zakłócenia i utratę zasilania przygotujemy najpierw na stanowisku z kontrolowanym źródłem i obciążeniem. Nie jest to polecenie odłączania akumulatora od pracującego motocykla. Wspólne testy logiki można współdzielić, ale próby granic zasilania i bilansu energii trzeba wykonać dla każdego deklarowanego zakresu.

## Decyzja właściciela i dalszy projekt

Właściciel zatwierdził obsługę AGM i motocyklowych LiFePO4 na tej samej PCB, z osobnymi profilami ochrony i testami zgodności. Wybór i utrwalanie profilu oraz kwalifikacja konkretnych konfiguracji wymagają projektu. Najpierw wykorzystać obecną Betę z AGM, a walidację LiFePO4 przygotować na osobnym akumulatorze/stanowisku. Ostateczny dobór toru, komponentów i zgodnych modeli przeprowadzimy wspólnie.

Modele referencyjne LiFePO4, zakres temperatur/napięć, dopuszczalny prąd czuwania, czas postoju i mierzalne kryteria pozostają otwarte. Zatwierdzenie po porównaniu zapisuje ADR-010; sama wcześniejsza odpowiedź C dotyczyła przygotowania analizy.
