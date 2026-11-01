# ADR-004 — zakres zapłonu CDI i indukcyjnego

Data: 2026-11-01. Status: zatwierdzony zakres; realizacja sprzętowa i parametry otwarte.

## Problem i opcje

Platforma ma współpracować z różnym osprzętem silników jednocylindrowych. Rozważano obsługę CDI oraz zapłonu indukcyjnego TCI/IDI albo przyjęcie jednego typu z dopuszczeniem wymiany niezgodnej cewki.

## Decyzja i podstawa zatwierdzenia

W odpowiedzi na pytanie 73 z 2026-11-01 właściciel wybrał obsługę obu typów: CDI i indukcyjnego TCI/IDI, z potwierdzeniem zgodności konkretnych cewek przez analizę i testy. Wymaganie: [SYS-067](../01-zakres-systemu.md). Obowiązuje wspólny wariant sprzętowy według SYS-002/015; zakres nie jest deklaracją zgodności ze wszystkimi cewkami OEM.

## Konsekwencje i otwarte dane

- Architektura musi uwzględnić różne tory sterowania i przekazywania energii. Parametry cewki i sterownika należy rozpatrywać łącznie; nie zakładać zamienności cewek CDI i indukcyjnych.
- Do określenia: liczba niezależnych kanałów, cewki/moduły referencyjne, parametry elektryczne, energia, czasy, zakres obrotów i warunki rozruchu. Źródło energii CDI oraz granica między ECU i ewentualnym zewnętrznym stopniem mocy pozostają otwarte.
- Nie wybrano układów scalonych ani pozostałych komponentów. Ważne elementy wybieramy wspólnie z właścicielem po analizie i porównaniu.
- [Cewka IG5128 z Bety](../interfaces/beta-cewka-zaplonowa-ig5128.md) pozostaje referencją wymagającą charakterystyki; jej zdjęcie nie potwierdza parametrów pracy.

## Proponowana weryfikacja

Dla obu typów przygotować reprezentatywne zestawy cewka–tor sterowania, najpierw do prób stanowiskowych, następnie właściwych prób silnikowych. Określić kryteria czasu zapłonu, energii/przebiegów, obciążeń elektrycznych i temperatury w przyjętym zakresie napięć, obrotów i rozruchu. Sprawdzić reakcje na utratę synchronizacji i ustalone usterki. Konkretne punkty pomiarowe, przyrządy, limity oraz procedury powstaną po charakterystyce interfejsów i projekcie torów. Nie wykonano prób; test jednej cewki nie potwierdza zgodności innych modeli.

Podstawa techniczna rozróżnienia CDI i TCI/IDI: [Microchip AN1980, s. 2–3](https://ww1.microchip.com/downloads/aemDocuments/documents/OTH/ApplicationNotes/ApplicationNotes/00001980C.pdf). Dokument producenta nie jest wyborem jego układów do DustONE.
