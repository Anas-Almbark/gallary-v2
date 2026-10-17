# Gallery App — Landing page (v2, light)

Responsive marketing site for **Gallery App**, a photo gallery app. Light-theme version of `gallary-app`, built with React 19, TypeScript and Vite. Same layout and section structure. The copy and interactions are about browsing, searching and editing photos.

## Run it

```bash
npm install
npm run dev       # http://localhost:5173
npm run build     # type-check + production build into dist/
npm run preview   # serve dist/ locally
```

## Structure

```
src/
  content.ts            # every string on the page (copy, plans, FAQ, download meta)
  styles/tokens.css     # colours, fonts, radii, breakpoints as CSS variables (light palette)
  styles/global.css     # reset, container, section header styles
  components/           # Button, Icon (inline SVG set), Photo (generated landscape images)
  hooks/                # useInterval, useReducedMotion
  sections/             # one tsx + css pair per landing section
    Nav, Hero, PhoneDemo, Marquee, Features, Edit,
    HowItWorks, Pricing, FAQ, Download, Footer
```

## Breakpoints

| Width        | Layout                                                             |
| ------------ | ------------------------------------------------------------------ |
| < 768px      | Single column, 20px gutters                                        |
| 768–1023px   | Tablet: two-column grids, three-up steps, trust row visible        |
| ≥ 1024px     | Nav links, two phones in hero, 4-column bento                      |
| ≥ 1440px     | 1200px container centred                                           |

## Interactions

- **Hero headline** words come into focus one by one on load.
- **Phone demo**: the library thumbnails load in one by one. Tap any photo to open the full-screen viewer, then swipe (or use the arrows, the filmstrip, or the ← → keys) to browse. The heart toggles a favourite, which shows on the library tile. Back (or Esc) returns to the grid. On desktop, a second phone behind shows the viewer.
- **Marquee** loops right-to-left over 30s and pauses on hover.
- **Live search** in the features bento types a query every few seconds and highlights the matching photos.
- **Edit section**: drag the compare slider (pointer or keyboard arrows) to see the original next to the edited photo. Pick a look (Vivid, Warm, Cool, Mono, Fade) to change the edited side.
- **Coupon box** validates demo codes `GALLERY10` and `WELCOME20` and updates both plan prices.
- **FAQ** accordion, first item open by default.
- **QR tiles** are generated placeholders with a sweeping scan line. Replace `qrMatrix` in `Download.tsx` with a real QR before launch.
- All animations respect `prefers-reduced-motion`.

## Photos

There are no image files. `components/Photo.tsx` draws seeded SVG landscapes (sunset, beach, mountains, forest, snow, night, desert, lake). To use real photos, swap `<Photo …/>` for `<img>` tags in `PhoneDemo.tsx`, `Features.tsx` and `Edit.tsx`.

## Things to swap before shipping

- Brand name in `content.ts` (`brand`, `footer`) and the `<title>` in `index.html`.
- Store links and APK URL in `content.ts` (`download.platforms[].buttons`).
- Coupon validation in `Pricing.tsx` (currently a local lookup).
- Privacy / Terms URLs and contact email in `content.ts`.
