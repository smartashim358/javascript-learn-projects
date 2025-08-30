# JavaScript Learn Projects

A curated, hands-on collection of **JavaScript (DOM-first) mini projects** that grow from **basics → intermediate → advanced**. Each project is small, focused, and designed to strengthen your understanding of the **Document Object Model (DOM)**, events, templates, mutation observers, storage, and fetch.

> Perfect for daily practice and building a strong base for front‑end or full‑stack dev work.

---

## Table of Contents
- [Why This Repo](#why-this-repo)
- [Quick Start](#quick-start)
- [Recommended Stack](#recommended-stack)
- [Project Structure](#project-structure)
- [Project Index](#project-index)
- [Detailed Projects](#detailed-projects)
  - [01 — Hello DOM](#01--hello-dom)
  - [02 — Styles & Classes](#02--styles--classes)
  - [03 — Dynamic List (Fruits)](#03--dynamic-list-fruits)
  - [04 — Event Delegation To‑Do](#04--event-delegation-to-do)
  - [05 — Templates & Fragments](#05--templates--fragments)
  - [06 — MutationObserver](#06--mutationobserver)
  - [07 — Fetch + DOM](#07--fetch--dom)
  - [08 — LocalStorage Persistence](#08--localstorage-persistence)
- [Best Practices](#best-practices)
- [How to Add a New Project](#how-to-add-a-new-project)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

---

## Why This Repo
- Learn DOM step‑by‑step with **real code**.
- Each folder is a **standalone** mini app you can open in the browser.
- Clean **HTML/CSS/JS** separation with **idiomatic DOM APIs**.
- Includes **challenge ideas** to push your skills further.

---

## Quick Start

### Option A — Just open in a browser
1. Clone the repo:
   ```bash
   git clone https://github.com/<your-username>/javascript-learn-projects.git
   cd javascript-learn-projects
   ```
2. Open any `index.html` directly in your browser.

### Option B — Use a local dev server (recommended)
- **VS Code + Live Server** extension, or
- **Python**:
  ```bash
  # From repo root
  python3 -m http.server 5500
  # then open http://localhost:5500 in your browser
  ```

---

## Recommended Stack
- **Editor**: VS Code
- **Browser**: Chrome/Edge/Firefox (latest)
- **Extensions**: Live Server, ESLint (optional), Prettier (optional)

---

## Project Structure
```
javascript-learn-projects/
├─ projects/
│  ├─ 01-hello-dom/
│  │  ├─ index.html
│  │  └─ script.js
│  ├─ 02-styles-and-classes/
│  │  ├─ index.html
│  │  └─ script.js
│  ├─ 03-dynamic-list-fruits/
│  │  ├─ index.html
│  │  └─ script.js
│  ├─ 04-event-delegation-todo/
│  │  ├─ index.html
│  │  └─ script.js
│  ├─ 05-templates-and-fragments/
│  │  ├─ index.html
│  │  └─ script.js
│  ├─ 06-mutation-observer/
│  │  ├─ index.html
│  │  └─ script.js
│  ├─ 07-fetch-and-dom/
│  │  ├─ index.html
│  │  └─ script.js
│  └─ 08-localstorage-persistence/
│     ├─ index.html
│     └─ script.js
├─ assets/               # images, icons, mock json, etc.
├─ docs/                 # notes, cheatsheets, diagrams
└─ README.md
```

> Tip: Keep each mini project self‑contained. Avoid global styles/scripts across folders so you learn setup each time.

---

## Project Index

- [x] **01 — Hello DOM**: selecting nodes, text vs HTML, basic events  
- [x] **02 — Styles & Classes**: `style`, `classList`, dynamic styles via `<style>` tag  
- [x] **03 — Dynamic List (Fruits)**: create/append/remove, inline styles, click events  
- [x] **04 — Event Delegation To‑Do**: parent listener, `dataset`, `closest`, edit/delete  
- [x] **05 — Templates & Fragments**: `<template>`, `cloneNode`, `DocumentFragment`  
- [x] **06 — MutationObserver**: observe changes, log mutations  
- [x] **07 — Fetch + DOM**: fetch JSON, render cards/list dynamically  
- [x] **08 — LocalStorage Persistence**: store & restore app state

> Add more: keyboard shortcuts, drag & drop, IntersectionObserver, forms & validation, accessibility.

---

## Detailed Projects

### 01 — Hello DOM
**Goals**: DOM selection & simple manipulation.
```html
<h1 id="title">Hello World</h1>
<button id="btn">Change</button>
<script>
  const title = document.getElementById("title");
  document.getElementById("btn").addEventListener("click", () => {
    title.innerText = "Hello DOM!";
  });
</script>
```
**APIs**: `getElementById`, `innerText`, `addEventListener`  
**Try**: Use `querySelector`, `innerHTML`, `textContent` differences.

---

### 02 — Styles & Classes
**Goals**: Toggle styles via JS; inject `<style>`.
```html
<div id="box">Box</div>
<script>
  // Inject shared CSS
  const style = document.createElement("style");
  style.textContent = `.highlight{background: black;color: white;padding:12px;border-radius:10px}`;
  document.head.appendChild(style);

  const box = document.getElementById("box");
  box.addEventListener("click", () => box.classList.toggle("highlight"));
</script>
```
**APIs**: `style`, `classList.add/remove/toggle`, `<style>` injection  
**Try**: Animate with CSS transitions.

---

### 03 — Dynamic List (Fruits)
**Goals**: Create elements, events per item, tidy layout.
```html
<script>
  const style = document.createElement("style");
  style.textContent = `
    .listItem{padding:12px 14px;background:gray;color:white;
      box-shadow:2px 3px 4px rgba(0,0,0,.3);border:2px solid #111;border-radius:6px;cursor:pointer;margin:6px}
    ul{list-style:none;display:flex;gap:10px;margin-top:20px;padding:0}
  `;
  document.head.appendChild(style);

  const fruits = ["apple","orange","banana","grapes","pineapple"];
  const ul = document.createElement("ul");

  for (let i = 0; i < fruits.length; i++) {
    const li = document.createElement("li");
    li.className = "listItem";
    li.textContent = fruits[i];
    li.addEventListener("click", () => alert("You clicked " + fruits[i]));
    ul.appendChild(li);
  }

  document.body.appendChild(ul);
</script>
```
**APIs**: `createElement`, `appendChild`, `addEventListener`, inline & class styles  
**Try**: Keyboard navigation; delete on right‑click; filter items by input.

---

### 04 — Event Delegation To‑Do
**Goals**: Single listener on parent; use `dataset` & `closest`.
```html
<input id="todoInput" placeholder="task"><button id="add">Add</button>
<ul id="list"></ul>
<script>
  const list = document.getElementById("list");
  let id = 0;
  document.getElementById("add").addEventListener("click", () => {
    const v = document.getElementById("todoInput").value.trim();
    if (!v) return;
    const li = document.createElement("li");
    li.dataset.id = ++id;
    li.innerHTML = `${v} <button class="done">✔</button> <button class="del">🗑</button>`;
    list.appendChild(li);
  });

  list.addEventListener("click", (e) => {
    const li = e.target.closest("li");
    if (!li) return;
    if (e.target.classList.contains("done")) li.classList.toggle("done");
    if (e.target.classList.contains("del")) li.remove();
  });
</script>
```
**APIs**: event bubbling, `closest`, `classList`, `dataset`  
**Try**: Inline edit on double‑click; filter completed tasks.

---

### 05 — Templates & Fragments
**Goals**: Efficient DOM creation with `<template>` and `DocumentFragment`.
```html
<template id="cardTpl">
  <li class="card"><h3 class="title"></h3></li>
</template>
<ul id="cards"></ul>
<script>
  const data = ["Alpha","Beta","Gamma"];
  const tpl = document.getElementById("cardTpl");
  const frag = document.createDocumentFragment();

  data.forEach(name => {
    const node = tpl.content.cloneNode(true);
    node.querySelector(".title").textContent = name;
    frag.appendChild(node);
  });

  document.getElementById("cards").appendChild(frag);
</script>
```
**APIs**: `<template>`, `cloneNode(true)`, `DocumentFragment`  
**Try**: Add images and buttons; reuse template across pages.

---

### 06 — MutationObserver
**Goals**: React to DOM changes programmatically.
```html
<ul id="target"></ul>
<script>
  const target = document.getElementById("target");
  const obs = new MutationObserver((mutations) => {
    console.log("Mutations:", mutations);
  });
  obs.observe(target, { childList: true, subtree: true });

  // Trigger changes
  target.appendChild(Object.assign(document.createElement("li"), {textContent:"Item 1"}));
  setTimeout(() => target.firstElementChild.remove(), 1000);
</script>
```
**APIs**: `MutationObserver`, `observe`, records  
**Try**: Use observer to auto‑save or animate new items.

---

### 07 — Fetch + DOM
**Goals**: Load data from an API (or local JSON) and render.
```html
<ul id="users"></ul>
<script>
  async function load(){
    const res = await fetch("assets/users.json"); // or public API
    const users = await res.json();
    const frag = document.createDocumentFragment();
    users.forEach(u => {
      const li = document.createElement("li");
      li.textContent = `${u.name} — ${u.email}`;
      frag.appendChild(li);
    });
    document.getElementById("users").appendChild(frag);
  }
  load();
</script>
```
**APIs**: `fetch`, `async/await`, fragments  
**Try**: Loading states, error handling, retry/backoff, filter/search.

---

### 08 — LocalStorage Persistence
**Goals**: Save simple state across reloads.
```html
<input id="note" placeholder="type...">
<script>
  const key = "note:text";
  const el = document.getElementById("note");
  el.value = localStorage.getItem(key) || "";
  el.addEventListener("input", () => localStorage.setItem(key, el.value));
</script>
```
**APIs**: `localStorage.getItem/setItem`, events  
**Try**: Persist To‑Do list; last view mode; theme (dark/light).

---

## Best Practices
- Prefer `querySelector/All` for flexibility.
- Use **event delegation** for lists/grids.
- Batch DOM updates with **fragments** to reduce reflow.
- Keep **CSS in classes**, use JS to toggle classes (not style everything inline).
- Make UI **accessible**: semantic HTML, focus states, labels, `aria-*` where needed.
- Handle **errors** and **empty states** when fetching.
- Keep functions **small** and **pure** where possible.

---

## How to Add a New Project
1. Create a new folder under `projects/NN-project-name/`.
2. Add `index.html`, `script.js`, and optional `style.css`.
3. Keep it standalone so it opens cleanly in a browser.
4. Update this README’s **Project Index** if needed.

---

## Contributing
Pull requests are welcome!  
- Keep examples **minimal** and **focused** on one concept.
- Use **vanilla JS** unless the example explicitly requires a library.
- Add comments and a short **README** per project if it’s non‑trivial.

---

## License
This repository is licensed under the **MIT License**.  
You are free to use, copy, modify, and distribute with attribution. See `LICENSE` (add one if missing).

---

## Author

**Ashim Nepali** (aka **smartashim358**)  
- Focus: JavaScript fundamentals, Java backend, blockchain & cybersecurity learning.  
- GitHub: https://github.com/smartashim358  
- Email: _add your preferred contact_

> If you use or learn from this repo, ⭐️ star it and share feedback—contributions and suggestions are most welcome!
