# Facit — Vecka 21 (JavaScript datastrukturer)

Facit till [uppgifter.md](./uppgifter.md). Avsett för lärare eller för elever **efter** egen försök.

- **Läsförståelse:** entydigt svar + kort förklaring.
- **Koduppgifter:** *exempellösning* — flera varianter kan vara korrekta.
- Uppgifter **8, 9, 19, 39, 59** finns inte i uppgiftsfilen (numreringen hoppar).

---

## 1 Funktioner

### 1 — Skriv en funktion som skriver "Hello"

**Exempellösning:**

```js
function greeting() {
    console.log("Hello");
}
greeting();
```

### 2 — Läsförståelse

**Ut:** `1337`  
**Varför:** `mystery(1338)` returnerar `1338 - 1`.

### 3 — `increase(x)`

**Exempellösning:**

```js
function increase(x) {
    return x + 1;
}
```

### 4 — Värden på a och b

| Variabel | Värde | Varför |
| --- | --- | --- |
| `a` | `2` | `1 < 10` → `1 * 2` |
| `b` | `30` | `10` är inte `< 10` → `10 + 20` |

### 5 — Vad gör koden?

Konverterar Fahrenheit till Celsius och skriver ut resultatet.

**Ut:** `10`  
**Varför:** `(50 - 32) / 1.8 = 10`.

### 6 — Vad gör funktionen?

Returnerar det **större** av de två argumenten (max av `first` och `second`).

### 7 — `cheer`

**Enklast (tre rader):**

```js
function cheer() {
    console.log("Bra jobbat!");
    console.log("Bra jobbat!");
    console.log("Bra jobbat!");
}
```

**Med loop:**

```js
function cheer() {
    for (let i = 0; i < 3; i++) {
        console.log("Bra jobbat!");
    }
}
```

### 10

**Ut:** `9`  
**Varför:** `foo(3)` → `3 * 3`. Function declaration *hoistas*, så `foo` finns när raden `const a = foo(3)` körs.

### 11

**Ut:** `15`  
**Varför:** `3 * 5`.

### 12

**Ut:** `125`  
**Varför:** `foo(2) = 10`, `foo(3) = 15` → `foo(25) = 5 * 25`.

### 13

**Ut:** `true`  
**Varför:** `12 > 10` är sant.

### 14

**Ut:** `test` (en rad)  
**Varför:** `foo` tar inga parametrar; argumentet `"hej"` ignoreras.

### 15

**Ut:** `7`  
**Varför:** Parametern `a` i `foo` är en **lokal kopia** — `a++` påverkar inte den yttre `let a`. Yttre `a` blir `5 + 2 = 7`.

### 16

**Ut:** `8`  
**Varför:** `2 * 2 * 2`. Här är `foo` en function expression tilldelad `const` (körs rad för rad, men `foo` är redan definierad innan anropet på nästa rad).

### 17

**Ut:** `18`  
**Varför:** `goo` anropar funktionen `foo` med `3` → `2 * 3 * 3`.

### 18

**Ut:** `18`  
**Varför:** `foo()` gör `++a` (a blir 6, returnerar 6). Sedan `a += 6 * 2` → `6 + 12 = 18`.

### 20 — Medelvärde (två varianter)

```js
function printAverage(x, y) {
    const average = (x + y) / 2;
    console.log("Medelvärdet är: ", average);
}

function average(x, y) {
    return (x + y) / 2;
}

printAverage(4, 6);   // Medelvärdet är: 5
console.log(average(10, 20)); // 15
```

### 21 — Tre tal

```js
function average(x, y, z) {
    return (x + y + z) / 3;
}
```

### 22 — `avoid`

```js
function avoid(skip) {
    for (let i = 1; i <= 10; i++) {
        if (i === skip) continue;
        console.log(i);
    }
}
```

### 23 — `sum`

```js
function sum(from, to) {
    let total = 0;
    for (let i = from; i <= to; i++) {
        total += i;
    }
    return total;
}
// sum(3, 5) → 12
```

### 24 — `sum` även om from > to

```js
function sum(from, to) {
    if (from > to) {
        [from, to] = [to, from];
    }
    let total = 0;
    for (let i = from; i <= to; i++) {
        total += i;
    }
    return total;
}
// sum(25, 20) → samma som sum(20, 25)
```

Alternativ utan destructuring: använd `Math.min` / `Math.max` för loopgränserna.

---

## 2 Objekt

