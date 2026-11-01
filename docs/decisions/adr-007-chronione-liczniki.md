# ADR-007 — chronione całkowite motogodziny i ODO

Data: 2026-11-01. Status: zatwierdzone liczniki i ograniczenia użytkownika końcowego; realizacja i role serwisowe otwarte.

## Decyzja i źródło

W odpowiedzi na pytanie 80 właściciel wybrał licznik motogodzin oraz całkowity ODO. W doprecyzowaniu tego samego dnia wymagał odporności na manipulację użytkownika i braku możliwości zmiany lub korekty z poziomu użytkownika końcowego. Potwierdził ponownie zakres: motogodziny i ODO. Nie przyjął liczników pomocniczych A/B.

ECU nalicza i trwale przechowuje oba liczniki; HMI i Windows prezentują rzeczywiste dane ECU. Użytkownik nie ma operacji ustawiania, korekty ani kasowania sum. Ograniczenie obejmuje również diagnostykę, development tool, konfigurację i aktualizacje dostępne użytkownikowi. Wymagania: [SYS-074–076](../01-zakres-systemu.md).

## Konsekwencje

Ochrona wymaga projektu interfejsów ECU, pamięci i cyklu życia firmware. Samo ukrycie pola edycji w Windows nie realizuje wymagania. Przed wyborem MCU i pamięci trzeba określić model zagrożeń oraz role użytkownika, rozwoju i serwisu. Inicjalizacja w motocyklu używanym oraz zachowanie historii przy wymianie ECU wymagają osobnej decyzji.

[Założenia architektury i plan weryfikacji](../architecture/chronione-liczniki.md) są miejscem szczegółowego opracowania. Nie wybrano komponentów, kryptografii ani trwałych blokad debuggera; odporność nie została jeszcze potwierdzona próbami.
