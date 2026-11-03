# ADR-011 — niezależne zestawy map i strojenie na żywo

Data: 2026-11-03. Status: **zatwierdzony zakres funkcji; realizacja otwarta**.

## Problem i opcje

Aplikacja Windows ma umożliwiać strojenie map. Należało rozstrzygnąć, czy zmienione wartości mogą być stosowane podczas pracy silnika, czy dopiero po jego zatrzymaniu. Przełączanie maksymalnie trzech gotowych zestawów z HMI jest już wymagane przez SYS-028.

## Decyzja i podstawa

Windows umożliwia zmianę wybranych wartości map podczas pracy silnika. Dopuszczalny zakres i zabezpieczenia określimy w projekcie. ECU pozostaje wykonawcą i właścicielem aktywnych danych.

Źródło: odpowiedź właściciela **A na pytanie 101** w rozmowie projektowej: „Tak — wybrane wartości map można zmieniać podczas pracy silnika; dopuszczalny zakres i zabezpieczenia określimy w projekcie”.

W odpowiedzi **A na pytanie 102** właściciel przyjął maksymalnie trzy niezależne, kompletne zestawy uzgodnionych map dla jednej konfiguracji silnika: „Trzy niezależne, kompletne zestawy uzgodnionych map — np. zapłonu i paliwa w silniku wtryskowym”. Rozważanym wariantem była wspólna baza z trzema profilami korekt.

Doprecyzowanie zapisano w istniejącym SYS-028. Powiązania: SYS-007, SYS-028, SYS-047, SYS-094 i SYS-095. Reguły operacji rozwijamy w [specyfikacji map i konfiguracji](../interfaces/mapy-i-konfiguracja.md).

W odpowiedzi **A na pytanie 103** właściciel przyjął: „Trwały zapis tylko przy zgaszonym silniku, na wyraźne polecenie użytkownika”. Regułę zapisano jako SYS-095. Rozważany wariant zapisu na polecenie również podczas pracy silnika nie został wybrany.

## Skutki i sprawy otwarte

- Architektura ECU, protokołu i Windows ma uwzględnić przyjmowanie, sprawdzanie i stosowanie zmian bez zakłócenia sterowania silnikiem.
- W pakiecie F02 określimy dozwolone pola, zakresy zmian, spójny moment ich zastosowania, potwierdzenie rzeczywistego stanu, zachowanie po utracie sesji/zasilania i zmianie aktywnego zestawu.
- Trwałe utrwalanie zmian map jest dostępne tylko po wyraźnym poleceniu z Windows przy zgaszonym silniku; dopuszczenie egzekwuje ECU. Zmiana zastosowana na żywo nie zapisuje się automatycznie.
- Potwierdzanie zatrzymania, warunki zasilania, integralność/przerwanie zapisu i reakcja na rozpoczęcie rozruchu podczas operacji wymagają projektu. Przywracanie poprzednich danych, utrata sesji i wybór danych po restarcie pozostają otwarte.
- Każdy z maksymalnie trzech zestawów zawiera własne wartości uzgodnionych map. Konkretna lista map i wspólnych parametrów konfiguracji nadal wymaga specyfikacji F02.
- Rozmiar i organizacja danych mają uwzględniać niezależne zestawy oraz strojenie na żywo; potrzebna pamięć, przepustowość i granice czasowe wymagają obliczeń przed wyborem MCU i protokołu.

## Weryfikacja

Plan obejmie odrębne wartości zestawów i edycję jednego bez zmiany pozostałych, a także zmianę dozwolonej wartości podczas pracy, potwierdzenie danych aktywnych, odrzucenie danych niedopuszczonych i wpływ na czas sterowania. Sprawdzimy dopuszczenie trwałego zapisu na polecenie przy zgaszonym silniku i odrzucenie go podczas pracy oraz brak automatycznego utrwalania zmian na żywo. Oddzielnie sprawdzimy utratę sesji, przełączenie zestawu, zanik zasilania i próbę rozruchu podczas zapisu według przyjętych później reguł. Najpierw stanowisko/symulator, następnie właściwa konfiguracja silnika; procedury i kryteria wykonawcze powstaną po określeniu tych reguł. Brak implementacji i wyników prób.
