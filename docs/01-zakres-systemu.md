# DustWorx — zakres systemu ECU / HMI / aplikacja Windows

Status: punkt wyjścia do wymagań; zakres zapisany na podstawie opisu właściciela projektu. Propozycje i otwarte decyzje wymagają dalszego uzgodnienia.

## 1. Cel

Opracowanie systemu sterowania motocyklem obejmującego ECU, HMI na kierownicy oraz jedną aplikację Windows do konfiguracji, strojenia, personalizacji HMI, diagnostyki, aktualizacji i prac rozwojowych.

## 2. Wymagania wynikające z opisu

| ID | Wymaganie |
| --- | --- |
| SYS-001 | ECU steruje pracą silnika jednocylindrowego. |
| SYS-002 | Ten sam wariant sprzętowy ECU obsługuje silniki dwusuwowe i czterosuwowe bez zmian na PCB. |
| SYS-003 | Wybór silnika 2T lub 4T jest dostępny przez konfigurację w aplikacji Windows. |
| SYS-004 | ECU steruje akcesoriami motocykla, w tym światłami, wentylatorem i rozrusznikiem; sposób podłączenia obciążeń pozostaje do ustalenia. |
| SYS-005 | ECU komunikuje się z HMI na kierownicy przez CAN. |
| SYS-006 | Jedna aplikacja Windows obsługuje ECU oraz HMI. |
| SYS-007 | Aplikacja umożliwia konfigurację ECU i strojenie silnika za pomocą map. |
| SYS-008 | Aplikacja umożliwia dostosowanie wyglądu ekranu HMI. |
| SYS-009 | Aplikacja umożliwia diagnostykę ECU i HMI. |
| SYS-010 | Aplikacja umożliwia aktualizację oprogramowania ECU i HMI. |
| SYS-011 | Aplikacja zawiera narzędzia rozwojowe do testowania i debugowania ECU oraz komunikacji CAN. |
| SYS-012 | ECU obsługuje silniki z gaźnikiem oraz z wtryskiem paliwa. Rodzaje i parametry układów wtryskowych pozostają do ustalenia. |
| SYS-013 | ECU jest przeznaczone do instalacji motocykla z akumulatorem o napięciu nominalnym 12 V. Zakres napięć pracy i zachowanie podczas rozruchu pozostają do określenia. |
| SYS-014 | ECU obsługuje silniki z gaźnikiem bez TPS oraz z gaźnikiem z TPS (czujnikiem położenia przepustnicy). |
| SYS-015 | Wspólna PCB ECU zawiera sprzęt potrzebny do obsługi wariantów gaźnikowych oraz KTM TPI i TBI, bez przeróbek PCB ani wymiany obsady komponentów między tymi zastosowaniami. Konkretne modele, roczniki i granice parametrów elektrycznych pozostają do określenia przed zamknięciem projektu sprzętu. |

## 3. Proponowany podział odpowiedzialności

- **ECU:** sterowanie silnikiem i akcesoriami, pomiary, wykrywanie usterek oraz reakcje na błędy. Sterowanie wymagające precyzyjnego czasu realizowane lokalnie w ECU.
- **HMI:** prezentacja informacji oraz obsługa poleceń kierowcy przesyłanych do ECU. Zakres poleceń do ustalenia.
- **Aplikacja Windows:** wspólne środowisko z modułami konfiguracji, map, edycji HMI, diagnostyki, aktualizacji i narzędzi rozwojowych.

Propozycje do uwzględnienia w wymaganiach szczegółowych:

- Określić działanie ECU po utracie HMI, CAN lub połączenia z komputerem.
- Oddzielić konfigurację silnika, kalibrację map i projekt wyglądu HMI; określić ich wersje i zgodność z oprogramowaniem urządzeń.
- Ustalić warunki dopuszczające zapis map, zmianę typu silnika, aktualizację i testy wyjść.
- Zdefiniować ograniczenia narzędzi rozwojowych i sposób wejścia w tryb testowy.
- Zdefiniować odzyskiwanie urządzenia po przerwaniu aktualizacji.

### Zasada integracji z motocyklem — ustalenie właściciela

