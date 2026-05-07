# 10 — Tailwind CSS: From Beginner to Advanced

---

## 📌 What is Tailwind CSS?

**Tailwind CSS** is a **utility-first CSS framework**. Instead of writing custom CSS classes, you use small, pre-built utility classes directly in your HTML.

### Traditional CSS approach:
```html
<!-- HTML -->
<button class="btn">Click Me</button>
```
```css
/* CSS file */
.btn {
    background-color: blue;
    color: white;
    padding: 10px 20px;
    border-radius: 6px;
    font-size: 16px;
}
```

### Tailwind approach:
```html
<!-- No CSS needed! The classes ARE the styles -->
<button class="bg-blue-500 text-white px-5 py-2.5 rounded-md text-base">
    Click Me
</button>
```

---

## 🤔 Why Use Tailwind?

| Traditional CSS | Tailwind CSS |
|----------------|-------------|
| Write CSS separately | Write styles inline in HTML |
| Name every class | No naming needed |
| CSS file grows over time | CSS file stays small (only includes used classes) |
| Context switching between files | Everything in one place |
| Easy to break things | Predictable utility classes |

---

## 🚀 Part 1: Setup

### Method 1: CDN (Quick Start — for learning only)

Add this to your HTML `<head>`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tailwind Demo</title>
    <!-- Tailwind CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-50 text-gray-800">
    <h1 class="text-3xl font-bold text-blue-600">Hello Tailwind!</h1>
</body>
</html>
```

> ⚠️ CDN is for learning only. For real projects, use the CLI installation.

---

### Method 2: CLI Installation (For Real Projects)

```bash
# Step 1: Initialize a project
npm init -y

# Step 2: Install Tailwind
npm install tailwindcss --save-dev

# Step 3: Create config file
npx tailwindcss init

# Step 4: Configure source paths in tailwind.config.js:
# content: ["./src/**/*.{html,js}"]

# Step 5: Add Tailwind directives to your CSS file (input.css):
# @tailwind base;
# @tailwind components;
# @tailwind utilities;

# Step 6: Build CSS
npx tailwindcss -i ./input.css -o ./output.css --watch

# Step 7: Link output.css in your HTML
```

---

## 🎨 Part 2: Core Utility Classes

### Spacing: Padding (`p`) and Margin (`m`)

Tailwind uses a spacing scale. Each unit = 4px.

```html
<!-- Padding: p-{size} -->
<div class="p-4">   16px padding all sides  </div>
<div class="p-8">   32px padding all sides  </div>
<div class="px-4">  16px left & right       </div>
<div class="py-6">  24px top & bottom       </div>
<div class="pt-2">  8px top only            </div>
<div class="pb-4">  16px bottom only        </div>
<div class="pl-6">  24px left only          </div>
<div class="pr-6">  24px right only         </div>

<!-- Margin: m-{size} -->
<div class="m-4">   16px margin all sides   </div>
<div class="mx-auto"> center horizontally   </div>
<div class="mt-8">  32px top margin         </div>
<div class="mb-4">  16px bottom margin      </div>
<div class="space-x-4"> <!-- gap between children (flex) --> </div>
<div class="space-y-4"> <!-- gap between children (flex column) --> </div>
```

**Common scale:**
| Class | Value |
|-------|-------|
| `p-0` | 0px |
| `p-1` | 4px |
| `p-2` | 8px |
| `p-4` | 16px |
| `p-6` | 24px |
| `p-8` | 32px |
| `p-10` | 40px |
| `p-12` | 48px |
| `p-16` | 64px |

---

### Colors

Tailwind has a full color palette with 10 shades (100-900) per color.

```html
<!-- Background colors -->
<div class="bg-white">White</div>
<div class="bg-gray-100">Light gray</div>
<div class="bg-blue-500">Medium blue</div>
<div class="bg-blue-900">Dark blue</div>
<div class="bg-red-500">Red</div>
<div class="bg-green-500">Green</div>
<div class="bg-yellow-400">Yellow</div>
<div class="bg-purple-600">Purple</div>
<div class="bg-slate-800">Dark slate</div>

