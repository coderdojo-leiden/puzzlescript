### Inhoud

- [1 - Aan de slag met PuzzleScript](1-aan-de-slag-met-puzzlescript.md)
- [2 - Maak je eigen regels](2-maak-je-eigen-regels.md)
- [3 - Kleuren en plaatjes](3-kleuren-en-plaatjes.md)
- [4 - Sla je werk op](4-sla-je-werk-op.md)
- [5 - Nieuwe voorwerpen-en-winnen](5-nieuwe-voorwerpen-en-winnen.md)
- [6 - Geluid](6-geluid.md)
- [7 - Een woord vormen](7-een-woord-vormen.md)
- [8 - Er kan nog veel meer](8-er-kan-nog-veel-meer.md)

# 5 - Nieuwe voorwerpen en winnen

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

