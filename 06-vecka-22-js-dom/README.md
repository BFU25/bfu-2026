# Miniräknaren
Du ska bygga en webbapp för en miniräknare.

**Mall från lektionen:** [miniraknare-mall/](./miniraknare-mall/) — färdig HTML/CSS/JS för level 1 (`1`, `2`, `3`, `+`, `C`, `=`). Läs `script.js` med kommentarer och bygg vidare i egen mapp.

## Beskrivning
När man laddar webbsidan ska den visa en miniräknare. Kodexempel här: [CodePen designskiss](https://codepen.io/david-zocom/pen/VwOpzEb?editors=1100).

### Level 1
Man ska kunna addera (lägga ihop) tal. Till exempel ska miniräknaren räkna ut `1 + 1` till `2`. Användaren klickar för på knappen "1", sedan på "+", sedan på "1" igen. Då ska appen visa resultatet "2".

Om man klickar på `1 + 2 + 3` ska man få resultatet `6`. Resultatet och senast valda knapp ska visas i appen.

Tips: börja med knapparna 1,2,3,+.

---
### Level 2
Man ska kunna subtrahera tal och alla siffror ska gå att använda.

---
### Level 3
Man ska kunna använda räknesätten multiplikation och division också.

---
### Level 4
Det ska finnas en knapp för att starta om miniräknaren från början. Dvs sätta resultatet till noll.

Två nya operatorer, roten ur och kvadraten på tidigare resultat. Tips: `Math.sqrt(x)` för roten och `x * x` för kvadraten.

---
### Level 5
När användaren förväntas välja en siffra ska alla operatorer vara avstängda. Det vill säga knapparna ska vara oklickbara.

Använd `element.disabled = true` och `element.disabled = false` för att stänga av och sätta på en individuell knapp.

När man å andra sidan förväntas välja en operator ska alla sifferknappar vara avstängda.

---
### Level 6
Varje gång man klickar på en knapp ska historiken uppdateras med en ny rad. (Se designskissen.)

---
### Level 7
Stöd för tangentbordet. När man trycker på tangenterna för 1-9 och de enkla operatorerna ska det ha samma effekt som om man hade klickat på respektive knappar.

---
### Level 8
Två minnesplatser, med möjlighet att spara ett resultat i varje. Sedan ska man kunna plocka ut ett tidigare resultat och fortsätta från det.

Gör uppgift 8 och 9 i vilken ordning du vill.

---
### Level 9
Möjlighet att hoppa tillbaka till en tidigare plats i historiken. (Du behöver jobba med listor för tidigare resultat, i stället för bara en variabel.)

---
### Level 10
Om du kommit så här långt har du bra koll på JavaScript i webbläsaren. Några fler saker du kan titta på, för att utmana dig själv:
+ spara appens tillstånd med `localStorage` ([länk här](https://javascript.info/localstorage))
+ animeringar med [`transition`](https://developer.mozilla.org/en-US/docs/Web/CSS/transition) och [`@keyframes`](https://developer.mozilla.org/en-US/docs/Web/CSS/@keyframes)


---

### Finns det något man inte ska använda i uppgiften?
Ja! Undvik:

+ att skriva `<button onclick=` inuti din HTML. HTML ska vara i sin fil, CSS i sin fil, och JavaScript i sina filer. Blanda inte!

+ funktionen `alert()` som visar ett popup-meddelande. Använd istället antingen console.log eller HTML-element och innerText för att visa meddelanden.

+ att lägga `<script>` sist i `<body>`. Script-taggen hör hemma inuti `<head>`.

+ att använda `window.location.reload()`, den laddar om hela webbsidan. Det är best practice att återställa JavaScript-variablerna till sina initiala värden.


---