Priorytetem jest zachowanie seryjnych czujników i osprzętu silnika w możliwie największym zakresie, o ile pozwala na to zgodność techniczna z ECU. Nie oznacza to potwierdzonej zgodności ze wszystkimi elementami OEM ani bezwzględnego zakazu ich wymiany. Ewentualne odstępstwa należy uzasadnić wynikami analizy.

Wiązka motocykla może być modyfikowana lub zaprojektowana od nowa, w tym przez zastosowanie adapterów i zmianę złączy. Samo dopasowanie wiązki nie stanowi potwierdzenia zgodności elektrycznej.

Dla wybranych modeli przed doborem interfejsów PCB należy zinwentaryzować i sprawdzić parametry czujników, cewek, wtryskiwaczy oraz pozostałych elementów wykonawczych. Wynik analizy ma wskazywać elementy zachowywane, potrzebne adaptacje i ewentualne wymiany wraz z uzasadnieniem.

### Pożądana funkcja: rozruch kopniakiem przy osłabionym akumulatorze

Intencja właściciela: umożliwić rozruch silnika kopniakiem, gdy podłączony akumulator 12 V nie wystarcza do użycia rozrusznika, ale nadal zasila elektronikę. Praca bez energii z akumulatora nie jest wymagana w ramach tej funkcji.

Status: funkcja pożądana, do analizy wykonalności i określenia mierzalnych kryteriów. Nie jest jeszcze gwarantowaną zdolnością systemu. Ocena ma objąć cały tor rozruchu: ECU, czujniki, zapłon oraz — przy wtrysku — układ paliwowy. Wariant gaźnikowy i wtryskowy należy ocenić oddzielnie.

