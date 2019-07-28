### Inhoud

- [1 - Aan de slag met PuzzleScript](1-aan-de-slag-met-puzzlescript.md)
- [2 - Maak je eigen regels](2-maak-je-eigen-regels.md)
- [3 - Kleuren en plaatjes](3-kleuren-en-plaatjes.md)
- [4 - Sla je werk op](4-sla-je-werk-op.md)
- [5 - Nieuwe voorwerpen en winnen](5-nieuwe-voorwerpen-en-winnen.md)
- [6 - Geluid](6-geluid.md)
- [7 - Een woord vormen](7-een-woord-vormen.md)
- [8 - Er kan nog veel meer](8-er-kan-nog-veel-meer.md)

# 7 - Een woord vormen

Stel dat we het spel willen aanpassen zodat we niet meer saaie kistjes op een rijtje zetten, maar letters die een woord vormen. Misschien wel je eigen naam! In dit voorbeeld gebruiken we het woord `CODE`.

We moeten eerst voor elke letter een voorwerp toevoegen in het `OBJECTS` gedeelte:

```
LetterC C
Yellow Black
01110
10000
10000
10000
01110

LetterO O
Blue Black
01100
10010
10010
10010
01100

LetterD D
Green Black
11100
10010
10010
10010
11100

LetterE E
Red Black
11110
10000
11100
10000
11110
```

We willen dat al deze letters zich gedragen als een `Kistje`. Om het makkelijk voor onszelf te maken hernoemen we eerst in `OBJECTS` het `Kistje` naar `GewoonKistje`:

```
GewoonKistje @
(Een kistje dat de speler kan duwen)
White Gray DarkGray
00001
01112
01112
01112
12222
```

En dan voegen we deze regels toe bovenaan `LEGEND`:

```
(Alle voorwerpen die je kunt schuiven)
Kistje = GewoonKistje or LetterC or LetterO or LetterD or LetterE
```

Hiermee hebben we een groep voorwerpen gemaakt die `Kistje` heet en `GewoonKistje` plus onze `Letter`s bevat. Omdat onze bestaande regels allemaal `Kistje` gebruiken, werken ze nu voor deze hele groep "schuifbare voorwerpen".

Natuurlijk willen we niet dat drie *letters* op een rij ook altijd verdwijnen, dus moeten we wel die regel aanpassen zodat die alleen werkt voor `GewoonKistje`:

```
late [ GewoonKistje | GewoonKistje | GewoonKistje ] -> [ | | ]
```

Tot slot willen we zorgen dat de vier letters van het woord `CODE` verdwijnen (of veranderen in muntjes) als ze in de juiste volgorde gezet worden. We kunnen hiervoor de regel voor drie kistjes kopi&euml;ren en aanpassen. Lukt het je om de regel zelf aan te passen? Als het niet lukt, bekijk dan de hint.

<details><summary>HINT</summary><code>late [ LetterC | LetterO | LetterD | LetterE ] -> [ | | | ]
</code></details>

Test of alles goed werkt door een level te ontwerpen waarin je de letters C, O, D en E tot een woord moet vormen. Bijvoorbeeld:

```
#########
#.......#
#.S.e...#
#..c.d..#
#...o..##
#.....##.
#######..
```

### Wat je kunt proberen ###
- Duw de letters eens in volgorde `EDOC`, dus `CODE` gespiegeld. Wat gebeurt er? Hoe komt dat, denk je?<br/>
  Als je geen richting opgeeft, werken regels in alle richtingen. Zet `RIGHT` voor de regel die het woord `CODE` herkent als je wilt dat het alleen van links naar rechts werkt.
- **UITDAGING**: Je kunt nu maar 1 kistje tegelijk duwen. Stel dat je wilt dat je wel meerdere kistjes tegelijk kunt duwen. Heb je enig idee wat voor regel je daarvoor zou moeten toevoegen?
  <details><summary>HINT</summary>Je zou een regel moeten toevoegen die zegt dat het ene kistje het andere kistje in beweging kan brengen, net als een speler een kistje in beweging kan brengen. Dan kan de speler het eerste kistje in beweging brengen, dat kistje kan het volgende kistje in beweging brengen, enzovoorts.</details>

### Meer idee&euml;n?

Je kunt vast zelf nog meer voorwerpen en regels bedenken om een leuk puzzelspel mee te maken. Hier zijn nog een paar suggesties om je op gang te helpen:

- Voeg voorwerpen `Sleutel` en `Schatkist` toe. De speler kan de sleutel duwen net als een kistje. Als de sleutel naast de schatkist staat, gaat de schatkist open (verandert in een muntje). Alle schatkisten moeten geopend worden om het level te winnen.
- Maak schuifbare voorwerpen met verschillende kleuren, bijvoorbeeld en rode en een blauwe ballon. Als een rode ballon een blauwe ballon raakt, wordt de blauwe ballon ook rood. Het doel is om alle ballonnen rood te maken.
- Maak een voorwerp `Schaap`. De `Speler` is de herdershond; zodra die naast een schaap staat, vlucht het schaap een vakje weg van de speler. Doel is weer om drie schapen op een rij te krijgen. (als voor een regel een vakje per se leeg moet zijn, gebruik dan `no Voorwerp` of `no Object`)
  <details><summary>HINT</summary><code>[ Speler | Schaap | no Voorwerp ] -> [ Speler | | Schaap ]</code></details>
- Maak een spel waarbij er twee `Speler`s per level zijn. Als twee spelers elkaar raken, verdwijnen ze en kun je het level niet meer oplossen. Je moet het level dus oplossen (bijv. 3 kistjes op een rij krijgen) zonder de spelers elkaar te laten raken.

## Is dat alles wat je met PuzzleScript kan? [Nee, er is nog veel meer! >>](8-er-kan-nog-veel-meer.md)
