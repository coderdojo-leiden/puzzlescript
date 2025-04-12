**Inhoud**

- [(terug naar het begin)](index.md)
- [8 - Waarmee wil je verder?](8-waarmee-verder.md)
- [9 - Spelers met karakter](9-spelers-met-karakter.md)
- [10 - Animatie](10-animatie.md)
- [11 - Actie](11-actie.md)
- [12 - Grotere levels en editor](12-grote-levels-editor.md)
- [13 - Op avontuur!](13-op-avontuur.md)
- [14 - Meer voorbeelden](14-meer-voorbeelden.md)

# 11 - Actie

Een PuzzleScript-level verandert meestal alleen wanneer de speler een stap zet. Maar soms wil je dat ook iets gebeurt als de speler stilstaat.

## Rollende bal

Stel dat we willen dat de speler een bal kan duwen, en die bal begint dan te bewegen en stopt pas als hij ergens tegenaan botst.

We beginnen heel eenvoudig:

```
========
OBJECTS
========

Background .
Darkgreen

Muur #
Darkgray

Speler S
Blue Black
.000.
01010
00000
.000.
00.00

StilstaandeBal *
Orange White
.000.
01000
00000
00000
.000.

=======
LEGEND
=======

Player = Speler

Object = StilstaandeBal or Muur or Player

=======
SOUNDS
=======

================
COLLISIONLAYERS
================

Background
Object

======
RULES
======

(Zet Bal in beweging)
[ > Player | StilstaandeBal ] -> [ Player | > StilstaandeBal ] SFX0

==============
WINCONDITIONS
==============


=======
LEVELS
=======

##########
#........#
#.*......#
#.....*..#
#........#
#.*......#
#.s......#
##########

```

Als je deze code draait, zie je dat de speler de bal een vakje kan duwen, maar de bal stopt dan weer. We zouden willen dat de bal door blijft rollen.

Het lastige aan PuzzleScript is dat er geen manier is om de beweegrichting van de bal te onthouden (in een variabele of iets dergelijks).

De oplossing is om extra objecten aan te maken, een voor elke richting. Ze krijgen allemaal hetzelfde plaatje:

```
BalOmhoog
Orange White
.000.
01000
00000
00000
.000.

BalRechts
Orange White
.000.
01000
00000
00000
.000.

BalOmlaag
Orange White
.000.
01000
00000
00000
.000.

BalLinks
Orange White
.000.
01000
00000
00000
.000.
```

We passen de `LEGEND` ook aan:

```
=======
LEGEND
=======

Player = Speler

(De vier richtingen voor een bewegende bal)
BewegendeBal = BalOmhoog or BalRechts or BalOmlaag or BalLinks

(En bal staat stil of beweegt)
Bal = StilstaandeBal or BewegendeBal

Object = Bal or Muur or Speler
```

Het spel werkt nu nog steeds hetzelfde, want we hebben nog niets gedaan met onze nieuwe objecten.

We zullen regels moeten toevoegen om de `StilstaandeBal` om te zetten in een van de vier `BewegendeBal` objecten.

Als je een bal naar rechts rolt, heb je deze regel nodig:

    [ RIGHT StilstaandeBal ] -> [ RIGHT BalRechts ]

Hier staat: "vervang een `StilstaandeBal` die naar rechts beweegt door een `BalRechts` die naar rechts beweegt".

Nu verandert de `StilstaandeBal` dus in een `BalRechts`, maar hij blijft nog niet doorrollen. Maak daarvoor deze regel aan:

    [ BalRechts ] -> [ RIGHT BalRechts ]

Oftewel: "Een `BalRechts` moet altijd naar rechts bewegen."

We hebben nog 1 regel nodig: als een `BewegendeBal` ergens tegenaan botst, willen we dat het weer een gewone `StilstaandeBal` wordt:

    [ > BewegendeBal | Object ] -> [ StilstaandeBal | Object ]

Een ding wat we ook niet moeten vergeten, is om van ons PuzzleScript spel een "realtime" spel te maken. Dat betekent dat de regels ook uitgevoerd worden als de speler stilstaat. Zet bovenin je code (waar ook `title` staat) deze regel:

    realtime_interval 0.2

