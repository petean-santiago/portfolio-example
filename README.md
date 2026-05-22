# SP Portfolio — Astro Landing Page Template

A modern, opinionated portfolio landing page built with **Astro.js**. Bento grid layout, bold typography, animated background, and 3D hover effects on key cards. Designed to be easy to customize and maintain.

---

## Sections included

- Hero with animated stats card
- About (bio, skills, availability)
- Selected work / case studies
- Process (4-step workflow)
- Testimonials & clients
- Contact with social links

---

## Tech stack

| Tool                                                 | Purpose                              |
| ---------------------------------------------------- | ------------------------------------ |
| [Astro](https://astro.build)                         | Framework — zero JS by default       |
| [Syne](https://fonts.google.com/specimen/Syne)       | Display font — headings              |
| [DM Sans](https://fonts.google.com/specimen/DM+Sans) | Body font                            |
| Vanilla CSS                                          | Per-component scoped styles          |
| Vanilla JS                                           | 3D tilt interactions (RAF-throttled) |

No UI libraries. No Tailwind. No unnecessary dependencies.

---

## Getting started

### Prerequisites

- Node.js `18+`
- npm or pnpm

### Installation

```bash
# 1. Clone the repo
git clone https://github.com/tu-usuario/sp-portfolio.git
cd sp-portfolio

# 2. Install dependencies
npm install

# 3. Start dev server
npm run dev
```

Open [http://localhost:4321](http://localhost:4321) in your browser.

### Build for production

```bash
npm run build
npm run preview   # preview the production build locally
```

---

## Project structure

```
sp-portfolio/
├── public/
│   └── favicon.svg
├── src/
│   ├── assets/
│   │   └── photo.jpg          ← your profile photo here
│   ├── layouts/
│   │   └── BaseLayout.astro   ← HTML shell, CSS variables, Google Fonts
│   ├── components/
│   │   ├── Background/
│   │   │   ├── Background.astro
│   │   │   └── Background.css  ← animated blobs + dot grid + grain
│   │   ├── Navbar/
│   │   │   ├── Navbar.astro
│   │   │   └── Navbar.css      ← floating pill nav, availability badge
│   │   ├── Hero/
│   │   │   ├── Hero.astro
│   │   │   └── Hero.css        ← main card + stats card with 3D tilt
│   │   ├── About/
│   │   │   ├── About.astro
│   │   │   └── About.css       ← bio, skills pills, availability card
│   │   ├── Work/
│   │   │   ├── Work.astro
│   │   │   └── Work.css        ← case study cards with 3D tilt + shimmer
│   │   ├── Process/
│   │   │   ├── Process.astro
│   │   │   └── Process.css     ← 4-step workflow + CTA card
│   │   ├── Social/
│   │   │   ├── Social.astro
│   │   │   └── Social.css      ← testimonial + client grid
│   │   └── Contact/
│   │       ├── Contact.astro
│   │       └── Contact.css     ← email CTA + social links 2x2
│   └── pages/
│       └── index.astro         ← composes all components
├── astro.config.mjs
├── package.json
└── README.md
```

One component per folder, one CSS file per component. No global styles except CSS variables defined in `BaseLayout.astro`.

---

## Customization

### 1. Personal info

Edit each component's frontmatter (the `---` block at the top of each `.astro` file):

**`Navbar.astro`** — your name and role:

```astro
<div class="navbar__logo-name">Your Name</div>
<div class="navbar__logo-role">Your Title</div>
```

**`Hero.astro`** — headline, description, stats:

```astro
<h1 class="hero__title">Your<br/><em>headline</em><br/>here.</h1>

<!-- Stats bars — edit --w to set the fill percentage -->
<div class="hero__stats-bar-fill" style="--w: 75%"></div>
```

**`About.astro`** — bio text, location, languages, skills:

```astro
const skills = [
  { label: 'Figma',    active: true  },
  { label: 'Framer',   active: false },
  // add or remove as needed
];
```

**`Work.astro`** — case studies:

```astro
const projects = [
  {
    id:     '01',
    tag:    'SaaS · Product Design · 2024',
    title:  'Your Project Name',
    desc:   'Short description of the project.',
    color:  'linear-gradient(135deg, #1a2a1a, #2d4a1e)', // thumbnail bg
    accent: '#C8F53E',                                    // accent color
    href:   '/case-studies/your-project',
  },
];
```

**`Process.astro`** — workflow steps:

```astro
const steps = [
  { num: '01', label: 'Your Step' },
  // ...
];
```

**`Social.astro`** — testimonial and client names:

```astro
const testimonial = {
  quote:    'Your testimonial text here.',
  initials: 'AB',
  name:     'Client Name',
  role:     'Role · Company',
};

const clients = ['Client A', 'Client B', 'Client C'];
```

**`Contact.astro`** — email and social links:

```astro
const socials = [
  { label: 'Red profesional', name: 'LinkedIn',   href: 'https://linkedin.com/in/you', bg: 'dark' },
  { label: 'Portfolio visual', name: 'Dribbble',  href: 'https://dribbble.com/you',   bg: 'dark' },
  { label: 'Código & repos',   name: 'GitHub',    href: 'https://github.com/you',     bg: 'navy' },
  { label: 'Comunidad',        name: 'Twitter / X', href: 'https://x.com/you',        bg: 'red'  },
];
```

```astro
<a href="mailto:you@yourdomain.com" class="contact__email">
  you@yourdomain.com ↗
</a>
```

### 2. Profile photo

Drop your photo at `src/assets/photo.jpg` (`.png` and `.webp` also work).  
Recommended size: vertical orientation, minimum `840×1040px`.

```astro
---
import { Image } from 'astro:assets';
import photo from '../../assets/photo.jpg';
---
<Image src={photo} alt="Your name" width={420} height={520} />
```

### 3. Colors

All colors are CSS variables in `BaseLayout.astro`. Change them once, they update everywhere:

```css
:root {
  --color-bg: #f5f0e8; /* page background      */
  --color-text: #1a1a1a; /* primary text          */
  --color-muted: #888888; /* secondary text        */
  --color-yellow: #ffb547; /* primary accent        */
  --color-red: #ff6b6b; /* availability / alert  */
  --color-navy: #2d2d5e; /* stats / testimonial   */
  --color-green-bg: #e8f5e9; /* skills card bg        */
}
```

### 4. Fonts

Fonts are loaded from Google Fonts in `BaseLayout.astro`. To swap them, replace the `<link>` tag and update:

```css
:root {
  --font-display: "Your Display Font", sans-serif;
  --font-body: "Your Body Font", sans-serif;
}
```

---

## Interactions

| Card               | Hover effect                                      |
| ------------------ | ------------------------------------------------- |
| Hero (yellow)      | 3D magnetic tilt following cursor                 |
| Stats (navy)       | 3D tilt + decorative internal circles             |
| Work cards         | Per-axis 3D tilt + shimmer sweep + dynamic shadow |
| Bio (dark)         | Scale + slight rotate                             |
| Skills (green)     | Scale + rotate                                    |
| Availability (red) | Scale + colored shadow                            |
| Process steps      | Individual translateY                             |
| CTA (dark)         | TranslateY + skewY                                |
| Contact main       | TranslateY + rotate + yellow shadow               |
| Social links       | TranslateY with per-color rotation or scale       |

All 3D tilts use `requestAnimationFrame` throttling and `backface-visibility: hidden` to prevent flickering at card edges.

---

## Adding new sections

Every section follows the same pattern:

```
src/components/YourSection/
├── YourSection.astro   ← markup + data + optional <script>
└── YourSection.css     ← styles scoped to this section
```

Then import it in `pages/index.astro`:

```astro
import YourSection from '../components/YourSection/YourSection.astro';

<YourSection />
```

---

## Deployment

This is a static Astro site — deploys to any static host with zero config.

### Vercel

```bash
npm i -g vercel && vercel
```

### Netlify

```bash
npm i -g netlify-cli && netlify deploy --build
```

### Cloudflare Pages

Connect your GitHub repo in the dashboard.

- Build command: `npm run build`
- Output directory: `dist`

### GitHub Pages

```js
// astro.config.mjs
export default defineConfig({
  site: "https://tu-usuario.github.io",
  base: "/sp-portfolio",
});
```

---

## Browser support

Chrome, Firefox, Safari, Edge — latest versions.  
3D tilt effects are mouse-only and degrade gracefully on touch devices.

---

## License

MIT — use it, fork it, ship it. Credit appreciated but not required.

---

## Acknowledgements

Design inspired by WonderKids Landing Page by Paperpillar and Swirlzy Food Brand by Halo UI/UX, both on Dribbble.

Built with [Astro](https://astro.build) ✦
