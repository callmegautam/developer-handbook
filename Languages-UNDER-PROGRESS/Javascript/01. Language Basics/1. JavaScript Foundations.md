## 🧭 JavaScript Foundations

### 🧩 What is JavaScript?

JavaScript (JS) is a **high-level**, **interpreted**, **dynamically typed**, and **prototype-based** programming language primarily used to make web pages interactive.  
It runs on the client (browser) and server (via Node.js), making it the only language that truly unifies both environments.

**Key traits:**

- **Single-threaded:** Executes one task at a time.
    
- **Event-driven & asynchronous:** Uses event loops and callbacks instead of multi-threading.
    
- **Prototype-based OOP:** Objects inherit directly from other objects (not from classes, though ES6 added class syntax).
    
- **Interpreted & JIT compiled:** Modern engines optimize JS code at runtime.
    

---

### 📜 Brief History

- **1995:** Created by _Brendan Eich_ at Netscape in 10 days, originally called _Mocha_, then _LiveScript_, finally _JavaScript_ (marketing move to ride Java’s popularity).
    
- **1997:** Standardized by _ECMA International_ as **ECMAScript (ES)**.
    
- **2009:** Node.js introduced — running JS outside browsers.
    
- **2015 (ES6):** Major update introducing `let`, `const`, classes, modules, arrow functions, promises, etc.
    
- **Now:** Annual updates (ES7 → ESNext).
    

---

### ⚙️ JavaScript Engines

A **JS engine** reads, optimizes, and executes your code.  
Each environment has its own engine:

|Engine|Creator|Used In|
|---|---|---|
|**V8**|Google|Chrome, Node.js, Deno|
|**SpiderMonkey**|Mozilla|Firefox|
|**JavaScriptCore (Nitro)**|Apple|Safari|
|**Chakra**|Microsoft|Edge (legacy)|

**V8** is the most famous — it compiles JS to machine code using a **Just-In-Time (JIT)** compiler for speed.

---

### 🌐 JS Runtime Environments

A **runtime** is the ecosystem where JS code executes — engine + APIs + event loop.

#### 1. **Browser Runtime**

- Engine: V8 / SpiderMonkey / etc.
    
- Provides **Web APIs**: `DOM`, `fetch`, `setTimeout`, `localStorage`, etc.
    
- JS interacts with HTML, CSS, and the DOM.
    

#### 2. **Node.js**

- Engine: V8
    
- Provides **Node APIs**: `fs`, `http`, `process`, `Buffer`, etc.
    
- No DOM or `window`, but has `global`.
    

#### 3. **Deno**

- Built by the same creator as Node.js.
    
- Secure by default, supports TypeScript natively.
    
- Uses modern ES modules instead of CommonJS.
    

---

### 🧠 Execution Context and Global Object

#### Execution Context

It’s the **environment in which JS code is evaluated and executed.**

There are **three types**:

1. **Global Execution Context (GEC):**  
    Created when JS first runs. Defines global scope, creates global object and `this`.
    
2. **Function Execution Context (FEC):**  
    Created for every function call.
    
3. **Eval Execution Context (rare):**  
    For code inside `eval()` (almost never used).
    

Each context has two phases:

1. **Creation Phase:**
    
    - Memory is allocated for variables/functions.
        
    - Variables are initialized to `undefined` (hoisting).
        
2. **Execution Phase:**
    
    - Code runs line by line, variables get actual values.
        

#### Global Object

- **Browser:** `window`
    
- **Node.js:** `global`
    
- **Deno:** `globalThis` (standardized)
    

`globalThis` is now a **universal global reference** across all runtimes.

**Example:**

```js
console.log(this === window); // true (in browser)
console.log(globalThis); // works everywhere
```

---

### 📆 ECMAScript Versions and Compatibility

**ECMAScript (ES)** = Official specification of JavaScript.  
**JavaScript** = Implementation of that spec.

**Major versions:**

- **ES3 (1999):** Standardization of basic features.
    
- **ES5 (2009):** Strict mode, JSON, `Object.create`, `Array.forEach`, etc.
    
- **ES6 (2015):** Massive update — `let`, `const`, classes, arrow functions, modules, promises, etc.
    
- **ES7+ (2016 → ESNext):** Smaller, annual updates — async/await, optional chaining, nullish coalescing, etc.
    

Use **Babel** or **TypeScript** for transpiling modern JS into backward-compatible code for older browsers.
