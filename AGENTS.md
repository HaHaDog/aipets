# AIPets（AI宠物圈）

An e-commerce template built with Astro 5, React 19, and Tailwind CSS 4. Features a fully functional shopping cart, favorites system, blog, and product catalog with static site generation.

## Project Overview

This is a modern e-commerce frontend application designed for speed, SEO, and user experience. It uses Astro's island architecture to deliver mostly static HTML with minimal JavaScript, hydrating only the interactive components that need it.

### Key Features

- **Shopping Cart**: Full cart functionality with add/remove/update quantities, persistent via localStorage
- **Favorites/Wishlist**: Save products for later, persisted to localStorage
- **Product Catalog**: 20 tech products across categories (Computers, Phones, Audio, Accessories)
- **Blog Section**: Content marketing pages with static generation
- **Checkout Flow**: Multi-step checkout UI with order summary
- **Responsive Design**: Mobile-first approach with Tailwind CSS

## Technology Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| Astro | 5.16.11 | Static site generator & framework |
| React | 19.2.3 | Interactive UI components (islands) |
| Tailwind CSS | 4.1.18 | Utility-first styling |
| DaisyUI | 5.5.14 | Tailwind component library |
| Nanostores | 1.1.0 | Global state management |
| TypeScript | - | Type safety |
| Swiper | 12.0.3 | Image carousels/sliders |
| Sonner | 2.0.7 | Toast notifications |
| astro-icon | 1.1.5 | Icon system (Iconify/Lucide/MDI) |

## Project Structure

```
/
├── public/                 # Static assets (favicon only)
├── src/
│   ├── components/         # Reusable UI components
│   │   ├── about/          # About page sections
│   │   ├── blog/           # Blog-related components
│   │   ├── cart/           # Cart drawer component
│   │   ├── categories/     # Category listing components
│   │   ├── checkout/       # Checkout flow components
│   │   ├── contact/        # Contact page components
│   │   ├── favorites/      # Favorites list (React)
│   │   ├── footer/         # Site footer
│   │   ├── home/           # Homepage sections
│   │   ├── navbar/         # Navigation bar
│   │   ├── products/       # Product cards, gallery, info
│   │   └── ui/             # Generic UI (buttons, breadcrumbs, toaster)
│   ├── data/               # Mock data
│   │   ├── products.ts     # Product catalog (20 items)
│   │   ├── blogData.js     # Blog posts
│   │   └── home.ts         # Homepage data
│   ├── layouts/            # Astro layouts
│   │   ├── Base.astro      # Legacy base layout
│   │   └── Layout.astro    # Main layout (used)
│   ├── pages/              # File-based routing
│   │   ├── blog/           # Blog index & [slug] dynamic routes
│   │   ├── category/       # [category] dynamic routes
│   │   ├── product/        # [slug] dynamic product pages
│   │   ├── 404.astro       # Not found page
│   │   ├── about.astro
│   │   ├── checkout.astro
│   │   ├── contact.astro
│   │   ├── favorites.astro
│   │   └── index.astro     # Homepage
│   ├── store/              # Global state management
│   │   ├── cartStore.ts    # Cart state & logic
│   │   └── favoriteStore.ts # Favorites state
│   └── styles/
│       └── global.css      # Tailwind imports
├── astro.config.mjs        # Astro configuration
├── package.json
├── tsconfig.json           # TypeScript config (strict)
└── README.md
```

## Build and Development Commands

```bash
# Install dependencies
npm install

# Start development server (localhost:4321)
npm run dev

# Build for production (outputs to ./dist/)
npm run build

# Preview production build locally
npm run preview
```

## Architecture Patterns

### 1. Islands Architecture

Most components are Astro (`.astro`) files that render to static HTML. React (`.tsx`) is used only for highly interactive components:

- **React Components**: `FavoritesList.tsx`, `ToasterComponent.tsx`
- **Astro Components**: Everything else, with client-side scripts for interactivity

### 2. State Management with Nanostores

Shared state between Astro and React components using Nanostores:

```typescript
// src/store/cartStore.ts
import { persistentAtom } from '@nanostores/persistent';

export const cartItems = persistentAtom<CartItem[]>('cart_items', [], {
    encode: JSON.stringify,
    decode: JSON.parse,
});
```

State is persisted to localStorage automatically. Stores can be used in:
- React components via `useStore()` hook from `@nanostores/react`
- Astro component scripts via direct subscription

