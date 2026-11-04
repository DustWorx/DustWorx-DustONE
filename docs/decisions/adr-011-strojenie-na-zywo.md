# ADR-011 — niezależne zestawy map i strojenie na żywo

Data: 2026-11-03. Status: **zatwierdzony zakres funkcji; realizacja otwarta**.

## Problem i opcje

Aplikacja Windows ma umożliwiać strojenie map. Należało rozstrzygnąć, czy zmienione wartości mogą być stosowane podczas pracy silnika, czy dopiero po jego zatrzymaniu. Przełączanie maksymalnie trzech gotowych zestawów z HMI jest już wymagane przez SYS-028.

## Decyzja i podstawa

Windows umożliwia zmianę wybranych wartości map podczas pracy silnika. Dopuszczalny zakres i zabezpieczenia określimy w projekcie. ECU pozostaje wykonawcą i właścicielem aktywnych danych.

Źródło: odpowiedź właściciela **A na pytanie 101** w rozmowie projektowej: „Tak — wybrane wartości map można zmieniać podczas pracy silnika; dopuszczalny zakres i zabezpieczenia określimy w projekcie”.

W odpowiedzi **A na pytanie 102** właściciel przyjął maksymalnie trzy niezależne, kompletne zestawy uzgodnionych map dla jednej konfiguracji silnika: „Trzy niezależne, kompletne zestawy uzgodnionych map — np. zapłonu i paliwa w silniku wtryskowym”. Rozważanym wariantem była wspólna baza z trzema profilami korekt.

Doprecyzowanie zapisano w istniejącym SYS-028. Powiązania: SYS-007, SYS-028, SYS-047, SYS-094, SYS-095, SYS-099, SYS-100 i SYS-101. Reguły operacji rozwijamy w [specyfikacji map i konfiguracji](../interfaces/mapy-i-konfiguracja.md).

W odpowiedzi **A na pytanie 103** właściciel przyjął: „Trwały zapis tylko przy zgaszonym silniku, na wyraźne polecenie użytkownika”. Regułę zapisano jako SYS-095. Rozważany wariant zapisu na polecenie również podczas pracy silnika nie został wybrany.

W odpowiedzi **A na pytanie 104** właściciel przyjął: „Pozostawić ostatnio zastosowane wartości aktywne w bieżącej pracy ECU”. Po utracie połączenia z Windows nie wykonujemy automatycznego trwałego zapisu; doprecyzowano SYS-094. Reguła dotyczy bieżącej pracy, bez rozstrzygnięcia wyboru danych po restarcie ECU.

W odpowiedzi **A na pytanie 108** (2026-11-04) właściciel przyjął: „Ostatnio wybrany prawidłowy zestaw — ECU zapamiętuje wybór”. Po ponownym uruchomieniu ECU wybiera go spośród zestawów trwale zapisanych, także bez HMI (SYS-099). To rozstrzyga regułę wyboru; mechanizm zapamiętywania i obsługa błędnych danych pozostają do projektu.

W odpowiedzi **A na pytanie 109** (2026-11-04) właściciel przyjął powrót do trwale zapisanych wartości po zwykłym śnie/wybudzeniu i odrzucenie niezapisanych zmian (SYS-100), bez automatycznego trwałego zapisu. Rozważane zachowanie roboczych wartości przez sen nie jest wymaganiem.

W odpowiedzi **A na pytanie 110** (2026-11-04) właściciel przyjął: „Tak — można zmieniać robocze wartości aktywnego i nieaktywnych zestawów; edycja nie przełącza zestawu”. Zmiany nieaktywnego zestawu wpływają na silnik dopiero po jego świadomym wybraniu (SYS-101). Wariant ograniczenia edycji podczas pracy do aktywnego zestawu nie został wybrany. Trwały zapis nadal podlega SYS-095.

## Skutki i sprawy otwarte

- Architektura ECU, protokołu i Windows ma uwzględnić przyjmowanie, sprawdzanie i stosowanie zmian bez zakłócenia sterowania silnikiem.
- W pakiecie F02 określimy dozwolone pola, zakresy zmian, spójny moment ich zastosowania, potwierdzenie rzeczywistego stanu, ponowne połączenie, zastosowanie reguły snu/wybudzenia i zmianę aktywnego zestawu.
- Trwałe utrwalanie zmian map jest dostępne tylko po wyraźnym poleceniu z Windows przy zgaszonym silniku; dopuszczenie egzekwuje ECU. Zmiana zastosowana na żywo nie zapisuje się automatycznie.
- Potwierdzanie zatrzymania, warunki zasilania, integralność/przerwanie zapisu i reakcja na rozpoczęcie rozruchu podczas operacji wymagają projektu. Utrata sesji zachowuje zastosowane wartości w bieżącej pracy. Restart aktywuje ostatnio wybrany prawidłowy zestaw z trwale zapisanych danych. Po prawidłowym śnie/wybudzeniu obowiązuje powrót do zapisanych wartości. Cofanie edycji w bieżącej pracy, ponowne połączenie, szczegóły sekwencji i walidacja danych wyboru pozostają otwarte.
- Zapamiętanie wyboru zestawu nie oznacza automatycznego utrwalenia zmienianych wartości map. Sposób i moment zapisu identyfikatora wyboru określimy w projekcie z zachowaniem reguł danych.
- Każdy z maksymalnie trzech zestawów zawiera własne wartości uzgodnionych map. Konkretna lista map i wspólnych parametrów konfiguracji nadal wymaga specyfikacji F02.
- Rozmiar i organizacja danych mają uwzględniać niezależne zestawy, roboczą edycję aktywnego i nieaktywnych zestawów oraz strojenie na żywo. Potrzebna pamięć, przepustowość i granice czasowe wymagają obliczeń przed wyborem MCU i protokołu; nie przesądzamy sposobu przechowywania roboczych danych.

## Weryfikacja

Plan obejmie odrębne wartości zestawów i edycję jednego bez zmiany pozostałych, a także zmianę dozwolonej wartości podczas pracy, potwierdzenie danych aktywnych, odrzucenie danych niedopuszczonych i wpływ na czas sterowania. Edycja aktywnego i nieaktywnych zestawów nie może sama przełączyć zestawu; zmiany nieaktywnego zestawu mają wpływać na silnik dopiero po jego świadomym wybraniu. Sprawdzimy dopuszczenie trwałego zapisu na polecenie przy zgaszonym silniku i odrzucenie go podczas pracy oraz brak automatycznego utrwalania zmian na żywo. Sprawdzimy zachowanie zastosowanych wartości po utracie sesji i brak automatycznego utrwalenia. Sprawdzimy odtworzenie ostatniego prawidłowego wyboru po restarcie z HMI i bez HMI. Sprawdzimy odrzucenie roboczej edycji po prawidłowym śnie/wybudzeniu bez automatycznego trwałego zapisu. Oddzielnie sprawdzimy przerwanie sekwencji snu, ponowne połączenie, przełączenie zestawu, błędne dane i próbę rozruchu podczas zapisu według przyjętych później reguł. Najpierw stanowisko/symulator, następnie właściwa konfiguracja silnika; procedury i kryteria wykonawcze powstaną po określeniu tych reguł. Brak implementacji i wyników prób.