Do ustalenia: minimalne napięcie i dostępny prąd pod obciążeniem, chemia i stan akumulatora, temperatura, obciążenia aktywne podczas rozruchu oraz warunki mechaniczne rozruchu. Nie przyjmujemy arbitralnego progu 12 V jako granicy działania rozrusznika. Napięcie spoczynkowe nie zastępuje oceny pod obciążeniem: [Yuasa — badanie akumulatora ołowiowego](https://www.yuasabatteries.com.au/resources/expert-advice/how-to-test-a-lead-acid-battery).

## 4. Decyzje potrzebne przed doborem sprzętu

| Obszar | Do ustalenia |
| --- | --- |
| Silnik | Pierwszy motocykl testowy: Beta 300 RR Racing / Race Edition, 2015, wskazany przez właściciela. Według właściciela gaźnik, zapłon i instalacja są fabryczne. Do potwierdzenia podczas inwentaryzacji: parametry i stan osprzętu. Do ustalenia: maksymalne obroty oraz reprezentatywne jednostki 4T, TPI i TBI. Obsługa gaźnika z TPS i bez TPS oraz TPI/TBI jest wymagana (SYS-012, SYS-014, SYS-015). |
| Zapłon | Typy obsługiwanych układów i cewek; wymagane interfejsy sterujące. |
| Synchronizacja | Czujniki wału i ewentualnie wałka, ich sygnały oraz układy znaczników. |
| Układ paliwowy | Rodzaj układu wtryskowego, liczba i parametry wtryskiwaczy, sterowanie pompą. |
| Instalacja | Akumulator nominalnie 12 V (SYS-013). Do określenia: zakres napięć, chemia akumulatora i warunki rozruchu. Pożądany rozruch kopniakiem z osłabionym, podłączonym akumulatorem; rozruch bez energii z akumulatora nie jest wymagany. |
| Akcesoria | Pełna lista odbiorników, prądy robocze i rozruchowe, sterowanie bezpośrednie lub przez przekaźniki/styczniki. |
| Pomiary | Lista czujników, zakresy i wymagana dokładność. |
| HMI | Ekran, sposób obsługi, prezentowane dane i zakres personalizacji. |
| Połączenie z PC | Sposób fizycznego podłączenia do ECU/HMI; CAN między urządzeniami nie przesądza interfejsu komputera. |
| Debugowanie | Rozróżnić podgląd danych, testy wyjść i analizę CAN od debugowania programu przez interfejs debuggera. |
| Warunki pracy | Temperatura, woda, pył, drgania, miejsce montażu oraz docelowe zastosowanie motocykla. |

## 5. Następny rezultat inżynierski

Po inwentaryzacji Bety 300 RR Racing 2015 i określeniu docelowych wariantów 4T, TPI i TBI oraz instalacji elektrycznej: opracować listę wejść/wyjść ECU, granice obsługiwanego sprzętu oraz architekturę blokową. Następnie ustalić mierzalne kryteria weryfikacji wymagań i plan prób. Dobór komponentów PCB następuje po zamknięciu tych danych.

## 6. Sposób realizacji i współpracy

Ustalenia właściciela projektu z 2026-10-15:

- Cały proces inżynierski prowadzimy wspólnie w rozmowie: organizację projektu, wymagania, funkcjonalność, architekturę, elektronikę, dobór każdego komponentu, schematy, projekt PCB, mechanikę oraz weryfikację.
- Firmware przygotowuje właściciel projektu z Codexem. Wspólna praca inżynierska obejmuje wymagania, interfejsy i kryteria weryfikacji potrzebne do jego implementacji.
- Pytania przedstawiamy pojedynczo, z przygotowanymi wariantami odpowiedzi. Gdy wybór wymaga danych technicznych lub porównania, przedstawiamy podstawy i konsekwencje przed decyzją.
- Ustalenia i wyniki prac zapisujemy w repozytorium DustWorx/DustWorx-DustONE zgodnie z jego strukturą.
- Obsługa gaźnika z TPS i bez TPS oraz KTM TPI/TBI została potwierdzona przez właściciela. Pierwszym motocyklem testowym jest jego Beta 300 RR Racing / Race Edition z 2015 r.; jednostki referencyjne 4T i konkretne generacje układów wtryskowych pozostają do ustalenia.

## 7. Motocykl referencyjny i zakres weryfikacji

**Potwierdzone przez właściciela:** dostępny jest cały motocykl Beta 300 RR Racing / Race Edition, rocznik 2015, przeznaczony do pierwszych testów. Wersję Racing / Race Edition wskazał właściciel. Według jego wiedzy gaźnik, układ zapłonowy i instalacja elektryczna są fabryczne. Jest to deklaracja właściciela; oznaczenia, parametry i zgodność ze stanem fabrycznym wymagają potwierdzenia podczas inwentaryzacji. Producent udostępnia instrukcje tej rodziny w [indeksie dokumentacji Beta](https://www.betamotor.com.au/support/off-road/); parametry konkretnego egzemplarza wymagają inwentaryzacji.

Beta służy do pierwszej integracji. Jej wyposażenie nie ogranicza docelowego zakresu PCB. Wymagania dotyczące gaźnika z TPS i bez TPS, 4T oraz TPI/TBI muszą być uwzględnione przed zamknięciem projektu sprzętu, również gdy nie można ich sprawdzić na tym motocyklu.

Weryfikację dzielimy na próby dostępne na Becie oraz próby stanowiskowe i późniejsze próby na innych jednostkach. Wynik na Becie nie potwierdza zgodności z pozostałymi wariantami. Właściciel dopuszcza późniejsze testy funkcji nieweryfikowalnych na dostępnym motocyklu; plan weryfikacji należy przygotować wraz z wymaganiami.

### Podstawy do dalszej analizy sprzętu

- KTM opisuje TPI MY2018 jako wtrysk z dwoma wtryskiwaczami w kanałach przepłukujących: [KTM — prezentacja TPI](https://press.ktm.com/News_Detail.aspx?id=49472&menueid=3050).
- KTM EXC MY2024 stosuje TBI oraz elektroniczne sterowanie zaworem wydechowym: [KTM — prezentacja EXC MY2024](https://press.ktm.com/news-challenge-accepted-the-2024-ktm-exc-range-is-here-to-redefine-limits?id=179901&l=uk&menueid=5904).

Są to przykłady do ustalenia zakresu, nie zatwierdzona lista wspieranych motocykli ani kompletna specyfikacja elektryczna. Do analizy: kanały wtrysku, zapłon, pompa paliwa, ewentualna pompa oleju, sterowanie zaworem wydechowym, czujniki i synchronizacja. Nie wybrano jeszcze liczby kanałów, sterowników wyjściowych ani szczegółowych interfejsów elektrycznych do osprzętu OEM.
