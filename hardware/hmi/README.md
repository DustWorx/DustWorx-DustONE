# Sprzęt HMI

Miejsce na edytowalne schematy i PCB, BOM oraz kontrolowane eksporty produkcyjne HMI na kierownicy.

Wymagania bazowe: komunikacja z ECU po CAN, fizyczne przyciski i ekran bez dotyku. Parametry ekranu, interfejsów wejściowych i zasilania oraz komponenty pozostają do ustalenia.

Narzędzie EDA: **Autodesk Fusion Electronics**, płatna subskrypcja właściciela projektu.

Wymagania i otwarte decyzje: [zakres systemu](../../docs/01-zakres-systemu.md).

SYS-255 zachowuje przyjęte funkcje i interfejsy HMI; dodatkowe zewnętrzne porty do nieokreślonych urządzeń są poza zakresem. Wewnętrzne zasoby, magistrale i punkty testowe ocenić w architekturze; ważne układy wybrać wspólnie. [Zakres i plan weryfikacji F04](../../docs/requirements/f04-akcesoria-i-io.md#zakres-zewnętrznych-portów).

SYS-256 dodaje wybudzanie HMI przez ECU po nowym użyciu dowolnego hamulca. Tor i czasy przekazania wybudzenia pozostają do projektu; gotowość lub sprawność HMI nie warunkują obsługi światła hamowania przez ECU. [Ustalenie i plan próby F04](../../docs/requirements/f04-akcesoria-i-io.md#wybudzanie-przez-hamulce).

SYS-257 wymaga rozróżnienia żądania awaryjnych od pojedynczego kierunkowskazu w obsłudze HMI. W oszczędzaniu dostępne są awaryjne, a pojedyncza strona i klakson niedostępne; ECU pozostaje wykonawcą żądań i źródłem statusów. Sposób obsługi i stany awaryjnych pozostają do ustalenia w F04/projekcie, bez wyboru nowego przycisku ani portu. [Zakres F04](../../docs/requirements/f04-akcesoria-i-io.md#odbiorniki-w-oszczędzaniu-energii).
