# JavaScript Identifiers vs Literals

## Example Snippet

```js
let name = "Alex";
//   ^^     ^^^^^^
//   |        |
//   |     Literal (the actual value)
// Identifier (the container name)
```

---

## Comparison Table

| Aspect              | Identifier                                            | Literal                                                  |
|---------------------|-------------------------------------------------------|----------------------------------------------------------|
| **What it is**      | A named label for a variable, function, or property   | A fixed value written directly into the source code      |
| **Mutability**      | Points to a value that can change (unless `const`)    | Represents a fixed, unchangeable value                   |
| **Quotation**       | Never wrapped in quotes                               | Strings wrapped in quotes; other types use syntax        |
| **Examples**        | `totalAmount`, `getUser`, `_cache`, `$id`             | `42`, `"Hello"`, `true`, `[1, 2, 3]`, `{ age: 25 }`     |
| **In memory**       | A reference (pointer) to where data is stored         | The actual data itself (or its representation)           |

---

## Detailed Breakdown

### What is an Identifier?

An identifier is a name you create to refer to variables, functions, or properties.

**Rules:**
- Must start with a letter (`a-z`, `A-Z`), underscore (`_`), or dollar sign (`$`)
- Cannot start with a digit
- Can contain letters, digits, underscores, or dollar signs after the first char
- Case-sensitive (`user` vs `User` are different)
- Cannot be a reserved keyword (`let`, `function`, `class`, etc.)

```js
// ✅ Valid identifiers
let firstName = "Alex";
const $price = 99;
function _calculate() {}

// ❌ Invalid identifiers
let 1user = "Mark";      // Starts with a digit
let user-name = "Mark";  // Hyphen not allowed
let const = 10;          // 'const' is a reserved keyword
```

### What is a Literal?

A literal is data provided directly in the code — the actual value.

```js
let count = 5;                  // 5 is a numeric literal
let greeting = "Hello";         // "Hello" is a string literal
let isOnline = true;            // true is a boolean literal
let numbers = [10, 20, 30];     // [10, 20, 30] is an array literal
let config = { theme: "dark" }; // { theme: "dark" } is an object literal
let message = `Hi ${name}`;     // `Hi ${name}` is a template literal
```

---

## Identifier → Literal Pipeline

```
┌─────────────────┐      ┌─────────────────┐      ┌─────────────────┐
│  Write code     │ ───► │  JavaScript      │ ───► │  Memory         │
│  in Editor      │      │  Engine (V8)     │      │  Allocation     │
│                 │      │                  │      │                 │
│  let price = 99 │      │  Parses token    │      │  Stack: price ──┼──┐
│  ^^^^^   ^^     │      │  → identifier    │      │  Heap: 99       │  │
│  ident  literal │      │  → numeric lit   │      │                 │  │
└─────────────────┘      └─────────────────┘      └─────────────────┘  │
                                                         ┌──────────────┘
                                                         │
                                                  Reference link
                                                  identifier → literal
```

---

## Quick Rule of Thumb

| If you want to...                    | That's a...     |
|--------------------------------------|-----------------|
| Name something (variable, function)  | **Identifier**  |
| Write a concrete value               | **Literal**     |
| Reassign or reuse a value            | **Identifier**  |
| Fix a constant in your code          | **Literal**     |

---

> **TL;DR:** An identifier is the *name tag* you give to data. A literal is the *actual data* itself. `let age = 25;` — `age` is the identifier (label), `25` is the literal (value).
