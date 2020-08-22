# PuzzleScript 3


## PS RESEARCH
- DUNGEONSCRIPT: 3D VERSIE PUZZELSCRIPT
  http://dungeonscript.farbs.org/editor.html
- FORKS:
  https://pedropsi.github.io/game-tools.html#Puzzlescript-forks-or-mods 
- boek
  https://www.bol.com/nl/f/make-your-own-puzzlescript-game/9200000097203793/
- accessible puzzlescript
  https://philschatz.com/puzzlescript/
- Flying kick
  https://www.puzzlescript.net/play.html?p=7324598
- https://www.draknek.org/games/puzzlescript/
- EnigMash (overhead / gravity)
  https://jacklance.github.io/PuzzleScript/play.html?p=cfdcc6e23f1fb3e9de2fd42fafaf4d4c
- Paper over AI om PuzzleScript op te lossen en games te genereren
  https://groups.csail.mit.edu/icelab/content/puzzlescript-ai



## OPZET


Eerste 7 chapters blijven hetzelfde. Kinderen die die al gedaan hebben kunnen door bij chapter 8

- 8 - kies waarmee je verder wilt:
  -  9 - betere spelersprites, kleuren, muziek en de ingebouwde leveleditor
  - 10 - leven in de brouwerij: animatie en actie
  - 11 - een avonturenspel maken
  - 12 - moeilijk: explosies, elementen van meer dan 1 vakje maken
    en hoe je problemen kunt oplossen
    NOTE: dit zouden ook meerdere hoofdstukken kunnen worden. Portal ook nog?
  - 13 - voor wie er nog niet genoeg van heeft

- 9 - betere spelersprites, kleur, muziek en leveleditor:
  - achtergrondmuziek
  - alle kleuren anders (palet)
  - leveleditor

- 10 - leven in de brouwerij: animatie en actie!
  - realtime_interval
  - animatie
  - bal rollen tot die tegen muur botst
  - vijanden die vanzelf bewegen (vleermuizen)
  - vijand die op je afkomt zodra hij "lined" up met jou is

- 11 - op avontuur: grotere velden, praten en verzamelen
  - grotere levels; flickscreen/zoomscreen
  - verschillende soorten vloeren, bijv. knop
  - actietoets gebruiken
  - praten met npc
  - voorwerpen oppakken en gebruiken


- 12 - MOEILIJK: explosies / grotere elementen / problemen oplossen:
  - (verf)bom laten afgaan, kettingreacties
  - debug/verbose_logging
  - hoe worden regels precies uitgevoerd?
    https://www.puzzlescript.net/Documentation/executionorder.html
    Korte samenvatting: regels worden een voor een zo vaak mogelijk toegepast. Zet <code>debug</code> en <code>verbose_logging</code> bovenin om precies te zien hoe het werkt.</dd>
  - run_rules_on_level_start
  - OF: maak 2x2 puzzel om te winnen
  - OF: duw 2x2 blokken (erg moeilijk)
  - portals

13 - Voor wie er nog niet genoeg van heeft
  - alle nuttige links (documentatie, tutorials) op een rijtje
  - voorbeeldspellen



## Oude PS3 aantekeingen

- snake game? (random)
- rigid bodies
- tellen...??

- ik wil een vijand die je achtervolgt
  OPLOSSING:
  * richting speler bewegen als die niet "lined up" is, is lastig. Je zou een hoop hulpobjecten moeten
    maken en de vijand richting die hulpobjecten laten bewegen. Kan wel maar erg ingewikkeld.

- meerdere soorten vloeren
- powerup oppakken om iets speciaals te kunnen doen
- portals
 
## SIMILAR TO PS?
- http://tools.odie.us/
- BITSY:
  https://www.shimmerwitch.space/bitsyTutorial.html


