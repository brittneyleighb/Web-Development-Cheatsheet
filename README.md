# Web Development Cheatsheet

A reference covering the full web development stack: from how the internet delivers a webpage, through HTML, CSS, JavaScript, mobile design, server-side Node.js and PHP, relational databases, React, and accessibility.

**How this document is organized:**
- **Part 1** — Conceptual summary with analogies.
- **Part 2** — Quick-lookup cheatsheet with copy-pasteable code.
- **Part 3** — Component deep-dives: what each major piece *is*, *why* it's useful, and *how* it contributes to the stack.
- **Part 4** — Alphabetical glossary of terms.
- **Part 5** — Curated resources for further learning, especially distributed web applications.

---

## Part 1 — Module Summaries

### 1. Introduction to Web Programming

Before any coding, you need a mental picture of what's happening when you type a URL. The web is a giant **postal system for documents**.

- **The internet** is the road network — physical wires and wireless connections between computers.
- **The Web** (built on the internet) is one specific service running on those roads: documents linked together by hypertext.
- **IP addresses** are house numbers (e.g., `198.51.100.7`). **Domain names** like `wikipedia.org` are friendly nicknames; **DNS** is the phonebook that translates names to numbers.
- **HTTP** is the language two computers speak when one asks for a webpage and the other answers. **HTTPS** is the same conversation, encrypted.
- A **URL** is a complete mailing address: `protocol://domain:port/path?query#fragment`.
- A **web server** is a program that hands out webpages when asked. A **web browser** is the program that asks, then renders the result.
- The big three client-side languages: **HTML** for structure (the skeleton), **CSS** for presentation (the clothes), **JavaScript** for behavior (the muscles).

### 2. HTML Fundamentals

HTML is a **markup language**, not a programming language — it labels content rather than computing anything. Tags are like sticky notes on a manuscript saying "this is a heading" or "this is a list."

Every HTML document has a fixed scaffold: `<!DOCTYPE html>`, `<html>`, `<head>` (metadata, title, links to stylesheets), and `<body>` (visible content). Elements come in opening/closing pairs (`<p>...</p>`); a few are self-closing (`<br>`, `<img>`).

Core elements you'll use constantly: paragraphs `<p>`, line breaks `<br>`, six heading levels `<h1>`–`<h6>`, emphasis `<em>` and `<strong>`, ordered/unordered lists `<ol>`/`<ul>` with `<li>` items, tables (`<table>`, `<tr>`, `<th>`, `<td>`), images `<img src="..." alt="...">`, and links `<a href="...">`.

Two rules you'll thank yourself for: always include `alt` text on images (accessibility + a fallback when the image fails), and use **semantic** elements (`<section>`, `<article>`, `<nav>`) instead of generic `<div>` everywhere — semantic HTML is like labeling boxes in a moving truck instead of leaving them blank.

### 3. More HTML

This is where HTML gets practical for real applications.

**Containers** — `<div>` is a generic block-level box; `<span>` is a generic inline box. Use them as wrappers when no semantic element fits.

**Forms** — the bridge between users and servers. A `<form action="..." method="post">` collects input from widgets like `<input>` (with type attributes for text, email, password, number, date, checkbox, radio, file), `<textarea>`, `<select>`/`<option>`, and `<button>`. The `name` attribute is what gets sent to the server; the `id` connects to a `<label>`. Modern HTML adds widgets like color pickers, range sliders, and date pickers — all just different `type` values on `<input>`.

**Audio and video** — `<audio>` and `<video>` elements with `src` and `controls` attributes embed media without plugins.

### 4. CSS Fundamentals

If HTML is the skeleton, CSS is **the wardrobe and the lighting**. Every CSS rule has the same shape:

```css
selector {
  property: value;
  property: value;
}
```

**Three places CSS can live**: inline (`style="..."` on a single element — last resort), embedded (`<style>` block in the `<head>`), or external (`<link rel="stylesheet" href="styles.css">` — best practice, like keeping recipes in a cookbook instead of scribbling them on each plate).

**Selectors** match elements: tag (`p`), class (`.warning`), id (`#main`), descendant (`nav a`), child (`nav > a`), pseudo-class (`a:hover`), pseudo-element (`p::first-line`).

**The cascade and specificity**: when multiple rules match the same element, the more specific rule wins. The hierarchy: inline > id > class > tag. Think of it as a courtroom — louder, more specific arguments override general ones.

**The Box Model** is the single most important CSS concept. Every element is four nested rectangles: **content** (the kid), **padding** (the inner cushion around the kid), **border** (the picture frame), **margin** (the personal space outside the frame). Setting `box-sizing: border-box` makes width/height include padding and border — almost always what you want.

### 5. More CSS

Modern layout. Float-based hacks are dead; we now have two purpose-built systems:

**Flexbox** — one-dimensional layout. Set `display: flex` on a container; its children become flex items that you arrange in a row or column. Think of it as **lining up books on a single shelf**, where you control spacing, alignment, and wrap. Key properties: `flex-direction`, `justify-content` (main axis), `align-items` (cross axis), `gap`, `flex-wrap`.

**Grid** — two-dimensional layout. Set `display: grid` and define rows and columns with `grid-template-columns` / `grid-template-rows`. Like **planning a chessboard** — you place items into named cells. Use grid for whole-page layouts; use flexbox for components inside those cells.

**Positioning** — `static` (default), `relative` (offset from where it would normally be), `absolute` (positioned relative to nearest positioned ancestor), `fixed` (relative to viewport, ignores scrolling), `sticky` (acts relative until it hits a threshold, then fixed).

**Transitions and animations** — `transition: property duration easing` smoothly interpolates between states. `@keyframes` plus `animation` gives you full control over multi-step animations. **Sass** is a CSS preprocessor that adds variables, nesting, and mixins; it compiles to plain CSS.

### 6. JavaScript Fundamentals

JavaScript is the **brain** that runs in the browser (and increasingly on servers via Node.js). It's an interpreted, dynamically typed language standardized as **ECMAScript**.

