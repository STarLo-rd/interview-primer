### **CSS & Styling**

1. **What are the different ways to apply CSS to a webpage?**

#### **Answer:**

CSS can be applied to a webpage in **three ways**:

1. **Inline CSS:**

   - Using the `style` attribute directly within an HTML tag.
   - Example:

   ```html
   <p style="color: red;">This is an inline styled paragraph.</p>
   ```

2. **Internal CSS:**

   - Defined within the `<style>` tag in the `<head>` section of the HTML document.
   - Example:

   ```html
   <style>
     p {
       color: blue;
     }
   </style>
   ```

3. **External CSS:**
   - Defined in an external `.css` file and linked to the HTML using the `<link>` tag.
   - Example:
   ```html
   <link rel="stylesheet" href="styles.css" />
   ```

✅ **Best Practice:** Use **external CSS** for better maintainability and separation of concerns.

---

### **2. What is the box model in CSS?**

#### **Answer:**

The **CSS Box Model** describes how elements are structured and how space is allocated around them. It consists of:

1. **Content**: The actual content of the element (e.g., text or images).
2. **Padding**: The space between the content and the border.
3. **Border**: A line surrounding the padding (optional).
4. **Margin**: The outermost space between the element and its neighbors.

| Component   | Description                                         |
| ----------- | --------------------------------------------------- |
| **Content** | Area where the content (text, images) is displayed. |
| **Padding** | Space around the content, inside the border.        |
| **Border**  | The border surrounding the padding.                 |
| **Margin**  | Space outside the border, separating elements.      |

✅ **Box Model Formula:**

```css
element's total width = content width + left padding + right padding + left border + right border + left margin + right margin
```

---

### **3. What is the difference between `display: block`, `display: inline`, and `display: inline-block`?**

#### **Answer:**

| `display` Value    | Behavior                                                                | Examples                    |
| ------------------ | ----------------------------------------------------------------------- | --------------------------- |
| **`block`**        | Takes up the full width, starts on a new line, can set width and height | `<div>`, `<p>`, `<header>`  |
| **`inline`**       | Only takes up as much width as its content, cannot set width/height     | `<span>`, `<a>`, `<strong>` |
| **`inline-block`** | Behaves like an inline element but allows width and height              | `<img>`, custom elements    |

✅ **Use `block`** for structural elements (like `<div>`).  
✅ **Use `inline`** for text or small elements (like `<span>`).  
✅ **Use `inline-block`** when you need a hybrid of `inline` and `block`.

---

### **4. What is CSS specificity and how does it work?**

#### **Answer:**

CSS specificity determines which style rule is applied when there are conflicting styles. It’s calculated based on the **selectors** used. The specificity score is calculated using a four-part value:

1. **Inline styles** (e.g., `style="color: red;"`) – **Highest specificity**
2. **IDs** (e.g., `#header`)
3. **Classes, attributes, and pseudo-classes** (e.g., `.button`, `[type="text"]`, `:hover`)
4. **Elements and pseudo-elements** (e.g., `div`, `p`, `::after`) – **Lowest specificity**

#### **Specificity Hierarchy Example:**

```css
#header {
  color: red;
} /* ID selector */
.button {
  color: blue;
} /* Class selector */
div {
  color: green;
} /* Element selector */
```

✅ **Calculation:**

- Inline styles: `1,0,0,0`
- ID: `0,1,0,0`
- Class: `0,0,1,0`
- Element: `0,0,0,1`

---

### **5. What is Flexbox, and how does it work?**

#### **Answer:**

**Flexbox** (Flexible Box Layout) is a layout model that allows easy alignment and distribution of space among items within a container, even if their sizes are unknown or dynamic.

#### **Key Properties:**

1. **For the Container:**

   - `display: flex`: Defines a flex container.
   - `flex-direction`: Defines the direction of items (`row`, `column`).
   - `justify-content`: Aligns items horizontally (e.g., `center`, `space-between`).
   - `align-items`: Aligns items vertically (e.g., `stretch`, `center`).
   - `flex-wrap`: Allows items to wrap to the next line (e.g., `wrap`).

2. **For the Items:**
   - `flex`: Defines how an item grows relative to other items.
   - Example:
   ```css
   .item {
     flex: 1;
   }
   ```

#### **Example:**

```html
<div class="container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

```css
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.item {
  flex: 1;
}
```

✅ **Flexbox is ideal for creating responsive and dynamic layouts** where items need to be aligned in both axes.

---

### **6. What is CSS Grid, and how does it differ from Flexbox?**

#### **Answer:**

**CSS Grid** is a two-dimensional layout system for creating complex layouts. While **Flexbox** is better for **1D layouts** (either rows or columns), **Grid** allows for **2D layouts** (rows and columns).

#### **Key Concepts:**

1. **Grid Container**: Defines a grid with `display: grid`.
2. **Grid Items**: Define the layout of items using `grid-template-columns`, `grid-template-rows`, etc.
3. **Example:**

```html
<div class="grid-container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
.item {
  border: 1px solid #ccc;
}
```

#### **Difference from Flexbox:**

- **Flexbox** is better for simpler, linear layouts (either horizontal or vertical).
- **Grid** is better for more complex, 2D layouts with rows and columns.

---

### **7. What are pseudo-classes and pseudo-elements in CSS?**

#### **Answer:**

**Pseudo-classes** and **pseudo-elements** are used to apply styles to specific parts of elements or states.

#### **Pseudo-classes**:

Define the state of an element (e.g., `:hover`, `:focus`).

```css
a:hover {
  color: red;
}
```

#### **Pseudo-elements**:

Target specific parts of an element (e.g., `::before`, `::after`).

```css
p::before {
  content: "→ ";
}
```

---

### **8. What is the difference between `position: absolute`, `position: relative`, and `position: fixed`?**

#### **Answer:**

| Property       | Behavior                                                                        | Use Case                                                                     |
| -------------- | ------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| **`absolute`** | Element is positioned relative to its nearest positioned ancestor (non-static). | Useful for elements that need to be placed precisely within a container.     |
| **`relative`** | Element is positioned relative to its normal position.                          | Used to adjust an element’s position without affecting the layout of others. |
| **`fixed`**    | Element is positioned relative to the viewport (fixed on screen).               | Ideal for sticky elements (e.g., fixed navigation bar).                      |

---

### **9. What is the `z-index` property, and how does it work?**

#### **Answer:**

The **`z-index`** property controls the **stacking order** of elements along the **z-axis** (depth). Higher values are displayed **in front of** lower values.

✅ **Usage:**

```css
div {
  position: absolute;
  z-index: 10;
}
span {
  position: absolute;
  z-index: 5;
}
```

#### **Important Notes:**

- `z-index` only works on **positioned elements** (`relative`, `absolute`, `fixed`, `sticky`).
- Elements with the same `z-index` are stacked in the order they appear in the HTML.

---
