# F02 — przegląd map, konfiguracji i strojenia

Stan na 2026-11-09. **Gotowy do kontroli właściciela.** F02 obejmuje decyzje 101–104 i 108–165. Po akceptacji karty zapisujemy zamknięcie pakietu w [statusie projektu](../00-proces-i-status.md). [Rejestr SYS](../01-zakres-systemu.md), [operacje i przypadki prób](../interfaces/mapy-i-konfiguracja.md) oraz [ADR-011](../decisions/adr-011-strojenie-na-zywo.md) zawierają szczegóły.

## Przyjęty zakres

| Obszar | Ustalenia | Wymagania |
| --- | --- | --- |
| Zawartość zestawów | Maksymalnie trzy niezależne zestawy map dla jednej konfiguracji silnika. Pojedyncze nastawy są wspólne. Wyposażony 2T ma osobną mapę zaworu wydechowego w każdym zestawie. Gaźnik bez TPS ma krzywą zapłonu od obrotów, a z TPS mapę od obrotów i położenia przepustnicy. Wtrysk dobiera role TPS i pomiarów ciśnienia do konfiguracji silnika. | SYS-028, SYS-118–120, SYS-125–127 |
| Wybór z HMI | ECU przyjmuje zmianę podczas jazdy i na postoju, także przy zgaszonym silniku i zachowanym zasilaniu. Po przyjęciu może czekać na dopuszczony moment przez ustalony czas. HMI pokazuje stan ECU. Uzgodniono wygaśnięcie, ponowny wybór, anulowanie i utratę HMI. Po restarcie ECU może odtworzyć faktycznie zastosowany zestaw z poprawnego zapisu. Zmiana oczekująca przed restartem wygasa. | SYS-047, SYS-099, SYS-138–151 |
| Strojenie w Windows | Wybrane wartości aktywnych i nieaktywnych zestawów można zmieniać na żywo. Grupa zmian jest sprawdzana i stosowana w całości. Zastosowane zmiany pozostają roboczo po utracie Windows. Po zwykłym śnie i wybudzeniu ECU wraca do zapisanych wartości. Pełna podmiana i przywrócenie zapisanego zestawu wymagają zgaszonego silnika. | SYS-094, SYS-100–101, SYS-107, SYS-114–117 |
| Trwały zapis map | Jawne polecenie przy zgaszonym silniku zapisuje wybrany zestaw albo wszystkie. Uzgodniono blokady rozruchu, sprawdzenie sumy, odzyskanie poprawnych map i flagę błędu. Przyjęty zapis z kompletem danych i prawidłowym zasilaniem ECU kończy mimo odłączenia Windows. | SYS-095, SYS-108–113 |
| Usterki i kalibracja awaryjna | Gaźnik z uszkodzonym TPS korzysta ze wspólnej zweryfikowanej krzywej awaryjnej. Wtrysk z TPS i pomiarem ciśnienia może pracować po utracie jednego z nich na kalibracji zweryfikowanej dla tej usterki. Brak takiej kalibracji lub utrata obu pomiarów oznacza kontrolowane zatrzymanie. Wyjątki przy utracie jedynego wymaganego pomiaru wymagają dokumentacji OEM i prób DustONE. Usterka wymagająca pracy awaryjnej albo zatrzymania wymusza „Standard” do najbliższej pracy nominalnej i blokuje przełączanie. | SYS-121–124, SYS-128–138 |
| Krytyczna konfiguracja | Transfer i wdrożenie przy zgaszonym silniku wymagają jawnego polecenia i blokad rozrusznika, zapłonu i wtrysku. Uzgodniono reakcje na rozłączenie, błąd oraz powrót zasilania. Brak potwierdzonej poprawnej konfiguracji utrzymuje blokady i dostęp z Windows. | SYS-003, SYS-102–106 |
| Reset i pierwsza konfiguracja | Potwierdzony reset przywraca ustawienia fabryczne i usuwa stary profil, mapy oraz historię DTC z zamrożonymi ramkami. Eksport jest dostępny przed resetem. ECU kończy przyjęty reset samodzielnie i wznawia go po powrocie zasilania. Reset użytkownika zachowuje ODO i motogodziny, a korekta liczników przenoszonego ECU ma odrębne uprawnienie producenta. Projekt nowego profilu może czekać w ECU po restarcie. Rozruch wymaga zatwierdzenia kompletnego profilu i zgodnego „Standard”. | SYS-025, SYS-076–077, SYS-152–156 |

ECU rozstrzyga wykonanie operacji i udostępnia rzeczywisty stan. HMI obsługuje wybór zestawu i pokazuje wynik. Windows przygotowuje, przesyła i odczytuje dane oraz inicjuje zatwierdzane przez użytkownika operacje.

## Weryfikacja i przekazanie

[Macierz weryfikacji](../verification/macierz-wymagan.md) łączy wymagania z próbami sterowania, blokad, zasilania, CAN, HMI, Windows, diagnostyki i ochrony liczników. Plan F02 obejmuje też uszkodzone dane, przerwane sesje i zasilanie, odmowę rozruchu bez kompletnego profilu oraz późniejszą aktywację po dodaniu „Standard”. Beta 300 RR Racing 2015 jest punktem odniesienia dla gaźnika bez TPS. Dla pozostałych konfiguracji potrzebne są reprezentatywne stanowiska i silniki.

| Etap lub pakiet | Przekazanie | Odpowiedzialność |
| --- | --- | --- |
| Etap 3 — dane | Dane referencyjne osprzętu, pomiarów i strategii dla konkretnych silników. | Asystent przygotowuje analizę i listę danych. Właściciel dostarcza dane i pomiary motocykla. |
| Etap 4 — architektura | Szczegółowe listy map i pola strojenia, limity oraz warunki przełączania. Formaty, zgodność profilu i map, trwałość zapisów, odzyskiwanie, blokady i interfejsy. | Asystent przygotowuje projekt i uzasadnienie. Właściciel zatwierdza decyzje konstrukcyjne zgodnie z procesem. |
| Etap 5 i 11 — próby | Kryteria liczbowe, stanowiska i procedury, później dowody z rzeczywistych ECU, HMI, Windows i właściwych silników. | Asystent przygotowuje procedury i analizuje wyniki. Właściciel wykonuje próby fizyczne. |
| F03, F05–F07 | Reakcje ochronne poza ustaleniami map, prezentacja stanów w HMI, przebieg obsługi w Windows oraz diagnostyka i uprawnienia. | Ustalenia trafiają do właściwych pakietów z [kolejki zakresu](domkniecie-zakresu-funkcjonalnego.md). |

Kontrola właściciela dotyczy zakresu funkcji. Gotowość produktu wymaga późniejszego wdrożenia i wyników prób.
