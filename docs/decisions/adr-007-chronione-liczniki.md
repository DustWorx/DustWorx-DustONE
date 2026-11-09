# ADR-007 — chronione całkowite motogodziny i ODO

Data decyzji 2026-11-01. Uzupełnienie 2026-11-09. Zakres chronionych liczników i uprawnienia zatwierdzono. Szczegóły realizacji pozostają otwarte.

## Decyzja i źródło

W odpowiedzi na pytanie 80 właściciel wybrał licznik motogodzin oraz całkowity ODO. W doprecyzowaniu tego samego dnia wymagał odporności na manipulację użytkownika i braku możliwości zmiany lub korekty z poziomu użytkownika końcowego. Potwierdził ponownie zakres: motogodziny i ODO. Nie przyjął liczników pomocniczych A/B.

ECU nalicza i trwale przechowuje oba liczniki; HMI i Windows prezentują rzeczywiste dane ECU. Użytkownik nie ma operacji ustawiania, korekty ani kasowania sum. Ograniczenie obejmuje również diagnostykę, development tool, konfigurację i aktualizacje dostępne użytkownikowi. Wymagania: [SYS-074–077](../01-zakres-systemu.md).

W odpowiedzi A na pytanie 81 z 2026-11-01 właściciel zatwierdził chronioną procedurę producenta/serwisu: inicjalizację nowego ECU lub przeniesienie udokumentowanych wartości, z rejestrem każdej operacji. Uprawnienie to nie przysługuje użytkownikowi końcowemu. Szczegóły autoryzacji, dowodów oraz rejestru pozostają do projektu.

W odpowiedzi na **pytanie 162** (2026-11-09) właściciel zastrzegł zmianę ODO lub motogodzin przy przełożeniu używanego ECU do innego motocykla wyłącznie dla producenta projektu. Producent może zmienić jeden lub oba liczniki. ECU egzekwuje uprawnienie, a każda wykonana operacja jest rejestrowana (SYS-153). Reset ustawień w trybie użytkownika zachowuje oba liczniki zgodnie z SYS-152.

## Konsekwencje

Ochrona wymaga projektu interfejsów ECU, pamięci i cyklu życia firmware. Samo ukrycie pola edycji w Windows nie realizuje wymagania. Przed wyborem MCU i pamięci trzeba określić model zagrożeń oraz zasady rozdzielenia dostępu użytkownika, rozwoju i serwisu. Dla inicjalizacji i przenoszenia wartości według SYS-077 oraz zmiany producenta według SYS-153 należy opracować autoryzację, wiarygodność dokumentowanych wartości, trwałość rejestru oraz zachowanie przy przerwaniu operacji.

[Założenia architektury i plan weryfikacji](../architecture/chronione-liczniki.md) są miejscem szczegółowego opracowania. Nie wybrano komponentów, kryptografii ani trwałych blokad debuggera; odporność nie została jeszcze potwierdzona próbami.
