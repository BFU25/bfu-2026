# Lektionskod — JavaScript & DOM (vecka 22)

Dagens lektion är uppdelad i **tre delar**. Varje del är en egen “checkpoint” — koden du hade när vi gick vidare till nästa moment.

Kopiera kodblocken till egna filer om du vill köra exempelen lokalt (se nedan).

---

## Så testar du en del

1. Skapa en tom mapp, t.ex. `dom-del1`.
2. Skapa tre filer: `index.html`, `style.css`, `script.js`.
3. Kopiera HTML, CSS och JS från den del du vill köra.
4. Öppna `index.html` med **Live Server** (eller dra filen till webbläsaren).

I HTML-exemplen länkar vi till `style.css` och `script.js` — filnamnen måste stämma.

---

## Del 1 — Hämta element och lyssna på händelser

**Vi tränar:** `querySelector`, `innerText`, `addEventListener` (`click`, `change`).

### HTML (`index.html`)

```html
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM del 1</title>
    <script src="script.js" defer></script>
</head>
<body>
    <h1 id="title">Rubrik från HTML</h1>
    <p class="output">Något ska hända</p>
    <button id="my-btn">Klicka på mig</button>
    <button>Rör mig inte</button>
    <label>Ditt namn:</label>
    <input type="text" id="name-input" />
</body>
</html>
```

### JavaScript (`script.js`)

```js
// Hämta element från HTML med CSS-selektorer (# = id, . = klass)
let title = document.querySelector("#title");
let btn = document.querySelector("#my-btn");
let output = document.querySelector(".output");
let userInput = document.querySelector("#name-input");

// Ändra texten som visas i elementet (ersätter all text i taggen)
title.innerText = "JS har tagit över!";

// Lyssna på händelser: "click" när användaren klickar, "change" när input ändras
btn.addEventListener("click", handleClick);
userInput.addEventListener("change", showName);

function handleClick() {
    output.innerText = "Hej! Du klickade";
}

function showName() {
    // .value är det användaren skrivit i textfältet
    output.innerText = "Hej " + userInput.value;
}
```

Del 1 behöver ingen CSS.

---

## Del 2 — Räkna klick och styra med klasser

**Vi tränar:** state med variabel utanför funktionen, `disabled`, `classList.toggle`.

### HTML (`index.html`)

```html
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM del 2</title>
    <link rel="stylesheet" href="style.css" />
    <script src="script.js" defer></script>
</head>
<body>
    <button id="eat-btn">Ät en frukt</button>
    <p class="output"></p>
    <button id="color-btn">Byt färg</button>
</body>
</html>
```

### CSS (`style.css`)

```css
.hot {
    background-color: hotpink;
    color: white;
}
```

### JavaScript (`script.js`)

```js
let btn = document.querySelector("#eat-btn");
let output = document.querySelector(".output");
let btn2 = document.querySelector("#color-btn");

// Variabel utanför funktionen = "minne" mellan klick (räknar frukter)
let count = 0;

btn.addEventListener("click", eatFruit);
btn2.addEventListener("click", changeColor);

function eatFruit() {
    count = count + 1;
    output.innerText = "Du har ätit " + count + " frukter.";

    // Efter 3 klick: stäng av knappen så den inte går att klicka igen
    if (count >= 3) {
        btn.disabled = true;
        output.innerText += " Du är mätt!";
    }
}

function changeColor() {
    // toggle: lägger till klassen om den saknas, tar bort den om den finns
    output.classList.toggle("hot");
}
```

---

## Del 3 — Skapa element och många knappar

**Vi tränar:** `createElement`, `appendChild`, `querySelectorAll`, `data-*` / `dataset`, `e.target`.

### HTML (`index.html`)

```html
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM del 3</title>
    <script src="script.js" defer></script>
</head>
<body>
    <ul id="fruit-list"></ul>

    <div id="keypad">
        <button class="calc-btn" data-value="1">1</button>
        <button class="calc-btn" data-value="2">2</button>
        <button class="calc-btn" data-value="3">3</button>
        <button class="calc-btn" data-value="4">4</button>
    </div>
</body>
</html>
```

### JavaScript (`script.js`)

```js
let fruits = ["Äpple", "Banan", "Päron", "Jordgubbar"];

// Tom <ul> i HTML – vi fyller den med <li> från JavaScript
let list = document.querySelector("#fruit-list");

for (let i = 0; i < fruits.length; i++) {
    let newElement = document.createElement("li");
    newElement.innerText = fruits[i];
    list.appendChild(newElement);
}

// querySelectorAll ger en lista med alla matchande element
let allBtns = document.querySelectorAll(".calc-btn");

for (let i = 0; i < allBtns.length; i++) {
    allBtns[i].addEventListener("click", function (e) {
        // e.target = elementet som klickades
        // data-value i HTML blir dataset.value i JS
        console.log(e.target.dataset.value);
    });
}
```

Öppna **Utvecklarverktyg → Console** och klicka på knapparna för att se värdet.

---

## Nästa steg

- **Projekt:** [Miniräknaren](../README.md)
- **Mall från lektionen (level 1):** [miniraknare-mall/](../miniraknare-mall/) — kör `index.html` med Live Server och bygg vidare i egen kopia
