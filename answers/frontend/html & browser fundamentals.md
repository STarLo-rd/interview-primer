### **1. What is the difference between `<script>`, `<script async>`, and `<script defer>`?**

#### **Answer:**

- `<script>`: By default, scripts are **parsed and executed immediately** when encountered, blocking the rendering of the page until execution is complete.
- `<script async>`: The script is fetched and executed **as soon as possible**, **without blocking** the HTML parsing. Useful for independent scripts like ads or analytics.
- `<script defer>`: The script is fetched in parallel but **executed only after the entire HTML document is parsed**, **in order**. Ideal for scripts that depend on the DOM structure.

✅ **Use `defer` for scripts that manipulate the DOM** and **`async` for independent scripts.**

---

### **2. How does the browser render a web page? (Explain the critical rendering path.)**

#### **Answer:**

The **Critical Rendering Path (CRP)** is the sequence of steps a browser takes to render a page:

1. **HTML Parsing:** Converts HTML into a **DOM Tree**.
2. **CSS Parsing:** Converts CSS into a **CSSOM (CSS Object Model) Tree**.
3. **JavaScript Execution:** JavaScript modifies the DOM and CSSOM if needed.
4. **Render Tree Construction:** Combines **DOM + CSSOM** to determine what elements need to be painted.
5. **Layout:** Determines the exact position and size of elements.
6. **Painting:** Renders pixels on the screen based on the calculated layout.
7. **Compositing:** Combines layers and applies effects like transformations and animations.

✅ **Performance Tip:** Minimize render-blocking resources (`CSS` and `JS`), use `defer`/`async`, and optimize images.

---

### **3. What is the difference between `localStorage`, `sessionStorage`, and cookies?**

#### **Answer:**

| Storage Type     | Lifetime                                     | Storage Limit | Accessible From         | Purpose                                             |
| ---------------- | -------------------------------------------- | ------------- | ----------------------- | --------------------------------------------------- |
| `localStorage`   | **Persistent** (until manually cleared)      | 5-10MB        | Same-origin pages       | Store long-term data (e.g., themes, user settings)  |
| `sessionStorage` | **Per session** (cleared when tab is closed) | 5MB           | Same-origin pages       | Store temporary session data                        |
| Cookies          | Can have **expiration**                      | ~4KB          | Sent with HTTP requests | Store small user data (e.g., authentication tokens) |

✅ **Use `localStorage/sessionStorage` for client-side storage. Use cookies for authentication/session management.**

---

### **4. What are web components? How do they work?**

#### **Answer:**

**Web Components** allow the creation of **reusable, encapsulated HTML elements** using:

1. **Custom Elements (`customElements.define`)** – Define new HTML tags.
2. **Shadow DOM (`attachShadow`)** – Encapsulates styles and markup.
3. **HTML Templates (`<template>` and `<slot>`)** – Define reusable HTML content.

#### **Example:**

```html
<my-button></my-button>

<script>
  class MyButton extends HTMLElement {
    constructor() {
      super();
      let shadow = this.attachShadow({ mode: "open" });
      shadow.innerHTML = `<button>Click Me</button>`;
    }
  }
  customElements.define("my-button", MyButton);
</script>
```

✅ **Web components help in creating reusable UI components without frameworks.**

---

### **5. How does the event loop work in the browser?**

#### **Answer:**

The **event loop** in JavaScript handles asynchronous operations. It has:

1. **Call Stack:** Executes synchronous code.
2. **Web APIs:** Handles async operations (setTimeout, fetch, etc.).
3. **Task Queue (Callback Queue):** Stores completed async tasks to be executed when the stack is empty.
4. **Microtask Queue:** Stores promises and mutation observers (executed before tasks).

#### **Example of Event Loop Execution Order:**

```js
console.log("Start");

setTimeout(() => console.log("Timeout"), 0);
Promise.resolve().then(() => console.log("Promise"));

console.log("End");
```

**Output:**

```
Start
End
Promise
Timeout
```

✅ **Promises (`Microtasks`) execute before `setTimeout` (`Macrotasks`).**

---

Great! Let’s go deeper into **HTML & Browser Fundamentals** and discuss more core concepts.

---

## **1. What is the difference between HTML, XHTML, and HTML5?**

### **Answer:**

