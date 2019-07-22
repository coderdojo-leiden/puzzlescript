# PuzzleScript: een logisch puzzelspel ontwerpen

# INTRODUCTIE

## Voorbeelden van logische puzzelspellen

### Soko Ban

Een van de eerste puzzelspellen. Je moet kistjes duwen en op de juiste plekken neerzetten.

<img src="images/Sokoban_ani.gif" alt="Sokoban" height="400" />

### Stephen’s Sausage Roll
Je moet worstjes over grillplaten rollen om ze te bakken, maar ze niet laten verbranden.

<img alt="Stephen's Sausage Roll" src="images/stephens-sausage-roll.gif" height="400" />

### Baba is You
Je kunt als spelende de regels van het spel veranderen zodat je bijvoorbeeld door muren heen kunt lopen.

<img alt="Baba is You" src="images/Baba_is_you_gameplay.gif" height="400" />

### A good snowman is hard to build
Je kunt sneeuwballen van verschillende grootte rollen en opstapelen om sneeuwmannen te maken.

[ontwerp in PuzzleScript](https://www.puzzlescript.net/play.html?p=2cdfc7d5c5b0fa557745)

<img alt="Snowman PuzzleScript" src="images/snowman-ps.png" height="400" />

(Daarna als een volledig spel gebouwd)

<img alt="A good snowman is hard to build" src="images/AGoodSnowman_Animated_Demo.gif" height="400">

### Meer voorbeelden

- Block Faker https://droqen.itch.io/block-faker (zie ook PuzzleScript examples)

### VRAAG: Ken je nog meer van dit soort spellen? Of heb je zelf een leuk idee?

## VRAAG: Wat hebben deze spellen met elkaar gemeen?

Bijvoorbeeld:
- Je moet logisch nadenken om een puzzel op te lossen
- Het speelveld bestaat uit vakjes
- Er zijn muren en voorwerpen die kunnen bewegen, zoals kistjes, sneeuwballen of worstjes
- Je bestuurt meestal 1 figuurtje
- Je ziet het meestal van bovenaf (maar opzij kan ook)
- Graphics zijn meestal vrij eenvoudig; daar draait het niet om
- ...

## Hoe ontwerp je zo’n spel?

- (terugverwijzen naar game design coderdojo)
- Je hebt misschien veel leuke ideeën voor puzzelspellen.
- Maar je weet pas of het een goed idee is als je het hebt uitgeprobeerd.
- Als het veel werk is om een idee uit te proberen, kun je niet snel een hoop verschillende dingen proberen.
- PuzzleScript is ontworpen om snel veel ideeën te kunnen proberen, door iemand die veel puzzelspelletjes gemaakt heeft. (zie bijv. https://www.increpare.com/)
- Het is ook al gebruikt door veel anderen. De maker van “A good snowman…” heeft zijn spel eerst in PuzzleScript ontworpen voor hij een mooie uitvoering gemaakt heeft.
- PuzzleScript heeft maar hele eenvoudige graphics: voor elk vakje kun je maar 5x5 pixels doen. Dat is expres, zodat je maar weinig tijd aan de graphics hoeft te besteden. Het gaat om het uitproberen van je idee.

# AAN DE SLAG

## 1 - Bekijk het voorbeeldspel

Open het [voorbeeldproject](https://www.puzzlescript.net/editor.html?hack=3339807a4a320fd66df5e1785998836c). Dit is een simpel spelletje waarbij je kistjes kunt schuiven en moet proberen er drie op een rij te krijgen.

Aan de linkerkant zie je de code van het project. Het lijkt misschien ingewikkeld, maar we zullen het stap voor stap bekijken.

Rechtsboven kun je het spel testen. Klik een keer in het rechterbovengedeelte en druk dan op de letter X om het spel te starten.

Je bestuurt een figuurtje met de pijltjestoetsen. Als je tegen een kistje aanloopt, duw je het een vakje verder. Je kunt maar 1 kistje tegelijk duwen.

Probeer maar om drie kistjes op een rij te krijgen (naast elkaar of boven elkaar). Als het lukt, verdwijnen ze. Als alle kistjes verdwenen zijn, ga je naar het volgende level.

TIP: als je op Z drukt, maak je je laatste beweging ongedaan. Zo kun je snel foutjes herstellen. Je kunt ook overnieuw beginnen door R te drukken.

## 2 - Maak zelf een level

Er zijn nu maar 2 levels, en ze zijn niet erg moeilijk op te lossen. Laten we een level toevoegen.

De levels staan in het `LEVELS` gedeelte van het programma, helemaal onderaan. Voeg bijvoorbeeld deze tekst toe net onder de kop `LEVELS`, zodat het er zo uitziet:

```
=======
LEVELS
=======

#####
#P..#
#.@@#
#.@.#
#####
```

Klik nu op "RUN" bovenaan de pagina om je code te controleren en het spel opnieuw te starten. Selecteer in het gedeelte rechtsboven de optie "new game" (met pijltje omhoog) en druk op X. Nu speel je het level wat je net hebt toegevoegd.

Zie je hoe de tekens overeenkomen met de muren, kistjes en de speler? En waar staat de punt (.) voor?

### Wat je kunt proberen ###
- Maak het level breder door alle regels langer te maken, of hoger door meer regels toe te voegen.<br/>LET OP: elke regel voor een level moet even lang zijn, anders krijg je een foutmelding wanneer je op RUN klikt.
- Voeg muren en/of kistjes toe om level het moeilijker te maken.
- Wat gebeurt er als er twee keer een P in het level staat?
- Je kunt ook instructies aan de speler tonen aan het begin of tussen de levels. Zet daarvoor regels die beginnen met het woord `message ` (boodschap), gevolgd door wat je aan de speler wil tonen.

### Tips
- Wil je terug naar het titelscherm terwijl je een level aan het spelen bent? Druk op Esc.
- Als je iets hebt aangepast in het programma, kun je in plaats van "RUN" ook op "REBUILD" klikken. Het spel wordt dan niet opnieuw opgestart, maar bijgewerkt terwijl je in hetzelfde level blijft.


## Maak je eigen regels

Dit programma beschrijft dus een puzzelspel, maar hoe werkt het? En hoe kunnen we de regels veranderen?

De regels van het spel staan beschreven in de gedeeltes RULES. Daar zien we de regels die bepalen hoe kistjes in het spel zich gedragen:

De eerste regel zorgt ervoor dat de speler (Player) kistjes kan schuiven:
```
[ > Speler | Kistje ] -> [ > Speler | > Kistje  ]
```

De tweede regel zorgt ervoor dat drie kistjes op een rij verdwijnen:
```
late [ Kistje | Kistje | Kistje ] -> [ | | ]
```

Zoals je ziet, heeft elke regel een pijltje (`->`) in het midden. Als PuzzleScript de situatie tegenkomt die links van het pijltje staat, vervangt hij die door wat rechts van het pijltje staat.

De eerste regel kun je dus zo lezen: "Als een speler richting een kistje beweegt, zet het kistje dan ook in beweging."

De tweede regel kun je lezen als "Als drie kistjes op een rij staan, vervang ze dan door drie lege plekken."

### Wat je kunt proberen ###
- Hoe zou je *vier* in plaats van drie kistjes op een rij kunnen laten verdwijnen?
  <details><summary>HINT</summary>Voeg zowel links en rechts een extra vakje toe in de regel. Vakjes worden gescheiden door <code>|</code>. Links en rechts van het pijltje moeten altijd evenveel vakjes staan.</details>
- Begrijp je wat `>` betekent in de eerste regel? Wat gebeurt er als je de tweede `>` weghaalt (bij `Speler` rechts van het pijltje)?
  <details><summary>HINT</summary><code>&gt;</code> heeft met beweging te maken. <code>&gt; Speler</code> betekent hier in feite: een naar het kistje bewegende speler.</details>
- Wat gebeurt er als je de eerste regel aanpast naar `[ > Speler | Kistje ] -> [ Kistje | Speler ]`? Lukt het je nu nog om drie kistjes op een rij krijgen?
- Hoe zou je de eerste regel aan kunnen passen om kistjes niet te duwen, maar te trekken?   <details><summary>HINT</summary>Als <code>&gt; Speler</code> betekent "een speler die naar het kistje beweegt", hoe zou je dan "een speler die van het kistje af beweegt" zeggen?</details>
- Kun je het ook zo maken dat je kistjes kan duwen EN trekken?
  <details><summary>HINT</summary>Je kunt de eerste regel kopieren voor je 'm aanpast zoals bij de vorige vraag.</details>
- Waarvoor dient het woordje `late` in de tweede regel? Probeer het eens weg te halen en kijk wat er gebeurt als je drie kistjes op een rij zet.
  <details><summary>HINT</summary>Zonder het woordje <code>late</code> win je niet direct als je drie kistjes op een rij zet, maar pas als je nog een stap doet.</details>

## Kies je kleuren en teken (hele kleine) plaatjes

PuzzleScript ziet er heel eenvoudig uit: elk vakje heeft maar 5 x 5 pixels. Dat is expres, omdat het belangrijker is om snel ideeen uit te proberen dan om het direct mooi te maken. Als je helemaal tevreden bent met je ontwerp, kun je het uitwerken in een andere programmeertaal met mooie graphics.

Natuurlijk is het wel belangrijk dat je in PuzzleScript duidelijk ziet wat wat is, anders wordt testen wel erg moeilijk. Daarom kun je simpele plaatjes maken in het `OBJECTS` (voorwerpen) gedeelte.

In dit gedeelte bepaal je welke voorwerpen je spel heeft en hoe ze er uit zien. Hier is bijvoorbeeld de `Speler`:

```
Speler S
darkgray brown lightblue blue
.000.
.111.
22222
.333.
.3.3.
```

Zoals je ziet staat op de eerste regel de naam van het voorwerp, in dit geval `Speler`, gevolgd door de letter die je hiervoor wilt gebruiken in je levels (`S`). Op de tweede regel kun je een aantal kleuren zetten met spaties ertussen. Daarna volgen vijf regels met 5 tekens per regel die de pixels van het plaatje vormen. Daarbij is `0` de eerste kleur, `1` de tweede, enzovoorts. `.` betekent "geen kleur".

(je kunt de laatste 5 regels ook weglaten, zoals bijv. bij `Achtergrond`. Dan krijg je alleen een gekleurd blokje te zien)

Deze kleurnamen kun je gebruiken: `black`, `white`, `lightgray`, `gray`, `darkgray`, `red`, `darkred`, `lightred`, `brown`, `darkbrown`, `lightbrown`, `orange`, `yellow`, `green`, `darkgreen`, `lightgreen`, `blue`, `lightblue`, `darkblue`, `purple`, `pink`, `transparent`. Ook hex-codes (als je die toevallig kent van CSS) werken, zoals `#ffff00`.

### Wat je kunt proberen ###
- Pas de kleuren of de 5x5 pixel plaatjes aan zoals jij wilt.

## Sla je werk op!

Nu je een aantal dingen hebt aangepast, wil je jouw spel natuurlijk niet zomaar kwijtraken. Gelukkig kun je in PuzzleScript je werk op een paar manieren opslaan. Mogelijkheid 1 en 2 zijn het makkelijkst.

### 1 - Lokaal opslaan (SAVE)

Klik op SAVE links bovenaan de pagina om je werk lokaal op te slaan. Dat wil zeggen dat het op deze laptop in deze browser bewaard wordt. Het is verstandig om dit regelmatig te doen, zodat je geen werk kwijtraakt als bijvoorbeeld de batterij van de laptop leeg is. 

Als je met je eigen laptop werkt, is SAVE de simpelste manier om je werk op te slaan zodat je later verder kunt. Werk je op een leenlaptop, dan zul je het op een andere manier moeten opslaan als je er later verder mee wilt.

### 2 - De code naar jezelf mailen of opslaan in een bestand

Je kunt het hele PuzzleScript-programma natuurlijk naar jezelf mailen, of het opslaan in een bestand op een USB-stickje.

Om het PuzzleScript-programma naar het klembord te kopi&euml;ren: klik op het programma en druk Ctrl+A (alles selecteren). Als het hele programma geselecteerd is, druk je op Ctrl+C (kopi&euml;ren). Daarna kun je het plakken (met Ctrl+V) in een mailtje of een leeg tekstbestand (in het programma Kladblok). (Als je op een Apple laptop werkt, gebruik je Appeltje+A, Appeltje+C en Appeltje+V)

Als je volgende keer weer verder wilt, doe je het omgekeerde: je opent je mailtje of bestand met de code, selecteert alles, gaat naar PuzzleScript, verwijdert daar alle code, en plakt jouw eigen code.

### 3 - Delen (SHARE)

Het is met PuzzleScript mogelijk om je puzzelspel op te slaan en te delen met anderen via GitHub. Je hebt hiervoor wel een (gratis) GitHub-account nodig (dat kun je [hier](https://github.com/join) aanvragen).

Klik op SHARE bovenin. PuzzleScript zegt dat je toestemming moet geven voor het delen. Klik op de link die rechtsonderin verschijnt en geef toestemming. Klik dan opnieuw op SHARE en PuzzleScript toont rechtsonderin twee links: een link naar de source code, voor als je er zelf verder mee wilt werken, en een link waar mensen je spel op volledig scherm kunnen spelen.

Let op: als je nog wijzigingen maakt aan een spel dat je hebt geSHAREd, moet je het opnieuw SHAREn om deze wijzigingen ook op te slaan. Je krijgt weer twee nieuwe links naar de laatste versie van je spel.

### 4 - Exporteren (EXPORT)

Het is ook mogelijk om je spel op te slaan zodat je het kunt spelen zonder met internet verbonden te zijn. Druk hiervoor op EXPORT. Je downloadt een HTML-bestand waar het hele spel in zit. Dit bestand kun je alleen niet makkelijk meer wijzigen, dus als je nog verder wilt werken aan het spel, kun je beter een van de bovenstaande manieren gebruiken.

## Voeg een nieuw soort voorwerp toe

In het `OBJECTS` gedeelte staan alle voorwerpen die in het spel kunnen voorkomen, inclusief de `Achtergrond` ("leeg vakje") en de `Speler`. Je kunt hier dus ook nieuwe soorten voorwerpen toevoegen.

Als je een voorwerp toevoegt in `OBJECTS`, werkt het alleen als je het ook toevoegt aan de lijst `Voorwerp` onder het gedeelte `LEGEND`. Als je een nieuw voorwerp `Muntje` toevoegt bijvoorbeeld, zet je het zo bij `Voorwerp`:

```
Voorwerp = Muur or Speler or Kistje or Muntje
```

("or" is Engels voor "of", dus eigenlijk staat er "Een `Voorwerp` is een `Muur`, `Speler`, `Kistje` of `Muntje`")

### Wat je kunt proberen ###
- Voeg een nieuw voorwerp toe, bijvoorbeeld `Muntje`. Kies een of meer kleuren en maak er een 5x5 pixel plaatje bij.
- Zorg dat er een letter of teken bij je nieuwe voorwerp staat, net als bijv. de `S` achter `Speler`. Gebruik dit teken om het voorwerp aan een level toe te voegen en kijk het of werkt.
- Zonder extra regels gedraagt je nieuwe voorwerp zich hetzelfde als een `Muur`. Kun je een regel toevoegen die zegt "Als de speler tegen een muntje aanloopt, verdwijnt het muntje"?
  <details><summary>HINT</summary>Maak een regel die lijkt op de kistjes-duwen regel, maar vervang <code>Kistje</code> door <code>Muntje</code> en laat Muntje rechts van het pijltje helemaal weg.</details>
- Stel dat je drie `Kistje`s op een rij elk in een `Muntje` wilt veranderen in plaats van ze te laten verdwijnen. Heb je een idee hoe je dat kunt aanpakken? Probeer of het werkt.
  <details><summary>HINT</summary>Pas het gedeelte rechts van het pijltje in de tweede regel aan.</details>

## Bepaal hoe je wint

Hoe weet PuzzleScript wanneer je een level gewonnen hebt? Dat staat bij het gedeelte `WINCONDITIONS`. Nu staat daar deze winconditie:

```
no Kistje
```

Dit betekent "geen Kistje", oftewel: je wint het level als alle kistjes verdwenen zijn (wat gebeurt als je er drie op een rij hebt gezet).

### Wat je kunt proberen ###
- Kun je zorgen dat je alleen wint als niet alleen alle kistjes weg zijn, maar je ook alle muntjes hebt opgepakt?
  <details><summary>HINT</summary>Je kunt een tweede eis toevoegen aan <code>WINCONDITIONS</code> die zegt dat er naast kistjes ook geen muntjes meer mogen zijn.</details>
- Stel dat we het spel willen veranderen zodat je wint als je tussen twee kistjes in staat. Hoe zou je dat kunnen doen?
  <details><summary>HINT1</summary>Je kunt een regel maken die de speler laat verdwijnen als die tussen twee kistjes staat. Pas hiervoor de tweede regel aan.</details>
  <details><summary>HINT2</summary>Je moet ook nog de winconditie aanpassen zodat je wint als er geen <code>Speler</code> meer is.</details>

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
- Speel voor elke stap die de speler zet een geluid.
  <details><summary>HINT</summary>Gebruik <code>Speler Move</code></details>
- Speel verschillende geluiden als de speler een kistje duwt of trekt.
  <details><summary>HINT</summary>Verander de regel <code>Kistje Move 975507</code> in <code>SFX1 975507</code> en voeg nog een SFX2 toe en koppel deze aan de duw- en trekregels net zoals hierboven met SFX0.</details>
- Speel een geluid als de speler probeert te bewegen of duwen maar het lukt niet (bijvoorbeeld omdat hij tegen een muur aanloopt). Gebruik hiervoor in plaats van <code>Move</code> het woord <code>CantMove</code> ("can't move" = "kan niet bewegen").

Alle mogelijkheden van geluiden vind je [hier](https://www.puzzlescript.net/Documentation/sounds.html) (in het Engels).

## Een woord vormen

Stel dat we het spel willen aanpassen zodat we niet meer saaie kistjes op een rijtje zetten, maar letters die een woord vormen. Misschien wel je eigen naam. In dit voorbeeld gebruiken we het woord `CODE`.

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
White Gray DarkGray Black
00001
01112
01112
01112
12222
```

En dan voegen we deze regel to aan `LEGEND`:

```
Kistje = GewoonKistje or LetterC or LetterO or LetterD or LetterE
```

Hiermee hebben we een groep voorwerpen gemaakt die `Kistje` heet en `GewoonKistje` plus onze `Letter`s bevat. Omdat onze bestaande regels allemaal `Kistje` gebruiken, werken ze nu voor deze hele groep voorwerpen.

Natuurlijk willen we niet dat drie letters op een rij altijd direct verdwijnen, dus moeten we wel die regel aanpassen zodat die alleen werkt voor `GewoonKistje`:

```
late [ GewoonKistje | GewoonKistje | GewoonKistje ] -> [ | | ] SFX0
```

Tot slot willen we zorgen dat de vier letters van het woord `CODE` verdwijnen als ze in de juiste volgorde gezet worden. Lukt het je om de regel zelf aan te passen? Als het niet lukt, bekijk dan de hint.

<details><summary>HINT</summary><code>late [ LetterC | LetterO | LetterD | LetterE ] -> [ | | | ] SFX0
</code></details>

Test of alles goed werkt door een level te ontwerpen waarin je de letters C, O, D en E tot een woord moet vormen. Bijvoorbeeld:

```
#########
#.......#
#.S.e...#
#..doc..#
#......##
#.....##.
#######..
```

### Wat je kunt proberen ###
- Duw de letters eens in volgorde `EDOC`, dus `CODE` gespiegeld. Wat gebeurt er? Hoe komt dat, denk je?<br/>
  Als je geen richting opgeeft, werken regels in alle richtingen. Zet `RIGHT` voor de regel die het woord `CODE` herkent als je wilt dat het alleen van links naar rechts werkt.
- **UITDAGING**: Je kunt nu maar 1 kistje tegelijk duwen. Stel dat je wilt dat je wel meerdere kistjes tegelijk kunt duwen. Heb je enig idee wat voor regel je daarvoor zou moeten toevoegen?
  <details><summary>HINT</summary>Je zou een regel moeten toevoegen die zegt dat het ene kistje het andere kistje in beweging kan brengen, net als een speler een kistje in beweging kan brengen. Dan kan de speler het eerste kistje in beweging brengen, dat kistje kan het volgende kistje in beweging brengen, enzovoorts.</details>

## Extra mogelijkheden

Misschien had je al gezien dat helemaal bovenaan het programma deze regels staan:

```
title Mijn puzzelspel
author jij
homepage www.puzzlescript.net
```

Je kunt je spel hier een naam geven en je eigen naam erbij zetten. Maar in dit gedeelte van het programma kun je ook bepaalde extra mogelijkheden van PuzzleScript activeren. Hier zijn er een paar:

<dl>

  <dt><code>color_palette <em>nummer</em></code></dt>
  <dd>Gebruik een andere kleurenpalet (alle kleuren zien er iets anders uit). Nummer mag 1-14 zijn.</dd>

  <dt><code>background_color <em>kleur</em></code></dt>
  <dd>Gebruk een andere achtergrondkleur voor titelscherm, berichten, etc.</dd>

  <dt><code>text_color <em>kleur</em></code></dt>
  <dd>Verandert de tekstkleur.</dd>

  <dt><code>scanline</code></dt>
  <dd>Tekent je spel met horizontale strepen, zodat het er (nog meer) uitziet als een heel ouderwets computerspelletje.</dd>

  <dt><code>youtube wygy721nzRc</code></dt>
  <dd>Laat het geluid van een YouTube-video als achtergrondmuziek horen. Let op, dit werkt alleen als je "SHARE" gebruikt, niet in de PuzzleScript-editor. Je moet de unieke "naam" van de youtube-video weten. Dit vind je door naar het adres te kijken, bijvoorbeeld `https://www.youtube.com/watch?v=wygy721nzRc`. Het gedeelte na `v=` is de "naam" die je hier moet gebruiken.</dd>

  <dt><code>debug<br/>verbose_logging</code></dt>
  <dd>Toon hoe PuzzleScript jouw regels heeft uitgeschreven en hoe ze worden toegepast. Interessant als je wilt begrijpen hoe PuzzleScript werkt, of een moeilijk probleem probeert op te lossen.</dd>

</dl>

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


