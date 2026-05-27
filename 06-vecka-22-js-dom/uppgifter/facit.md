# Facit — Vecka 22 (JavaScript & DOM)

Facit till [README.md](./README.md) (övningarna). Avsett för lärare eller för elever **efter** egen försök.

- **Läsförståelse:** vad som händer + kort förklaring.
- **Koduppgifter:** *exempellösning* — flera varianter kan vara korrekta.
- Numreringen hoppar (t.ex. 7–9, 15–19) — samma nummer som i uppgiftsfilen.

---

## Läsförståelse (1–5)

Förutsätter att HTML/CSS/JS från uppgift 1 är inlagda och att skriptet körs när sidan laddats.

### 1 — Vad gör koden?

1. `output` pekar på `<p class="output">`.
2. `innerText = ''` tömmer stycket.
3. `innerText += 'Hello    world'` — texten **Hello    world** visas (mellanslagen behålls med `innerText`).
4. `classList.toggle('hot')` — klassen `hot` läggs till (eller tas bort om den redan fanns). Första gången: **rosa bakgrund** enligt CSS.

**På sidan:** ett stycke med texten `Hello    world` och rosa bakgrund (om `hot` togglades på).

### 2 — Vidare JavaScript

`elem` blir första barnet i `.container`, dvs `<h1>`.

`innerHTML += '<br>' + elem.innerText` lägger till radbrytning + rubrikens text i `output`.

**Resultat i `output`:** först innehållet från uppgift 1, sedan ny rad, sedan ungefär ` DOM-manipulation med JavaScript ` (inklusive mellanslag i rubriken).

**OBS:** `innerHTML` tolkar HTML-taggar — här bara `<br>`, men blanda helst inte `innerHTML` med opålitlig användardata.

### 3 — Varför fungerar det inte?

`querySelector('output')` söker elementet **`<output>`** (taggnamn), inte klassen `.output`.

I HTML finns `<p class="output">`, inte `<output>` → variabeln blir **`null`**.

**Typiskt felmeddelande:**  
`TypeError: Cannot read properties of null (reading 'innerText')`  
(eller liknande på svenska/engelska i konsolen).

**Rätt selektor:** `document.querySelector('.output')` eller `'p.output'`.

### 4 — Klick på mystery-knappen

Registrerar `click` på `#mystery-button`. Vid klick körs `f()` → `output.innerText` blir **`It's a mystery`**.

### 5 — Lista vid klick

`g` körs också vid klick (ytterligare lyssnare på samma knapp).

Varje klick: skapar `<li>?</li>` och `list.append(x)` — en **`?`** per klick i `.mystery-list`.

**OBS:** Både uppgift 4 och 5 körs vid samma klick om båda är registrerade (texten uppdateras *och* ett nytt listelement läggs till).

---

## 6 — Hello world-projekt

**Exempellösning (utdrag):**

`index.html`:

```html
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="UTF-8">
    <title>Hello world</title>
    <link rel="stylesheet" href="style.css">
    <script src="script.js" defer></script>
</head>
<body>
    <p class="output"></p>
</body>
</html>
```

`style.css` — minst border, padding, margin, color, background-color på `.output`.

`script.js`:

```js
const output = document.querySelector(".output");
output.innerText = "Hello world!";
```

---

## Knappar och formulär (10–14)

### 10 — Byt färg

**Idé:** CSS-klasser `.gray` / `.white` (eller liknande) + `classList.toggle` vid klick.

```js
const btn = document.querySelector("#toggle-color");
const body = document.body; // eller en wrapper

btn.addEventListener("click", () => {
    body.classList.toggle("gray");
    body.classList.toggle("white");
});
```

Alternativ: en klass `is-gray` som togglas.

### 11 — Göm/visa "Byt färg"

**Idé:** variabel `isVisible` + `visibility: hidden` / `visible` eller `opacity`.

```js
let isVisible = true;
const colorBtn = document.querySelector("#toggle-color");
const hideBtn = document.querySelector("#hide-btn");

hideBtn.addEventListener("click", () => {
    isVisible = !isVisible;
    colorBtn.style.visibility = isVisible ? "visible" : "hidden";
});
```

### 12 — För- och efternamn

**Idé:** två inputs, `input` eller `keyup`/`change`, uppdatera `<p>`.

```js
const first = document.querySelector("#first-name");
const last = document.querySelector("#last-name");
const msg = document.querySelector(".welcome");

function updateName() {
    msg.innerText = `Välkommen ${first.value} ${last.value}.`;
}

first.addEventListener("input", updateName);
last.addEventListener("input", updateName);
```

**`keyup` vs `change`:** `input`/`keyup` uppdaterar medan man skriver; `change` brukar trigga när fältet **tappar fokus** efter ändring.

### 13 — Prenumerationsnivåer

**Idé:** varje “Select”-knapp sätter en aktiv klass på rätt block, tar bort från övriga.

```js
const tiers = document.querySelectorAll(".tier");

function selectTier(chosen) {
    tiers.forEach((tier) => {
        tier.classList.toggle("selected", tier === chosen);
    });
}

document.querySelector("#select-free").addEventListener("click", () => {
    selectTier(document.querySelector("#tier-free"));
});
// … likadant för billig/dyr
```

CSS: `.tier.selected { … highlight … }`.

### 14 — Trafikljus

**Enkel sekvens:** state-variabel `step` (0 = rött, 1 = gult, 2 = grönt), vid klick byt klass på lamporna.

**Realistisk sekvens (5 steg):**  
rött → rött+gult → grönt → gult → rött.

