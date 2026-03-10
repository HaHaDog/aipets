# AIPets（AI宠物圈）

E-commerce template built with **Astro 5**, **React 19**, and **Tailwind CSS 4**. Designed for speed, SEO, and specific aesthetic appeal, featuring a fully functional shopping cart, favorites system, blog, and more.

![astroEcommers](https://github.com/user-attachments/assets/dff02a23-5c09-4737-85a5-60d00fea14af)


## ✨ Features

- **⚡ Blazing Fast**: Built on top of Astro's next-gen island architecture.
- **🎨 Modern Design**: Styled with Tailwind CSS 4 and DaisyUI 5 for a premium look and feel.
- **🛒 Shopping Cart**: Fully functional cart with persistent state using Nanostores.
- **❤️ Whishlist/Favorites**: Save your favorite items with persistent local storage.
- **📦 Product Catalog**: Dynamic product listing with category filtering.
- **📝 Blog Section**: Integrated blog for content marketing and SEO.
- **📱 Fully Responsive**: Mobile-first design that looks great on all devices.
- **🔍 Search**: Instant product search functionality.
- **� Checkout UI**: polished checkout page interface.
- **🔔 Notifications**: Toast notifications for user interactions (Sonner).
- **🖼️ Carousels**: Interactive product sliders using Swiper.

## 🛠️ Tech Stack

- **Framework**: [Astro 5.0](https://astro.build/)
- **UI Integrations**: [React 19](https://react.dev/)
- **Styling**: [Tailwind CSS 4.0](https://tailwindcss.com/) & [DaisyUI 5](https://daisyui.com/)
- **State Management**: [Nanostores](https://github.com/nanostores/nanostores)
- **Icons**: [Iconify](https://iconify.design/) (Lucide & MDI)
- **Animations**: CSS Transitions & Micro-interactions

## 📂 Project Structure

```text
/
├── public/           # Static assets
├── src/
│   ├── assets/       # Optimized images and assets
│   ├── components/   # Reusable UI components
│   │   ├── cart/     # Cart related components
│   │   ├── checkout/ # Checkout flow components
│   │   ├── home/     # Homepage sections
│   │   ├── navbar/   # Navigation bar
│   │   ├── products/ # Product displays
│   │   └── ui/       # Generic UI elements (buttons, inputs)
│   ├── data/         # Mock data (products, static content)
│   ├── layouts/      # Astro layouts (Base, etc.)
│   ├── pages/        # File-based routing
│   │   ├── category/ # Dynamic category pages
│   │   ├── product/  # Dynamic product details
│   │   └── ...       # Other static pages (About, Contact)
│   ├── store/        # Global state (Cart, Favorites)
│   └── styles/       # Global styles
└── astro.config.mjs  # Astro configuration
```

## 🚀 Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/E-commer-Astro.git
   cd E-commer-Astro
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the development server**
   ```bash
   npm run dev
   ```

4. **Build for production**
   ```bash
   npm run build
   ```

## 🧞 Commands

| Command           | Action                                       |
| :---------------- | :------------------------------------------- |
| `npm run dev`     | Starts local dev server at `localhost:4321`  |
| `npm run build`   | Build your production site to `./dist/`      |
| `npm run preview` | Preview your build locally, before deploying |
