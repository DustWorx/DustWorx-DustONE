# ADR-009 — oświetlenie i oszczędzanie energii po zgaszeniu

Data: 2026-11-01. Status: zakres funkcjonalny wskazany przez właściciela; parametry i szczegółowe reguły otwarte.

## Decyzja i źródło

W odpowiedzi na pytanie 87 właściciel wybrał przejście z włączonych mijania/drogowych na przednie i tylne pozycyjne po zgaszeniu silnika. Przy zgaszonym silniku użytkownik może ponownie włączyć mijania lub drogowe z HMI. ECU ma na bieżąco nadzorować napięcie i przed uśpieniem wyłączać pozycyjne oraz zbędne odbiorniki włączone z HMI, gdy napięcie spadnie poniżej progu. Wymagania: [SYS-083–089](../01-zakres-systemu.md).

Uzasadnienie właściciela: ograniczyć rozładowanie akumulatora, zachowując możliwość świadomego użycia oświetlenia po zatrzymaniu silnika.

## Konsekwencje

Rozszerza to nadzór napięcia wymagany już dla wentylatora. Ustalić profil akumulatora, tor pomiarowy, próg, potwierdzenie spadku, listę odbiorników, priorytety oraz wartości parametrów powrotu. W odpowiedzi A na pytanie 88 właściciel zatwierdził odrzucanie żądań ponownego włączenia przez ECU i dodał komunikat HMI o wymaganym uruchomieniu silnika (SYS-085/086). W odpowiedzi A na pytanie 89 właściciel zatwierdził wyjście w normalnym użytkowaniu po potwierdzeniu pracy silnika i utrzymaniu napięcia powyżej progu powrotu przez ustalony czas; do tego momentu odcięcie pozostaje aktywne (SYS-087). Samo naciśnięcie START nie potwierdza pracy silnika.

W odpowiedzi na pytanie 90 właściciel wybrał powrót zależny od funkcji: mijania/drogowe i dodatkowe odbiorniki użytkownika pozostają wyłączone do nowego polecenia, a uzgodnione funkcje ochrony silnika, np. wentylator, działają automatycznie według bieżącej potrzeby i własnych zabezpieczeń (SYS-088/089). Ręczne wymuszenie wentylatora nie jest samo odtwarzane.

[Analiza i plan weryfikacji](../architecture/oszczedzanie-energii.md) oddzielają ten zakres od rekomendacji histerezy, filtracji i nieustalonych parametrów, szczegółowej listy odbiorników i trybu warsztatowego. Parametrów liczbowych, mechanizmów i komponentów nie wybrano; działania na produkcie jeszcze nie potwierdzono.