<!-- Text colors -->
<p class="text-gray-800">Dark text</p>
<p class="text-gray-400">Muted text</p>
<p class="text-blue-600">Blue text</p>
<p class="text-white">White text</p>
<p class="text-red-500">Error text</p>
<p class="text-green-600">Success text</p>

<!-- Border colors -->
<div class="border border-gray-200">Border</div>
<div class="border-2 border-blue-500">Blue border</div>
```

---

### Typography

```html
<!-- Font size -->
<p class="text-xs">    Extra small (12px) </p>
<p class="text-sm">    Small (14px)       </p>
<p class="text-base">  Base (16px)        </p>
<p class="text-lg">    Large (18px)       </p>
<p class="text-xl">    XL (20px)          </p>
<p class="text-2xl">   2XL (24px)         </p>
<p class="text-3xl">   3XL (30px)         </p>
<p class="text-4xl">   4XL (36px)         </p>
<p class="text-5xl">   5XL (48px)         </p>
<p class="text-6xl">   6XL (60px)         </p>

<!-- Font weight -->
<p class="font-thin">      Thin     </p>
<p class="font-light">     Light    </p>
<p class="font-normal">    Normal   </p>
<p class="font-medium">    Medium   </p>
<p class="font-semibold">  Semibold </p>
<p class="font-bold">      Bold     </p>
<p class="font-extrabold"> Extrabold</p>
<p class="font-black">     Black    </p>

<!-- Text alignment -->
<p class="text-left">  Left     </p>
<p class="text-center">Center   </p>
<p class="text-right"> Right    </p>

<!-- Line height -->
<p class="leading-tight">  Tight (1.25)  </p>
<p class="leading-normal"> Normal (1.5)  </p>
<p class="leading-loose">  Loose (2)     </p>

<!-- Letter spacing -->
<p class="tracking-tight">  Tight  </p>
<p class="tracking-normal"> Normal </p>
<p class="tracking-wide">   Wide   </p>
<p class="tracking-widest"> Widest </p>

<!-- Text decoration -->
<p class="underline">         Underline         </p>
<p class="line-through">      Strikethrough      </p>
<p class="no-underline">      No underline       </p>
<p class="uppercase">         UPPERCASE          </p>
<p class="capitalize">        Capitalized        </p>
```

---

## 📐 Part 3: Layout

### Flexbox in Tailwind

```html
<!-- Basic flex container -->
<div class="flex">...</div>

<!-- Direction -->
<div class="flex flex-row">       <!-- Left to right (default) --> </div>
<div class="flex flex-col">       <!-- Top to bottom --> </div>
<div class="flex flex-row-reverse"> <!-- Right to left --> </div>

<!-- Justify content (main axis) -->
<div class="flex justify-start">    <!-- [A B C          ] --> </div>
<div class="flex justify-center">   <!-- [    A B C       ] --> </div>
<div class="flex justify-end">      <!-- [          A B C ] --> </div>
<div class="flex justify-between">  <!-- [A     B     C   ] --> </div>
<div class="flex justify-around">   <!-- [ A   B   C      ] --> </div>
<div class="flex justify-evenly">   <!-- [  A  B  C  ] --> </div>

<!-- Align items (cross axis) -->
<div class="flex items-start">    <!-- Top --> </div>
<div class="flex items-center">   <!-- Middle (most used!) --> </div>
<div class="flex items-end">      <!-- Bottom --> </div>
<div class="flex items-stretch">  <!-- Stretch (default) --> </div>

<!-- Wrap -->
<div class="flex flex-wrap">    <!-- Wrap to next line --> </div>
<div class="flex flex-nowrap">  <!-- Don't wrap (default) --> </div>

<!-- Gap -->
<div class="flex gap-4">        <!-- 16px gap --> </div>
<div class="flex gap-x-4 gap-y-2"> <!-- Different horizontal/vertical --> </div>

<!-- Flex item sizing -->
<div class="flex">
    <div class="flex-1">Takes equal space</div>
    <div class="flex-1">Takes equal space</div>
    <div class="flex-none w-48">Fixed 192px</div>