| Feature            | HTML                       | XHTML                     | HTML5                                |
| ------------------ | -------------------------- | ------------------------- | ------------------------------------ |
| **Syntax**         | Flexible, case-insensitive | Strict, well-formed XML   | More relaxed, supports new elements  |
| **Doctype**        | `<!DOCTYPE HTML PUBLIC>`   | `<!DOCTYPE html PUBLIC>`  | `<!DOCTYPE html>` (simplified)       |
| **Closing Tags**   | Not always required        | Must be explicitly closed | Some elements can omit               |
| **Error Handling** | Browser ignores errors     | Must be well-formed       | More tolerant of errors              |
| **New Features**   | Basic structure            | No new features           | Supports multimedia, APIs, semantics |

✅ **HTML5 is the modern standard** with support for **semantic tags, multimedia, and APIs** like `localStorage`, `WebSockets`, etc.

---

## **2. What are semantic HTML elements? Why are they important?**

### **Answer:**

**Semantic HTML** elements **describe the content** in a meaningful way, improving readability and accessibility.

✅ **Examples of semantic elements:**

- `<header>` – Defines the header section.
- `<nav>` – Navigation links.
- `<article>` – Represents an independent article.
- `<section>` – Groups related content.
- `<aside>` – Sidebar content.
- `<footer>` – Footer section.

❌ **Non-semantic elements:**

- `<div>` and `<span>` – Used for styling but have no meaning.

✅ **Why Use Semantic HTML?**

1. **SEO-friendly** – Helps search engines understand content.
2. **Improves Accessibility (a11y)** – Screen readers can interpret content better.
3. **Better maintainability and readability**.

---

## **3. How do browsers handle HTML parsing?**

### **Answer:**

The **browser rendering process** (Critical Rendering Path) involves **HTML parsing** in the following steps:

1. **Tokenization:** The browser reads HTML as a stream of characters and converts them into tokens.
2. **DOM Tree Construction:** Tokens are converted into **nodes**, creating the **DOM (Document Object Model)**.
3. **CSSOM Construction:** CSS is parsed into a **CSS Object Model (CSSOM)**.
4. **Render Tree:** The **DOM + CSSOM** are combined to determine the layout.
5. **Layout and Painting:** The browser calculates positions and paints elements onto the screen.

✅ **Performance Tip:** Avoid render-blocking **CSS & JavaScript** to improve page load speed.

---

## **4. What are meta tags in HTML, and why are they important?**

### **Answer:**

**Meta tags** provide metadata (information about the page) that helps search engines, browsers, and social media platforms.

✅ **Common Meta Tags:**

```html
<meta charset="UTF-8" />
<!-- Character Encoding -->
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<!-- Responsive Design -->
<meta name="description" content="This is a sample webpage." />
<!-- SEO Optimization -->
<meta name="robots" content="index, follow" />
<!-- Tells search engines to index -->
<meta property="og:title" content="My Page Title" />
<!-- Open Graph for social media -->
```

✅ **Why Use Meta Tags?**

- Improve **SEO rankings**.
- Ensure **proper encoding** (avoid character issues).
- Control **responsiveness** for mobile users.
- Provide **rich previews on social media** (Open Graph, Twitter Cards).

---

## **5. What is the difference between an iframe and a frame in HTML?**

### **Answer:**

| Feature            | `<iframe>`                                 | `<frame>`                         |
| ------------------ | ------------------------------------------ | --------------------------------- |
| **Usage**          | Embeds another webpage inside a page       | Used in `<frameset>` (Deprecated) |
| **Modern Support** | Still used in modern web development       | Deprecated in HTML5               |
| **Flexibility**    | Can be styled with CSS and JavaScript      | Difficult to style properly       |
| **Security**       | Can be restricted with `sandbox` attribute | Vulnerable to security issues     |

✅ **`<iframe>` is still used** for embedding YouTube videos, maps, and external content.  
❌ **`<frame>` is deprecated** and should not be used.

✅ **Example of `<iframe>` usage:**

```html
<iframe src="https://www.example.com" width="600" height="400"></iframe>
```

⚠ **Security Tip:** Use the `sandbox` attribute to restrict iframe behavior (e.g., prevent scripts from running).

---

## **6. What is the difference between a block-level and an inline element?**

### **Answer:**

| Feature                         | Block-level Elements                                       | Inline Elements                                          |
| ------------------------------- | ---------------------------------------------------------- | -------------------------------------------------------- |
| **Definition**                  | Takes up the full width of its parent container            | Only takes up as much width as necessary                 |
| **Starts on a New Line?**       | Yes                                                        | No                                                       |
| **Can Contain Other Elements?** | Yes (both block and inline)                                | No (usually only text or other inline elements)          |
| **Examples**                    | `<div>`, `<p>`, `<h1>`–`<h6>`, `<ul>`, `<li>`, `<section>` | `<span>`, `<a>`, `<strong>`, `<em>`, `<img>`, `<button>` |

