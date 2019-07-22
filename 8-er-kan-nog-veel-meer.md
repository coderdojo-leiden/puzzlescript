### Inhoud

- [1 - Aan de slag met PuzzleScript](1-aan-de-slag-met-puzzlescript.md)
- [2 - Maak je eigen regels](2-maak-je-eigen-regels.md)
- [3 - Kleuren en plaatjes](3-kleuren-en-plaatjes.md)
- [4 - Sla je werk op](4-sla-je-werk-op.md)
- [5 - Nieuwe voorwerpen-en-winnen](5-nieuwe-voorwerpen-en-winnen.md)
- [6 - Geluid](6-geluid.md)
- [7 - Een woord vormen](7-een-woord-vormen.md)
- [8 - Er kan nog veel meer](8-er-kan-nog-veel-meer.md)

# 8 - Er kan nog veel meer

## Leveleditor

Er zit ook een leveleditor ingebouwd in PuzzleScript. Klik op LEVEL EDITOR bovenin om hem te activeren. Je kunt je level dan in het spel bewerken.

Als je tevreden bent over je level, moet je nog wel op het S-knopje klikken boven je level. Onder je level verschijnt dan de code voor het level. Deze moet je zelf kopi&euml;ren en plakken in het `LEVELS` gedeelte van de code, anders worden je wijzigingen niet opgeslagen!

## Extra opties

Misschien had je al gezien dat helemaal bovenaan het programma deze regels staan:

```
title Mijn puzzelspel
author jij
homepage www.puzzlescript.net
```

Je kunt je spel hier een naam geven en je eigen naam erbij zetten. Maar in dit gedeelte van het programma kun je ook bepaalde extra opties van PuzzleScript opgeven. Hier zijn een paar interessante:

<dl>

  <dt><code>color_palette <em>nummer</em></code></dt>
  <dd>Gebruik een andere kleurenpalet (alle kleuren zien er iets anders uit). Nummer mag 1-14 zijn.</dd>

  <dt><code>background_color <em>kleur</em></code></dt>
  <dd>Gebruk een andere achtergrondkleur voor titelscherm, berichten, etc.</dd>

  <dt><code>text_color <em>kleur</em></code></dt>
  <dd>Verandert de tekstkleur.</dd>

  <dt><code>scanline</code></dt>
  <dd>Tekent je spel met horizontale strepen, zodat het er (nog meer) uitziet als een heel ouderwets computerspelletje.</dd>
  
  <dt><code>noaction</code></dt>
  <dd>Verbergt de regel "X to action" op het titelscherm. De meeste puzzelspellen hebben behalve de pijltjestoetsen geen aparte actietoets,
  dus dan is deze instructie niet nodig.</dd>

  <dt><code>youtube wygy721nzRc</code></dt>
  <dd>Laat het geluid van een YouTube-video als achtergrondmuziek horen. Let op, dit werkt alleen als je "SHARE" gebruikt, niet in de PuzzleScript-editor. Je moet de unieke "code" van de youtube-video weten. Dit vind je door naar het adres te kijken, bijvoorbeeld `https://www.youtube.com/watch?v=wygy721nzRc`. Het gedeelte na `v=` is de code die je hier moet gebruiken.</dd>

  <dt><code>debug<br/>verbose_logging</code></dt>
  <dd>Toon hoe PuzzleScript jouw regels heeft uitgeschreven en hoe ze worden toegepast. Interessant als je beter wilt begrijpen hoe PuzzleScript werkt, of een moeilijk probleem probeert op te lossen.</dd>

</dl>

## Vragen en antwoorden

<dl>

  <dt>Hoe kun je meerdere kistjes tegelijk schuiven?</dt>
  <dd>Gebruik deze twee regels:<br/><code>
  [ > Speler | Kistje ] -> [ > Speler | > Kistje ]<br/>
  [ > Kistje | Kistje ] -> [ > Kistje | > Kistje ]
  </code></dd>

  <dt>Hoe kun je de actietoets (X) in een spel gebruiken?</dt>
  <dd>...</dd>

  <dt>Hoe kun je een ander soort vloer maken waar voorwerpen op kunnen staan?</dt>
  <dd>...</dd>

  <dt>Hoe kun je het zo maken dat een geduwd kistje doorbeweegt tot het tegen een muur botst?</dt>
  <dd>...</dd>

  <dt>Kan je een 'vijand' maken die naar de speler toe beweegt zodra hij die ziet?</dt>
  <dd>...</dd>

  <dt>Kun je animatie gebruiken?</dt>
  <dd>Ja, zie <a href="https://stuartspixelgames.com/2017/04/06/how-to-do-animation-in-puzzlescript/">hier.</a></dd>

  <dt>Kan je een knop maken die deuren opent als de speler of een kistje er op staat?</dt>
  <dd>Ja, zie <a href="https://stuartspixelgames.com/2016/06/05/checking-multiple-conditions-in-puzzle-script/">hier.</a></dd>

  <dt>Kan je kistjes laten verdwijnen als ze in een vierkant staan?</dt>
  <dd>Ja, maar dit is wat lastiger. ...</a></dd>

  <dt>Kan je bijvoorbeeld een verfbom maken die alle voorwerpen om zich heen een bepaalde kleur geeft?</dt>
  <dd>Ja, maar dit is wat lastiger. ...</a></dd>

</dl>


## Voorbeeldspellen

Misschien heb je bovenin al "Load example" zien staan. Bij PuzzleScript zitten een aantal voorbeeldspellen waar je van kunt leren. Sla eerst jouw spel op (SAVE) en selecteer dan een van de spellen uit de lijst om de code te bekijken.

(Let op, jouw code wordt overschreven, maar je kunt altijd terug naar de laatst opgeslagen versie door de bovenste optie bij "Load" te kiezen)

Hier zijn nog een aantal andere hele knappe PuzzleScript-spellen die niet in de lijst voorbeelden staan:

  - [Pac-Man](https://www.puzzlescript.net/play.html?p=6847686)
  - [Heroes of Sokoban](https://www.puzzlescript.net/play.html?p=6860122)
  - [Dungeon Janitor](https://www.puzzlescript.net/play.html?p=6866423)
  - [Make friends with every cat](https://w.itch.io/herding-cats)
  - [Islands](https://rosden.itch.io/islands)

Een hele verzameling uitdagende puzzelspellen van de maker van PuzzleScript (Stephen Lavelle, bijnaam 'increpare') vind je op https://www.increpare.com/


## Meer informatie

Klik op DOCS bovenin om de (Engelse) [documentatie](https://www.puzzlescript.net/Documentation/documentation.html) van PuzzleScript te bekijken. Hierin staan nog een aantal mogelijkheden die hier niet genoemd zijn.

Er zijn ook een aantal stap-voor-stap instructies ("tutorials" in het Engels) voor PuzzleScript. Je vindt ze [hier](https://stuartspixelgames.com/puzzle-script-tutorials/).