</div>

<!-- Perfect centering (very common!) -->
<div class="flex items-center justify-center h-screen">
    <p>Perfectly Centered!</p>
</div>
```

---

### Grid in Tailwind

```html
<!-- Define grid columns -->
<div class="grid grid-cols-1">   <!-- 1 column --> </div>
<div class="grid grid-cols-2">   <!-- 2 columns --> </div>
<div class="grid grid-cols-3">   <!-- 3 columns --> </div>
<div class="grid grid-cols-4">   <!-- 4 columns --> </div>
<div class="grid grid-cols-12">  <!-- 12 columns (like Bootstrap) --> </div>

<!-- Gap in grid -->
<div class="grid grid-cols-3 gap-4">      <!-- Equal gap --> </div>
<div class="grid grid-cols-3 gap-x-6 gap-y-4"> <!-- Different axes --> </div>

<!-- Span columns -->
<div class="grid grid-cols-4">
    <div class="col-span-2">Spans 2 columns</div>
    <div class="col-span-1">1 column</div>
    <div class="col-span-1">1 column</div>
    <div class="col-span-4">Full width row</div>
</div>

<!-- Span rows -->
<div class="row-span-2">Spans 2 rows</div>
```

---

## 📱 Part 4: Responsive Design

Tailwind uses **breakpoint prefixes** before any class.

### Breakpoints:
| Prefix | Min-width | Device |
|--------|-----------|--------|
| (none) | 0px | Mobile (default) |
| `sm:` | 640px | Small tablets |
| `md:` | 768px | Tablets |
| `lg:` | 1024px | Laptops |
| `xl:` | 1280px | Desktops |
| `2xl:` | 1536px | Large screens |

```html
<!-- Mobile: 1 col, tablet: 2 cols, desktop: 3 cols -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
    <div>Card</div>
    <div>Card</div>
    <div>Card</div>
</div>

<!-- Responsive text size -->
<h1 class="text-2xl md:text-4xl lg:text-6xl font-bold">
    Responsive Heading
</h1>

<!-- Hide on mobile, show on desktop -->
<nav class="hidden md:flex gap-6">
    <a href="#">Home</a>
    <a href="#">About</a>
</nav>

<!-- Show on mobile, hide on desktop -->
<button class="md:hidden">☰ Menu</button>

<!-- Responsive padding -->
<section class="px-4 md:px-8 lg:px-16 py-10 md:py-20">
    ...
</section>
```

---

## 🧩 Part 5: Real-World Components

### Button Component
```html
<!-- Primary Button -->
<button class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2.5 px-6 rounded-lg transition-colors duration-200 active:scale-95">
    Get Started
</button>

<!-- Outline Button -->
<button class="border-2 border-blue-600 text-blue-600 hover:bg-blue-600 hover:text-white font-semibold py-2 px-6 rounded-lg transition-all duration-200">
    Learn More
</button>

<!-- Danger Button -->
<button class="bg-red-500 hover:bg-red-600 text-white font-medium py-2 px-5 rounded-md transition-colors">
    Delete
</button>
```

### Card Component
```html
<div class="bg-white rounded-2xl shadow-lg overflow-hidden hover:shadow-xl transition-shadow duration-300 max-w-sm">
    <img src="https://picsum.photos/400/200" alt="Card Image" class="w-full h-48 object-cover">
    <div class="p-6">
        <span class="text-xs font-semibold uppercase tracking-widest text-blue-600">Category</span>
        <h3 class="text-xl font-bold text-gray-900 mt-2 mb-3">Card Title Here</h3>
        <p class="text-gray-500 text-sm leading-relaxed">
            This is a card description. It provides more detail about the content.
        </p>
        <a href="#" class="inline-block mt-4 text-blue-600 font-semibold hover:text-blue-800 transition-colors">
            Read More →
        </a>
    </div>