### 30

**Ut:** `Kisse`

### 31

**Ut:** `My cat Kisse is brown`

### 32

**Ut (två rader):**

```
Welcome to Red Street 12.
Here lives Karen
```

**Varför:** `residents[3]` är fjärde elementet (index 3).

### 33

**Ut:** `I am Gromit and I live on the Moon`

### 34

**Ut:** `{ x: 100, y: 100 }` (objektet som skrivs ut i konsolen)

**Varför:** Efter `obj.x = obj.y` är båda 100. Raden `obj.y = obj.x` sätter `y` till samma värde som `x` redan har — klassisk “swap”-fälla.

### 35 — Bok på bibliotek

```js
let book = {
    title: "Jorden runt på 80 dagar",
    author: "Jules Verne",
    borrowed: true,
};
```

### 36 — Koordinater och cirklar

**Exempellösning:**

```js
function getCoordinates(x, y) {
    return { x, y };
}

function getCircle(centerX, centerY, radius) {
    return { x: centerX, y: centerY, radius };
}

function circleArea(circleObject) {
    return 3.14 * circleObject.radius * circleObject.radius;
}

function getCircumference(topLeft, bottomRight) {
    const width = bottomRight.x - topLeft.x;
    const height = bottomRight.y - topLeft.y;
    return (width + height) * 2;
}

let c = getCircle(0, 0, 1.7846);
let cArea = circleArea(c);           // ≈ 10.00 (3.14 * 1.7846²)
let p1 = getCoordinates(0, 10);
let p2 = getCoordinates(5, 12);
let rectangleCircumference = getCircumference(p1, p2); // 14
```

**Förväntade värden (ungefär):**

| Variabel | Värde |
| --- | --- |
| `c` | `{ x: 0, y: 0, radius: 1.7846 }` |
| `cArea` | ≈ `10.0` |
| `p1` | `{ x: 0, y: 10 }` |
| `p2` | `{ x: 5, y: 12 }` |
| `rectangleCircumference` | `14` (bredd 5, höjd 2) |

### 37 — Sprite

```js
function moveRight(steps, character) {
    character.position.x += steps;
}
function moveLeft(steps, character) {
    character.position.x -= steps;
}
function moveUp(steps, character) {
    character.position.y -= steps;
}
function moveDown(steps, character) {
    character.position.y += steps;
}

moveRight(3, sprite); // position.x blir 17
```

### 38 — Modellering

Inget entydigt facit. Exempel på struktur:

```js
const film = {
    title: "Inception",
    year: 2010,
    genre: "sci-fi",
    cast: ["Leonardo DiCaprio", "Joseph Gordon-Levitt"],
};

const animal = {
    species: "Varg",
    habitats: ["Europa", "Asien", "Nordamerika"],
    diet: "köttätare",
};

const city = {
    name: "Karlstad",
    country: "Sverige",
    population: 95000,
};
```

---

## 3 Listor

### 50

**Ut:** `3` (index 1)

### 51

**Ut:** `gris`

### 52

**Ut:** `apa` (första elementet efter push)

### 53

**Ut:** `[3, 5, 7, 9]`  
**Varför:** `shift()` tar bort `2` först, `pop()` tar bort `12` sist.

### 54

**Ut:** `["apa", "gorilla"]`  
**Varför:** `slice(2, 4)` — index 2 och 3, slutindex exkluderat.

### 55

**Ut (sex rader):** `g`, `k`, `h`, `v`, `z`, `a`  
**Varför:** Första tecknet i varje sträng.

### 56

**Ut (tre rader):** `ananas`, `apelsin`, `banan`  
**Varför:** Loop när `i > 2`, dvs index 3, 4, 5.

### 57

**Ut:** `20`  
**Varför:** Summerar element **större än 3:** `7 + 8 + 5 = 20`.

### 58

**Ut:** `20`  
**Varför:** Summerar element på index **större än 3:** `8 + 5 + 3 + 4 = 20`.

### 60 — Array-metoder

Inget facit — elever ska experimentera. På genomgång: visa t.ex. `filter` på namn längre än 6 tecken, `map` till versaler, `sort` alfabetiskt.

**Kort exempel att visa på lektion:**

```js
australianAnimals.forEach((animal) => console.log(animal));
const longNames = australianAnimals.filter((a) => a.length > 6);
const upper = australianAnimals.map((a) => a.toUpperCase());
const sorted = [...australianAnimals].sort();
```
