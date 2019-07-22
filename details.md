# MEER DETAIL

## Hoe werkt PuzzleScript?

Een PuzzleScript-programma bestaat uit een paar gedeeltes:

- OBJECTS, welke objecten jouw spel heeft (bijvoorbeeld: Player, Kistje, Doel), hoe ze er uit zien (een enkele kleur of een plaatje van 5x5 pixels) en welk teken je gebruikt in levels voor dat object. Background en Player zijn speciaal en moeten altijd bestaan.
- (LEGEND: een andere manier om een teken op te geven voor een object)
- SOUNDS: om geluiden te koppelen aan gebeurtenissen, bijvoorbeeld als een kistje op een doel terechtkomt.
- COLLISIONLAYERS, welke lagen jouw spel heeft. De meeste spellen hebben 1 of 2 lagen, de grond en de objecten die er op staan. Je moet zeggen welke objecten bij de grond horen (zoals Doel) en welke op de grond staan (zoals Player en Kistje). Kistje kan alleen bovenop Doel staan als ze op verschillende lagen staan. Background is een speciale laag die altijd moet bestaan.
- RULES, regels die bepalen hoe de objecten, inclusief de Player, zich gedragen. Bijvoorbeeld dat een kistje gaat bewegen als de speler er tegen duwt.
- WINCONDITIONS: wanneer heeft de speler het level gewonnen? Bijvoorbeeld: als alle kistjes op een Doel-vakje staan.
- LEVELS: de puzzels zelf, getekend met behulp van de tekens die je voor elk object hebt opgegeven.

```
[ >  Player | Crate ] -> [  >  Player | > Crate  ]     
```

## PuzzleScript geavanceerde voorbeelden

- PuzzleScript games:
  - [Pac-Man](https://www.puzzlescript.net/play.html?p=6847686)
  - [Heroes of Sokoban](https://www.puzzlescript.net/play.html?p=6860122)
  - [Dungeon Janitor](https://www.puzzlescript.net/play.html?p=6866423)
  - [Make friends with every cat](https://w.itch.io/herding-cats)
  - [Islands](https://rosden.itch.io/islands)
- (Zie deze thread: https://news.ycombinator.com/item?id=17477484)
- [Tutorials](https://stuartspixelgames.com/puzzle-script-tutorials/)
  - [animatie](https://stuartspixelgames.com/2017/04/06/how-to-do-animation-in-puzzlescript/)
  - [zwaartekracht](https://stuartspixelgames.com/2017/04/07/how-to-do-gravity-in-puzzle-script/)
- Maker van PuzzleScript (increpare) heeft zelf een hoop coole game gemaakt, o.a. Stephen’s Sausage Roll


