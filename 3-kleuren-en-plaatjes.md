### Inhoud

- [1 - Aan de slag met PuzzleScript](1-aan-de-slag-met-puzzlescript.md)
- [2 - Maak je eigen regels](2-maak-je-eigen-regels.md)
- [3 - Kleuren en plaatjes](3-kleuren-en-plaatjes.md)
- [4 - Sla je werk op](4-sla-je-werk-op.md)
- [5 - Nieuwe voorwerpen en winnen](5-nieuwe-voorwerpen-en-winnen.md)
- [6 - Geluid](6-geluid.md)
- [7 - Een woord vormen](7-een-woord-vormen.md)
- [8 - Er kan nog veel meer](8-er-kan-nog-veel-meer.md)

# 3 - Kleuren en plaatjes

## Kies je kleuren en teken (hele kleine) plaatjes

PuzzleScript ziet er heel eenvoudig uit: elk vakje heeft maar 5 x 5 pixels. Dat is expres, omdat het belangrijker is om snel ideeen uit te proberen dan om het direct mooi te maken. Als je helemaal tevreden bent met je ontwerp, kun je het uitwerken in een andere programmeertaal met mooie graphics.

Natuurlijk is het wel belangrijk dat je in PuzzleScript duidelijk ziet wat wat is, anders wordt testen wel erg moeilijk. Daarom kun je simpele plaatjes maken in het `OBJECTS` (voorwerpen) gedeelte.

In dit gedeelte bepaal je welke voorwerpen je spel heeft en hoe ze er uit zien. Hier is bijvoorbeeld de `Speler`:

```
Speler S
(Het figuurtje dat je bestuurt)
darkgray brown lightblue blue
.000.
.111.
22222
.333.
.3.3.
```

Zoals je ziet staat op de eerste regel de naam van het voorwerp, in dit geval `Speler`, gevolgd door de letter die je hiervoor wilt gebruiken in je levels (`S`). De tweede regel is optioneel; alles wat tussen haakjes staat is commentaar in PuzzleScript. Op de volgende regel kun je een aantal kleuren zetten met spaties ertussen. Daarna volgen vijf regels met 5 tekens per regel die de pixels van het plaatje vormen. Daarbij is `0` de eerste kleur, `1` de tweede, enzovoorts. `.` betekent "geen kleur".

(je kunt de laatste 5 regels ook weglaten, zoals bijv. bij `Achtergrond`. Dan krijg je alleen een gekleurd blokje te zien)

Deze kleurnamen kun je gebruiken: `black`, `white`, `lightgray`, `gray`, `darkgray`, `red`, `darkred`, `lightred`, `brown`, `darkbrown`, `lightbrown`, `orange`, `yellow`, `green`, `darkgreen`, `lightgreen`, `blue`, `lightblue`, `darkblue`, `purple`, `pink`, `transparent`. Ook hex-codes (als je die toevallig kent van CSS) werken, zoals `#ffff00`.

### Wat je kunt proberen ###
- Pas de kleuren of de 5x5 pixel plaatjes aan zoals jij wilt.

## Als je je werk niet kwijt wilt raken, bekijk dan snel [de volgende stap! >>](4-sla-je-werk-op.md)