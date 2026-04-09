# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static HTML portfolio site showcasing design work. There is no build process, framework, or dependencies—just HTML, CSS, and JavaScript. Files can be served directly via any static web server.

## Development Commands

**Serve locally for development:**
```bash
python -m http.server 8000
# or: npx http-server
# or: ruby -run -ehttpd . -p8000
```
Then open `http://localhost:8000`

**No linting, tests, or build steps required.** Changes are instant.

## Architecture

The portfolio uses a **HUD-based interface** (Head-Up Display) with fixed UI chrome at the top and bottom, while content scrolls in the middle:

- **`index.html`** – Main portfolio landing page with case study teasers and about section
- **`split-payment.html`** – Full case study deep-dive for a specific project (Split Payment redesign)
- **`assets/`** – Images, SVGs, PDF resume, and design documentation screenshots

### Key UI Patterns

1. **HUD Top** (`#hud-top`)
   - Fixed navbar with logo, navigation pills, and resume button
   - Uses backdrop blur and semi-transparent background for modern glassmorphism
   - Scrolling content passes underneath

2. **HUD Bottom** (`#hud-bottom`)
   - Fixed footer with status indicator, social links, and zoom controls
   - Stays above scrolling content

3. **Design System**
   - All colors and spacing use CSS custom properties (`:root { --bg, --ink, --purple, etc. }`)
   - Font stack: Plus Jakarta Sans (primary), DM Mono (code/mono)
   - Rounded corners default to `--r: 20px`
   - Consistent shadow system with light/dark variants

4. **Navigation**
   - Index page has nav pills (About, Work, etc.) linking to page sections
   - Split Payment case study has a back button to return to index
   - Top navigation links to external resume PDF

### Design Tokens to Know

- **Colors**: `--bg` (background), `--ink` (main text), `--ink-soft`, `--ink-muted`, `--purple` (accent), `--coral`, `--mint`, `--yellow`
- **Elevation**: `--shadow` (subtle), `--shadow-lg` (prominent)
- **Typography**: `--font` for body, `--mono` for code
- **Spacing**: Consistent padding/gap of 12px, 16px, 20px units

## Common Changes

### Adding a New Case Study
1. Create a new `.html` file in the root (e.g., `my-project.html`)
2. Copy the structure from `split-payment.html` (nav, progress bar, hero section)
3. Update the nav back button to link to `index.html`
4. Add case study content sections with consistent spacing
5. Add a teaser card to `index.html` portfolio grid linking to the new page

### Updating Colors/Theme
All colors are in the `:root` CSS variables block at the top of each HTML file. Update variables there to change the entire site's look. If theme applies to both pages, update both files' `:root` sections.

### Adding Navigation Links
- **To nav pills** (index only): Add `<button>` to `#nav-pills` and link to page sections with `#anchor-id`
- **To social links** (bottom HUD): Add `<a>` to `.hud-socials` with the desired URL
- **Case study teaser**: Add a card div with image, title, description, and link to new HTML file

### Optimize Images
SVGs in assets are preferred for icons and illustrations (they scale perfectly). Raster images (PNG) should be optimized before commit. No image processing pipeline exists—resize and compress manually if needed.

## File Structure

```
sushmita-portfolio/
├── index.html           # Main portfolio page
├── split-payment.html   # Case study example
├── assets/              # Images, SVGs, PDF, screenshots
│   ├── avatar.png
│   ├── sp-*.png         # Split Payment case study screenshots
│   ├── *.svg            # Illustration and icon SVGs
│   └── resume.pdf
├── .gitignore           # Excludes DS_Store and logs
└── CLAUDE.md            # This file
```

## Notes

- **No JavaScript bundling**: All JS is embedded in `<script>` tags within HTML
- **No CSS preprocessing**: All CSS is inline `<style>` blocks
- **Responsive design**: Uses flexbox, grid, and media queries (no framework)
- **Performance**: Fonts are preconnected from Google Fonts CDN for faster loading
- **Accessibility**: Use semantic HTML, maintain color contrast, provide alt text for images

## Testing in Browser

Open the HTML directly in a browser or serve via local server. Check:
- Responsive behavior (resize window or inspect mobile viewport)
- HUD top/bottom remain fixed while content scrolls
- All navigation links work
- External links (resume, socials) open correctly
- Hover states on buttons and links