</div>
```

### Navbar Component
```html
<nav class="bg-white shadow-sm sticky top-0 z-50">
    <div class="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">
        <!-- Logo -->
        <a href="/" class="text-xl font-bold text-gray-900">BrandLogo</a>

        <!-- Desktop Links -->
        <ul class="hidden md:flex items-center gap-8 list-none">
            <li><a href="#" class="text-gray-600 hover:text-gray-900 transition-colors font-medium">Home</a></li>
            <li><a href="#" class="text-gray-600 hover:text-gray-900 transition-colors font-medium">About</a></li>
            <li><a href="#" class="text-gray-600 hover:text-gray-900 transition-colors font-medium">Blog</a></li>
            <li>
                <a href="#" class="bg-blue-600 hover:bg-blue-700 text-white px-5 py-2 rounded-lg transition-colors font-medium">
                    Get Started
                </a>
            </li>
        </ul>

        <!-- Mobile Menu Button -->
        <button class="md:hidden text-gray-600 text-2xl">☰</button>
    </div>
</nav>
```

---

## ⚙️ Part 6: Customization with `tailwind.config.js`

```javascript
// tailwind.config.js
module.exports = {
    // Tell Tailwind where your HTML/JS files are
    content: [
        "./src/**/*.{html,js,jsx,ts,tsx}",
        "./index.html"
    ],

    theme: {
        extend: {
            // Add custom colors
            colors: {
                primary: {
                    50:  '#eff6ff',
                    100: '#dbeafe',
                    500: '#3b82f6',
                    600: '#2563eb',
                    700: '#1d4ed8',
                    900: '#1e3a8a',
                },
                brand: '#6c47ff',
            },

            // Add custom fonts
            fontFamily: {
                sans: ['Inter', 'system-ui', 'sans-serif'],
                display: ['Outfit', 'sans-serif'],
            },

            // Add custom screen sizes
            screens: {
                'xs': '480px',
                '3xl': '1920px',
            },

            // Add custom spacing
            spacing: {
                '18': '4.5rem',
                '88': '22rem',
            },

            // Add custom border radius
            borderRadius: {
                '4xl': '2rem',
            },

            // Add custom animations
            keyframes: {
                shimmer: {
                    '0%': { backgroundPosition: '-200% 0' },
                    '100%': { backgroundPosition: '200% 0' },
                }
            },
            animation: {
                shimmer: 'shimmer 1.5s infinite',
            }
        },
    },

    plugins: [],
}
```

---

## 🧪 Complete Tailwind Landing Page

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tailwind Landing Page</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style> body { font-family: 'Inter', sans-serif; } </style>
</head>
<body class="bg-white text-gray-900">

    <!-- NAVBAR -->
    <nav class="border-b border-gray-100 sticky top-0 bg-white/80 backdrop-blur-sm z-50">
        <div class="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">
            <span class="text-xl font-bold text-blue-600">TailwindApp</span>
            <div class="hidden md:flex items-center gap-8">
                <a href="#" class="text-gray-600 hover:text-gray-900 transition-colors">Features</a>
                <a href="#" class="text-gray-600 hover:text-gray-900 transition-colors">Pricing</a>
                <a href="#" class="text-gray-600 hover:text-gray-900 transition-colors">Docs</a>
                <a href="#" class="bg-blue-600 hover:bg-blue-700 text-white px-5 py-2 rounded-lg transition-colors font-medium text-sm">
                    Get Started →
                </a>
            </div>
        </div>
    </nav>

    <!-- HERO -->
    <section class="py-24 px-6 text-center">
        <div class="max-w-4xl mx-auto">
            <span class="bg-blue-50 text-blue-700 text-xs font-semibold px-3 py-1 rounded-full uppercase tracking-widest">
                Now with AI
            </span>
            <h1 class="text-5xl md:text-7xl font-extrabold mt-6 mb-6 bg-gradient-to-r from-blue-600 to-violet-600 bg-clip-text text-transparent leading-tight">
                Build Beautiful<br>Interfaces Fast
            </h1>
            <p class="text-gray-500 text-lg md:text-xl max-w-2xl mx-auto leading-relaxed mb-10">
                Use Tailwind CSS to create stunning, responsive designs without ever leaving your HTML.
            </p>
            <div class="flex flex-col sm:flex-row gap-4 justify-center">
                <a href="#" class="bg-blue-600 hover:bg-blue-700 text-white font-semibold px-8 py-3.5 rounded-xl transition-all hover:shadow-lg hover:shadow-blue-200 hover:-translate-y-0.5">
                    Start Building →
                </a>
                <a href="#" class="border border-gray-200 hover:border-gray-300 text-gray-700 font-semibold px-8 py-3.5 rounded-xl transition-colors">
                    View Docs
                </a>
            </div>
        </div>
    </section>

    <!-- FEATURES GRID -->
    <section class="py-20 px-6 bg-gray-50">
        <div class="max-w-6xl mx-auto">
            <h2 class="text-3xl font-bold text-center mb-4">Everything You Need</h2>
            <p class="text-gray-500 text-center mb-12 max-w-xl mx-auto">Tailwind gives you the building blocks to create any design.</p>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div class="bg-white p-8 rounded-2xl shadow-sm hover:shadow-md transition-shadow border border-gray-100">
                    <div class="text-3xl mb-4">⚡</div>
                    <h3 class="font-bold text-lg mb-2">Lightning Fast</h3>
                    <p class="text-gray-500 text-sm leading-relaxed">Build UIs 10x faster than writing custom CSS from scratch.</p>
                </div>
                <div class="bg-white p-8 rounded-2xl shadow-sm hover:shadow-md transition-shadow border border-gray-100">
                    <div class="text-3xl mb-4">📱</div>
                    <h3 class="font-bold text-lg mb-2">Fully Responsive</h3>
                    <p class="text-gray-500 text-sm leading-relaxed">Mobile-first design with intuitive responsive breakpoints.</p>
                </div>
                <div class="bg-white p-8 rounded-2xl shadow-sm hover:shadow-md transition-shadow border border-gray-100">
                    <div class="text-3xl mb-4">🎨</div>
                    <h3 class="font-bold text-lg mb-2">Customizable</h3>
                    <p class="text-gray-500 text-sm leading-relaxed">Extend the design system with your own colors, fonts, and spacing.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- FOOTER -->
    <footer class="py-10 text-center text-gray-400 text-sm border-t border-gray-100">
        <p>&copy; 2025 TailwindApp. Built with Tailwind CSS. ❤️</p>
    </footer>

</body>
</html>
```