### 3. Client-Side Interactivity in Astro

Astro components add interactivity using `<script>` tags that run on the client:

```astro
<script>
    import { cartItems } from '../../store/cartStore';
    
    cartItems.subscribe((items) => {
        // Update UI when cart changes
    });
    
    // Re-init on view transitions
    document.addEventListener('astro:page-load', initComponents);
</script>
```

### 4. Dynamic Routes (SSG)

Product and blog pages use static generation with `getStaticPaths()`:

```astro
---
export async function getStaticPaths() {
    return products.map((product) => ({
        params: { slug: product.slug },
        props: { product },
    }));
}
---
```

### 5. Styling Approach

- **Tailwind CSS 4**: Imported via `@import "tailwindcss"` in global.css
- **DaisyUI**: Added as plugin via `@plugin "daisyui"`
- **Custom CSS**: Component-level `<style>` tags for animations and specific overrides
- **CSS Variables**: DaisyUI theme variables used throughout

## Data Structure

### Product Interface

```typescript
interface Product {
    id: string;
    name: string;
    title: string;
    price: number;
    description: string;
    category: string;
    subcategory?: string;
    stock: number;
    images: string[];
    slug: string;
    badge?: string;
    discount?: number;
    specs?: { label: string; value: string }[];
}
```

### Cart Item Interface

```typescript
interface CartItem {
    id: string;
    name: string;
    price: number;
    image: string;
    quantity: number;
    category?: string;
    discount?: number;
    stock?: number;
}
```

## Key Components Reference

| Component | Type | Purpose |
|-----------|------|---------|
| `Layout.astro` | Layout | Main page wrapper with navbar, footer, cart drawer |
| `NavBar.astro` | UI | Sticky header with cart/favorites counts |
| `CartDrawer.astro` | UI | Slide-out cart panel with item management |
| `CardProduct.astro` | Product | Product card with image slider, add to cart/fav |
| `FavoritesList.tsx` | React | Favorites page grid with add-to-cart |
| `ProductGallery.astro` | Product | Image carousel on product detail |
| `ProductInfo.astro` | Product | Price, specs, add to cart on detail page |

## Development Guidelines

### Adding a New Product

Edit `src/data/products.ts` and add to the `products` array following the Product interface.

### Adding a New Page

Create a `.astro` file in `src/pages/`. Use `Layout.astro` as the wrapper:

```astro
---
import Layout from "../layouts/Layout.astro";
---

<Layout>
    <div class="max-w-7xl mx-auto px-6">
        <!-- Content -->
    </div>
</Layout>
```

### Using Icons

Icons are from Lucide via astro-icon:

```astro
---
import { Icon } from "astro-icon/components";
---

<Icon name="lucide:heart" class="w-6 h-6" />
```

### State Management Best Practices

1. **Read state**: Use `.get()` for one-time reads, `.subscribe()` for reactive updates
2. **Update state**: Always use store actions (e.g., `addToCart()`, not `cartItems.set()`)
3. **Persistence**: Use `persistentAtom` from `@nanostores/persistent` for data that should survive reloads

## Configuration Files

### astro.config.mjs

```javascript
import { defineConfig } from 'astro/config';
import react from '@astrojs/react';
import tailwindcss from '@tailwindcss/vite';
import icon from 'astro-icon';

export default defineConfig({
    integrations: [react(), icon()],
    vite: {
        plugins: [tailwindcss()]
    }
});
```

### tsconfig.json

Extends Astro's strict config with React JSX transform.

## Testing

This project does not currently have automated tests. Manual testing checklist:

- [ ] Add/remove items from cart
- [ ] Update quantities (check stock limits)
- [ ] Add/remove favorites
- [ ] Navigate product pages
- [ ] Test responsive layout on mobile
- [ ] Verify localStorage persistence
- [ ] Test checkout flow UI

## Deployment

Build output is a static site in `./dist/` directory. Deploy to any static host:

- Vercel
- Netlify
- GitHub Pages
- Cloudflare Pages

No server-side runtime required.

## Notes for AI Agents

1. **Product images** are loaded from external URLs (Unsplash, etc.), not local files
2. **Stock management** is simulated via localStorage overrides in `cartStore.ts`
3. **No real payment processing** - checkout is UI-only
4. **Data is static** - all products are in `products.ts`, no database
5. **Language**: The project uses English for UI text but has Spanish lang attribute in HTML
6. **Client directives**: React components use `client:load` for hydration
