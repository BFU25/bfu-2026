# Miniräknare — mall från lektionen

Färdig **startmall** för veckans projekt [Miniräknaren](../README.md). Den motsvarar det vi byggde live: knapparna `1`, `2`, `3`, `+`, `C` och `=`, plus enkel addition.

Mallen är medvetet **enkel** (level 1). I projektuppgiften utökar du med fler siffror, `-`, `*`, `/`, m.m.

## Köra mallen

1. Öppna mappen `miniraknare-mall` i VS Code.
2. Högerklicka på `index.html` → **Open with Live Server**.

Filer:

| Fil | Innehåll |
| --- | --- |
| `index.html` | Knappar med `data-value`, display |
| `style.css` | Utseende (kan bytas mot CodePen-designen) |
| `script.js` | Logik med kommentarer — börja här när du läser koden |

## Så hänger koden ihop

```text
Klick på knapp → läs dataset.value → uppdatera state → uppdatera display
```

**State** (variabler utanför funktionen):

- `currentNumber` — det som användaren skriver nu
- `previousNumber` — första talet efter man tryckt `+`
- `activeOperator` — vilken räkneoperation som väntar (`+` eller `null`)

**Flöde för `2 + 3 =`:**

1. Klick `2` → `currentNumber` blir `"2"`, display visar 2.
2. Klick `+` → `previousNumber = "2"`, `currentNumber` nollställs, `activeOperator = "+"`.
3. Klick `3` → `currentNumber` blir `"3"`.
4. Klick `=` → `Number("2") + Number("3")` → display visar 5.

## Kopiera till eget projekt

Du får kopiera hela mappen eller bara filerna till en egen mapp (t.ex. `mitt-projekt/`) och bygga vidare där. Behåll samma filnamn eller uppdatera länkarna i `index.html`.

## Relaterat material

- [Lektionskod (del 1–3)](../lektionskod/README.md) — DOM-grunderna vi byggde innan mallen
- [Projektuppgift Miniräknaren](../README.md) — alla levels
