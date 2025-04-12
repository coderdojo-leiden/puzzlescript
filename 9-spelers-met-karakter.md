**Inhoud**

- [(terug naar het begin)](index.md)
- [8 - Waarmee wil je verder?](8-waarmee-verder.md)
- [9 - Spelers met karakter](9-spelers-met-karakter.md)
- [10 - Animatie](10-animatie.md)
- [11 - Actie](11-actie.md)
- [12 - Grotere levels en editor](12-grote-levels-editor.md)
- [13 - Op avontuur!](13-op-avontuur.md)
- [14 - Meer voorbeelden](14-meer-voorbeelden.md)

# 9 - Spelers met karakter

PuzzleScript heeft maar heel simpele plaatjes. Toch is het leuk als je je spelerfiguur wat meer een eigen karakter kunt geven.

Hier leer je hoe je de speler (ietsje) groter kunt maken, en hoe je verschillende plaatjes kunt tonen afhankelijk van welke richting de speler op kijkt.

## Spelerfiguur van formaat

Wat als we de spelerfiguur twee vakjes hoog willen tekenen? Dat kan eigenlijk niet in PuzzleScript, maar met een trucje kunnen we het toch voor elkaar krijgen: we tekenen gewoon een extra object boven ons `Speler` object.

Eerst moeten we de twee objecten ontwerpen die samen onze lange speler vormen. Het onderste object blijft gewoon `Speler` heten; dit is onze "echte" speler, wat PuzzleScript betreft. Het bovenste gaat `SpelerBovenkant` heten; dit bestaat alleen om het figuurtje er leuker uit te laten zien. Bijvoorbeeld:

```
SpelerBovenkant
Green Yellow Black Brown
.333.
12121
.111.
00000
00000

Speler S
Green Yellow Black Blue
00000
13331
.3.3.
.3.3.
```

Zie je hoe deze twee plaatjes samen 1 plaatje vormen? Je kunt het misschien beter zien als we de tussenregels weglaten:

```
.333.
12121
.111.
00000
00000
00000
13331
.3.3.
.3.3.
```

Ook al heb je nu een `SpelerBovenkant` object gemaakt, het wordt nog niet gebruikt in het spel. Als je het nu start, heeft de speler alleen een onderlichaam. Hoe lossen we dat op?

In het gedeelte `COLLISIONLAYER` kun je je spel meerdere lagen geven. Zo kun je zorgen dat sommige objecten met elkaar botsen en andere niet. De `SpelerBovenkant` willen we niet laten botsen met het vakje waarin het getekend wordt (de speler staat niet echt in dat vakje natuurlijk), dus we maken een extra laag aan voor dit object:

```
================
COLLISIONLAYERS
================

Background

(Alle gewone spelobjecten: speler, muren)
Object

(We zetten het bovenlichaam op een aparte laag omdat het in hetzelfde vakjes als een muur getekend moet kunnen worden)
SpelerBovenkant
```

Nu moeten we eerst zorgen dat de speler ook echt een bovenlichaam krijgt. Maak daarvoor deze `RULE` aan:

```
(Geef speler een bovenlichaam als die er nog geen heeft
UP [ Speler | no SpelerBovenkant ] -> [ Speler | SpelerBovenkant ]
```

`UP` ("omhoog") betekent hier: voer deze regel alleen "van onder naar boven" uit, zodat het bovenlichaam bovenop de speler komt en niet eronder of ernaast, wat raar zou zijn.

Probeer het eens uit. Krijgt de speler een bovenlichaam of niet? Wat als je een stap doet?

We willen dus dat deze regel direct gedraaid wordt als we ons spel starten, niet pas na de eerste stap. Dat kunnen we aangeven door deze regel bovenaan onze PuzzleScript-code te zetten (waar ook `title` staat):

    run_rules_on_level_start

Dit betekent "draai de regels als het level start". Probeer het maar uit.

We hebben nog steeds een probleem: ons bovenlichaam loopt niet met ons mee! Hoe lossen we dat nou weer op? In feite willen we zeggen "Als ons onderlichaam gaat bewegen, zorg dan dat ons bovenlichaam mee beweegt". Ook hier gebruiken we weer een `UP` regel voor, en we gebruiken het woordje `MOVING` ("bewegend") om de regel alleen voor bewegende spelers toe te passen:

```
(Als de speler beweegt, beweeg dan ook zijn bovenlichaam
 We gebruiken weer UP omdat we weten dat het bovenlichaam altijd op de speler staat)
UP [ MOVING Speler | SpelerBovenkant ] -> [ MOVING Speler | MOVING SpelerBovenkant ]
```