---

## 📊 Tailwind Quick Reference

| Category | Examples |
|---------|----------|
| **Padding** | `p-4`, `px-6`, `py-3`, `pt-2`, `pb-8` |
| **Margin** | `m-4`, `mx-auto`, `mt-8`, `mb-4` |
| **Size** | `w-full`, `w-1/2`, `h-screen`, `h-16`, `max-w-6xl` |
| **Colors** | `bg-blue-500`, `text-gray-800`, `border-red-200` |
| **Typography** | `text-xl`, `font-bold`, `text-center`, `uppercase` |
| **Flex** | `flex`, `flex-col`, `items-center`, `justify-between`, `gap-4` |
| **Grid** | `grid`, `grid-cols-3`, `col-span-2`, `gap-6` |
| **Border** | `border`, `rounded-lg`, `rounded-full`, `rounded-2xl` |
| **Shadow** | `shadow`, `shadow-md`, `shadow-lg`, `shadow-xl` |
| **States** | `hover:bg-blue-700`, `focus:ring-2`, `active:scale-95` |
| **Responsive** | `md:flex`, `lg:grid-cols-3`, `hidden md:block` |
| **Opacity** | `opacity-50`, `bg-blue-500/20` |
| **Transition** | `transition-colors`, `duration-300`, `ease-in-out` |
| **Transform** | `hover:-translate-y-1`, `hover:scale-105` |

---

> 🎉 **Congratulations! You've completed the complete Frontend Development Notes!**
>
> **Review Order:**
> 1. HTML Notes: `01-introduction` → `09-advanced-html`
> 2. CSS Notes: `01-introduction` → `09-animations`
> 3. Tailwind CSS: `10-tailwind-css` (this file!)
