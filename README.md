# Unit 8.7 – Forms & Event Listeners

In this lesson you’ll practice:
- Reading input from **radio buttons**, **checkboxes**, and a **select (dropdown)**.
- Wiring buttons with **`addEventListener('click', ...)`** (no inline `onclick`).
- Computing a **pizza total** from size, toppings, and service method.
- Writing results to the page with **`textContent`** (no `alert`, no `prompt`, no `console.log` for output).

---

## 💸 Pricing Rules (use these exact values)

**Sizes (radio, name=`rg`):**
- Small = **$7.50**
- Medium = **$10.00**
- Large = **$12.50**
- XL = **$15.00**

**Toppings (checkboxes, name=`cb`):**  
Each selected topping adds **$0.50**.

**Service (select `#serviceSelect`):**
- `dinein` → **$0.00** extra  
- `takeout` → **$0.00** extra  
- `delivery` → **$3.00** extra

> Show a total to two decimals (e.g., `$13.50`). Write all output to `#myPara` with `textContent`.

---

## ✅ Required IDs (for autograding)

**Inputs / Controls**
- Name input: `myInput`
- Calculate button: `btnCalc`
- Clear button: `clearBtn`
- Size radios (name=`rg`): `r1`, `r2`, `r3`, `r4`
- Toppings checkboxes (name=`cb`): `cb1` … `cb8` (eight total)
- Service dropdown: `serviceSelect` (options with values: `dinein`, `takeout`, `delivery`)

**Output**
- Paragraph / div for results: `myPara`

---

## 🧭 Crash Course

### Radio buttons
```html
<input type="radio" name="rg" id="r1" value="7.5">
<label for="r1">Small</label>
```
- All radios in a **group** share the same `name`.
- Exactly one is `checked` at a time. Read the **checked** one to get its `.value`.

### Checkboxes
```html
<input type="checkbox" name="cb" id="cb1" value="Cheese">
```
- Each checked box contributes **$0.50** to total.
- Loop over all with `document.getElementsByName('cb')`.

### Dropdown (select)
```html
<select id="serviceSelect">
  <option value="dinein">Dine-In</option>
  <option value="takeout">Take-Out</option>
  <option value="delivery">Delivery (+$3)</option>
</select>
```
- Read with `document.getElementById('serviceSelect').value`.

### Event Listeners
Use **`addEventListener`** on buttons (no inline `onclick` in HTML):
```js
document.getElementById('btnCalc').addEventListener('click', onCalcClick);
document.getElementById('clearBtn').addEventListener('click', onClearClick);
```

---

## 💻 Starter Code

### `index.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Unit 8.7 – Forms & Event Listeners</title>
  <link rel="stylesheet" href="styles.css" />
  <script src="script.js" defer></script>
</head>
<body>
  <h1>Pizza Builder</h1>

  <label for="myInput">Name:</label>
  <input id="myInput" placeholder="Enter your name" />

  <h3>Size</h3>
  <input type="radio" name="rg" id="r1" value="7.5"><label for="r1">Small ($7.50)</label><br>
  <input type="radio" name="rg" id="r2" value="10"><label for="r2">Medium ($10.00)</label><br>
  <input type="radio" name="rg" id="r3" value="12.5" checked><label for="r3">Large ($12.50)</label><br>
  <input type="radio" name="rg" id="r4" value="15"><label for="r4">XL ($15.00)</label><br>

  <h3>Toppings ($0.50 each)</h3>
  <div>
    <input type="checkbox" name="cb" id="cb1" value="Cheese"><label for="cb1">Cheese</label>
    <input type="checkbox" name="cb" id="cb2" value="Mushrooms"><label for="cb2">Mushrooms</label>
    <input type="checkbox" name="cb" id="cb3" value="Onions"><label for="cb3">Onions</label>
    <input type="checkbox" name="cb" id="cb4" value="Peppers"><label for="cb4">Peppers</label>
    <input type="checkbox" name="cb" id="cb5" value="Olives"><label for="cb5">Olives</label>
    <input type="checkbox" name="cb" id="cb6" value="Sausage"><label for="cb6">Sausage</label>
    <input type="checkbox" name="cb" id="cb7" value="Pepperoni"><label for="cb7">Pepperoni</label>
    <input type="checkbox" name="cb" id="cb8" value="Pineapple"><label for="cb8">Pineapple</label>
  </div>

  <h3>Service</h3>
  <select id="serviceSelect">
    <option value="dinein">Dine-In</option>
    <option value="takeout">Take-Out</option>
    <option value="delivery">Delivery (+$3)</option>
  </select>

  <div style="margin-top: 1rem;">
    <button id="btnCalc">Calculate</button>
    <button id="clearBtn">Start Over</button>
  </div>

  <p id="myPara"></p>
</body>
</html>
```
---

## 🧪 What the Autograder Checks

1. All required elements & IDs exist.  
2. **No inline `onclick`** on buttons; uses `addEventListener`.  
3. Large + 2 toppings, dine-in → **$13.50**.  
4. Small, no toppings, delivery → **$10.50**.  
5. XL + all 8 toppings, dine-in → **$19.00**.  
6. Clear resets inputs and output - resets default size to large.

---

## Common Pitfalls
- Forgetting `defer` on `<script>` tag.  
- Using `prompt`/`alert`/`console.log` for output.  
- Wrong prices or rounding errors.
- Not setting size to large on Clear button
