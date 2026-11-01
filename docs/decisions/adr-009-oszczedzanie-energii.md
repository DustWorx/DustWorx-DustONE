# ADR-009 — oświetlenie i oszczędzanie energii po zgaszeniu

Data: 2026-11-01. Status: zakres funkcjonalny wskazany przez właściciela; parametry i szczegółowe reguły otwarte.

## Decyzja i źródło

W odpowiedzi na pytanie 87 właściciel wybrał przejście z włączonych mijania/drogowych na przednie i tylne pozycyjne po zgaszeniu silnika. Przy zgaszonym silniku użytkownik może ponownie włączyć mijania lub drogowe z HMI. ECU ma na bieżąco nadzorować napięcie i przed uśpieniem wyłączać pozycyjne oraz zbędne odbiorniki włączone z HMI, gdy napięcie spadnie poniżej progu. Wymagania: [SYS-083/084](../01-zakres-systemu.md).

Uzasadnienie właściciela: ograniczyć rozładowanie akumulatora, zachowując możliwość świadomego użycia oświetlenia po zatrzymaniu silnika.

## Konsekwencje

Rozszerza to nadzór napięcia wymagany już dla wentylatora. Ustalić profil akumulatora, tor pomiarowy, próg, potwierdzenie spadku, listę odbiorników, priorytety oraz warunki powrotu. Zasady poleceń HMI podczas oszczędzania są przedmiotem pytania 88 i nie zostały jeszcze przyjęte.

[Analiza i plan weryfikacji](../architecture/oszczedzanie-energii.md) oddzielają ten zakres od rekomendacji histerezy, filtracji i obsługi powrotu. Parametrów liczbowych, mechanizmów i komponentów nie wybrano; działania na produkcie jeszcze nie potwierdzono.