✅ **Use block elements for structure, inline elements for small content inside paragraphs or other elements.**

---

## **7. What is the difference between `innerHTML`, `innerText`, and `textContent`?**

### **Answer:**

| Property      | What It Returns                                         | Affects HTML?        | Performance              |
| ------------- | ------------------------------------------------------- | -------------------- | ------------------------ |
| `innerHTML`   | Includes **HTML tags** inside the element               | ✅ Yes (parses HTML) | ❌ Slower (renders HTML) |
| `innerText`   | Returns **only visible text** (ignores hidden elements) | ❌ No                | ✅ Faster                |
| `textContent` | Returns **all text (including hidden text)**            | ❌ No                | ✅ Fastest               |

✅ **Example:**

```html
<div id="test">Hello <strong>World</strong></div>
<script>
  console.log(document.getElementById("test").innerHTML); // "Hello <strong>World</strong>"
  console.log(document.getElementById("test").innerText); // "Hello World"
  console.log(document.getElementById("test").textContent); // "Hello World"
</script>
```

⚠ **Security Tip:** Avoid using `innerHTML` with untrusted data to prevent **XSS attacks**.

---

## **8. What is the difference between progressive rendering and lazy loading?**

### **Answer:**

- **Progressive Rendering:** A technique where **critical content is loaded first**, while the rest loads in the background.  
  ✅ Example: Using **lazy loading for images, skeleton loaders, server-side rendering (SSR)**.
- **Lazy Loading:** Delays loading of **non-critical** resources **until they are needed**.  
  ✅ Example: Lazy loading images with `loading="lazy"`:
  ```html
  <img src="image.jpg" loading="lazy" alt="Lazy Loaded Image" />
  ```

✅ **Both improve performance** by reducing initial load time.

---

## **9. How does preloading and prefetching work in browsers?**

### **Answer:**

| Technique                              | When It Loads                           | Purpose                                               |
| -------------------------------------- | --------------------------------------- | ----------------------------------------------------- |
| **Preload** (`<link rel="preload">`)   | Loads resource early in high priority   | Load fonts, scripts, or images before they are needed |
| **Prefetch** (`<link rel="prefetch">`) | Loads resource when the browser is idle | Load pages or assets **for future navigation**        |

✅ **Example:**

```html
<link rel="preload" href="styles.css" as="style" />
<link rel="prefetch" href="next-page.html" />
```

**Use preloading for critical resources and prefetching for anticipated navigation.**

---

Here are the answers to the additional **HTML & Browser Fundamentals** questions:

---

### **1. What is a critical resource in the browser, and how can we optimize loading?**

#### **Answer:**

A **critical resource** is any file necessary for rendering the webpage, such as:

- HTML
- CSS (render-blocking)
- JavaScript (if it modifies the DOM)
- Fonts (if required for layout)
- Images (if necessary for layout)

#### **Optimizations:**

1. **Minimize Critical Resources:** Reduce the number of CSS/JS files.
2. **Lazy Load Non-Essential Resources:** Use `loading="lazy"` for images and `async` for scripts.
3. **Use Preloading:** Load important assets earlier:
   ```html
   <link rel="preload" href="styles.css" as="style" />
   ```
4. **Defer Non-Critical JS Execution:** Use `defer` for scripts that interact with the DOM.
5. **Compress Assets:** Use Gzip/Brotli for faster delivery.
6. **Use Content Delivery Networks (CDN):** Distribute assets globally for reduced latency.

✅ **Goal:** Reduce render-blocking time and improve First Contentful Paint (FCP).

---

### **2. What is the difference between render-blocking and non-blocking resources?**

#### **Answer:**

| Type of Resource    | Blocks Rendering? | Example                     | Optimization                  |
| ------------------- | ----------------- | --------------------------- | ----------------------------- |
| **Render-Blocking** | Yes               | CSS, synchronous JavaScript | Minify, preload, defer, async |
| **Non-Blocking**    | No                | Images, async/defer scripts | Lazy load, prefetch           |

✅ **Render-blocking resources prevent the browser from displaying content** until they load.

### **Optimizations for Render-Blocking Resources:**

1. **Defer JavaScript Execution:**
   ```html
   <script defer src="script.js"></script>
   ```
