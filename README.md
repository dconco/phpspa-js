# ⚡ phpspa-js

**`phpspa-js`** is the lightweight JavaScript runtime for [phpSPA](https://github.com/dconco/phpspa), a PHP framework that mimics Single Page Application behavior without the complexity of a frontend framework.

It handles client-side navigation, page transitions, script execution, component styling, and event hooks — all designed to work with dynamic content rendered from PHP.

---

## 🚀 Installation

You can include `phpspa-js` either via **CDN** or host it yourself.

### ✅ CDN (Recommended)

```html
<script src="https://cdn.jsdelivr.net/npm/phpspa-js"></script>
````

### 🔧 Manual (GitHub)

Clone or download from the repo:

```bash
git clone https://github.com/dconco/phpspa-js.git
```

Then include it in your layout:

```html
<script src="/path/to/phpspa-js/dist/phpspa.min.js"></script>
```

---

## 🌐 Usage

Once included, `phpspa-js` automatically enhances `<Link />` tags with `data-type="phpspa-link-tag"` and enables seamless navigation between registered components.

You don’t need to do anything fancy — just generate links using your backend that look like this:

```html
<a href="/dashboard" data-type="phpspa-link-tag">Dashboard</a>
```

---

## 🧠 Core API

### 📥 `phpspa.navigate(url, mode = "push")`

Navigates to a new route dynamically. Internally fetches the component content, updates the `targetID`, `<title>`, styles, and scripts.

* `url`: Can be a string or `URL` object.
* `mode`: `"push"` (default) adds a new history entry, `"replace"` modifies the current one.

```js
phpspa.navigate("/profile", "replace");
```

---

### ↩️ `phpspa.back()`, `phpspa.forward()`

Handles SPA-style backward or forward navigation using browser history.

```js
phpspa.back();     // like window.history.back()
phpspa.forward();  // like window.history.forward()
```

---

### 📌 Event System

Use `phpspa.on()` to register event hooks:

```js
phpspa.on("beforeload", ({ route }) => {
    console.log("Navigating to", route);
});

phpspa.on("load", ({ route, success, error }) => {
    if (success) {
        console.log("Loaded:", route);
    } else {
        console.error("Failed to load", route, error);
    }
});
```

#### Available Events

| Event Name   | Description                             |
| ------------ | --------------------------------------- |
| `beforeload` | Fired before route is loaded            |
| `load`       | Fired after load is completed or failed |

Event callbacks receive an object:

```ts
{
  route: string,
  success?: boolean,
  error?: Error
}
```

---

## 🧩 Component Scripts

Each component can include inline scripts using:

```html
<script data-type="phpspa/script">
    console.log("Component script ran");
</script>
```

These are **dynamically executed** when the component is loaded via `phpspa.navigate()` or browser navigation. They won’t run on initial page load unless rendered by PHP.

---

## 🎨 Component Styles

Components can also define scoped styles:

```html
<style data-type="phpspa/css">
    .button { color: red; }
</style>
```

These styles are:

* Appended to the `<head>` dynamically
* Automatically cleaned up when navigating to another route

---

## 🧼 Scroll Restoration

`phpspa-js` supports native scroll restoration:

```js
history.scrollRestoration = "auto";
```

This ensures each component can handle scroll behavior without interference.

---

## 📦 Built for Integration

This script is tightly coupled with [phpSPA (PHP)](https://github.com/dconco/phpspa), and it's designed to work with its component system.

---

## 🔧 Development Notes

### Structure

* CDN build: `phpspa.min.js`
* Event system: `phpspa.on("load", ...)`
* History API used for SPA behavior
* Graceful fallback when JS is disabled

---

## 📜 License

MIT © Dave Conco

---