```js
const steps = [
    ["red"],
    ["red", "yellow"],
    ["green"],
    ["yellow"],
    ["red"],
];
let step = 0;

function showLights() {
    const lamps = { red: ..., yellow: ..., green: ... };
    // nollställ alla, tänd de i steps[step]
    step = (step + 1) % steps.length;
}
```

Flexbox: kolumn med tre `div`, `border-radius: 50%`, klasser `.on-red`, `.on-yellow`, `.on-green`.

---

## Fruktlista (20–24)

**OBS i uppgift 21:** texten säger “uppgift 10” — men meningen är **uppgift 20** (fruktlistan).

### 20 — Rendera 10 frukter

```js
const fruits = ["Äpple", "Pärön", "Banan", "Citron", "Mango", "Kiwi", "Plommon", "Vindruva", "Ananas", "Hallon"];
const container = document.querySelector(".fruit-output");

document.querySelector("#show-fruits").addEventListener("click", () => {
    container.innerText = fruits.join(", ");
    // eller som <ul> med loop
});
```

### 21 — Räkna ätna frukter

```js
let count = 0;
const output = document.querySelector(".output");

document.querySelector("#eat-btn").addEventListener("click", () => {
    count++;
    const ord = count === 1 ? "frukt" : "frukter";
    output.innerText = `Du har ätit ${count} ${ord}.`;
});
```

### 22 — Lägg till frukt

```js
function renderFruits() {
    const list = document.querySelector("#fruit-list");
    list.innerHTML = "";
    for (let i = 0; i < fruits.length; i++) {
        const li = document.createElement("li");
        li.innerText = fruits[i];
        list.appendChild(li);
    }
}

document.querySelector("#add-btn").addEventListener("click", () => {
    const name = document.querySelector("#fruit-input").value.trim();
    if (name) {
        fruits.push(name);
        renderFruits();
    }
});
```

### 23 — “Välj frukt” per rad

Vid `renderFruits`, lägg till knapp per `li`:

```js
const btn = document.createElement("button");
btn.innerText = "Välj frukt";
btn.addEventListener("click", () => {
    document.querySelector(".output").innerText = `Du valde ${fruits[i]}!`;
});
li.appendChild(btn);
```

### 24 — Ta bort frukt

```js
removeBtn.addEventListener("click", () => {
    fruits.splice(i, 1);
    renderFruits();
});
```

`renderFruits()` om efter varje ändring håller HTML och array synkade.

---

## 30 — Todo-lista

**Struktur:**

```js
let todos = []; // { id, text, done }

function renderTodos() {
    const ul = document.querySelector("#todo-list");
    ul.innerHTML = "";
    for (const todo of todos) {
        const li = document.createElement("li");
        const checkbox = document.createElement("input");
        checkbox.type = "checkbox";
        checkbox.checked = todo.done;
        checkbox.addEventListener("change", () => {
            todo.done = checkbox.checked;
        });
        const span = document.createElement("span");
        span.innerText = todo.text;
        li.append(checkbox, span);
        ul.appendChild(li);
    }
}

// Lägg till: todos.push({ id: Date.now(), text: input.value, done: false }); renderTodos();
```

**Ta bort / redigera:** knappar per rad som `splice`/`find` i arrayen och anropar `renderTodos()` igen.

Inget entydigt UI-facit — fokus på data i array + omrendering vid ändring.

---

## 40 — Adressbok

**Kärna:**

```js
let contacts = []; // { id, name, email }

function clearHtml() {
    document.querySelector("#contact-list").innerHTML = "";
}

function renderContacts() {
    clearHtml();
    const list = document.querySelector("#contact-list");
    for (const c of contacts) {
        const li = document.createElement("li");
        li.innerHTML = `
            <span>${c.name}</span> — <span>${c.email}</span>
            <button class="remove">Remove</button>
            <button class="edit">Edit</button>
        `;
        li.querySelector(".remove").addEventListener("click", () => {
            contacts = contacts.filter((x) => x.id !== c.id);
            renderContacts();
        });
        list.appendChild(li);
    }
}

document.querySelector("#re-render").addEventListener("click", renderContacts);
document.querySelector("#clear-all").addEventListener("click", clearHtml);
```

| Deluppgift | Idé |
| --- | --- |
| Lägg till kontakt | `push` objekt med `id`, sedan `renderContacts()` |
| Clear all | töm bara HTML (`innerHTML = ""`) — data kvar om du inte också tömmer `contacts` |
| Re-render | `renderContacts()` från `contacts` |
| Remove | ta bort från array **och** anropa `renderContacts()` |
| Edit | visa `input` i raden, spara `name`/`email` på `change` eller knapp “Spara” |
| (Svår) Byt ordning | `findIndex` + `splice` i array, sedan omrendera |
| Sökfält | `contacts.filter(c => c.name.includes(q) \|\| c.email.includes(q))` och rendera bara träffar |

**OBS:** I uppgiftstexten saknas `>` i `<button Re-render` — ska vara `<button>Re-render</button>`.

---

## Snabbreferens — vanliga misstag

| Misstag | Rätt |
| --- | --- |
| `querySelector('output')` | `querySelector('.output')` |
| Glömma `render()` efter array-ändring | Anropa omrendering efter varje `push`/`splice` |
| Flera `addEventListener` på samma knapp utan att tänka igenom | Alla registrerade funktioner körs vid klick |
| `innerHTML` med användartext | Risk för XSS — använd `innerText` eller sanera |
