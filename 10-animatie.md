**Inhoud**

- [(terug naar het begin)](index.md)
- [8 - Waarmee wil je verder?](8-waarmee-verder.md)
- [9 - Spelers met karakter](9-spelers-met-karakter.md)
- [10 - Animatie](10-animatie.md)
- [11 - Actie](11-actie.md)
- [12 - Grotere levels en editor](12-grote-levels-editor.md)
- [13 - Op avontuur!](13-op-avontuur.md)

# 10 - Animatie

## Frames

Eenvoudige animatie is niets anders dan snel achter elkaar verschillende plaatjes laten zien.

Laten we een flakkerend vlammetje proberen te maken. Eerst tekenen we de 3 plaatjes van onze animatie (je noemt zulke plaatjes *frames*):

```
Vlam1 f
White Yellow Orange Red
..3..
.323.
32123
21112
.101.

Vlam2
White Yellow Orange Red
..23.
.323.
22133
2112.
.012.

Vlam3
White Yellow Orange Red
.3.3.
..22.
.1123
21012
.201.
```

> **WIST JE DAT?** Zoals je ziet gebruiken we de kleuren wit, geel, oranje en rood. Het heetste gedeelte van een vlam is het midden, en dit heeft de meest intense kleur (wit). Hoe verder naar de rand van de vlam, hoe minder heet en hoe minder intens de kleur, van geel naar oranje naar rood.

Het is altijd handig om zo'n serie plaatjes te groeperen. Zet dit bij `LEGEND`:

    Vlam = Vlam1 or Vlam2 or Vlam3 or Vlam4

en voeg `Vlam` ook toe aan `Object`:

    Object = Muur or Speler or Vlam

Doordat we de groep `Vlam` hebben aangemaakt, kunnen we die handig gebruiken in een `RULE`, bijvoorbeeld om roekeloze spelers te waarschuwen:

    [ > Speler | Vlam ] -> message Auw, dat is heet!

Zet nu een vlam in je level (`f`) en probeer het spel. Je ziet als het goed is de vlam, maar natuurlijk nog geen animatie. Die gaan we nu toevoegen.

## Regelvolgorde

Als eerste poging zou je dit kunnen doen:

```
[ Vlam1 ] -> [ Vlam2 ]
[ Vlam2 ] -> [ Vlam3 ]
[ Vlam3 ] -> [ Vlam1 ]
```

Hier staat "verander `Vlam1` in `Vlam2`, `Vlam2` in `Vlam3` en `Vlam3` weer in `Vlam1`." Dit klinkt goed, toch? Maar als je dit probeert, zul je zien dat het plaatje van de vlam niet verandert.

Dat komt door de volgorde van de regels: in deze volgorde wordt `Vlam1` in `Vlam2` veranderd, waarna onmiddelijk die `Vlam2` in `Vlam3` veranderd wordt, en tot slot die `Vlam3` weer teruggezet wordt naar `Vlam1`, zodat je niets bent opgeschoten.

Kun je zelf bedenken hoe je dit probleem zou kunnen oplossen?

<details><summary>HINT</summary>
Het probleem wordt veroorzaakt door de volgorde van de regels.
</details>

<details><summary>OPLOSSING</summary>
Zet de regels in omgekeerde volgorde, zodat ze niet meer achter elkaar op hetzelfde vakje toe te passen zijn.
</details>

Probeer het opnieuw. Het wordt nu iets beter: met iedere stap die de speler zet, verandert het vlammetje.

Maar wacht, het vlammetje springt nu heen en weer tussen *twee* plaatjes; een van onze frames wordt overgeslagen!

Kun je een oplossing bedenken?

<details><summary>HINT</summary>

Dit probleem lijkt veel op het vorige probleem dat we hadden: de eerste regel verandert <code>Vlam3</code> in <code>Vlam1</code>, maar de derde regel verandert die <code>Vlam1</code> direct weer in <code>Vlam2</code>. Dus <code>Vlam1</code> wordt nooit getoond.
</details>

<details><summary>OPLOSSING</summary>

Een eenvoudige manier om dit probleem op te lossen is om een extra plaatje <code>Vlam4</code> te maken dat een kopie is van <code>Vlam1</code> en de regels uit te breiden met dit extra frame. Dan wordt nog steeds een van de vier frames overgeslagen, maar dat is niet erg, want de drie frames die je oorspronkelijk getekend had, worden netjes getoond.
</details>

## Realtime

Eigenlijk willen we natuurlijk liever dat het vlammetje voortdurend verandert, ook als de speler even niet beweegt.

Dat kan door hier een *realtime* ("echte tijd") PuzzleScript-spel van te maken. Zet de volgende regel bovenaan je PuzzleScript-code (waar ook `title` staat):

    realtime_interval 0.1

Dit betekent dat tien keer per seconde de regels automatisch worden uitgevoerd. Als je het spel weer draait, zul je zien dat het vlammetje automatisch verandert. Als je het vlammetje sneller of langzamer wilt laten veranderen, pas dan het getal aan. Probeer bijvoorbeeld 0.2 of 0.15.

## Nog net iets mooier...

*(dit stukje kun je rustig overslaan, maar misschien vind je het interessant)*

Het valt je misschien op dat het vlammetje ineens sneller verandert als je snel met de speler rondloopt. Dat komt doordat de animatieregels bij elke stap van de speler ook nog eens toegepast worden.

Er zijn twee manieren om het vlammetje een constante animatiesnelheid te geven. De eerste is om de loopsnelheid van de speler te beperken met deze regel bovenaan je PuzzleScript-code:

    throttle_movement

Het nadeel is dat dit soms minder prettig bestuurt; je kunt dan niet meer hard door het level lopen als je dat zou willen.

Er is een andere truc, maar die maakt de animatieregels wat minder leesbaar. Je zou ze dan zo moeten maken:

    [ STATIONARY Speler ] [ Vlam4 ] -> [ Speler ] [ Vlam1 ]

`STATIONARY` betekent "niet bewegend". Eigenlijk staat hier dus "als de speler niet aan het bewegen is, verander dan `Vlam4` in `Vlam1`. Daardoor wordt zo'n animatieregel alleen uitgevoerd tijdens de *realtime* stappen en niet wanneer de speler beweegt. Als je dit doet, heb je `throttle_movement` niet meer nodig.

Het complete animatie-voorbeeld vind je <a target="_blank" href="https://www.puzzlescript.net/editor.html?hack=4fc3b3968df8081d290352fec929ba49">hier</a>.

