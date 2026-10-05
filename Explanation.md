# ClothCart — Project Explanation

## 1. Project Overview

**ClothCart** is a frontend-only e-commerce demo website for selling clothing. All product data is mocked on the client side. The goal is to deliver a polished shopping experience inspired by **Myntra** and **AJIO** with a **Material 3 dark-theme** aesthetic.

### Key Goals

| Goal | Description |
|---|---|
| **Visual polish** | Dark theme with Material 3 color tokens, smooth transitions |
| **Responsive layout** | Works on mobile, tablet, and desktop viewports |
| **Search & filter** | Real-time search-as-you-type with category filtering |
| **Product detail** | Modal overlay with full product information |
| **User profile** | A section showing user avatar and metadata |
| **Loading experience** | Branded splash screen with animated spinner on refresh |

---

## 2. Design Philosophy

### Inspiration
- **Myntra / AJIO** — card-based product grids, bold imagery, clean typography.
- **Material 3 (Material You)** — tonal surface colors, rounded corners, elevation via subtle shadows.
- **Dark theme** — reduces eye strain, makes product images pop, feels premium.

### Color Palette (Material 3 — Dark)

| Token | Hex | Usage |
|---|---|---|
| `surface` | `#121212` | Page background |
| `surface-container` | `#1E1E1E` | Cards, modals |
| `primary` | `#D0BCFF` | Buttons, active indicators |
| `on-primary` | `#381E72` | Text on primary surfaces |
| `secondary` | `#CCC2DC` | Secondary actions, chips |
| `on-surface` | `#E6E1E5` | Body text |
| `outline` | `#938F99` | Borders, dividers |

### Typography
- **Heading / Logo**: `Roboto Slab` (via Google Fonts CDN)
- **Body / UI**: `Inter` or system default sans-serif

### Motion (Framer Motion)
- **Standard easing**: `cubic-bezier(0.2, 0, 0, 1)` — most UI transitions
- **Emphasized easing**: `cubic-bezier(0.05, 0.7, 0.1, 1)` — modal enter/exit
- Duration: 200–400 ms for micro-interactions, 500 ms for page transitions

---

## 3. Technical Stack

| Technology | Role |
|---|---|
| **React 18+** | Component-based UI library |
| **TypeScript 5+** | Static typing for props, state, data models |
| **Tailwind CSS 3.4+** | Utility-first styling with dark-theme config |
| **Framer Motion 11+** | Declarative animations and transitions |
| **Vite 5+** | Dev server & build tool |

> **Note:** The description mentions `next/font/google` for Roboto Slab. Since this is a Vite + React project, we load the font via a `<link>` tag from Google Fonts CDN instead.

---

## 4. File Structure

```
ClothCart/
├── public/
│   └── favicon.svg
├── src/
│   ├── assets/images/              # Product images & placeholders
│   ├── components/
│   │   ├── LoadingScreen.tsx        # Splash screen with spinner
│   │   ├── Navbar.tsx               # Top bar — search, profile toggle
│   │   ├── SearchBar.tsx            # Expandable search input
│   │   ├── ProductCard.tsx          # Single product tile
│   │   ├── ProductGrid.tsx          # Responsive grid of ProductCards
│   │   ├── ProductModal.tsx         # Full-detail product overlay
│   │   ├── UserProfile.tsx          # User info panel
│   │   ├── CategoryChips.tsx        # Filter chip row
│   │   └── ui/
│   │       ├── Spinner.tsx          # Circular progress indicator
│   │       ├── Chip.tsx             # Reusable filter chip
│   │       └── Backdrop.tsx         # Dark overlay behind modals
│   ├── data/
│   │   ├── products.ts             # Mock product catalogue
│   │   └── user.ts                 # Mock user profile
│   ├── hooks/
│   │   ├── useSearch.ts            # Debounced search logic
│   │   └── useBodyScrollLock.ts    # Lock scroll when modal open
│   ├── types/
│   │   └── index.ts                # TypeScript interfaces
│   ├── utils/
│   │   └── filterProducts.ts       # Search + category filtering
│   ├── App.tsx                     # Root component
│   ├── App.css                     # Minimal overrides
│   ├── index.css                   # Tailwind directives + CSS vars
│   ├── main.tsx                    # Entry point
│   └── vite-env.d.ts              # Vite type declarations
├── index.html                      # HTML shell
├── tailwind.config.ts              # Custom theme config
├── tsconfig.json                   # TypeScript config
├── vite.config.ts                  # Vite config
└── package.json                    # Dependencies & scripts
```

### What Each Key File Does

| File | Purpose |
|---|---|
| `LoadingScreen.tsx` | Splash screen on page refresh. Shows "ClothCart" in Roboto Slab with a Material 3 spinner. Fades out after ~2s. |
| `Navbar.tsx` | Fixed top bar with logo, collapsible SearchBar, and user-avatar button. |
| `SearchBar.tsx` | Expanding input field. Updates shared `searchQuery` state; grid re-filters in real time. |
| `ProductCard.tsx` | Single product — image, title, price, discount badge. Opens ProductModal on click. |
| `ProductGrid.tsx` | Responsive CSS Grid of ProductCards with staggered entry animations. |
| `ProductModal.tsx` | Overlay with product image, title, description, sizes, price, and "Add to Cart". |
| `UserProfile.tsx` | Slide-in panel showing user avatar, name, email, and order history. |
| `CategoryChips.tsx` | Scrollable chip row ("All", "Men", "Women", "Kids", etc.). Filters the grid. |
| `products.ts` | Exports `Product[]` array with ~15–20 mock items. |
| `filterProducts.ts` | Pure function: `(products, query, category) → Product[]`. |

---

## 5. Screens

### 5.1 Loading Screen
- Renders on every full page load/refresh.
- Shows "ClothCart" in Roboto Slab + a circular spinner.
- Fades out after ~2 seconds via `AnimatePresence`.

### 5.2 Home Screen
- **Navbar**: Logo, expandable search, profile avatar.
- **Category chips**: Horizontal filter chips.
- **Product grid**: Responsive — 2 cols mobile, 3 cols tablet, 4 cols desktop.

### 5.3 Product Modal
- Scale + fade animation on open.
- Shows large image, title, price, sizes, description.
- Closes on backdrop click, close button, or Escape key.

### 5.4 User Profile
- Slides in from the right.
- Shows avatar, name, email, join date, order count.

---

## 6. Data Flow

All state lives in `App.tsx`. No global state library needed.

- `isLoading` → controls LoadingScreen visibility
- `searchQuery` → updated by SearchBar, consumed by ProductGrid
- `activeCategory` → updated by CategoryChips, consumed by ProductGrid
- `selectedProduct` → set on card click, opens ProductModal

---

## 7. Build & Run

```bash
npm install        # Install dependencies
npm run dev        # Start dev server
npm run build      # Production build
npm run preview    # Preview production build
```
