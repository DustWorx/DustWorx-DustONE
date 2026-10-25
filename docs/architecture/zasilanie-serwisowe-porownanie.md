# Zasilanie podczas serwisu — porównanie

Data: 2026-10-25. Status: analiza do decyzji właściciela po pytaniu 65; wariant nie został wybrany. Podstawa: [ADR-003](../decisions/adr-003-wybudzanie-bez-wlacznika.md), SYS-026/027 i SYS-056/057 w [zakresie systemu](../01-zakres-systemu.md).

## Zakres wariantów

- **A — zewnętrzne 12 V:** akumulator motocykla lub zasilacz warsztatowy zasila ECU/HMI; połączenie z komputerem zapewnia komunikację i detekcję podłączenia.
- **B — zasilanie serwisowe z PC:** kabel komputera zasila elektronikę ECU i HMI bez zewnętrznego 12 V, do konfiguracji, odczytu diagnostyki i aktualizacji. Wyjścia mocy pozostają wyłączone w tym trybie. Testy odbiorników wymagają właściwego zasilania 12 V.

Dla B analizujemy USB jako kandydata do przesyłania danych i energii. Interfejs serwisowy, jego lokalizacja i topologia nie zostały jeszcze wybrane.

| Kryterium | A — 12 V | B — zasilanie elektroniki z PC |
| --- | --- | --- |
| Na motocyklu, z podłączonym akumulatorem | Jeden kabel PC do obsługi ECU i HMI. | Również jeden kabel PC. |
| Na stole, bez zewnętrznego 12 V | Potrzebny zasilacz 12 V. | Bez zasilacza 12 V, jeśli port i projekt zapewnią wymagany budżet mocy. |
| Dodatkowy tor zasilania na PCB | Obsługa komunikacji i wykrywania PC przy istniejącym zasilaniu urządzeń. | Dodatkowe wejście energii, wybór źródła, ograniczanie prądu i ochrona przed zasilaniem wstecznym; możliwe dodatkowe przetwarzanie napięć. |
| HMI | Zasilanie z toru instalacji. | Trzeba zapewnić doprowadzenie energii z punktu serwisowego do HMI i uwzględnić ekran w bilansie. CAN przesyła dane; energia wymaga odpowiednich przewodów zasilających. |
| Testowanie obciążeń | Możliwe przy dostatecznej wydajności zasilania 12 V i spełnieniu warunków testowych. | Także wymaga zewnętrznego 12 V; sam tryb zasilania z PC obejmuje elektronikę. |
| Odłączenie kabla PC podczas aktualizacji | Utrata komunikacji; zasilanie 12 V może nadal podtrzymywać urządzenia. | Przy braku 12 V możliwa jednoczesna utrata komunikacji i zasilania. |

Oba warianty zachowują jeden wspólny punkt obsługi ECU/HMI. Dodatkowy zasilacz w A dotyczy przede wszystkim pracy na stole lub motocykla bez odpowiedniego zasilania z akumulatora.

## Ograniczenia mocy USB

USB 2.0 w odpowiednim skonfigurowanym stanie pozwala na pobór do 500 mA przy nominalnych 5 V, czyli 2,5 W na wejściu. Limit 900 mA / 4,5 W dotyczy odpowiednich urządzeń USB 3.x; urządzenie USB 2.0 nie uzyskuje go automatycznie przez podłączenie do portu USB 3.x. Dostępny prąd zależy od stanu urządzenia i magistrali. Źródło: [USB-IF — Peripheral Power Consumption](https://compliance.usb.org/index.asp?Format=Standard&UpdateFile=Policies).

USB-C może udostępniać 1,5 A lub 3 A przy 5 V, czyli 7,5 W lub 15 W, jeśli źródło sygnalizuje taką możliwość, a odbiornik poprawnie ją wykrywa. Do tych poziomów przy 5 V nie jest konieczne USB PD; PD stanowi osobny mechanizm uzgadniania zasilania. Sam kształt złącza nie gwarantuje dostępnej mocy. Źródło: [USB-IF — USB Type-C System Overview, slajdy 8 i 17](https://www.usb.org/sites/default/files/D1T1-2%20-%20USB%20Type-C%20System%20Overview.pdf).

To limity wejścia, przed stratami przetwornic i przewodów. Nie wybrano jeszcze procesorów, pamięci, ekranu ani podświetlenia, więc pobór ECU/HMI nie został określony. Nie potwierdzono zasilania całego zestawu z dowolnego portu. Ewentualne ograniczenie jasności ekranu lub zakresu działania wymaga jawnego określenia trybu serwisowego.

## Konsekwencje projektu i próby

Dla B należy zaprojektować rozdzielenie źródeł zasilania PC/pojazd, ochronę przed przepływem wstecznym i zasilaniem odbiorników motocykla z portu PC, oraz sprzętowe warunki wyłączenia wyjść mocy w trybie zasilania samej elektroniki. Sposób doprowadzenia energii do HMI zależy od wybranych napięć i wiązki. Dokładny wpływ na gabaryty oraz BOM poznamy po projekcie torów.

Blokada usypiania SYS-057 dotyczy zarządzania stanami urządzeń przy dostępnym zasilaniu. Zachowanie po odcięciu energii przez port PC, uśpieniu komputera lub wyjęciu kabla wymaga specyfikacji. W obu wariantach potrzebna jest procedura odzyskiwania po przerwaniu aktualizacji.

Przed zatwierdzeniem B: bilans mocy i rozruchu elektroniki, obsługiwane porty/kable, reakcja na niedostateczną moc, jednoczesne podłączenie 12 V i PC, przełączanie źródeł, brak zasilania wstecznego i próbne przerwanie aktualizacji obu urządzeń. Testów sprzętu nie wykonano.

## Rekomendacja do decyzji

Na obecnym etapie rekomendujemy **A**, ze względu na kompaktowość ECU i mniejszy zakres dodatkowego toru zasilania. W motocyklu z podłączonym akumulatorem zachowuje wygodę jednego kabla PC. Jest to ocena projektowa; brak jeszcze liczbowego porównania powierzchni PCB i kosztów.

**B** ma wartość przy częstym serwisie zestawu poza motocyklem bez zasilacza. Jeśli właściciel wybierze ten zakres, należy uwzględnić go w schemacie i PCB, a następnie zweryfikować budżet mocy obu urządzeń i wymagania wobec portu komputera.
