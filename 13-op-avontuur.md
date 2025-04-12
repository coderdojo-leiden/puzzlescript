**Inhoud**

- [(terug naar het begin)](index.md)
- [8 - Waarmee wil je verder?](8-waarmee-verder.md)
- [9 - Spelers met karakter](9-spelers-met-karakter.md)
- [10 - Animatie](10-animatie.md)
- [11 - Actie](11-actie.md)
- [12 - Grotere levels en editor](12-grote-levels-editor.md)
- [13 - Op avontuur!](13-op-avontuur.md)
- [14 - Meer voorbeelden](14-meer-voorbeelden.md)

# 13 - Op avontuur!

In het [vorige hoofdstuk](13-grote-levels-editor.md) heb je gezien hoe je grotere levels kunt maken. Maar zo'n wijde wereld moet natuurlijk wel gevuld worden met interessante mogelijkheden. Daar gaan we nu mee aan de slag.

Je kunt <a target='_blank' href='https://www.puzzlescript.net/editor.html?hack=637f03e3c4899dec47f2d98b868a80db'>dit spel</a> met meerdere 'kamers' bijvoorbeeld als beginpunt gebruiken.

## Gesprekjes

Het is in een avonturenspel natuurlijk leuk als je andere wezens tegenkomt waar je mee kunt praten.

Misschien komen we wel een konijn tegen:

```
Konijn K
Gray Black
.0.0.
00000
01010
.000.
00000
```

Vergeet niet om het `Konijn` ook toe te voegen aan de `Object` groep onder `LEGEND`, en natuurlijk ergens in je wereld een konijn te plaatsen (met de letter `K` in de code, of via de editor).

Het konijn doet natuurlijk nog niets tot we er een regel voor aanmaken. Voeg een `RULE` toe zodat je een gesprekje kunt voeren door tegen het konijn aan te lopen:

    [ > Speler | Konijn ] -> message Ik ben Flappie, wie ben jij?

Als het goed is, stelt Flappie zich nu voor. Het is wel leuk als hij meer dan een ding zegt. Dat kun je doen door meerdere konijn-objecten te maken:

```
Konijn1 K
Gray Black
.0.0.
00000
01010
.000.
00000

Konijn2
Gray Black
.0.0.
00000
01010
.000.
00000

Konijn3
Gray Black
.0.0.
00000
01010
.000.
00000
```

Maak in het `LEGEND` gedeelte een groep `Konijn` aan waar al deze objecten in zitten:

    Konijn = Konijn1 or Konijn2 or Konijn3

Pas nu de regel die hierboven hadden gemaakt als volgt aan:

    [ > Speler | Konijn1 ] -> [ Speler | Konijn2 ] message Ik ben Flappie, wie ben jij?

Als je het spel draait, zal het konijn de eerste keer dat je tegen 'm aan loopt iets zeggen, maar daarna niet meer. Dat komt doordat de regel hierboven er een `Konijn2` van heeft gemaakt. Je moet dus nog regel(s) toevoegen die zorgt dat `Konijn2` ook iets terugzegt. Lukt dat?

<details><summary>OPLOSSING</summary>

<code>
[ > Speler | Konijn2 ] -> [ Speler | Konijn3 ] message Ik heb zo'n trek!<br/>
[ > Speler | Konijn3 ] -> [ Speler | Konijn1 ] message Heb je misschien een wortel voor me?
</code>

Zoals je ziet maken we bij de tweede regel van <code>Konijn2</code> een <code>Konijn3</code> en bij de derde regel maken we er weer een <code>Konijn1</code> van. Hierdoor kun je het gesprekje nog eens herhalen als je vergeten was wat Flappie ook alweer precies zei.

</details>

Hier zie je het <a target='_blank' href='https://www.puzzlescript.net/editor.html?hack=3caebd413f61fac7ce77bd60861efc2d'>resultaat</a>.

## Voorwerpen

Natuurlijk moeten er voorwerpen te vinden zijn in je spel die je verder helpen.

### Duwen

