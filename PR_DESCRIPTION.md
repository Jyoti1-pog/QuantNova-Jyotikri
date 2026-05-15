# feat: add responsive site footer with navigation, social link, and copyright

## Summary

The landing page previously ended abruptly after the **Tech Stack** section
with no footer, hurting UI consistency and bottom-of-page navigation.

This PR adds a clean, fully responsive footer that matches the existing
dark blue → purple gradient + glass-card design language, so the page now
closes off properly with navigation, branding, and copyright.

## What changed

| File | Change |
| ---- | ------ |
| `frontend/index.html` | Added the footer markup + a scoped `<style>` block, inserted after the `#tech-stack` section. **This is the file actually served at `/`.** |
| `frontend/src/components/Footer.tsx` | New equivalent React `<Footer />` component for the trading-terminal shell (ready for when the React entry is mounted). |
| `frontend/src/App.tsx` | Imports and renders `<Footer onNavigate={setSection} />` inside `terminal-main`. |
| `frontend/src/styles.css` | `.site-footer*` rules using the existing CSS variables. |

### Footer contents

- **Brand block** — QuantNova title with the existing blue→purple gradient
  treatment and a one-line tagline.
- **Navigate** — anchor links to the in-page sections: Home, Platform
  Vision, Roadmap, Tech Stack.
- **Resources** — GitHub Repository, Contributing Guide, Report an Issue,
  MIT License.
- **Connect** — GitHub link with inline SVG icon (placeholder
  Twitter/LinkedIn/Discord intentionally omitted since the project has no
  official profiles yet).
- **Copyright bar** — `© <year> QuantNova. Released under the MIT License.`
  with the year filled in dynamically so it never goes stale.

### Responsive behaviour

| Viewport | Layout |
| --- | --- |
| ≥ 960px | 4 columns |
| 600px – 960px | 2 columns |
| < 600px | 1 column, stacked |

## Screenshots

### Desktop — 4-column layout (≥ 960px)

![Footer on desktop](docs/screenshots/footer-desktop.png)

### Tablet — 2-column layout (600–960px)

![Footer on tablet](docs/screenshots/footer-tablet.png)

### Mobile — single-column stacked (< 600px)

![Footer on mobile](docs/screenshots/footer-mobile.png)

### Footer in context — full landing page

![Footer in full page context](docs/screenshots/footer-desktop-fullpage.png)

## Test plan

- [x] `npm run dev` and load the page — footer renders below the Tech
      Stack section
- [x] Resize desktop → tablet → mobile — layout collapses cleanly at
      960px and 600px with no overflow or clipped content
- [x] Copyright year reflects the current year (set via JS)
- [x] GitHub / Resources links open the correct pages in a new tab with
      `rel="noopener noreferrer"`
- [ ] `npm run build` — production build succeeds (run before merge)

## Notes

- No existing markup was modified; the footer is appended after
  `#tech-stack` and before the analytics script.
- No new runtime dependencies — the icon is inline SVG.
- The previously commented-out original footer (lines 855–968) was left
  untouched to keep this PR focused on the new addition.

---

🤖 Screenshots captured against the running dev build at
`http://localhost:5173/`.
