# 🎨 TailwindCSS Setup (v^3.4.17) for React + Vite + TypeScript

This guide documents how to install and configure TailwindCSS version `^3.4.17` in a **React + Vite + TypeScript** project.

---

## 🛠️ Step-by-Step Installation

### 1. Install TailwindCSS and dependencies

In your project root:

```bash
npm install -D tailwindcss@^3.4.17 postcss autoprefixer
```

Then generate config files:

```bash
npx tailwindcss init -p
```

This creates:

* `tailwind.config.js`
* `postcss.config.js`

---

## 📁 2. Configure `tailwind.config.js`

Update the `content` array to include your source files:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

---

## 🎨 3. Add Tailwind to your CSS

Create or update `src/index.css` (or `main.css`) with:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

---

## 🔗 4. Import CSS into your entry file

In `main.tsx`:

```ts
import './index.css'; // Adjust if your filename is different
```

---

## 🚀 5. Start Vite Dev Server

```bash
npm run dev
```

Test it by using Tailwind classes:

```tsx
<h1 className="text-3xl font-bold text-blue-500">Hello Tailwind!</h1>
```

---

## ✅ Done!

You’re now good to go with TailwindCSS v^3.4.17 🎉
Let me know if you want this in a downloadable `.md` file later when tools are working again 💻🔥