De simpelste manier om in PuzzleScript iets te doen met voorwerpen is door het zo te maken dat je het voorwerp kunt duwen, net als de blokjes in vorige hoofdstukken.

Laten we een wortel en een spruitje voor het konijn toevoegen. We maken ook meteen een extra versie van het konijn, `GevoerdKonijn`, zodat we kunnen 'onthouden' wanneer het konijn iets gegeten heeft.

```
Wortel W
Orange Green
...11
..001
..00.
.00..
0....

Spruitje P
Green
.....
.000.
.000.
.000.
.....

GevoerdKonijn
Gray Black
.0.0.
00000
01010
.000.
00000
```

Maak bij `LEGEND` een groep `Groente` en voeg die toe aan `Objects`:

```
Groente = Wortel or Spruitje
Objects = Muur or Speler or Konijn or Groente
```

Plaats nu een wortel en spruitje in je wereld (met de letters `W` en `P`). Plaats ze zo dat het mogelijk is om ze naar het konijn te duwen.

Met deze regels kunnen we de wortel en het spruitje naar het konijn duwen:

```
(Groente duwen)
[ > Speler | Groente ] -> [ > Speler | > Groente ]
```

Misschien is het leuk als het konijn de wortel wel wil maar het spruitje niet:

```
[ > Spruitje | Konijn ] -> [ Spruitje | Konijn ] message Ik hou niet van spruitjes!

(Konijn eet wortel op)
[ > Wortel | Konijn ] -> [    | GevoerdKonijn ]
```

Hoe zou je het zo kunnen maken dat het konijn je bedankt als je nog eens met hem praat nadat je 'm gevoerd hebt?

<details><summary>OPLOSSING</summary>
<code>
[ > Speler | GevoerdKonijn ] -> message Dankjewel, dat was lekker!
</code>
</details>

En kun je zorgen dat het konijn genoeg heeft aan 1 wortel en "nee dank je" zegt als je er nog een aanbiedt?

<details><summary>OPLOSSING</summary>
<code>
[ > Wortel | GevoerdKonijn ] -> message Ik heb genoeg gehad!
</code>
</details>

Hier is een <a target='_blank' href='https://www.puzzlescript.net/editor.html?hack=4c7c6ed93d844f701f8eecc462d5c189'>werkend voorbeeld</a>.

### Niet duwen maar dragen

Wat als we voorwerpen niet in het rond willen duwen, maar willen dat de speler het voorwerp oppakt en met zich mee draagt? Dat is wat lastiger, omdat we in PuzzleScript niet zomaar een lijst voorwerpen kunnen bijhouden die de speler bij zich draagt.

We kunnen wel een extra 'laag' (`COLLISIONLAYER`) gebruiken in PuzzleScript waar 'draagbare' voorwerpen zoals de wortel en het spruitje op staan:

```
================
COLLISIONLAYERS
================

(De 'grond')
Background

(Alle gewone spelobjecten: speler, konijn, muren)
Object

(Door de speler te dragen objecten, in dit geval de groente)
Groente
```

Doordat de groente nu op een aparte laag staat, is het mogelijk dat de speler en een van de groentes een vakje delen.

We moeten nu wel onze regels aanpassen zodat we voorwerpen dragen in plaats van duwen:

```
(Zodra de speler op het vakje van een draagbaar voorwerp staat, moet dat voorwerp met de speler meebewegen)
[ > Speler Groente ] -> [ > Speler > Groente ]
```

Als je wilt dat de speler een gedragen voorwerp ook weer neer kan leggen door op `x` te drukken, voeg dan deze regel toe:

```
(Zet draagbaar voorwerp neer op een lege plek naast speler)
[ ACTION Speler Groente | no Object no Groente ] -> [ Speler | Groente ]
```

`ACTION` betekent hier dat er net op `x` is gedrukt. PuzzleScript zal in dat geval zoeken naar een aangrenzend leeg vakje (geen `Object`, geen `Groente`) en zal daar de groente neerzetten.

We moeten ook onze regels voor het voeren van het konijn iets aanpassen, omdat de speler en het spruitje tegelijkertijd richting het konijn bewegen. Als je dit niet doet, komen de regels voor het voeren in de war met de regels voor het praten met het konijn:

```
(Konijn houdt niet van spruitjes)
[ > Speler > Spruitje | Konijn ] -> [ Speler Spruitje | Konijn ] message Ik hou niet van spruitjes!

(Konijn eet wortel op)
[ > Speler > Wortel | Konijn no GevoerdKonijn ] -> [ Speler | GevoerdKonijn ]

(Konijn hoeft maar 1 wortel)
[ > Speler > Wortel | GevoerdKonijn ] -> [ Speler Wortel | GevoerdKonijn ] message Ik heb genoeg gehad!

(Gevoerd konijn bedankt speler)
[ > Speler | GevoerdKonijn ] -> [ Speler | GevoerdKonijn ] message Dat was lekker, dankjewel!
```

Als het niet lukt, kijk dan hier voor een <a target='_blank' href='https://www.puzzlescript.net/editor.html?hack=1de16dcefbc0c6bee3bd9d9afc4fd634'>werkend voorbeeld</a>.

In een echt spel wil je natuurlijk dat het `Konijn` je iets geeft als dank voor de wortel, zodat je verder kan komen in het spel. Bijvoorbeeld een sleutel. Kun je bedenken hoe je dat doet?

<details><summary>OPLOSSING</summary>

Maak daarvoor een <code>OBJECT</code> <code>Sleutel</code> aan, voeg 'm toe aan <code>Objects</code> (onder <code>LEGEND</code>) en pas de regel voor het geven van de wortel aan:

<p><code>
[ > Speler > Wortel | Konijn no GevoerdKonijn ] -> [ Speler Sleutel | GevoerdKonijn ]
</code></p>

<p>(<code>Konijn no GevoerdKonijn</code> betekent dat het elk <code>Konijn</code> mag zijn, behalve <code>GevoerdKonijn</code>)</p>

</details>

## Geheime deuren, knoppen

Als we een deur willen maken die opengaat als je een knop indrukt, bijvoorbeeld door er een kistje op te zetten, heb je eerst een aantal `OBJECTS` nodig:

```
Kistje @
(Een kistje dat de speler kan duwen)
white gray darkgray
00001
01112
01112
01112
12222

Deur D
(De deur die je kunt openen met de knop)
brown darkbrown
.101.
01010
01010
01010
01010

DeurOpen O
(De deur als-ie geopend is)
brown
.....
0....
0....
0....
0....

Knop K
(De knop waarmee je de deur kunt openen)
blue
.....
.000.
.000.
.000.
.....
```

Je kunt van de deur natuurlijk ook een geheime deur maken! Pas daarvoor het plaatje aan zodat het er (bijna) hetzelfde uitziet als een muur.

Je kunt zelf kiezen waar je deze zaken in je wereld plaatst. Maar we moeten wel de `LEGEND` en `COLLISIONLAYERS` aanpassen. Bij `LEGEND`:

```
Vloer = Knop or DeurOpen

(Dit zijn al onze voorwerpen)
Voorwerp = Muur or Speler or Kistje or Muntje or Deur
```

Bij `COLLISIONLAYERS`:

```
================
COLLISIONLAYERS
================

Achtergrond

(We hebben een extra laag voor de knop en de open deur, omdat de speler of een kistje tegelijk op hetzelfde vakje moeten kunnen staan)
Vloer

Voorwerp
```

Je hebt natuurlijk een regel nodig zodat de Speler een kistje kan duwen:

```
(De Speler kan Kistjes duwen)
[ > Speler | Kistje ] -> [ > Speler | > Kistje ]
```

Om de deur open te laten gaan als er iets op de knop staat:

```
(Open deur als er een voorwerp op de knop staat, sluit 'm anders)
late [ Knop Voorwerp ] [ Deur ] -> [ Knop Voorwerp ] [ DeurOpen ]
late [ Knop no Voorwerp ] [ DeurOpen ] -> [ Knop ] [ Deur ]
```