**Variables**: `let` (block-scoped, reassignable), `const` (block-scoped, can't be reassigned), `var` (legacy, function-scoped — avoid).

**Types**: primitives — `number`, `string`, `boolean`, `null`, `undefined`, `symbol`, `bigint`. Everything else is an `object`.

**Equality gotcha**: `==` does type coercion (`"5" == 5` is `true`). `===` is strict (`"5" === 5` is `false`). **Always use `===`** unless you have a specific reason not to.

**Control flow**: `if`/`else`, `switch`, ternary `cond ? a : b`. Loops: `for`, `while`, `do/while`, `for...of` (values), `for...in` (keys — usually wrong choice for arrays).

**Functions** are first-class values. Three flavors:

```javascript
function classic(x) { return x * 2; }
const expr = function(x) { return x * 2; };
const arrow = x => x * 2;
```

Arrow functions don't bind their own `this` — that's both a feature and a footgun.

**Arrays** are flexible lists with methods like `push`, `pop`, `map`, `filter`, `reduce`, `forEach`, `find`. **Objects** are key-value bags: `const user = { name: "Ana", age: 30 };`. **Maps** are ordered key-value collections that allow non-string keys. **Built-in objects**: `String`, `Date`, `Math`. Errors are handled with `try`/`catch`/`finally` and thrown with `throw`.

### 7. JavaScript in the Browser

JavaScript becomes powerful when it can reach into the page and change it. The bridge is the **DOM (Document Object Model)** — the browser's live, in-memory representation of the HTML document as a tree.

The page is a **family tree**: the document is the root; every element is a node with a parent, possibly siblings, and possibly children. JavaScript can find any node and modify it.

**Finding nodes**: `document.getElementById("foo")`, `document.querySelector(".bar")` (single match using a CSS selector), `document.querySelectorAll("li")` (all matches).

**Modifying nodes**: `element.textContent`, `element.innerHTML` (be careful — security risk with user input), `element.setAttribute()`, `element.classList.add/remove/toggle()`, `element.style.color = "red"`.

**Event-driven programming**: the browser fires events (`click`, `input`, `submit`, `keydown`, `mouseover`, `load`). You attach listeners: `button.addEventListener("click", handler)`. The event object passed to your handler carries useful info like `event.target` (what was clicked) and methods like `event.preventDefault()`.

**Timers**: `setTimeout(fn, ms)` runs once after a delay; `setInterval(fn, ms)` runs repeatedly. Cancel with `clearTimeout` / `clearInterval`.

**Form validation**: catch the `submit` event, check input values, call `event.preventDefault()` if invalid.

**JSON** (JavaScript Object Notation) is a lightweight text format that mirrors JS object syntax — `JSON.parse()` text into an object, `JSON.stringify()` an object into text.

**Ajax / XMLHttpRequest** lets the page talk to a server in the background without a full reload — the technique that made modern web apps possible. (Modern code uses `fetch` instead.)

### 8. More JavaScript

Advanced features that turn JavaScript from "scripting" into "real engineering."

**Regular expressions** — pattern-matching mini-language. `/^\d{3}-\d{4}$/.test("555-1234")` checks a phone format. Methods: `.test()`, `.match()`, `.replace()`.

**Classes** (ES6+) — syntactic sugar over JavaScript's prototype-based inheritance. `class Animal { constructor(name) { this.name = name; } speak() {...} }`. Extend with `class Dog extends Animal`. ES13 added private fields with `#` prefix.

**Closures** — when a function "remembers" the variables from the scope where it was defined, even after that scope has finished. Like a backpack the function carries with it. Foundation of module patterns and many React hooks.

**Modules** — `export` from one file, `import` into another. Replaces the old "everything is global" mess. Modern: `import { thing } from './file.js';`.

**Strict mode** — `"use strict";` at the top of a file or function turns silent errors into thrown ones. Modules use it automatically.

**Web storage** — `localStorage` (persists across sessions) and `sessionStorage` (cleared when tab closes). Both store strings only; use `JSON.stringify` for objects.

**Canvas** — `<canvas>` element + JavaScript drawing API for 2D graphics, games, charts. You get a context (`canvas.getContext("2d")`) and call methods like `fillRect`, `arc`, `drawImage`.

**WebSockets** — a persistent, two-way connection to a server. Used for chat, multiplayer games, live dashboards.

**Promises and async/await** — modern way to handle asynchronous work. A Promise is an "IOU" object: it represents a value that will arrive later. Three states: pending, fulfilled, rejected. `.then()`/`.catch()` chains; `async`/`await` makes promise-based code read like synchronous code.

**Fetch API** — modern replacement for XMLHttpRequest. `fetch(url).then(r => r.json()).then(data => ...)` or with async/await:

```javascript
const response = await fetch(url);
const data = await response.json();
```

### 9. jQuery

A once-dominant library that smoothed over browser inconsistencies and gave terse syntax. Modern browsers and frameworks have made it largely unnecessary, but you'll still see it in legacy code.

Core idea: `$("selector")` returns a wrapped collection you can chain methods on. `$(".btn").addClass("active").on("click", handler)`.

Key features: selectors (CSS syntax), DOM manipulation (`html()`, `text()`, `append()`), events (`on`, `off`, `click`, `submit`), animations (`fadeIn`, `slideDown`), Ajax (`$.get`, `$.post`, `$.ajax`).

### 10. Mobile Web Development

Phones aren't tiny desktops; they have small screens, touch input, and varying network quality. **Responsive design** is the practice of making one site adapt to all of them.

**Viewport meta tag** — without `<meta name="viewport" content="width=device-width, initial-scale=1.0">`, mobile browsers pretend they're a 980-pixel-wide desktop and shrink everything. This single line tells them to behave.

**Media queries** — CSS that activates only under certain conditions:

```css
@media (max-width: 600px) {
  .sidebar { display: none; }
}
```

It's like having multiple outfits and putting on the right one based on the weather.

**Responsive images** — `srcset` lets the browser pick the best image size for the device, saving bandwidth on phones.

**Bootstrap** — a popular CSS framework with a 12-column grid, prebuilt components (navbars, modals, cards), and utility classes. Lets you build a respectable layout quickly without writing custom CSS.

### 11. Node.js (Server-Side JavaScript)

**Node.js** runs JavaScript outside the browser, on a server. Same language for front-end and back-end is one of the appeals.

**Front-end vs. back-end**: front-end is what runs in the user's browser (HTML/CSS/JS). Back-end is what runs on the server (Node, PHP, Python, databases). A **full-stack developer** does both.

**npm** is Node's package manager. `npm init` starts a project; `npm install express` adds a dependency. The `package.json` file is your project's recipe.

**Express** is the dominant Node web framework. The mental model: an Express app is a **conveyor belt** of middleware functions. A request enters one end, each middleware can inspect or modify it (parse JSON, check auth, log), and eventually a route handler sends a response.

```javascript
const express = require('express');
const app = express();
app.get('/users/:id', (req, res) => {
  res.send(`User ${req.params.id}`);
});
app.listen(3000);
```

**Pug** is a template engine that lets you generate HTML from server data using a concise indentation-based syntax.

**Database integration**: Node connects to **MySQL** (relational) via the `mysql2` module and **MongoDB** (document database) typically via **Mongoose**, an ODM that lets you define schemas for the otherwise schemaless MongoDB.

**RESTful APIs** — a convention for designing web APIs around resources and HTTP verbs: GET (read), POST (create), PUT/PATCH (update), DELETE (delete). Each resource has a URL like `/api/posts/42`.

**Authentication** — verifying who a user is. **Password hashing** (bcrypt) one-way scrambles passwords before storing them; you compare hashes at login, never store plaintext. **Token-based auth** (commonly **JWT**) issues a signed token on login that the client sends with each request, eliminating the need to look up sessions on every call.

### 12. PHP Fundamentals

**PHP** is a server-side language whose primary purpose is generating dynamic webpages. Files are usually `.php`; HTML and PHP can mix in the same file using `<?php ... ?>` tags.

Variables start with `$` (`$name = "Ana";`). Arrays handle both indexed (`$list = [1, 2, 3];`) and associative (`$user = ["name" => "Ana"];`). Conditionals and loops mirror C/JavaScript. Functions: `function greet($name) { return "Hi, $name"; }`.

**Includes** — `include 'header.php';` or `require 'config.php';` — are how PHP composes pages from reusable parts (think LEGO).

**Form handling** — when a form posts to a PHP script, the data is in `$_POST` (or `$_GET` for GET requests). Always **validate and sanitize** — never trust user input. PHP provides `filter_var` for common checks (email, URL, int).

### 13. More PHP

**File handling** — `fopen`, `fread`, `fwrite`, `fclose`, plus shortcuts like `file_get_contents`. **File uploads** come in via `$_FILES` and need careful validation (size, type, where you save them).

**Cookies** (`setcookie`) are small bits of data stored in the browser. **Sessions** (`$_SESSION`, started with `session_start()`) keep user state across requests using a server-side store with a cookie-based ID — like a coat-check ticket.

**Database access** — PHP traditionally used `mysql_*` (deprecated, insecure), then `mysqli`, and now **PDO (PHP Data Objects)**, a unified interface that supports many databases. Always use **prepared statements** to prevent SQL injection.

**Authentication** — implementing it yourself: hash passwords with `password_hash`, verify with `password_verify`, store user identity in `$_SESSION`.

### 14. Relational Databases and SQL

A **relational database** stores information about **entities** (things you care about — users, products, orders) in **tables**. Each row is one entity; each column is one attribute.

**SQL (Structured Query Language)** is the lingua franca of relational databases. The four operations together are **CRUD**: Create, Retrieve, Update, Delete.

**Schema definition**:

```sql
CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(255) UNIQUE
);
```

**Inserting**: `INSERT INTO users (name, email) VALUES ('Ana', 'ana@x.com');`

**Querying**: `SELECT name, email FROM users WHERE id = 1;`. Add `ORDER BY`, `LIMIT`, `GROUP BY`, `HAVING` as needed.

**Joining** combines rows from multiple tables. Think of joins as **stitching tables together along a shared seam** (a foreign key). `INNER JOIN` keeps only matching rows; `LEFT JOIN` keeps all rows from the left table even without a match.

```sql
SELECT u.name, o.total
FROM users u
INNER JOIN orders o ON o.user_id = u.id;
```

**Aggregate functions** — `COUNT`, `SUM`, `AVG`, `MIN`, `MAX` — usually paired with `GROUP BY`.

**Updating and deleting**: `UPDATE users SET email='new@x.com' WHERE id=1;` and `DELETE FROM users WHERE id=1;`. **Always include a WHERE clause unless you mean to affect every row** (a common career-defining mistake).

### 15. React

**React** is a JavaScript library for building user interfaces from reusable **components**. Instead of imperatively manipulating the DOM ("find this node, change its text"), you describe what the UI should look like for a given state, and React figures out the minimum changes needed. The mental shift: **declarative, not imperative.**

**JSX** is HTML-like syntax inside JavaScript. It compiles down to function calls.

```jsx
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}
```

**Components** are functions that return JSX. They take **props** (read-only inputs from a parent — like function arguments). They can have **state** (internal, mutable data; changing it triggers a re-render).

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

**Conditional rendering** uses standard JS expressions: `{loggedIn ? <Dashboard/> : <Login/>}`.

**Lists** — render arrays with `.map()` and a unique `key` prop on each item. The `key` lets React efficiently track which items changed.

**Forms** are usually **controlled components** — the input's value lives in state, and `onChange` updates it. The component is the single source of truth.

**Router** (`react-router-dom`) handles client-side navigation in a single-page app.

**Fetching data** — typically via `useEffect` + `fetch`, or libraries like React Query.

**Styling** — plain CSS files, CSS modules, styled-components, or framework integrations like **React Bootstrap**.

### 16. Web Accessibility (a11y)

Accessibility means designing so people with disabilities — visual, motor, hearing, cognitive — can use your site. It's both a moral and often legal requirement, and accessible sites tend to be better for everyone.

**Tools**: screen readers (VoiceOver, NVDA, JAWS), keyboard-only navigation, automated checkers (axe, Lighthouse).

**Page structure** — use semantic HTML (`<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>`). Headings should form a logical outline (don't skip levels). One `<h1>` per page.

**WAI-ARIA** — attributes that fill gaps when HTML alone can't express semantics: `role="button"`, `aria-label="Close menu"`, `aria-hidden="true"`. **First rule of ARIA: don't use ARIA when a native HTML element will do.**

**Color** — never convey information with color alone (think colorblind users). Maintain enough contrast (WCAG AA: 4.5:1 for body text).

**Images** — every `<img>` needs an `alt` attribute. Decorative images get `alt=""`. Meaningful ones describe content concisely.

**Links** — link text should make sense out of context. "Click here" is bad; "Read the privacy policy" is good.

**Forms** — every input needs a `<label>` properly associated (matching `for`/`id`). Group related inputs with `<fieldset>` and `<legend>`. Show clear error messages.

---

## Part 2 — Cheatsheet

### HTML skeleton

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header><nav>...</nav></header>
  <main>...</main>
  <footer>...</footer>
  <script src="app.js"></script>
</body>
</html>
```

### Common HTML elements

| Need | Element |
|---|---|
| Paragraph | `<p>` |
| Headings | `<h1>` through `<h6>` |
| Bold / italic (semantic) | `<strong>` / `<em>` |
| Unordered / ordered list | `<ul>`/`<ol>` with `<li>` |
| Table | `<table>` with `<tr>`, `<th>`, `<td>` |
| Image | `<img src="..." alt="...">` |
| Link | `<a href="...">text</a>` |
| Form | `<form action="..." method="post">` |
| Text input | `<input type="text" name="..." id="...">` |
| Label | `<label for="id">Text</label>` |
| Button | `<button type="submit">Go</button>` |
| Generic block / inline | `<div>` / `<span>` |
| Semantic regions | `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>` |

### CSS selectors

| Goal | Selector |
|---|---|
| All `<p>` | `p` |
| Class `warning` | `.warning` |
| Id `main` | `#main` |
| Descendant | `nav a` |
| Direct child | `nav > a` |
| Adjacent sibling | `h2 + p` |
| Attribute | `input[type="email"]` |
| Hover | `a:hover` |
| First child | `li:first-child` |
| nth | `tr:nth-child(odd)` |
| First line | `p::first-line` |
| Before / after | `p::before` / `p::after` |

### CSS box model & sizing

```css
* { box-sizing: border-box; }   /* width includes padding + border */
.box {
  width: 300px;
  padding: 16px;
  border: 2px solid black;
  margin: 8px;
}
```

### Flexbox quick reference

```css
.container {
  display: flex;
  flex-direction: row;        /* row | column */
  justify-content: center;    /* main axis: flex-start | center | space-between | space-around */
  align-items: center;        /* cross axis */
  gap: 1rem;
  flex-wrap: wrap;
}
.item { flex: 1; }            /* grow to fill */
```

### Grid quick reference

```css
.grid {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;     /* 3 columns: 25/50/25 */
  grid-template-rows: auto;
  gap: 1rem;
}
.item { grid-column: 1 / 3; }             /* span columns 1–2 */
```

### Media queries

```css
@media (max-width: 768px) {
  .sidebar { display: none; }
}
@media (prefers-color-scheme: dark) {
  body { background: #111; color: #eee; }
}
```

### JavaScript essentials

```javascript
// Variables
let mutable = 1;
const fixed = 2;

// Strings (use template literals)
const name = "Ana";
console.log(`Hi, ${name}`);

// Arrays
const nums = [1, 2, 3];
nums.push(4);
const doubled = nums.map(n => n * 2);
const evens = nums.filter(n => n % 2 === 0);
const sum = nums.reduce((a, b) => a + b, 0);

// Objects
const user = { name: "Ana", age: 30 };
const { name: userName } = user;       // destructuring
const copy = { ...user, age: 31 };     // spread

// Functions
const add = (a, b) => a + b;
function greet(name = "world") { return `Hi ${name}`; }

// Conditionals
const status = age >= 18 ? "adult" : "minor";

// Loops
for (const n of nums) { /* ... */ }
nums.forEach(n => console.log(n));
```

### DOM manipulation

```javascript
const el = document.querySelector(".btn");
const all = document.querySelectorAll("li");

el.textContent = "Hi";
el.classList.add("active");
el.setAttribute("disabled", "true");
el.style.color = "red";

el.addEventListener("click", e => {
  e.preventDefault();
  console.log(e.target);
});

const div = document.createElement("div");
div.textContent = "new";
parent.appendChild(div);
```

### Fetch (modern Ajax)

```javascript
async function loadUsers() {
  try {
    const res = await fetch("/api/users");
    if (!res.ok) throw new Error(res.statusText);
    const users = await res.json();
    return users;
  } catch (err) {
    console.error(err);
  }
}

// POST with body
await fetch("/api/users", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ name: "Ana" }),
});
```

### Promises and async/await

```javascript
// Promise chain
fetch(url).then(r => r.json()).then(data => console.log(data));

// async/await — same thing, more readable
async function main() {
  const r = await fetch(url);
  const data = await r.json();
  console.log(data);
}

// Run in parallel
const [a, b] = await Promise.all([fetchA(), fetchB()]);
```

### Node.js + Express minimal server

```javascript
const express = require('express');
const app = express();

app.use(express.json());                // parse JSON bodies

app.get('/api/users/:id', (req, res) => {
  res.json({ id: req.params.id });
});

app.post('/api/users', (req, res) => {
  const { name } = req.body;
  res.status(201).json({ name });
});

app.listen(3000, () => console.log('running on :3000'));
```

### npm commands

```bash
npm init -y                  # create package.json
npm install express          # add a dependency
npm install --save-dev jest  # add a dev dependency
npm uninstall pkg            # remove
npm run start                # run "start" script from package.json
npx some-tool                # run a package without installing globally
```

### PHP essentials

```php
<?php
// Variables and strings
$name = "Ana";
echo "Hello, $name";              // double quotes interpolate
echo 'Hello, ' . $name;           // concatenate

// Arrays
$list = [1, 2, 3];
$user = ["name" => "Ana", "age" => 30];

// Conditionals & loops
if ($age >= 18) { /*...*/ } else { /*...*/ }
foreach ($list as $n) { echo $n; }

// Functions
function greet($name = "world") {
  return "Hi $name";
}

// Form data
$email = $_POST['email'] ?? '';
if (!filter_var($email, FILTER_VALIDATE_EMAIL)) { /* invalid */ }

// PDO with prepared statements (safe)
$pdo = new PDO("mysql:host=localhost;dbname=app", $user, $pass);
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = :id");
$stmt->execute([':id' => 1]);
$row = $stmt->fetch();

// Sessions
session_start();
$_SESSION['user_id'] = 42;

// Password hashing
$hash = password_hash($plain, PASSWORD_DEFAULT);
if (password_verify($plain, $hash)) { /* ok */ }
?>
```

### SQL essentials

```sql
-- Create
CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(255) UNIQUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Insert
INSERT INTO users (name, email) VALUES ('Ana', 'ana@x.com');

-- Read
SELECT name, email FROM users WHERE id = 1;
SELECT * FROM users ORDER BY created_at DESC LIMIT 10;
SELECT COUNT(*) FROM users;
SELECT country, COUNT(*) AS n FROM users GROUP BY country HAVING n > 5;

-- Joins
SELECT u.name, o.total
FROM users u
INNER JOIN orders o ON o.user_id = u.id
WHERE o.total > 100;

-- Update / delete (always use WHERE!)
UPDATE users SET email = 'new@x.com' WHERE id = 1;
DELETE FROM users WHERE id = 1;
```

### React basics

```jsx
import { useState, useEffect } from 'react';

function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch('/api/users')
      .then(r => r.json())
      .then(data => { setUsers(data); setLoading(false); });
  }, []);   // [] = run once on mount

  if (loading) return <p>Loading...</p>;

  return (
    <ul>
      {users.map(u => <li key={u.id}>{u.name}</li>)}
    </ul>
  );
}

// Props
function Greeting({ name = "world" }) {
  return <h1>Hello, {name}</h1>;
}

// Controlled form
function NameForm() {
  const [value, setValue] = useState("");
  return (
    <form onSubmit={e => { e.preventDefault(); console.log(value); }}>
      <input value={value} onChange={e => setValue(e.target.value)} />
      <button type="submit">Send</button>
    </form>
  );
}
```

### Accessibility checklist

- Every page has a `<title>` and `lang` attribute on `<html>`.
- One `<h1>`; headings descend in order.
- Use semantic landmarks: `<header>`, `<nav>`, `<main>`, `<footer>`.
- Every `<img>` has `alt` text (empty `alt=""` for decorative).
- Every form `<input>` has a matching `<label>`.
- Color contrast meets WCAG AA (4.5:1 for body text).
- Site is fully usable with keyboard (Tab, Shift+Tab, Enter, Space).
- Focus indicators are visible (don't `outline: none` without a replacement).
- Don't convey meaning by color alone.
- Use ARIA only when native HTML can't express the meaning.

### HTTP status codes (the ones you'll actually see)

| Code | Meaning |
|---|---|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 301 / 302 | Permanent / temporary redirect |
| 400 | Bad Request (client error) |
| 401 | Unauthorized (not logged in) |
| 403 | Forbidden (logged in but not allowed) |
| 404 | Not Found |
| 409 | Conflict |
| 422 | Unprocessable Entity (validation failed) |
| 500 | Internal Server Error |
| 503 | Service Unavailable |

### REST conventions

| Verb | Path | Means |
|---|---|---|
| GET | `/posts` | List all posts |
| GET | `/posts/42` | Get post 42 |
| POST | `/posts` | Create a new post |
| PUT | `/posts/42` | Replace post 42 |
| PATCH | `/posts/42` | Partially update post 42 |
| DELETE | `/posts/42` | Delete post 42 |

### Security quick wins

- Always use HTTPS in production.
- Hash passwords (bcrypt/argon2) — never store plaintext.
- Use prepared statements / parameterized queries — never concatenate SQL.
- Escape user input before inserting into HTML to prevent XSS; prefer `textContent` over `innerHTML`.
- Validate input on both client and server (client validation is for UX, server is for safety).
- Set `Content-Security-Policy`, `X-Frame-Options`, and other security headers.
- Keep dependencies updated; run `npm audit` periodically.

---

## Part 3 — Component Deep-Dives

For each major piece of the stack: **what it is**, **why it's useful**, and **how it fits in**. The metaphor I'll use throughout: building a web app is like running a restaurant. The customer (browser) places an order; somewhere in the back, ingredients are stored, prepared, and assembled into a dish (a webpage or API response).

### DOM (Document Object Model)

**What it is.** When the browser loads an HTML document, it parses the text and builds an in-memory tree representing every element, attribute, and piece of text. That live tree is the DOM. JavaScript can read and modify this tree, and any change it makes is reflected on screen instantly.

**Why it's helpful to know.** The DOM is the **single interface between code and the visible page**. Without it, JavaScript would just be a calculator running in a void. Every front-end framework (React, Vue, Angular) is, at bottom, a clever way of efficiently updating the DOM. Understanding it directly makes you better at debugging, performance-tuning, and reading any front-end framework's source.

**How it contributes.** The DOM is what makes pages **interactive instead of static**. Every dropdown, drag-and-drop, autocomplete, or live-updating chart is JavaScript reaching into the DOM and mutating nodes. In the restaurant metaphor, the DOM is the **kitchen pass-through window** — the only place where what happens behind the scenes becomes visible to the customer.

### Fetch API

**What it is.** A modern, promise-based JavaScript API for making HTTP requests. It replaced the older, clunkier `XMLHttpRequest`. You give it a URL and options; it returns a `Promise` that resolves to a `Response` object you can read as JSON, text, or a blob.

**Why it's helpful to know.** Almost every interesting web app needs to talk to a server after the initial page load — to load more data, submit a form without a full reload, or fetch live updates. Fetch is the standard, browser-native way to do this. It's the **front-end side of every API integration**, REST call, and microservice handshake.

**How it contributes.** Fetch is what enables the **single-page application** pattern: the browser loads a shell once, then uses fetch to retrieve fresh data as the user navigates. It's also the backbone of communication between front-end and back-end services — the **walkie-talkie between the dining room and the kitchen** in the restaurant metaphor.

### Node.js

**What it is.** A runtime that lets you execute JavaScript outside the browser, on a server. It's built on Chrome's V8 engine and adds APIs the browser doesn't expose: file system access, networking, child processes. Released in 2009, it changed web development by letting one language run on both client and server.

**Why it's helpful to know.** Modern web tooling is overwhelmingly Node-based — build tools (Webpack, Vite), test runners (Jest, Vitest), linters (ESLint), and CLI utilities all run on Node. Even if you write your back-end in Python or Java, you'll still use Node for tooling. And it's a popular choice for building APIs, microservices, real-time apps, and serverless functions.

**How it contributes.** Node is the **back-of-house staff** of the restaurant — it preps the ingredients, takes orders, talks to suppliers (databases, third-party APIs), and assembles the dishes. Its **non-blocking, event-driven** model is particularly good at I/O-heavy workloads (lots of concurrent network calls), which is exactly what most web servers do.

### npm (Node Package Manager)

**What it is.** The default package manager for Node.js, and by extension the largest software registry in the world (over 2 million packages). The `npm` CLI tool reads a `package.json` file, installs declared dependencies into a `node_modules/` folder, and lets you run scripts.

**Why it's helpful to know.** Modern projects are not built from scratch — they're assembled from dozens or hundreds of open-source packages. Knowing how to install, update, and audit dependencies, and how to read a `package.json`, is non-negotiable. You'll also use `npx` constantly to run one-off tools without installing them globally.

**How it contributes.** npm is the **wholesale ingredient supplier**: instead of growing your own tomatoes, you order from packages that already work. The trade-off is supply-chain risk — `npm audit` and lockfiles (`package-lock.json`) exist precisely because you're trusting other people's code. Yarn and pnpm are popular alternatives that solve the same problem with different trade-offs.

### React

**What it is.** A JavaScript library (not a full framework) for building user interfaces from reusable, self-contained components. Created at Facebook in 2013. Its core idea: describe what the UI *should* look like for a given state, and React diffs that against the current DOM to apply the minimum changes.

**Why it's helpful to know.** React is the dominant front-end library — used by a huge share of modern web apps and the foundation for frameworks like Next.js. Even teams not using React are usually using something with the same model (Vue, Svelte, Solid). The mental model — **declarative components with one-way data flow** — is now the lingua franca of UI development.

**How it contributes.** React lets you build **complex, dynamic UIs without losing your sanity**. Without it (or something like it), keeping the DOM in sync with rapidly changing application state means hand-wiring dozens of event handlers and DOM mutations — error-prone and hard to maintain. React is the **plating system that always produces the same dish for the same ingredients**, and only re-plates the parts that actually changed.

### SQL (Structured Query Language)

**What it is.** The standardized language for talking to relational databases. Originally designed in the 1970s, still everywhere today. Used to define schemas, insert and update data, and — most importantly — query data with rich filtering, joining, and aggregating.

**Why it's helpful to know.** Almost every web app has a database, and most of those are relational. SQL is the **most portable and durable skill in this entire stack** — the syntax you learn for MySQL works (with minor tweaks) on PostgreSQL, SQLite, SQL Server, and Oracle, and the language has been stable for decades. Understanding SQL also gives you intuition for query performance, indexes, and database design.

**How it contributes.** SQL is the **pantry inventory system** — it knows what ingredients you have, where they are, and how to combine them efficiently. Modern alternatives like ORMs (Mongoose, Prisma, Sequelize) sit on top of SQL but never fully replace it; serious back-end engineers always learn SQL directly. It's also the language of **distributed databases** (Spanner, CockroachDB) and analytical engines (Snowflake, BigQuery), so the skill transfers far beyond classic web apps.

### PHP

**What it is.** A server-side scripting language designed specifically for the web. PHP files mix HTML and code; the server runs the code on each request and sends the resulting HTML to the browser. Created in 1994; still powers a huge fraction of the web (WordPress, Wikipedia, Slack at one point, and most of Facebook's early back-end).

**Why it's helpful to know.** Even though newer projects often pick Node, Python, or Go, **so much of the existing web is PHP** that you'll encounter it constantly — especially if you work with WordPress, Drupal, Magento, or legacy enterprise systems. Modern PHP (8+) is fast, has strong typing features, and a healthy ecosystem (Laravel, Symfony).

**How it contributes.** PHP is the **classic short-order cook** — it's optimized for the request-response cycle: take an order, do the work, send the dish, forget everything, repeat. That stateless model is part of why it scales horizontally so easily (just add more web servers behind a load balancer). It's also a low-friction entry into back-end web development since the deployment story can be as simple as uploading files to a server.

### How they fit together

A typical full-stack request, traced end to end:

```
Browser
  └── HTML/CSS renders structure (DOM is built)
       └── JavaScript runs in the browser
             └── User clicks "Load posts"
                  └── fetch('/api/posts')  ← Fetch API
                       └── Network → Server
                            └── Express app on Node.js receives request
                                 └── SQL query through MySQL/Postgres driver
                                      └── Database returns rows
                                 └── Server sends JSON response
                       └── Browser parses JSON
             └── React updates state, re-renders components
       └── DOM is patched, user sees new posts
```

Each layer has a single responsibility. Mastery comes from understanding *each layer's contract with the next* — not from memorizing every detail of any one.

---

## Part 4 — Glossary of Terms

A reference for terms used throughout this document and in modern web development. Listed alphabetically.

**Ajax** — Asynchronous JavaScript and XML. The original name for the technique of using JavaScript to fetch data from a server without reloading the page. The "X" is historical — most Ajax today exchanges JSON, not XML.

**API (Application Programming Interface)** — A defined contract for how software components talk to each other. A *web API* is one exposed over HTTP.

**ARIA (Accessible Rich Internet Applications)** — A set of HTML attributes (`role`, `aria-label`, etc.) that fill accessibility gaps that native HTML can't express.

**Async / await** — JavaScript syntax for writing promise-based code that reads like synchronous code. `await` pauses a function until a Promise resolves.

**Attribute** — A name-value pair on an HTML element, e.g., `href="..."`, `class="..."`.

**Back-end** — The server-side of a web application: databases, application servers, business logic. Code the user never sees directly.

**Bootstrap** — A CSS framework providing a 12-column grid, prebuilt components, and utility classes for rapid UI development.

**Box model** — The CSS rule that every element is a rectangle of nested boxes: content, padding, border, margin.

**Callback** — A function passed as an argument to another function, to be called later. The original way JavaScript handled asynchronous results before Promises.

**Cascade** — In CSS, the algorithm that decides which rule wins when multiple rules apply to the same element. Considers specificity, source order, and importance.

**Class** (HTML/CSS) — An attribute used to group elements for styling. **Class** (JS) — A blueprint for creating objects.

**Client-side** — Code that runs in the user's browser. Synonym for *front-end*.

**Closure** — A function that "remembers" the variables from the scope in which it was defined.

**Component** — In React, a reusable piece of UI defined as a function or class that returns JSX.

**Cookie** — A small piece of data stored in the browser and sent with each request to the same domain. Used for sessions, preferences, tracking.

**CRUD** — Create, Retrieve, Update, Delete — the four basic database operations.

**CSS (Cascading Style Sheets)** — The language for describing how HTML elements should look.

**DNS (Domain Name System)** — The phonebook of the internet: translates domain names like `example.com` to IP addresses.

**DOM (Document Object Model)** — The browser's in-memory tree representation of an HTML document, exposed to JavaScript.

**Endpoint** — A specific URL on a server that responds to requests, e.g., `GET /api/users/42`.

**Event** — A signal fired by the browser (click, scroll, keypress, etc.) that JavaScript can listen for and respond to.

**Express** — A minimal web framework for Node.js. The standard way to build HTTP APIs in Node.

**Fetch API** — Modern browser API for making HTTP requests, returning Promises.

**Flexbox** — CSS layout system for arranging items in a single row or column.

**Form** — An HTML element that collects user input and submits it to a server.

**Front-end** — Code that runs in the browser. Synonym for *client-side*.

**Full-stack** — A developer or skill set that spans both front-end and back-end.

**Grid** — CSS layout system for arranging items in a two-dimensional grid of rows and columns.

**HTML (HyperText Markup Language)** — The standard markup language for describing the structure of web documents.

**HTTP / HTTPS** — HyperText Transfer Protocol; the language browsers and servers use to communicate. HTTPS adds encryption.

**Hydration** — The process of attaching JavaScript event handlers to server-rendered HTML so it becomes interactive.

**IP address** — A computer's unique numerical address on a network.

**JavaScript / ECMAScript** — The programming language of the web browser; ECMAScript is the official standard.

**JSON (JavaScript Object Notation)** — A lightweight text format for representing structured data; the de facto standard for web APIs.

**JSX** — Syntax extension for JavaScript that looks like HTML, used in React. Compiles to function calls.

**JWT (JSON Web Token)** — A signed, self-contained token used to authenticate API requests.

**localStorage** — Browser storage that persists across sessions. Stores strings only.

**Media query** — A CSS rule that applies only when certain conditions (screen size, color scheme) are met.

**Middleware** — In Express, a function that sits in the request/response pipeline and can inspect or modify the request before it reaches the route handler.

**MongoDB** — A document-oriented (NoSQL) database that stores data as JSON-like documents.

**Mongoose** — An Object Document Mapper (ODM) that adds schema validation and query helpers on top of MongoDB.

**MVC (Model-View-Controller)** — A common architectural pattern: model holds data, view renders it, controller handles input.

**Node.js** — A runtime that lets you execute JavaScript outside the browser.

**npm** — The package manager and package registry for the Node.js ecosystem.

**ORM (Object-Relational Mapper)** — A library that maps database rows to language objects, hiding most SQL.

**Package** — A reusable bundle of code distributed via a package manager.

**PHP** — A server-side scripting language designed for web pages.

**Prepared statement** — A SQL query template with placeholders for values; the database compiles it once and executes safely with different inputs. Prevents SQL injection.

**Promise** — A JavaScript object representing the eventual result of an asynchronous operation. States: pending, fulfilled, rejected.

**Props** — In React, read-only inputs passed from a parent component to a child.

**React** — A JavaScript library for building UIs from components.

**REST (Representational State Transfer)** — An architectural style for web APIs centered on resources and HTTP verbs.

**Responsive design** — Design that adapts to different screen sizes and devices.

**Sanitization** — Cleaning user input to remove dangerous content before processing or displaying it.

**Schema** — A definition of the structure of data: tables and columns in SQL, fields in MongoDB, types in TypeScript.

**Selector** — In CSS, a pattern that matches HTML elements to style.

**Server-side** — Code that runs on the server. Synonym for *back-end*.

**Session** — Server-side state about a logged-in user, identified by a cookie.

**SPA (Single Page Application)** — A web app that loads a single HTML page and updates content via JavaScript without full reloads.

**SQL (Structured Query Language)** — The language for querying relational databases.

**SSR (Server-Side Rendering)** — Generating HTML on the server before sending it to the browser. Improves initial load and SEO.

**State** — In React, internal data owned by a component that, when changed, triggers a re-render.

**TLS / SSL** — Protocols that encrypt HTTP traffic, producing HTTPS.

**URL (Uniform Resource Locator)** — The address of a resource on the web.

**Validation** — Checking that user input meets expected rules (format, length, range).

**Viewport** — The visible area of a webpage in the browser.

**WebSocket** — A protocol that keeps a persistent two-way connection open between browser and server, used for real-time features.

**XSS (Cross-Site Scripting)** — A security vulnerability where attacker-controlled JavaScript runs in a victim's browser. Mitigated by escaping output and Content Security Policy.

---

## Part 5 — Further Reading & Resources

Curated learning resources, organized by area, with a strong emphasis on **distributed web applications** — the design patterns that let web systems scale across many machines.

### Official documentation (the canonical sources)

- **MDN Web Docs** — https://developer.mozilla.org — the definitive reference for HTML, CSS, JavaScript, and browser APIs. If a tutorial conflicts with MDN, trust MDN.
- **Web.dev** — https://web.dev — Google's curated guidance on performance, accessibility, and modern web best practices.
- **Node.js docs** — https://nodejs.org/en/docs/
- **Express** — https://expressjs.com
- **React** — https://react.dev (the new docs site, much better than the old one)
- **PHP manual** — https://www.php.net/manual/en/
- **PostgreSQL tutorial** — https://www.postgresql.org/docs/current/tutorial.html (excellent SQL learning resource even if you use MySQL)
- **MongoDB University** — https://learn.mongodb.com (free courses)
- **WHATWG HTML Living Standard** — https://html.spec.whatwg.org (the actual spec)

### Free interactive tutorials

- **freeCodeCamp** — https://www.freecodecamp.org — comprehensive free curriculum, project-based.
- **The Odin Project** — https://www.theodinproject.com — full-stack curriculum, JavaScript track is excellent.
- **JavaScript.info** — https://javascript.info — the best modern JavaScript tutorial on the web.
- **CSS Tricks: Complete Guide to Flexbox** — https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- **CSS Tricks: Complete Guide to Grid** — https://css-tricks.com/snippets/css/complete-guide-grid/
- **SQLBolt** — https://sqlbolt.com — interactive SQL lessons.
- **Mode SQL Tutorial** — https://mode.com/sql-tutorial/

### Distributed web applications — the deep stuff

A web application becomes "distributed" the moment its parts run on more than one machine: separate database server, multiple app servers behind a load balancer, third-party APIs, caches, message queues, microservices. These resources teach how to design those systems.

**Foundational reading:**

- **"Designing Data-Intensive Applications"** by Martin Kleppmann — the single best book on distributed systems for working engineers. Covers replication, partitioning, consistency, distributed transactions, batch and stream processing.
- **"Web Scalability for Startup Engineers"** by Artur Ejsmont — practical patterns for scaling from one server to many.
- **"Building Microservices"** by Sam Newman — the standard reference on microservice architecture.
- **"System Design Interview"** by Alex Xu — short, diagram-heavy walkthroughs of scaling classic systems (URL shortener, news feed, chat, etc.).

**Free online curricula:**

- **MIT 6.824: Distributed Systems** — https://pdos.csail.mit.edu/6.824/ — graduate-level course with public lectures, labs, and papers. The gold standard.
- **The System Design Primer** — https://github.com/donnemartin/system-design-primer — a free, open-source crash course.
- **Distributed Systems lecture series by Martin Kleppmann (Cambridge)** — https://www.youtube.com/playlist?list=PLeKd45zvjcDFUEv_ohr_HdUFe97RItdiB — companion lectures to the book above.
- **High Scalability blog** — http://highscalability.com — case studies of how real companies scale.

**Foundational papers worth reading once in your career:**

- *The Google File System* (2003) — origin of HDFS and modern distributed storage.
- *MapReduce* (2004) — origin of Hadoop and the batch-processing pattern.
- *Dynamo* (2007) — Amazon's eventually-consistent key-value store; foundation of Cassandra and DynamoDB.
- *Bigtable* (2006) — Google's wide-column store; foundation of HBase.
- *Paxos Made Simple* (Lamport, 2001) and *Raft* (Ongaro & Ousterhout, 2014) — distributed consensus algorithms.
- *CAP Twelve Years Later* (Brewer, 2012) — the author of the CAP theorem clarifying what it actually means.

Most are findable on https://www.usenix.org or https://cs.stanford.edu — search by title.

### REST, APIs, and microservices

- **"RESTful Web APIs"** by Leonard Richardson and Mike Amundsen — careful, principled API design.
- **REST API Tutorial** — https://restfulapi.net — practical conventions.
- **Microsoft REST API Guidelines** — https://github.com/microsoft/api-guidelines/blob/vNext/Guidelines.md — opinionated but well-justified.
- **gRPC** — https://grpc.io — the binary RPC alternative to REST, common in microservices.
- **GraphQL** — https://graphql.org — a query language for APIs, an alternative to REST for some workloads.

### Front-end performance & advanced topics

- **"High Performance Browser Networking"** by Ilya Grigorik — free online at https://hpbn.co — how the web actually works at the network level.
- **Patterns.dev** — https://www.patterns.dev — modern web patterns (rendering, data fetching, state management).
- **Refactoring UI** — https://www.refactoringui.com — practical visual design for engineers.

### Security

- **OWASP Top 10** — https://owasp.org/www-project-top-ten/ — the canonical list of web security risks.
- **OWASP Cheat Sheet Series** — https://cheatsheetseries.owasp.org — concrete defenses for each risk.
- **Mozilla Observatory** — https://observatory.mozilla.org — scan a site's security headers.

### Communities and ongoing reading

- **Hacker News** — https://news.ycombinator.com — a daily pulse on what engineers are reading.
- **Lobsters** — https://lobste.rs — smaller, higher-signal alternative to HN.
- **r/webdev** and **r/programming** on Reddit.
- **CSS Tricks newsletter** and **JavaScript Weekly** — well-curated weekly digests.

---

### Final advice

The web stack is wide, but most days you'll touch only a thin slice of it. Get fluent with the **HTML → CSS → JavaScript → DOM** loop first; that's the foundation everything else (Node, React, frameworks) is layered on top of. Build small projects end-to-end rather than reading endlessly — the only way to internalize this stack is to ship something messy and then improve it.

For each major piece of the stack: **what it is**, **why it's useful**, and **how it fits in**. The metaphor I'll use throughout: building a web app is like running a restaurant. The customer (browser) places an order; somewhere in the back, ingredients are stored, prepared, and assembled into a dish (a webpage or API response).

### DOM (Document Object Model)

**What it is.** When the browser loads an HTML document, it parses the text and builds an in-memory tree representing every element, attribute, and piece of text. That live tree is the DOM. JavaScript can read and modify this tree, and any change it makes is reflected on screen instantly.

**Why it's helpful to know.** The DOM is the **single interface between code and the visible page**. Without it, JavaScript would just be a calculator running in a void. Every front-end framework (React, Vue, Angular) is, at bottom, a clever way of efficiently updating the DOM. Understanding it directly makes you better at debugging, performance-tuning, and reading any front-end framework's source.

**How it contributes.** The DOM is what makes pages **interactive instead of static**. Every dropdown, drag-and-drop, autocomplete, or live-updating chart is JavaScript reaching into the DOM and mutating nodes. In the restaurant metaphor, the DOM is the **kitchen pass-through window** — the only place where what happens behind the scenes becomes visible to the customer.

### Fetch API

**What it is.** A modern, promise-based JavaScript API for making HTTP requests. It replaced the older, clunkier `XMLHttpRequest`. You give it a URL and options; it returns a `Promise` that resolves to a `Response` object you can read as JSON, text, or a blob.

**Why it's helpful to know.** Almost every interesting web app needs to talk to a server after the initial page load — to load more data, submit a form without a full reload, or fetch live updates. Fetch is the standard, browser-native way to do this. It's the **front-end side of every API integration**, REST call, and microservice handshake.

**How it contributes.** Fetch is what enables the **single-page application** pattern: the browser loads a shell once, then uses fetch to retrieve fresh data as the user navigates. It's also the backbone of communication between front-end and back-end services — the **walkie-talkie between the dining room and the kitchen** in the restaurant metaphor.

### Node.js

**What it is.** A runtime that lets you execute JavaScript outside the browser, on a server. It's built on Chrome's V8 engine and adds APIs the browser doesn't expose: file system access, networking, child processes. Released in 2009, it changed web development by letting one language run on both client and server.

**Why it's helpful to know.** Modern web tooling is overwhelmingly Node-based — build tools (Webpack, Vite), test runners (Jest, Vitest), linters (ESLint), and CLI utilities all run on Node. Even if you write your back-end in Python or Java, you'll still use Node for tooling. And it's a popular choice for building APIs, microservices, real-time apps, and serverless functions.

**How it contributes.** Node is the **back-of-house staff** of the restaurant — it preps the ingredients, takes orders, talks to suppliers (databases, third-party APIs), and assembles the dishes. Its **non-blocking, event-driven** model is particularly good at I/O-heavy workloads (lots of concurrent network calls), which is exactly what most web servers do.

### npm (Node Package Manager)

**What it is.** The default package manager for Node.js, and by extension the largest software registry in the world (over 2 million packages). The `npm` CLI tool reads a `package.json` file, installs declared dependencies into a `node_modules/` folder, and lets you run scripts.

**Why it's helpful to know.** Modern projects are not built from scratch — they're assembled from dozens or hundreds of open-source packages. Knowing how to install, update, and audit dependencies, and how to read a `package.json`, is non-negotiable. You'll also use `npx` constantly to run one-off tools without installing them globally.

**How it contributes.** npm is the **wholesale ingredient supplier**: instead of growing your own tomatoes, you order from packages that already work. The trade-off is supply-chain risk — `npm audit` and lockfiles (`package-lock.json`) exist precisely because you're trusting other people's code. Yarn and pnpm are popular alternatives that solve the same problem with different trade-offs.

### React

**What it is.** A JavaScript library (not a full framework) for building user interfaces from reusable, self-contained components. Created at Facebook in 2013. Its core idea: describe what the UI *should* look like for a given state, and React diffs that against the current DOM to apply the minimum changes.

**Why it's helpful to know.** React is the dominant front-end library — used by a huge share of modern web apps and the foundation for frameworks like Next.js. Even teams not using React are usually using something with the same model (Vue, Svelte, Solid). The mental model — **declarative components with one-way data flow** — is now the lingua franca of UI development.

**How it contributes.** React lets you build **complex, dynamic UIs without losing your sanity**. Without it (or something like it), keeping the DOM in sync with rapidly changing application state means hand-wiring dozens of event handlers and DOM mutations — error-prone and hard to maintain. React is the **plating system that always produces the same dish for the same ingredients**, and only re-plates the parts that actually changed.

### SQL (Structured Query Language)

**What it is.** The standardized language for talking to relational databases. Originally designed in the 1970s, still everywhere today. Used to define schemas, insert and update data, and — most importantly — query data with rich filtering, joining, and aggregating.

**Why it's helpful to know.** Almost every web app has a database, and most of those are relational. SQL is the **most portable and durable skill in this entire stack** — the syntax you learn for MySQL works (with minor tweaks) on PostgreSQL, SQLite, SQL Server, and Oracle, and the language has been stable for decades. Understanding SQL also gives you intuition for query performance, indexes, and database design.

**How it contributes.** SQL is the **pantry inventory system** — it knows what ingredients you have, where they are, and how to combine them efficiently. Modern alternatives like ORMs (Mongoose, Prisma, Sequelize) sit on top of SQL but never fully replace it; serious back-end engineers always learn SQL directly. It's also the language of **distributed databases** (Spanner, CockroachDB) and analytical engines (Snowflake, BigQuery), so the skill transfers far beyond classic web apps.

### PHP

**What it is.** A server-side scripting language designed specifically for the web. PHP files mix HTML and code; the server runs the code on each request and sends the resulting HTML to the browser. Created in 1994; still powers a huge fraction of the web (WordPress, Wikipedia, and many large platforms).

**Why it's helpful to know.** Even though newer projects often pick Node, Python, or Go, **so much of the existing web is PHP** that you'll encounter it constantly — especially if you work with WordPress, Drupal, Magento, or legacy enterprise systems. Modern PHP (8+) is fast, has strong typing features, and a healthy ecosystem (Laravel, Symfony).

**How it contributes.** PHP is the **classic short-order cook** — it's optimized for the request-response cycle: take an order, do the work, send the dish, forget everything, repeat. That stateless model is part of why it scales horizontally so easily (just add more web servers behind a load balancer). It's also a low-friction entry into back-end web development since the deployment story can be as simple as uploading files to a server.

### How they fit together

A typical full-stack request, traced end to end:

```
Browser
  └── HTML/CSS renders structure (DOM is built)
       └── JavaScript runs in the browser
             └── User clicks "Load posts"
                  └── fetch('/api/posts')  ← Fetch API
                       └── Network → Server
                            └── Express app on Node.js receives request
                                 └── SQL query through MySQL/Postgres driver
                                      └── Database returns rows
                                 └── Server sends JSON response
                       └── Browser parses JSON
             └── React updates state, re-renders components
       └── DOM is patched, user sees new posts
```

Each layer has a single responsibility. Mastery comes from understanding *each layer's contract with the next* — not from memorizing every detail of any one.

---

## Part 4 — Glossary of Terms

A reference for terms used throughout this document and in modern web development. Listed alphabetically.

**Ajax** — Asynchronous JavaScript and XML. The original name for the technique of using JavaScript to fetch data from a server without reloading the page. The "X" is historical — most Ajax today exchanges JSON, not XML.

**API (Application Programming Interface)** — A defined contract for how software components talk to each other. A *web API* is one exposed over HTTP.

**ARIA (Accessible Rich Internet Applications)** — A set of HTML attributes (`role`, `aria-label`, etc.) that fill accessibility gaps that native HTML can't express.

**Async / await** — JavaScript syntax for writing promise-based code that reads like synchronous code. `await` pauses a function until a Promise resolves.

**Attribute** — A name-value pair on an HTML element, e.g., `href="..."`, `class="..."`.

**Back-end** — The server-side of a web application: databases, application servers, business logic. Code the user never sees directly.

**Bootstrap** — A CSS framework providing a 12-column grid, prebuilt components, and utility classes for rapid UI development.

**Box model** — The CSS rule that every element is a rectangle of nested boxes: content, padding, border, margin.

**Callback** — A function passed as an argument to another function, to be called later. The original way JavaScript handled asynchronous results before Promises.

**Cascade** — In CSS, the algorithm that decides which rule wins when multiple rules apply to the same element. Considers specificity, source order, and importance.

**Class** (HTML/CSS) — An attribute used to group elements for styling. **Class** (JS) — A blueprint for creating objects.

**Client-side** — Code that runs in the user's browser. Synonym for *front-end*.

**Closure** — A function that "remembers" the variables from the scope in which it was defined.

**Component** — In React, a reusable piece of UI defined as a function or class that returns JSX.

**Cookie** — A small piece of data stored in the browser and sent with each request to the same domain. Used for sessions, preferences, tracking.

**CRUD** — Create, Retrieve, Update, Delete — the four basic database operations.

**CSS (Cascading Style Sheets)** — The language for describing how HTML elements should look.

**DNS (Domain Name System)** — The phonebook of the internet: translates domain names like `example.com` to IP addresses.

**DOM (Document Object Model)** — The browser's in-memory tree representation of an HTML document, exposed to JavaScript.

**Endpoint** — A specific URL on a server that responds to requests, e.g., `GET /api/users/42`.

**Event** — A signal fired by the browser (click, scroll, keypress, etc.) that JavaScript can listen for and respond to.

**Express** — A minimal web framework for Node.js. The standard way to build HTTP APIs in Node.

**Fetch API** — Modern browser API for making HTTP requests, returning Promises.

**Flexbox** — CSS layout system for arranging items in a single row or column.

**Form** — An HTML element that collects user input and submits it to a server.

**Front-end** — Code that runs in the browser. Synonym for *client-side*.

**Full-stack** — A developer or skill set that spans both front-end and back-end.

**Grid** — CSS layout system for arranging items in a two-dimensional grid of rows and columns.

**HTML (HyperText Markup Language)** — The standard markup language for describing the structure of web documents.

**HTTP / HTTPS** — HyperText Transfer Protocol; the language browsers and servers use to communicate. HTTPS adds encryption.

**Hydration** — The process of attaching JavaScript event handlers to server-rendered HTML so it becomes interactive.

**IP address** — A computer's unique numerical address on a network.

**JavaScript / ECMAScript** — The programming language of the web browser; ECMAScript is the official standard.

**JSON (JavaScript Object Notation)** — A lightweight text format for representing structured data; the de facto standard for web APIs.

**JSX** — Syntax extension for JavaScript that looks like HTML, used in React. Compiles to function calls.

**JWT (JSON Web Token)** — A signed, self-contained token used to authenticate API requests.

**localStorage** — Browser storage that persists across sessions. Stores strings only.

**Media query** — A CSS rule that applies only when certain conditions (screen size, color scheme) are met.

**Middleware** — In Express, a function that sits in the request/response pipeline and can inspect or modify the request before it reaches the route handler.

**MongoDB** — A document-oriented (NoSQL) database that stores data as JSON-like documents.

**Mongoose** — An Object Document Mapper (ODM) that adds schema validation and query helpers on top of MongoDB.

**MVC (Model-View-Controller)** — A common architectural pattern: model holds data, view renders it, controller handles input.

**Node.js** — A runtime that lets you execute JavaScript outside the browser.

**npm** — The package manager and package registry for the Node.js ecosystem.

**ORM (Object-Relational Mapper)** — A library that maps database rows to language objects, hiding most SQL.

**Package** — A reusable bundle of code distributed via a package manager.

**PHP** — A server-side scripting language designed for web pages.

**Prepared statement** — A SQL query template with placeholders for values; the database compiles it once and executes safely with different inputs. Prevents SQL injection.

**Promise** — A JavaScript object representing the eventual result of an asynchronous operation. States: pending, fulfilled, rejected.

**Props** — In React, read-only inputs passed from a parent component to a child.

**React** — A JavaScript library for building UIs from components.

**REST (Representational State Transfer)** — An architectural style for web APIs centered on resources and HTTP verbs.

**Responsive design** — Design that adapts to different screen sizes and devices.

**Sanitization** — Cleaning user input to remove dangerous content before processing or displaying it.

**Schema** — A definition of the structure of data: tables and columns in SQL, fields in MongoDB, types in TypeScript.

**Selector** — In CSS, a pattern that matches HTML elements to style.

**Server-side** — Code that runs on the server. Synonym for *back-end*.

**Session** — Server-side state about a logged-in user, identified by a cookie.

**SPA (Single Page Application)** — A web app that loads a single HTML page and updates content via JavaScript without full reloads.

**SQL (Structured Query Language)** — The language for querying relational databases.

**SSR (Server-Side Rendering)** — Generating HTML on the server before sending it to the browser. Improves initial load and SEO.

**State** — In React, internal data owned by a component that, when changed, triggers a re-render.

**TLS / SSL** — Protocols that encrypt HTTP traffic, producing HTTPS.

**URL (Uniform Resource Locator)** — The address of a resource on the web.

**Validation** — Checking that user input meets expected rules (format, length, range).

**Viewport** — The visible area of a webpage in the browser.

**WebSocket** — A protocol that keeps a persistent two-way connection open between browser and server, used for real-time features.

**XSS (Cross-Site Scripting)** — A security vulnerability where attacker-controlled JavaScript runs in a victim's browser. Mitigated by escaping output and Content Security Policy.

---

## Part 5 — Further Reading & Resources

Curated learning resources, organized by area, with a strong emphasis on **distributed web applications** — the design patterns that let web systems scale across many machines.

### Official documentation (the canonical sources)

- **MDN Web Docs** — https://developer.mozilla.org — the definitive reference for HTML, CSS, JavaScript, and browser APIs. If a tutorial conflicts with MDN, trust MDN.
- **Web.dev** — https://web.dev — Google's curated guidance on performance, accessibility, and modern web best practices.
- **Node.js docs** — https://nodejs.org/en/docs/
- **Express** — https://expressjs.com
- **React** — https://react.dev
- **PHP manual** — https://www.php.net/manual/en/
- **PostgreSQL tutorial** — https://www.postgresql.org/docs/current/tutorial.html (excellent SQL learning even if you use MySQL)
- **MongoDB University** — https://learn.mongodb.com (free courses)
- **WHATWG HTML Living Standard** — https://html.spec.whatwg.org

### Free interactive tutorials

- **freeCodeCamp** — https://www.freecodecamp.org — comprehensive free curriculum, project-based.
- **The Odin Project** — https://www.theodinproject.com — full-stack curriculum, JavaScript track is excellent.
- **JavaScript.info** — https://javascript.info — the best modern JavaScript tutorial on the web.
- **CSS Tricks: Complete Guide to Flexbox** — https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- **CSS Tricks: Complete Guide to Grid** — https://css-tricks.com/snippets/css/complete-guide-grid/
- **SQLBolt** — https://sqlbolt.com — interactive SQL lessons.
- **Mode SQL Tutorial** — https://mode.com/sql-tutorial/

### Distributed web applications — the deep stuff

A web application becomes "distributed" the moment its parts run on more than one machine: separate database server, multiple app servers behind a load balancer, third-party APIs, caches, message queues, microservices. These resources teach how to design those systems.

**Foundational reading:**

- **"Designing Data-Intensive Applications"** by Martin Kleppmann — the single best book on distributed systems for working engineers. Covers replication, partitioning, consistency, distributed transactions, batch and stream processing.
- **"Web Scalability for Startup Engineers"** by Artur Ejsmont — practical patterns for scaling from one server to many.
- **"Building Microservices"** by Sam Newman — the standard reference on microservice architecture.
- **"System Design Interview"** by Alex Xu — short, diagram-heavy walkthroughs of scaling classic systems (URL shortener, news feed, chat, etc.).

**Free online curricula:**

- **MIT 6.824: Distributed Systems** — https://pdos.csail.mit.edu/6.824/ — graduate-level course with public lectures, labs, and papers. The gold standard.
- **The System Design Primer** — https://github.com/donnemartin/system-design-primer — a free, open-source crash course.
- **Distributed Systems lecture series by Martin Kleppmann (Cambridge)** — https://www.youtube.com/playlist?list=PLeKd45zvjcDFUEv_ohr_HdUFe97RItdiB — companion lectures to the book above.
- **High Scalability blog** — http://highscalability.com — case studies of how real companies scale.

**Foundational papers worth reading once in your career:**

- *The Google File System* (2003) — origin of HDFS and modern distributed storage.
- *MapReduce* (2004) — origin of Hadoop and the batch-processing pattern.
- *Dynamo* (2007) — Amazon's eventually-consistent key-value store; foundation of Cassandra and DynamoDB.
- *Bigtable* (2006) — Google's wide-column store; foundation of HBase.
- *Paxos Made Simple* (Lamport, 2001) and *Raft* (Ongaro & Ousterhout, 2014) — distributed consensus algorithms.
- *CAP Twelve Years Later* (Brewer, 2012) — the author of the CAP theorem clarifying what it actually means.

Most are findable on https://www.usenix.org or via Google Scholar — search by title.

### REST, APIs, and microservices

- **"RESTful Web APIs"** by Leonard Richardson and Mike Amundsen — careful, principled API design.
- **REST API Tutorial** — https://restfulapi.net — practical conventions.
- **Microsoft REST API Guidelines** — https://github.com/microsoft/api-guidelines/blob/vNext/Guidelines.md — opinionated but well-justified.
- **gRPC** — https://grpc.io — the binary RPC alternative to REST, common in microservices.
- **GraphQL** — https://graphql.org — a query language for APIs, an alternative to REST for some workloads.

### Front-end performance & advanced topics

- **"High Performance Browser Networking"** by Ilya Grigorik — free online at https://hpbn.co — how the web actually works at the network level.
- **Patterns.dev** — https://www.patterns.dev — modern web patterns (rendering, data fetching, state management).
- **Refactoring UI** — https://www.refactoringui.com — practical visual design for engineers.

### Security

- **OWASP Top 10** — https://owasp.org/www-project-top-ten/ — the canonical list of web security risks.
- **OWASP Cheat Sheet Series** — https://cheatsheetseries.owasp.org — concrete defenses for each risk.
- **Mozilla Observatory** — https://observatory.mozilla.org — scan a site's security headers.

### Communities and ongoing reading

- **Hacker News** — https://news.ycombinator.com — a daily pulse on what engineers are reading.
- **Lobsters** — https://lobste.rs — smaller, higher-signal alternative to HN.
- **r/webdev** and **r/programming** on Reddit.
- **CSS Tricks newsletter** and **JavaScript Weekly** — well-curated weekly digests.

---

### Final advice

The web stack is wide, but most days you'll touch only a thin slice of it. Get fluent with the **HTML → CSS → JavaScript → DOM** loop first; that's the foundation everything else (Node, React, frameworks) is layered on top of. Build small projects end-to-end rather than reading endlessly — the only way to internalize this stack is to ship something messy and then improve it.
