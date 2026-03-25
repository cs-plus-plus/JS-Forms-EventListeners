# CS++ JavaScript — Lesson 8.7: Forms and Event Listeners

> **Lesson 8.7** | 100 Points | 6 Autograded Tests

In this assignment you will build a Pizza Builder form with radio buttons, checkboxes, and a dropdown. You will wire everything using `addEventListener` — no inline `onclick` attributes allowed.

---

## Table of Contents

1. [Concepts You Need](#concepts-you-need)
2. [Project Overview](#project-overview)
3. [Pricing Rules](#pricing-rules)
4. [Required IDs](#required-ids)
5. [File Structure](#file-structure)
6. [Autograding](#autograding)
7. [Try It Yourself — Practice Examples](#try-it-yourself--practice-examples)
8. [Tips for Success](#tips-for-success)
9. [FAQ](#faq)

---

## Concepts You Need

### addEventListener

`addEventListener` attaches a function to an element that runs when an event occurs. This is the modern way to handle events — do NOT use inline `onclick` attributes in your HTML.

```javascript
// In script.js (not in HTML)
document.getElementById("myBtn").addEventListener("click", function() {
    console.log("Button clicked!");
});
```

Why not `onclick`? Using `addEventListener`:
- Keeps JavaScript separate from HTML (separation of concerns)
- Allows multiple listeners on the same element
- Is the industry standard

### Radio Buttons

Radio buttons let the user select **exactly one** option from a group. All radios in a group share the same `name` attribute.

```html
<input type="radio" name="size" id="small" value="7.5">
<label for="small">Small ($7.50)</label>

<input type="radio" name="size" id="large" value="12.5" checked>
<label for="large">Large ($12.50)</label>
```

Reading the selected value in JavaScript:

```javascript
// Find the checked radio in the group
let selected = document.querySelector('input[name="size"]:checked');
let price = parseFloat(selected.value);  // e.g., 12.5
```

### Checkboxes

Checkboxes let the user select **zero or more** options:

```html
<input type="checkbox" name="topping" id="cheese" value="Cheese">
<label for="cheese">Cheese</label>
```

Counting checked checkboxes:

```javascript
let checkboxes = document.getElementsByName("topping");
let count = 0;
for (let cb of checkboxes) {
    if (cb.checked) {
        count++;
    }
}
```

### Select (Dropdown)

A dropdown lets the user pick one option from a list:

```html
<select id="serviceSelect">
    <option value="dinein">Dine-In</option>
    <option value="delivery">Delivery (+$3)</option>
</select>
```

Reading the selected value:

```javascript
let service = document.getElementById("serviceSelect").value;  // "dinein" or "delivery"
```

### The `defer` Attribute

When your `<script>` tag is in the `<head>`, the JavaScript runs before the HTML elements exist. Adding `defer` tells the browser to wait until the HTML is fully loaded:

```html
<script src="script.js" defer></script>
```

Without `defer`, `document.getElementById("btnCalc")` would return `null` because the button does not exist yet.

---

## Project Overview

Build a Pizza Builder page where the user:
1. Enters their name
2. Selects a pizza size (radio buttons)
3. Selects toppings (checkboxes, $0.50 each)
4. Selects a service type (dropdown)
5. Clicks "Calculate" to see the total
6. Clicks "Start Over" to reset the form

---

## Pricing Rules

**Sizes (radio buttons, name="rg"):**

| ID | Size | Price |
|----|------|-------|
| `r1` | Small | $7.50 |
| `r2` | Medium | $10.00 |
| `r3` | Large | $12.50 |
| `r4` | XL | $15.00 |

**Toppings (checkboxes, name="cb"):**
Each checked topping adds **$0.50**. There are 8 toppings total (IDs: `cb1` through `cb8`).

**Service (select, id="serviceSelect"):**

| Value | Extra Cost |
|-------|-----------|
| `dinein` | $0.00 |
| `takeout` | $0.00 |
| `delivery` | $3.00 |

**Total formula:**
```
total = sizePrice + (numberOfToppings * 0.50) + deliveryFee
```

Display the total in `#myPara` with `textContent`, formatted to two decimal places (e.g., `$13.50`).

---

## Required IDs

These exact IDs must exist in your HTML:

**Inputs:**
- Name input: `myInput`
- Size radios (name="rg"): `r1`, `r2`, `r3`, `r4`
- Topping checkboxes (name="cb"): `cb1`, `cb2`, `cb3`, `cb4`, `cb5`, `cb6`, `cb7`, `cb8`
- Service dropdown: `serviceSelect`

**Buttons:**
- Calculate: `btnCalc`
- Clear/Reset: `clearBtn`

**Output:**
- Results paragraph: `myPara`

---

## File Structure

```
JS-Forms-EventListeners/
├── index.html              <-- Pizza Builder form (provided)
├── script.js               <-- YOUR CODE GOES HERE
├── styles.css              <-- Optional styling
└── .github/
    └── workflows/
        └── classroom.yml   <-- Autograding tests (DO NOT MODIFY)
```

**Edit `script.js`** to add your event listeners and calculation logic. The starter `index.html` is provided with all the required elements.

---

## Autograding

| Test | What It Checks | Points |
|------|---------------|--------|
| Required elements exist | All buttons, radios, checkboxes, select, and output present | 15 |
| Uses addEventListener (no onclick) | No inline `onclick` attributes on buttons | 15 |
| Large + 2 toppings, dine-in | Total is $13.50 | 20 |
| Small + no toppings, delivery | Total is $10.50 | 20 |
| XL + all 8 toppings, dine-in | Total is $19.00 | 15 |
| Clear button resets form | All inputs cleared, size defaults to Large | 15 |

**Total: 100 points**

---

## Try It Yourself — Practice Examples

Create `practice.html` and `practice.js` to experiment without affecting your grade.

**practice.html:**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Practice - Event Listeners</title>
    <script src="practice.js" defer></script>
</head>
<body>
    <h1>Event Listener Practice</h1>

    <h3>Radio Buttons</h3>
    <input type="radio" name="color" id="red" value="red" checked>
    <label for="red">Red</label>
    <input type="radio" name="color" id="blue" value="blue">
    <label for="blue">Blue</label>

    <h3>Checkboxes</h3>
    <input type="checkbox" id="bold"> <label for="bold">Bold</label>
    <input type="checkbox" id="italic"> <label for="italic">Italic</label>

    <h3>Dropdown</h3>
    <select id="fontSize">
        <option value="12">Small</option>
        <option value="16">Medium</option>
        <option value="24">Large</option>
    </select>

    <br><br>
    <button id="showBtn">Show Selections</button>
    <p id="output"></p>
</body>
</html>
```

**practice.js:**
```javascript
// practice.js — event listener practice
document.getElementById("showBtn").addEventListener("click", function() {
    // Read radio
    let color = document.querySelector('input[name="color"]:checked').value;

    // Read checkboxes
    let bold = document.getElementById("bold").checked;
    let italic = document.getElementById("italic").checked;
    let styles = [];
    if (bold) styles.push("Bold");
    if (italic) styles.push("Italic");

    // Read dropdown
    let size = document.getElementById("fontSize").value;

    // Display
    let result = "Color: " + color;
    result += " | Styles: " + (styles.length > 0 ? styles.join(", ") : "None");
    result += " | Font size: " + size + "px";
    document.getElementById("output").textContent = result;
});
```

---

## Tips for Success

1. Add `defer` to your script tag: `<script src="script.js" defer></script>` — without this, your addEventListener calls will fail because the elements do not exist yet
2. Do NOT use `onclick` in your HTML — the test specifically checks that no buttons have inline onclick attributes
3. Use `parseFloat()` when reading radio values — they come as strings
4. Use `document.getElementsByName("cb")` and loop through to count checked toppings
5. Format the total with `.toFixed(2)` for consistent decimal display
6. The Clear button should reset the size to Large (check the `r3` radio) and clear all checkboxes

---

## FAQ

**Q: Why do I get "Cannot read properties of null" when I add an event listener?**
Your script runs before the HTML is loaded. Add `defer` to your script tag or move the `<script>` tag to the bottom of the `<body>`.

**Q: The test says I am using onclick — but I am not.**
Check your `index.html` carefully. If any button has `onclick="..."` in the HTML, remove it and use `addEventListener` in your JavaScript instead.

**Q: What should the Clear button do exactly?**
Reset the name input to empty, uncheck all toppings, set the size back to Large (r3 checked), set service to dine-in, and clear the output paragraph.

**Q: Do I need to display the customer's name in the output?**
The autograder does not check for the name in the output, but it is good practice to include it. Focus on getting the total calculation correct first.

**Q: How do I format the total as "$13.50"?**
Use: `"$" + total.toFixed(2)`

---

View all assignments and scoring breakdowns at [csplusplus.com/js-tests](https://csplusplus.com/js-tests)

*CS++ — AP Computer Science Principles — [csplusplus.com](https://csplusplus.com)*