Zoals je ziet staan er twee keer rechte haken `[]` links en rechts van de `->`. Zo'n regel kijkt naar meerdere vakjes die waar dan ook in de puzzel kunnen staan. Dus de eerste regel betekent "als er ergens in het level een vakje is met een `Knop` en een `Voorwerp`", en ergens anders in het level is een vakje met een `Deur`, dan moet die `Deur` een `DeurOpen` worden.

Het woordje `late` ("laat") hebben we nodig zodat deze regels toegepast worden nadat het kistje bewogen heeft. Probeer maar eens wat er gebeurd als je dit woordje weglaat.

Deze regels werken ook als je meerdere knoppen en deuren zou hebben. Als alle knoppen ingedrukt worden, gaan alle deuren open. Weet je hoe het komt dat het zo werkt?

<details><summary>ANTWOORD</summary>

De eerste regel opent elke deur als ergens in het level een ingedrukte knop is, maar de tweede regel sluit elke deur weer dicht als ergens in het level een niet ingedrukte knop is. Dus tot alle knoppen ingedrukt zijn, blijven alle deuren dicht.
</details>

Hier is een <a target='_blank' href='https://www.puzzlescript.net/editor.html?hack=d745b4dd69fc65d639036b265c50a90e'>werkend voorbeeld</a>.

Natuurlijk kun je ook een valstrik maken met een (bijna) onzichtbare knop waar de speler juist niet op moet gaan staan, omdat er dan bijvoorbeeld ergens een deur dichtgaat en de speler opgesloten zit.

## Magische drankjes

Magie is natuurlijk altijd leuk in een avonturenspel. Bijvoorbeeld een drankje waardoor je elastisch wordt en jezelf door de tralies heen kunt wringen om jezelf uit een gevangenis te bevrijden!

We hebben nu twee spelerobjecten nodig: een `GewoneSpeler` en een `MagischeSpeler`:

```
GewoneSpeler S
(Het figuurtje dat je bestuurt)
darkgray brown lightblue blue
.000.
.111.
22222
.333.
.3.3.

MagischeSpeler
(De speler, nadat die het drankje gedronken heeft)
darkgray
.000.
.000.
00000
.000.
.0.0.

Drankje D
(Een magisch drankje)
purple
..0..
..0..
.000.
.000.
.000.

Tralies T
white
0.0.0
0.0.0
0.0.0
0.0.0
0.0.0
```

Maak in `LEGEND` de groep `Speler` aan:

```
Speler = GewoneSpeler or MagischeSpeler
Player = Speler
```

(`Player = Speler` staat er alleen zodat PuzzleScript, dat overal Engels gebruikt, ook weet wat onze speler is)

We zetten de `Tralies` op een eigen `COLLISIONLAYER`, omdat de `MagischeSpeler` straks op hetzelfde vakje moet kunnen staan.

```
================
COLLISIONLAYERS
================
Achtergrond
Tralies
Voorwerp
```

Als je het drankje drinkt, willen we natuurlijk een magisch geluid laten horen:

```
=======
SOUNDS
=======
Drankje DESTROY 80302508
```

Kun jij nu de regels voor het magische drankje schrijven?

<details><summary>ANTWOORD</summary>

Deze regels heb je nodig:

<code>
(Als Speler het Drankje drinkt wordt die magisch)<br/>
[ > Speler | Drankje ] -> [ > MagischeSpeler |          ]<br/>
<br/>
(Gewone speler kan zich niet door tralies heen wringen)<br/>
[ > GewoneSpeler | Tralies ] -> CANCEL
</code>
</details>

Je wilt misschien dat je het drankje maar 1 keer kan gebruiken. Hoe zou je dat in een regel kunnen vangen?

<details><summary>ANTWOORD</summary>

<code>
(Als je door de tralies heen gaat, verlies je je magie weer)<br/>
[ > MagischeSpeler Tralies |    ] -> [ Tralies | GewoneSpeler ]
</code>
</details>

Hier is het <a target='_blank' href='https://www.puzzlescript.net/editor.html?hack=e2f8386673688e824e0a485d21e4311a'>werkende voorbeeld</a>.

## Wil je nog meer? [Er *IS* nog meer! >>](14-meer-voorbeelden.md)