(Je kunt grotere of kleinere getallen gebruiken, bijvoorbeeld 0.3 of 0.15, om het spel sneller of langzamer te laten gaan)

Probeer het eens uit. Wat gebeurt er nu als je een bal naar rechts duwt?

Kun je de regels voor de andere richtingen (links=`LEFT`, omhoog=`UP`, omlaag=`DOWN`) ook toevoegen, zodat je de bal in elke richting kan rollen?

Als je hier een echt spel van wilt maken, heb je natuurlijk nog een `WINCONDITION` nodig. Bijvoorbeeld dat er gaten zijn en je <a target='_blank' href='https://www.puzzlescript.net/editor.html?hack=2629d8f2cb707fa72f5ede9f9d7b420b'>alle ballen (of pompoenen in dit voorbeeld) in een gat moet rollen</a>. Je kunt zelf vast nog wel andere wincondities bedenken!

## Kunstmatige intelligentie...?

Laten we nu een uit zichzelf bewegend dier maken. Bijvoorbeeld een vleermuis die in het rond vliegt, en jouw hulp nodig heeft om wat sappige vliegen te vangen.

> **WIST JE DAT?**<br/>
> Vleermuizen kunnen in het aardedonker rondvliegen zonder ergens tegenaan te botsen. Dat doen ze door hele hoge piepgeluiden te maken en met hun grote oren te luisteren naar de echo. Zo 'horen' ze waar ze wel en niet kunnen vliegen, en zelfs waar insecten vliegen die ze kunnen vangen.

We beginnen met een aantal objecten:

```
title Vleermuis op vliegenjacht

(regels ook uitvoeren als de speler stilstaat)
realtime_interval 0.1

========
OBJECTS
========

Background .
Darkgreen

Muur #
Darkgray

Speler S
Blue Black
.000.
01010
00000
.000.
00.00

Vleermuis L
Black
0.0.0
00000
00000
0.0.0
..0..

Vlieg `
Black White
.....
.1.1.
..0..
.....
.....


=======
LEGEND
=======

Player = Speler
Object = Muur or Speler or Vleermuis

=======
SOUNDS
=======

Vlieg Destroy 41496107
EndLevel 84805900

================
COLLISIONLAYERS
================

Background
Vlieg
Object

======
RULES
======

(Vleermuis eet vlieg)
[ Vleermuis Vlieg ] -> [ Vleermuis ]

==============
WINCONDITIONS
==============

no Vlieg

=======
LEVELS
=======

message Laat de vleermuis alle vliegen opeten

####.#####.
#..#.#.`.#.
#..###.l.#.
#.......`#.
#..#.....#.
#..#.....#.
#.`#.....#.
####..####.
#..s..#....
#`....#....
#######....


###########
#`.......`#
#.........#
#..`...`..#
#.........#
#....l....#
#.........#
#..`...`..#
#...s.....#
#`.......`#
###########

```

Als je dit spel draait, beweegt de vleermuis nog niet. Om 'm te laten bewegen kunnen we dezelfde aanpak volgen als bij het rollen van de bal, maar laten we het dit keer net iets anders doen, met een *hulpobject* dat de richting onthoudt. Later leggen we uit waarom dit handig kan zijn.

Voeg de volgende vier hulpobjecten toe aan `OBJECTS`:

```
(vier hulpobjecten die de beweegrichting onthouden)

BeweegOmhoog
transparent

BeweegRechts
transparent

BeweegOmlaag
transparent

BeweegLinks
transparent
```

(`transparent` betekent dat deze objecten doorzichtig (en dus onzichtbaar) zijn)

Voeg dan deze regel toe aan de `LEGEND`, zodat we een groep `BeweegRichting` hebben:

    BeweegRichting = BeweegOmhoog or BeweegRechts or BeweegOmlaag or BeweegLinks

`BeweegRichting` komt op een eigen laag in het spel, omdat die op hetzelfde vakje als de vleermuis moet kunnen staan. Voeg de laag toe aan `COLLISIONLAYERS`:

```
================
COLLISIONLAYERS
================

