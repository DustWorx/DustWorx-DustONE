# Zasady pracy

## Dokumentacja

- Dokumentację prowadzimy po polsku, krótko i rzeczowo, w Markdown UTF-8. Nazwy katalogów i plików: małe litery ASCII, słowa rozdzielane myślnikiem.
- Każdy temat ma jedno miejsce źródłowe. W innych dokumentach stosujemy odsyłacze.
- Rozróżniamy: wymaganie właściciela, propozycję, zatwierdzoną decyzję i informację do ustalenia. Nie przedstawiamy założeń jako faktów.
- Wymagania otrzymują trwałe identyfikatory, początkowo SYS-001 itd. Identyfikatorów nie zmieniamy ani nie używamy ponownie po wycofaniu wymagania.
- Istotne decyzje zapisujemy w `docs/decisions/`, z uzasadnieniem i skutkami. Zatwierdzenie wymaga wskazania faktycznego potwierdzenia właściciela projektu.
- Wersję roboczą oznaczamy jako roboczą. Nie dopisujemy „final”, „final2” ani numerów kopii do nazw; historię zapewnia Git.
- Normy i rozbudowane elementy procesu wprowadzamy, gdy wynikają z zastosowania produktu lub dają konkretną wartość. Nie deklarujemy zgodności bez podstaw i weryfikacji.

## Zmiany w repozytorium

- `main` przechowuje aktualną, spójną wersję projektu. Dokumenty robocze mogą się tam znajdować, jeżeli mają jawny status.
- Początkową strukturę zapisujemy bezpośrednio na `main`. Kolejne zmiany prowadzimy w krótkich gałęziach tematycznych i przez pull request.
- Zalecane prefiksy gałęzi: `docs/`, `hardware/`, `firmware/`, `software/`, `tools/`.
- Jeden commit lub pull request obejmuje logicznie spójną zmianę. Opis zawiera cel oraz adekwatną weryfikację.
- Przed zapisem sprawdzamy aktualną zawartość repozytorium; nie nadpisujemy cudzych zmian ani historii.
- Decyzje wpływające na kilka części systemu aktualizują odpowiednie wymagania i interfejsy w tej samej zmianie.

## Pliki źródłowe i wyniki

- Pliki edytowalne są źródłem projektu. PDF, obrazy i pliki produkcyjne są eksportami powiązanymi z konkretną rewizją.
- Wyniki kompilacji publikujemy jako zasoby wydań GitHub, gdy powstanie proces wydawniczy. Nie przechowujemy ich jako kolejnych kopii w katalogach źródłowych.
- Nie dodajemy haseł, kluczy, danych dostępowych, prywatnych logów ani dokumentów bez prawa do ich publikacji.
- Testy jednostkowe przechowujemy przy danym komponencie; testy obejmujące współpracę urządzeń w `tests/`.
- Materiały lokalnego katalogu `sources/` są referencjami tylko do odczytu; nie kopiujemy ich automatycznie do repozytorium.
