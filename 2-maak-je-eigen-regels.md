### Inhoud

- [1 - Aan de slag met PuzzleScript](1-aan-de-slag-met-puzzlescript.md)
- [2 - Maak je eigen regels](2-maak-je-eigen-regels.md)
- [3 - Kleuren en plaatjes](3-kleuren-en-plaatjes.md)
- [4 - Sla je werk op](4-sla-je-werk-op.md)
- [5 - Nieuwe voorwerpen-en-winnen](5-nieuwe-voorwerpen-en-winnen.md)
- [6 - Geluid](6-geluid.md)
- [7 - Een woord vormen](7-een-woord-vormen.md)
- [8 - Er kan nog veel meer](8-er-kan-nog-veel-meer.md)

# 2 - Maak je eigen regels

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

### Tips: wijzigingen terugdraaien
- Als je je PuzzleScript code aan het bewerken bent, kun je je laatste wijzigingen altijd ongedaan maken met Ctrl+Z.
- Als je zorgt dat je je programma regelmatig opslaan (door SAVE te klikken of Ctrl+S te drukken), kun je ook terug naar eerdere opgeslagen versies door ze te selecteren bij de "Load" selectielijst bovenin.

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

