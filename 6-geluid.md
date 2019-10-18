### Inhoud

- [Inleiding](index.md)
- [1 - Aan de slag met PuzzleScript](1-aan-de-slag-met-puzzlescript.md)
- [2 - Maak je eigen regels](2-maak-je-eigen-regels.md)
- [3 - Kleuren en plaatjes](3-kleuren-en-plaatjes.md)
- [4 - Sla je werk op](4-sla-je-werk-op.md)
- [5 - Nieuwe voorwerpen en winnen](5-nieuwe-voorwerpen-en-winnen.md)
- [6 - Geluid](6-geluid.md)
- [7 - Een woord vormen](7-een-woord-vormen.md)
- [8 - Meer voorbeelden](8-meer-voorbeelden.md)
- [9 - Nog niet uitgepuzzeld?](9-er-kan-nog-veel-meer.md)

# 6 - Geluid

## Maak zelf geluiden en zet ze in het spel

In het voorbeeldspel staan al geluidjes voor het duwen van een kistje en het winnen van een level, maar je kunt deze geluiden aanpassen en meer geluiden toevoegen als je wilt.

PuzzleScript kan willekeurige geluidjes voor je maken, tot je er een vindt die je wilt gebruiken. Klik op de knopjes rechts in het midden om allerlei soorten geluidjes te maken:

![Knopjes voor geluiden](images/knoppen-geluidjes.png)

Iedere keer dat je op een knopje drukt, verschijnt een nummer in het gedeelte onder de knopjes. Je kunt op het nummer klikken om het geluidje nog eens te horen, en je kunt het nummer overnemen in je code om het geluid in je spel te gebruiken.

Geluiden zet je in het `SOUNDS` gedeelte van het programma. Dit ziet er nu zo uit:

```
=======
SOUNDS
=======

Kistje Move 975507
EndLevel 74356503
```

De eerste regel koppelt een geluidje aan het bewegen (Engels: `Move`) van een kistje. De tweede regel is het geluid dat je hoort als je het level wint.

Stel dat we een geluid willen koppelen aan het verdwijnen van drie kistjes. Dit doen we door het geluid aan de juiste regel te koppelen. Kies eerst een geluid dat je wilt gebruiken en voeg dat als volgt toe aan het `SOUNDS` gedeelte:

```
SFX0 70755702   (vervang het nummer door jouw eigen geluid!)
```

Je kunt het geluid wat we `SFX0` hebben genoemd nu afspelen door `SFX0` achteraan de kistjes-regel toe te voegen:

```
late [ Kistje | Kistje | Kistje ] -> [ | | ] SFX0
```

Je kunt ook `SFX1`, `SFX2`, etc. gebruiken als je meer geluiden aan regels wilt koppelen.

### Wat je kunt proberen ###
- Kies als je wilt andere geluiden voor het bewegen van een kistje of het winnen van het level.
- Als je in de vorige stap `Muntje` hebt toegevoegd: speel een geluid als je het muntje oppakt. Gebruik <code>Muntje Destroy <em>nummer</em></code> (destroy = vernietig, want als je het muntje oppakt verdwijnt het in feite)
- Speel voor elke stap die de speler zet een geluid.
  <details><summary>HINT</summary>Gebruik <code>Speler Move</code></details>
- Speel verschillende geluiden als de speler een kistje duwt of trekt.
  <details><summary>HINT</summary>Verander de regel <code>Kistje Move 975507</code> in <code>SFX1 975507</code> en voeg nog een SFX2 toe en koppel deze aan de duw- en trekregels net zoals hierboven met SFX0.</details>
- Speel een geluid als de speler probeert te bewegen of duwen maar het lukt niet (bijvoorbeeld omdat die tegen een muur aanloopt). Gebruik hiervoor in plaats van <code>Move</code> het woord <code>CantMove</code> ("can't move" = "kan niet bewegen").

Alle mogelijkheden van geluiden vind je <a href='https://www.puzzlescript.net/Documentation/sounds.html' target='_blank'>hier</a> (in het Engels).

## Een level waar je je eigen naam moet maken? Check [de volgende stap! >>](7-een-woord-vormen.md)