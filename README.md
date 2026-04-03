# CS++ JavaScript — Forms & Event Listeners

> **Unit 8.7** | 100 Points | 7 Automated Tests

In this assignment you will learn how to read values from HTML forms and wire buttons using `addEventListener()` — the modern way to handle user interactions.

---

## Table of Contents

1. [What Is addEventListener?](#what-is-addeventlistener)
2. [Reading Form Values](#reading-form-values)
3. [Radio Buttons](#radio-buttons)
4. [Checkboxes](#checkboxes)
5. [Dropdown (select)](#dropdown-select)
6. [Assignment](#assignment)
7. [Scoring Rubric](#scoring-rubric)
8. [Tips for Success](#tips-for-success)
9. [FAQ](#faq)

---

## What Is addEventListener?

In the previous assignment (Functions), buttons used `onclick` in the HTML. That works, but the modern and preferred approach is `addEventListener()`:

```javascript
let btn = document.getElementById("myButton");
btn.addEventListener("click", function() {
  // this code runs when the button is clicked
});
```

**Important:** Do NOT add `onclick` attributes in your HTML. The autograder checks that buttons use `addEventListener` only.

---

## Reading Form Values

To read the value from a text input:

```javascript
let name = document.getElementById("myInput").value;
```

To display text on the page:

```javascript
document.getElementById("output").textContent = "Hello!";
```

---

## Radio Buttons

Radio buttons let the user pick ONE option from a group. They share the same `name` attribute:

```html
<input type="radio" name="size" value="small"> Small
<input type="radio" name="size" value="large" checked> Large
```

To find which one is selected, loop through them:

```javascript
let radios = document.getElementsByName("size");
let selected = "";
for (let i = 0; i < radios.length; i++) {
  if (radios[i].checked) {
    selected = radios[i].value;
  }
}
```

---

## Checkboxes

Checkboxes let the user select MULTIPLE options:

```html
<input type="checkbox" name="topping" id="t1"> Cheese
<input type="checkbox" name="topping" id="t2"> Pepperoni
```

To count how many are checked:

```javascript
let boxes = document.getElementsByName("topping");
let count = 0;
for (let i = 0; i < boxes.length; i++) {
  if (boxes[i].checked) {
    count = count + 1;
  }
}
```

---

## Dropdown (select)

A `<select>` element creates a dropdown menu:

```html
<select id="color">
  <option value="red">Red</option>
  <option value="blue" selected>Blue</option>
</select>
```

To read the selected value:

```javascript
let color = document.getElementById("color").value;  // "blue"
```

---

## Assignment

Complete `script.js` by following the STEP comments. Use `addEventListener()` for all buttons — do NOT use `onclick` in the HTML.

### Warm-Up: Shout It! — 15 points

When the user types text and clicks "Shout":
- Read the text from the input
- Convert to uppercase and add "!" at the end
- Display in the output div
- Example: "hello" → "HELLO!"

### Pizza Builder — 60 points

Build a pizza order calculator:
- **Size**: Read the selected radio button value (Small $7.50, Medium $10.00, Large $12.50, XL $15.00)
- **Toppings**: Count checked checkboxes, multiply by $0.50
- **Service**: Read dropdown value (Dine In $0, Take Out $1.50, Delivery $3.00)
- **Total**: size + toppings + service fee
- Display: `[name], your total is $[total]` (with .toFixed(2))
- If name is empty, use "Customer"

The Clear button resets everything:
- Empty the name input
- Select Large radio
- Uncheck all toppings
- Set service to "dinein"
- Clear the output

### Code Quality — 25 points

- **No `onclick` in HTML** — buttons must not have onclick attributes (10 points)
- **Uses `addEventListener`** — source code contains addEventListener (5 points)
- **Required elements exist** — all IDs and form elements present (10 points)

---

## Scoring Rubric

| # | Test | Points | What the autograder checks |
|---|------|--------|---------------------------|
| 1 | Shout warm-up | 15 | "hello" → "HELLO!" in output |
| 2 | No onclick in HTML | 10 | btnCalc, clearBtn, btnShout have no onclick attribute |
| 3 | Uses addEventListener | 5 | Source code contains `addEventListener` |
| 4 | Required elements exist | 10 | All expected IDs and form elements |
| 5 | Large + 2 toppings dine-in = $13.50 | 20 | Price calculation |
| 6 | Small + no toppings + delivery = $10.50 | 20 | Price calculation |
| 7 | Clear resets form | 20 | All inputs reset to defaults |
| | **Total** | **100** | |

---

## Tips for Success

1. **Start with the Shout warm-up** — it's one addEventListener with simple logic
2. **Wire your buttons at the bottom of script.js** — after all function code
3. **Test edge cases** — what happens with no toppings? With all toppings?
4. **Check your math** — Large ($12.50) + 2 toppings ($1.00) + Dine In ($0) = $13.50
5. **Use `.toFixed(2)`** — always format the total to 2 decimal places

---

## FAQ

**Q: What's wrong with onclick?**
Inline `onclick` attributes mix HTML and JavaScript. `addEventListener` keeps them separate, which is cleaner and more maintainable. Professional code uses `addEventListener`.

**Q: How do I uncheck all checkboxes?**
Loop through them and set each one's `.checked` to `false`.

**Q: How do I set a radio button to checked?**
Set its `.checked` property to `true`: `document.getElementById("r3").checked = true;`

**Q: Why does my total show wrong numbers?**
Make sure you're using `parseFloat()` on the radio button value. Without it, you might be doing string concatenation instead of math.

---

View all assignments at [csplusplus.com/js-tests](https://csplusplus.com/js-tests)

*CS++ — AP Computer Science Principles — [csplusplus.com](https://csplusplus.com)*
