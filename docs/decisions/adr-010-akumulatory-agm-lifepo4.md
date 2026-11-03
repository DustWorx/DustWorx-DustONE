# ADR-010 — akumulatory AGM i LiFePO4 na wspólnej PCB

Data: 2026-11-03. Status: zakres zatwierdzony przez właściciela; realizacja i parametry otwarte.

## Decyzja i źródło

W pytaniu 95 właściciel najpierw poprosił o porównanie wpływu na elektronikę, oprogramowanie i testy. Po otrzymaniu porównania wybrał A: „AGM i LiFePO₄ — wspólna PCB, osobne profile i testy zgodności”. Zakres zapisano w [SYS-092](../01-zakres-systemu.md), z doprecyzowaniem klasy instalacji w SYS-013.

Rozważono także ograniczenie platformy do AGM. [Porównanie](../architecture/akumulatory-agm-lifepo4-porownanie.md) zachowuje tę alternatywę i uzasadnienie rekomendacji: szersza zgodność z konfiguracjami enduro przy projektowanej wspólnej PCB, kosztem dodatkowej kwalifikacji profili i prób.

Uzupełnienie z 2026-11-03: w odpowiedzi A na pytanie 96 właściciel przyjął minimum 4 tygodnie postoju bez doładowania z rezerwą na rozruch (SYS-093). Warunki początkowe i brakujące parametry opisuje [budżet energii postoju](../architecture/budzet-energii-postoju.md).

Doprecyzowanie z odpowiedzi B na pytanie 97: dla motocykla z rozrusznikiem i kopniakiem, jak Beta, wystarcza po postoju rozruch kopniakiem; bateria nadal zasila ECU i niezbędny osprzęt. Kryterium konfiguracji bez kopniaka pozostaje do uzgodnienia. Doprecyzowano SYS-093, zachowując jego identyfikator.

## Konsekwencje i ograniczenia

- Wspólny wariant sprzętowy ma obsługiwać oba typy bez zmiany obsady. Tor zasilania, jego ochronę i pomiar dobierzemy do uzgodnionych warunków; wykonalność potwierdzimy analizą i próbami.
- ECU ma osobne profile ochrony AGM/LiFePO4. Wybór, zapis, uprawnienia i warunki zmiany profilu są do projektu; HMI i Windows pozostają klientami ECU.
- Testy obejmują oba typy, zgodne modele/regulatory i uzgodnione granice pracy. Beta z AGM jest pierwszą konfiguracją, a nie dowodem zgodności LiFePO4.
- Zgodność ładowania i funkcje zabezpieczeń akumulatora zależą od modelu. Zakres nie oznacza przyjęcia każdego produktu danej chemii ani gwarancji działania bez dostępnej energii z baterii.
- Wartości napięć, temperatur, prądu czuwania i czasów, szczegóły profili oraz komponenty pozostają otwarte. Ważne elementy wybieramy wspólnie.

[Plan weryfikacji i analiza](../architecture/akumulatory-agm-lifepo4-porownanie.md) obejmują rozruch, zarządzanie energią, sen/wybudzanie, zanik/powrót zasilania i integrację. Nie wykonano jeszcze prób produktu.
