# JavaScript null vs undefined

## Example Snippet

```js
let a;        // a is undefined (JS engine sets this)
let b = null; // b is null (developer sets this)
```

---

## Comparison Table

| Aspect                 | `undefined`                                           | `null`                                                  |
|------------------------|-------------------------------------------------------|---------------------------------------------------------|
| **Meaning**            | Variable declared but no value assigned yet           | Intentional absence of any object value                  |
| **Who sets it**        | Automatically by the JavaScript engine                | Explicitly by the developer in code                      |
| **typeof Result**      | `"undefined"`                                         | `"object"` (legacy bug from JS v1)                      |
| **Math Operations**    | Evaluates to `NaN`                                    | Evaluates to `0`                                        |
| **JSON.stringify**     | Removed entirely from output                          | Preserved faithfully as `null`                          |
| **Intention**          | Unintentional (the engine says "nothing here yet")    | Intentional (the developer says "this is empty on purpose") |

---

## Detailed Breakdown

### Common Scenarios for `undefined`

**1. Uninitialized Variable**
```js
let user;
console.log(user); // undefined
```

**2. Missing Function Argument**
```js
function greet(name) {
  console.log(name);
}
greet(); // undefined (no argument passed)
```

**3. Non-Existent Property**
```js
const car = { brand: "Tesla" };
console.log(car.model); // undefined (property doesn't exist)
```

### Common Scenarios for `null`

**1. Explicit Reset / Cleanup**
```js
let currentSession = { id: 102 };
currentSession = null; // Intentional cleanup
```

**2. API / DOM Responses**
```js
const button = document.querySelector("#submit-btn");
// Returns null if no element matches the selector
```

---

## Equality Comparison

Because both represent "nothingness", they have unique equality behavior:

| Operator     | Expression                 | Result  | Why                                 |
|--------------|----------------------------|---------|-------------------------------------|
| Loose (`==`) | `null == undefined`        | `true`  | JS coerces both to "empty"          |
| Strict (`===`)| `null === undefined`      | `false` | Different types (`object` vs `undefined`) |

```js
console.log(null == undefined);  // true
console.log(null === undefined); // false
```

---

## Type Coercion & Nullish Handling

### The Nullish Coalescing Operator (`??`)

Use `??` to provide a fallback for **only** `null` or `undefined` — without catching other falsy values like `0` or `""`.

```js
let score = 0;
let defaultScore = score ?? 10;  // returns 0  (not caught — not null/undefined)

let enteredName = null;
let displayName = enteredName ?? "Guest"; // returns "Guest"
```

Compare this with `||` (logical OR):
```js
let score = 0;
let s1 = score || 10;  // returns 10 (0 is falsy — caught by ||)
let s2 = score ?? 10;  // returns 0  (0 is not null/undefined — safe with ??)
```

---

## null vs undefined — Decision Flow

```
         ┌─────────────────────────────────────┐
         │   Does the variable have a value?    │
         └─────────────────────────────────────┘
                          │
          ┌───────────────┴───────────────┐
          ▼                               ▼
    ┌─────────────┐              ┌─────────────────┐
    │    Yes      │              │      No          │
    └─────────────┘              └─────────────────┘
          │                               │
          ▼                               ▼
    Use the value              ┌──────────────────────┐
                               │ Who caused the gap?  │
                               └──────────────────────┘
                                        │
                     ┌──────────────────┴──────────────────┐
                     ▼                                     ▼
            ┌───────────────┐                     ┌───────────────────┐
            │  Engine       │                     │  Developer        │
            │  (unassigned) │                     │  (intentional)    │
            └───────────────┘                     └───────────────────┘
                     │                                     │
                     ▼                                     ▼
              `undefined`                              `null`
```

---

## Quick Rule of Thumb

| Scenario                                      | Use          |
|-----------------------------------------------|--------------|
| Variable declared but never assigned          | `undefined` (automatic) |
| Function argument not provided                | `undefined` (automatic) |
| Property / array index doesn't exist          | `undefined` (automatic) |
| Intentional "no value" / object absent        | `null` (explicit)       |
| Cleanup / reset a variable                    | `null` (explicit)       |

---

> **TL;DR:** `undefined` is JavaScript's way of saying "nothing was ever set here". `null` is the developer saying "I'm intentionally setting this to nothing". Use `??` to safely handle both without falsey-value surprises.