Als je het spel opnieuw draait, blijven de twee helften van de speler bij elkaar. Maar wat is dat? Als je van rechts of links met je onderlichaam tegen een muur loopt, gaat je bovenlichaam er nog steeds vandoor! Het is net alsof het bovenlichaam het bericht niet heeft doorgekregen dat het onderlichaam ergens tegenaan gebotst is. Om ons figuur ook in deze situatie gezond te houden, kunnen deze regel gebruiken:

```
(Als ons onderlichaam tegen een object botst, breek dan ALLE beweging af (CANCEL), ook die van het bovenlichaam.)
[ > Speler | Object ] -> CANCEL
```

Met `CANCEL` ("afbreken" of "annuleren") breek je alle beweging af, en zo voorkom je dat het bovenlichaam een eigen leven gaat leiden.

Mocht je vastlopen: hier is een <a target='_blank' href='https://www.puzzlescript.net/editor.html?hack=2336d6e249c0202156a9500b2a11f081'>werkend voorbeeld</a>.

## Links kijken, rechts kijken...

We gaan nu weer even terug naar een figuurtje van 1 vakje hoog, maar nu willen we dat je kunt zien welke kant dit figuurtje op kijkt.

We doen dit door 4 speler-objecten te maken: `SpelerOmlaag`, `SpelerOmhoog`, `SpelerLinks` en `SpelerRechts`:

```
(Voor elke richting die de speler op kan lopen, hebben we een apart plaatje)

SpelerOmlaag S
Blue Black White
.000.
01010
10001
01110
.000.

SpelerOmhoog
Blue Black
.000.
00000
00000
00000
.000.

SpelerLinks
Blue Black
.000.
01000
00010
11100
.000.

SpelerRechts
Blue Black
.000.
00010
01000
00111
.000.
```

Zoals je ziet hebben we alleen achter `SpelerOmlaag` een `S` staan. Een `S` in een level wordt dus een `SpelerOmlaag` object. We hebben geen letters nodig voor de andere richtingen; eentje is genoeg.

We hebben nu dus vier verschillende objecten voor onze speler. Dit is niet zo handig voor het schrijven van onze regels; we zouden dan elke regel vier keer moeten herhalen om te zorgen dat het met alle vier de richtingen werkt.

De oplossing is om een groep te maken met de naam `Speler`, waar de vier spelerobjecten toe behoren. Dit doen we bij het `LEGEND` gedeelte:

```
=======
LEGEND
=======

Speler = SpelerOmlaag or SpelerOmhoog or SpelerLinks or SpelerRechts
Player = Speler
Object = Muur or Speler
```

Als je het spel nu start, verandert de speler nog niet van richting; je blijft telkens het `SpelerOmlaag` plaatje zien. We moeten dus regels maken om het juiste speler-object te gebruiken voor elke richting.

Dit is een zo'n regel:

```
(Als de speler een bepaalde richting oploopt, zorg dan dat het juiste plaatje zichtbaar is)
[ LEFT  Speler ] -> [ LEFT  SpelerLinks  ]
```

Hier staan dus: "een naar links (`LEFT`) bewegende `Speler` moet worden vervangen door een `SpelerLinks` object". Zo zie je dus het correcte plaatje als je naar links loopt.

Kun je zelf de andere drie regels schrijven? De andere richtingen zijn `RIGHT` (rechts), `UP` (omhoog) en `DOWN` (omlaag).

Als je er niet uitkomt, is hier de <a target='_blank' href='https://www.puzzlescript.net/play.html?p=dd815485e4d6f6d0a4b50026ad176727'>oplossing</a>.

## Twee trucs combineren?

Als je het leuk vindt, kun je proberen om deze twee technieken te combineren: een figuurtje van twee vakjes hoog waaraan je kunt zien welke richting die uitkijkt.

Hoeveel extra objecten heb je hiervoor nodig denk je? En hoeveel extra regels?

<details><summary>Klik hier voor het antwoord</summary>

<p><b>Objecten:</b> vier richtingen voor het bovenlichaam en vier voor het onderlichaam, dus acht in totaal.</p>

<p><b>Regels:</b> vier extra regels om het bovenlichaam in de juiste richting te zetten en ook vier extra regels voor het onderlichaam, dus samen ook acht.</p>
</details>

Als je er niet uitkomt, kun je <a target='_blank' href='https://www.puzzlescript.net/editor.html?hack=13eafd53caae7e66bc5d2cc027dac9c2'>hier</a> kijken hoe je dit aanpakt.

## [Voeg wat beweging toe aan je spel! >>](10-animatie.md)