2. **Load CSS Efficiently:** Use `media="print"` to delay non-critical styles:
   ```html
   <link
     rel="stylesheet"
     href="styles.css"
     media="print"
     onload="this.media='all'"
   />
   ```
3. **Lazy Load Images:**
   ```html
   <img src="image.jpg" loading="lazy" alt="Example" />
   ```
4. **Use Web Fonts Efficiently:**
   - Use font-display: `swap` to prevent blocking rendering.
   ```css
   @font-face {
     font-family: "CustomFont";
     src: url("font.woff2") format("woff2");
     font-display: swap;
   }
   ```

✅ **Reducing render-blocking resources improves page speed and performance.**

---

### **3. How do Service Workers work in modern web applications?**

#### **Answer:**

A **Service Worker** is a background script that runs independently of the main page and enables:

- **Caching for offline support**
- **Push notifications**
- **Background sync**

### **How It Works:**

1. **Register the Service Worker:**
   ```js
   if ("serviceWorker" in navigator) {
     navigator.serviceWorker
       .register("/sw.js")
       .then(() => console.log("Service Worker registered"));
   }
   ```
2. **Service Worker Lifecycle:**

   - **Install:** Cache assets.
   - **Activate:** Remove old cache.
   - **Fetch:** Intercept network requests and serve cached data when offline.

3. **Example Fetch Event Handling (Offline Support):**
   ```js
   self.addEventListener("fetch", (event) => {
     event.respondWith(
       caches
         .match(event.request)
         .then((response) => response || fetch(event.request))
     );
   });
   ```

✅ **Service Workers enhance performance by enabling offline-first experiences and reducing server requests.**

---

### **4. What are Content Security Policies (CSP), and why are they important?**

#### **Answer:**

A **Content Security Policy (CSP)** is a security feature that helps prevent:

- **Cross-Site Scripting (XSS) attacks**
- **Data injection attacks**

### **How CSP Works:**

- It restricts which scripts, styles, and resources can load on a page.
- Enforced via the `Content-Security-Policy` HTTP header.

### **Example CSP Header:**

```http
Content-Security-Policy: default-src 'self'; script-src 'self' https://apis.example.com; object-src 'none';
```

- `default-src 'self'` → Only allow content from the same origin.
- `script-src 'self' https://apis.example.com` → Only allow scripts from the same origin and a trusted API.
- `object-src 'none'` → Block Flash/Java objects.

### **Best Practices:**

✅ **Avoid `unsafe-inline` and `unsafe-eval`** – These weaken CSP.  
✅ **Use nonce-based CSP** to allow specific inline scripts dynamically.

---

### **5. What is the Same-Origin Policy (SOP), and how does it affect web security?**

#### **Answer:**

**Same-Origin Policy (SOP)** is a browser security feature that prevents scripts from accessing content from a different origin.

✅ **An "origin" is defined as:**

```
protocol://domain:port
```

For example:

- `https://example.com` (origin) **cannot access** `https://another.com` (different origin).

### **How SOP Affects Web Security:**

1. **Prevents unauthorized access to sensitive data** (e.g., cookies, localStorage).
2. **Stops malicious scripts from different origins from reading private data.**

### **Bypassing SOP (Securely) with CORS:**

If a server allows cross-origin access, it sends a **CORS (Cross-Origin Resource Sharing)** header:

```http
Access-Control-Allow-Origin: https://trusted.com
```

✅ **Only allow trusted origins in CORS policies to avoid security risks.**

---

### **6. What are the differences between GET and POST requests in terms of browser behavior?**

#### **Answer:**

| Feature          | GET                                                     | POST                           |
| ---------------- | ------------------------------------------------------- | ------------------------------ |
| **Usage**        | Retrieve data                                           | Submit data                    |
| **Data in URL?** | Yes (query string)                                      | No (body)                      |
| **Cacheable?**   | Yes                                                     | No                             |
| **Security**     | Less secure (exposed in URL)                            | More secure (hidden in body)   |
| **Idempotent?**  | Yes (repeating the request doesn’t change server state) | No (repeating may modify data) |

✅ **Example of GET Request:**

```http
GET /users?id=123 HTTP/1.1
Host: example.com
```

✅ **Example of POST Request:**

```http
POST /users HTTP/1.1
Host: example.com
Content-Type: application/json

{ "name": "John Doe", "email": "john@example.com" }
```

✅ **When to use which?**

- Use **GET** for reading data (e.g., fetching user profiles).
- Use **POST** for actions that modify data (e.g., creating a user, submitting forms).

---
