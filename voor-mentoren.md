# PuzzleScript voor mentoren

## Wat is PuzzleScript?

Met PuzzleScript kun je eenvoudig logische puzzelspellen maken waarbij je een figuurtje bestuurt en bijvoorbeeld kistjes kunt duwen.

Het is volledig source code gebaseerd. Op [puzzlescript.net](https://www.puzzlescript.net/) is een soort IDE met voorbeeldspellen die je kunt bekijken en aanpassen.

Zie ook de [offici&euml;le documentatie](https://www.puzzlescript.net/Documentation/documentation.html).

## Voorbeeld

PuzzleScript toont als eerste voorbeeld een heel simpel spel, waarbij je kistjes moet duwen (Soko Ban). Hieronder bekijken we de code van het spel per sectie.

Bovenin de file staat de "prelude" met wat metadata. In deze sectie kunnen ook een aantal speciale opties ingesteld worden; daarover later meer.

```puzzlescript
title Simple Block Pushing Game
author David Skinner
homepage www.puzzlescript.net
```

Hierna worden de graphics van de objecten gedefinieerd. `.` is doorzichtig, `1` is de eerste kleur, etc.

```puzzlescript
========
OBJECTS
========

Background
lightgreen green
11111
01111
11101
11111
10111

Target
darkblue
.....
.000.
.0.0.
.000.
.....

Wall
brown darkbrown
00010
11111
01000
11111
00010

Player
black orange white blue
.000.
.111.
22222
.333.
.3.3.

Crate
orange
00000
0...0
0...0
0...0
00000
```

De volgende sectie koppelt tekens zoals `.` en `#` aan de objecten, zodat we daar levels mee kunnen tekenen.

`@ = Crate and Target` wil zeggen dat als je `@` in een level zet, op die plek zowel een `Target` als een `Crate` komen te staan.

Je kunt in deze sectie ook groepen objecten definieren, bijvoorbeeld `Animal = Dog or Cat`. Vervolgens kun je `Animal` dan in een rule gebruiken. (in dit voorbeeld niet gebruikt)

```puzzlescript
=======
LEGEND
=======

. = Background
# = Wall
P = Player
* = Crate
@ = Crate and Target
O = Target
```

De volgende sectie koppelt geluiden aan gebeurtenissen zoals `Crate move`, `Player move up` of `Player CantMove`. In de IDE kun je met de knopjes rechts in het midden random geluiden maken en het bijbehorende nummer naar je code kopiëren.

```puzzlescript
=======
SOUNDS
=======

Crate move 36772507
```

De volgende sectie bepaalt welke objecten met elkaar moeten botsen en welke niet. Ook bepaalt het de volgorde waarin objecten getekend worden.

`Background` moet sowieso altijd bestaan.

We willen dat we een `Crate` bovenop een `Target` kunnen zetten. Ze moeten dus niet botsen, dus ze staan elk op een eigen laag. `Player`, `Wall` en `Crate` kunnen natuurlijk geen vakje delen en moeten dus wel met elkaar botsen.

```puzzlescript
================
COLLISIONLAYERS
================

Background
Target
Player, Wall, Crate
```

Nu volgen de echte regels van het spel. Elke regel herkent een patroon en vervangt het door iets anders.

Hieronder betekent `[ > Player | Crate ] -> [ > Player | > Crate ]` dat als de speler tegen een kistje duwt, het kistje in beweging komt. Straks meer over regels.

```puzzlescript
======
RULES
======

[ > Player | Crate ]  ->  [ > Player | > Crate ] 

```

Wanneer heb je gewonnen? Hieronder staat `all Target on Crate`, dus als alle kistjes op een doelvakje staan. Andere condities zijn bijvoorbeeld `no Crate` (geen kistjes meer in het level) of `some Gold` (er is ergens goud in het level). Aan alle wincondities moet voldaan zijn.

```puzzlescript
==============
WINCONDITIONS
==============

all Target on Crate
```

Tot slot volgen de levels van het spel. Deze teken je met de tekens die je bij `LEGEND` aan objecten gekoppeld hebt.

```puzzlescript
=======
LEVELS
=======

####..
#.O#..
#..###
#@P..#
#..*.#
#..###
####..

######
#....#
#.#P.#
#.*@.#
#.O@.#
#....#
######
```

## Regels

De regels zijn het lastigste onderdeel van PuzzleScript. Daarom hier een lijst voorbeelden met uitleg.

### Duw kistje

    [ > Speler | Kistje ]  ->  [ > Speler | > Kistje ] 

Dit is een van de eenvoudigste regels. `> Speler` betekent "bewegende speler", of eigenlijk "speler probeert te bewegen".

`[ > Speler | Kistje ]` betekent "speler probeert in de richting van een kistje te lopen".

`->` betekent "als de situatie links optreedt, vervang die dan door de situatie rechts".

`[ > Speler | > Kistje ]` is dus de nieuwe situatie: speler en kistje proberen allebei te bewegen. Oftewel, de speler duwt het kistje.

Als een ander voorwerp het kistje blokkeert (d.w.z. op dezelfde `LAYER` staat), zullen noch het kistje noch de speler bewegen.


### 3 kistjes op een rij verdwijnen

    late [ Kistje | Kistje | Kistje ] -> [    |    |    ]

Als er 3 kistjes op een rij staan, verdwijnen ze met deze regel.

Er staat `late` voor omdat we willen dat deze regel pas wordt uitgevoerd nadat de speler (en voorwerpen) bewogen hebben.

Zonder `late` zou je 3 kistjes op een rij zetten en zou er eerst niets gebeuren. Pas als je daarna nog een stap zet, zou de "3 op een rij" regel uitgevoerd worden.

### Speler wisselt met kistje

    [ > Speler | Kistje ] -> [ Kistje | Speler ]

Als een speler richting een kistje beweegt, wisselen ze van plek.

### Speler trekt een kistje

    [ < Speler | Kistje ] -> [ < Kistje | < Speler ]

Je kunt deze regel natuurlijk ook combineren met het duwen als je wilt.

### Meerdere kistjes duwen

    [ > Speler | Kistje ]  ->  [ > Speler | > Kistje ]
    [ > Kistje | Kistje ]  ->  [ > Kistje | > Kistje ]

Door ook een regel toe te voegen die zegt dat het ene kistje het andere kan duwen, kan de speler meerdere kistjes tegelijk duwen.

Hetzelfde effect kun je bereiken door in de `LEGEND` sectie een groep aan te maken: `Duwer = Speler or Kistje`.

Gebruik dan deze regel:

    [ > Duwer | Kistje ] -> [ > Duwer | > Kistje ]

### Plakkerig kistje

    [ MOVING Kistje | Kistje ] -> [ MOVING Kistje | MOVING Kistje ]

`MOVING` kan in elke richting zijn, dus niet per se richting het andere kistje. Nu plakken alle kistjes aan elkaar en bewegen tegelijk dezelfde kant op.

### Een woord vormen

Maak objecten `LetterC`, `-O`, `-D` en `-E` en zorg dat je ze allemaal kunt schuiven (gebruik een groep `Letter`). Voeg dan deze regel toe:

    late RIGHT [ LetterC | LetterO | LetterD | LetterE ] -> [ | | | ]
    late DOWN  [ LetterC | LetterO | LetterD | LetterE ] -> [ | | | ]

Als je de letters zo schuift dat er CODE staat (van links naar rechts of van boven naar beneden, verdwijnen ze.)

Als je niet wilt dat het woord verdwijnt, maar de speler gewoon wint als ze het woord weten te vormen, maak je onzichtbaar object in de `OBJECTS` sectie:

    Trofee
    transparent

Zet de `Trofee` op een eigen laag, zodat die samen met een letter in een vakje kan staan.

Pas dan de regel aan:

    late RIGHT [ LetterC | LetterO | LetterD | LetterE ] -> [ LetterC Trofee | LetterO | LetterD | LetterE ]

In de sectie `WINCONDITIONS` zet je dan `some Trofee` (er bestaat ergens een Trofee in het level).

### Speler jaagt schapen op

Zorg dat in de `LEGEND` sectie `Voorwerp = Speler or Schaap` staat.

    [ Speler | Schaap | no Voorwerp ] -> [ Speler | | Schaap ]

Als de speler naast een schaap staat, en het vakje ernaast is leeg (bevat geen speler of schaap), rent het schaap naar het lege vakje.

### Spooky action at a distance

    [ Spook | ... | Speler |  ] -> [ > Spook | ... | Speler ]

Als het spook in dezelfde rij of kolom als de speler zit, doet het een stap richting de speler.

Let op, door de volgorde waarin regels worden toegepast werkt dit pas 1 "beurt" nadat de speler op 1 lijn met het spook is gekomen.

Je kunt dit oplossen met `late` regels (die na het bewegen van de speler uitgevoerd worden) en een onzichtbaar object `Temp` (zie eerder):

    (Spook doet een stap richting de speler)
    late [ Spook | no Spook | ... | Speler ] -> [ | Temp | ... | Speler ]
    late [ Temp ] -> [ Spook ]

We vervangen `Spook` tijdelijk door `Temp`. De reden is dat anders de 1e regel meerdere keren uitgevoerd wordt, zodat het spook direct naast de speler staat. Met deze aanpassing neemt het spook 1 stap per keer.

### Twee dimensies

PuzzleScript werkt vooral met voorwerpen op een rijtje; het herkennen van een vierkant van twee bij twee kistjes is lastig, maar wel mogelijk.

Net als voor veel PuzzleScript problemen maken we weer gebruik van een tijdelijk onzichtbaar voorwerp, in dit geval `TweeKistjes`.

    (Herken 2 kistjes naast elkaar)
    late RIGHT [ Kistje | Kistje ] -> [ Kistje TweeKistjes | Kistje ]

    (Herken 2 rijtjes kistjes)
    late DOWN  [ TweeKistjes | TweeKistjes ] -> WIN

    (Verwijder hulpobjecten weer als we niet gewonnen hebben)
    late [ TweeKistjes ] -> [ ]

### Voorwerp dragen

De speler kan voorwerpen dragen door ze aan een groep `Draagbaar` toe te voegen en op een aparte laag te zetten. Deze regel zorgt dat de speler het voorwerp meedraagt:

    (Zodra de speler op het vakje van een draagbaar voorwerp staat, moet dat voorwerp altijd met de speler meebewegen)
    [ > Speler Draagbaar ] -> [ > Speler > Draagbaar ]

En als je wilt dat de speler het voorwerp kan neerzetten door op de actieknop (`X`) te drukken:

    (Zet draagbaar voorwerp neer op een lege plek naast speler)
    [ ACTION Speler Draagbaar | no Object no Draagbaar ] -> [ Speler | Draagbaar ]

### Knop opent deur

Als je wilt dat een knop een deur ergens in het level opent als de speler of een ander `Voorwerp` er op staat:

    (Open deur als er een voorwerp op de knop staat, sluit 'm anders)
    late [ Knop Voorwerp ] [ Deur ] -> [ Knop Voorwerp ] [ DeurOpen ]
    late [ Knop no Voorwerp ] [ DeurOpen ] -> [ Knop ] [ Deur ]

De knop moet op zijn eigen layer staan.

De knop en de deur hoeven niet in dezelfde rij of kolom van het level te staan; zoals je ziet kun je ook

    [ ] [ ]

patronen maken die verschillende plekken in het level aangeven.