Background
BeweegRichting
Vlieg
Object
```

Nu moeten we de regels gaan bepalen. Laten we zeggen dat de vleermuis altijd naar rechts begint te bewegen:

```
(Laat een stilstaande vleermuis bewegen)
[ Vleermuis no BeweegRichting ] -> [ Vleermuis BeweegRechts ]
```

Hier staat dus: "Een vleermuis die nog geen `BeweegRichting` heeft, krijgt het hulpobject `BeweegRechts` in z'n vakje.

Op zichzelf doet dit nog niets (het hulpobject is onzichtbaar en we hebben nog geen regel die de vleermuis echt in beweging zet). Om de vleermuis in beweging te brengen, voegen we een regel toe:

```
(Zet de bewegingsrichting van de vleermuis op basis van het hulpobject)
[ Vleermuis BeweegOmhoog ] -> [ UP Vleermuis UP BeweegOmhoog ]
```

Zoals je ziet staat er aan de rechterkant van de `->` TWEE keer `UP`; dat is omdat niet alleen de `Vleermuis` maar ook de `BeweegRichting` (in dit geval `BeweegOmhoog`) mee moet bewegen.

Als je het spel nu probeert, beweegt de vleermuis naar rechts tot die iets raakt en stopt dan. Als we de vleermuis rondjes willen laten vliegen, zal hij bijvoorbeeld telkens rechtsaf moeten slaan als hij iets raakt. Voeg dus de volgende regel toe:

    RIGHT [ RIGHT Vleermuis | Object ] -> [ DOWN Vleermuis DOWN BeweegOmlaag | Object ]

Dit is een behoorlijk ingewikkelde regel, zoals je kunt zien. We gaan er stap voor stap doorheen:

- De eerste `RIGHT` zorgt ervoor dat deze regel maar in 1 richting bekeken wordt; dus alleen voor een `Vleermuis` met een `Object` rechts ervan
- De tweede `RIGHT` zegt dat de `Vleermuis` naar rechts aan het bewegen moet zijn. Oftewel: hij staat op het punt om tegen het `Object` te botsen.
- Aan de rechterkant van het pijltje `->` staat `BeweegOmlaag` zodat dat het nieuwe richting-hulpobject wordt.
- De eerste keer `DOWN` zorgt ervoor dat de `Vleermuis` omlaag gaat bewegen.
- De tweede keer `DOWN` zorgt ervoor dat het hulpobject `BeweegOmlaag` tegelijk met de vleermuis omlaag beweegt, zodat ze bij elkaar blijven.

Als je het spel draait, zul je zien dat de vleermuis nu eerst naar rechts beweegt, en als hij ergens tegenaan botst, beweegt hij verder naar beneden.

Kun jij nu de andere regels invullen, zodat de vleermuis echt in rondjes vliegt?

Kijk <a target='_blank' href='https://www.puzzlescript.net/editor.html?hack=89bc7e7e1785814d2605c210ef86c8bf'>hier</a> als je er niet uitkomt. Als het gelukt is, kun je met de speler het pad van de vleermuis blokkeren en de vleermuis zo helpen om alle vliegen op te eten.

> **Waarom gebruikten we een losse `BeweegRichting`**? <br/><br/>
> Bij de rollende bal hadden we gewoon vier objecten die de rollende bal voorstelden. Waarom gebruiken we nu dan hulpobjecten op een aparte laag en niet `VleermuisLinks`, `VleermuisOmhoog`, etc.?<br/><br/>
> De aanpak met hulpobjecten is inderdaad niet nodig, maar kan wel handig zijn als je het nog mooier wilt maken. Bijvoorbeeld als je verschillende soorten wezens wilt maken die allemaal in een rondje bewegen, maar sommige zijn vriendelijk en anderen zijn gevaarlijk. Je hoeft dan niet van elk wezen vier versies te maken, plus een heleboel regels voor elk soort wezen, maar kunt dezelfde hulpobjecten hergebruiken voor elk wezen.

## Je kunt ook [grotere levels maken! >>](12-grote-levels-editor.md)