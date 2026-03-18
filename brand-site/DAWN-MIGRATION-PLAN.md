# Dutton Brown — Dawn Theme Migration Plan

A phased plan to migrate from Shopify Impact to a custom Dawn theme that fully expresses the Dutton Brown brand. This is a living document. Update it as decisions are made and deliverables ship.

---

## Current Inventory

### What Exists (Concept Pages)

| Page Type | File | Status | Notes |
|-----------|------|--------|-------|
| Homepage | `index.html` | Brand-compliant | Revised to grays+orange UI. Color strip + branded footer. |
| Product Listing / Collection | `product-listing-concept.html` | Brand-compliant | Most complete concept. Filters, swatches, trade pricing, view toggle, pagination |
| Trade Program | `trade-concept.html` | Brand-compliant | Grays+orange. Font weights fixed (300/400/600). Ready to port |
| Trade Hub | `trade-hub-concept.html` | Brand-compliant | Extended trade experience with resources and account features |
| Blog / Editorial | `blog-concept.html` | Brand-compliant | Poppins-only (DM Serif removed). Border-radius zeroed. Surface color fixed. |
| Rebates Program | `rebates-concept.html` | Brand-compliant | Hero revised to #4A4A4A. Headline weights 300. Color strip + footer added. |
| Product Detail Page | `product-page-concept.html` | Concept done | Two-column layout, gallery, swatches, accordion tabs. Needs review against locked decisions. |
| Cart Drawer | `cart-drawer-concept.html` | Concept done | Slide-out drawer pattern with line items, upsell slot |
| About / Our Story | `about-concept.html` | Brand-compliant | Color strip fixed. Border-radius zeroed. Georgia serif removed. |
| Contact | `contact-concept.html` | Concept done | Form + business info |
| FAQ | `faq-concept.html` | Brand-compliant | Accordion pattern. Category pill border-radius updated. |
| 404 | `404-concept.html` | Concept done | Brand moment with search + collection links |
| Mobile Nav | `mobile-nav-concept.html` | Brand-compliant | Full-screen overlay. Demo eyebrow + notice dot border-radius updated. |

### What Exists (Design System)

| Asset | File | Status |
|-------|------|--------|
| Design tokens | `css/tokens.css` | Production-ready. 139 lines. Colors, type scale, spacing, shadows, transitions |
| Component library | `css/components.css` | Production-ready. Buttons, cards, grids, nav, footer, utilities |
| Brand guidelines | `brand-guidelines.html` | Reference document. Comprehensive. |
| Logo (dark bg) | `logo-dutton-brown-white-orange.svg` | Ready |
| Logo (light bg) | `logo-dutton-brown-gray-orange.svg` | Ready |
| Brand guide PDF | `Dutton Brown Brand Guide.pdf` | Source of truth for brand voice, usage rules |

### What Does NOT Exist (Gaps)

| Page Type | Priority | Complexity | Notes |
|-----------|----------|------------|-------|
| **Search Results** | High | Medium | No concept. Needs product card reuse + empty state |
| **Customer Account Pages** | Medium | Medium | Login, register, order history, addresses. Shopify has defaults but they need styling |
| **Announcement Bar** | Medium | Low | Trade banner, sale messaging, shipping thresholds |
| **Password / Coming Soon** | Low | Low | Pre-launch gate page |

---

## Design Decisions — LOCKED

All 10 decisions are finalized. These apply to every page, template, and touchpoint.

### 1. Border Radius: Subtle, not bubbly

Minimal radius (`4px`) on UI elements — buttons, cards, inputs, images, panels. We favor clean, straight lines over the rounded-everything trend, but a slight soften is welcome. Avoid anything above `8px` on standard UI; nothing should look "pillowy."

**Exception:** Color swatches stay circular (`border-radius: 50%`). They represent color, not UI. Circles are how the eye reads color samples.

**Updated in:** `tokens.css` (`--db-radius: 4px`), `components.css` (all component radii).

**Form fields** follow the same radius. Full form field spec:
- Border: `1px solid #D6D0C8`, darkens to `#4A4A4A` on focus
- Background: `#FFFFFF`, no box-shadow (focus = border change only)
- Text: Poppins 400, 1rem, `#4A4A4A`; placeholders Poppins 300, `#8A8078`
- Labels: Poppins 600, 0.875rem, `#4A4A4A`, letter-spacing normal (mixed-case labels don't need tracking)
- Select dropdowns: `appearance: none` + custom SVG chevron, `padding-right: 2.5rem`
- File upload: `1px dashed #D6D0C8`, 4px radius
- Submit button: `#4A4A4A` fill, white text, Poppins 600, sentence case, letter-spacing normal; hover → `#FF9912`
- Required asterisk: `#D97706`; error messages: `#9F2C00`

### 2. Font Weights: 300, 400, 600

Three weights only. Ship three Poppins files, no more.
- **300 (Light)** — The dominant voice. Body text, descriptions, headlines at large sizes. This is what makes the site feel premium.
- **400 (Regular)** — Functional UI. Navigation, form inputs, labels, captions.
- **600 (Semibold)** — Emphasis. Section overlines, CTAs, button text, key headings. Buttons use sentence case (not uppercase) with letter-spacing normal. Only uppercase elements (overlines, table headers) use wide tracking (0.05em+).

500 (Medium) and 700 (Bold) are eliminated. Display and H1 now use light weight (300) at large sizes — size creates hierarchy, not weight. H4 uses regular (400) instead of medium.

**Updated in:** `tokens.css` (weight tokens), `components.css` (typography classes).

### 3. Blog Typography: Poppins only

One typeface across the entire site. No DM Serif Display. No serif anywhere. Poppins at 300 weight in large sizes (36-48px) creates editorial elegance without the cognitive break of switching font families between store and blog.

If a serif is ever introduced, it will be a deliberate brand evolution — not during migration.

### 4. Hero Backgrounds: Three options only

| Background | Use |
|-----------|-----|
| `#4A4A4A` (dark gray) | Impact moments: homepage hero, trade program hero |
| `#F7F5F2` (warm off-white) | Content pages: blog, FAQ, about, contact |
| `#FFFFFF` (white) | Commerce pages: collections, PDP, cart, search |

No orange as a section background — it overpowers product photography. Orange lives in accent elements: buttons, overlines, swatch rings, CTAs. Never as a wall of color.

No signature colors as section backgrounds. Ever. They are product colors, not UI colors.

**Concepts revised:** Homepage and Rebates updated to grays+orange (2026-02-18).

### 5. Product Card: Simplified

**Keep on collection cards:** Product type overline, product name, mini color swatches (up to 5 + overflow), price, hover actions (Quick View + Add to Cart). One badge max per card (New OR Bestseller, not both).

**Remove from collection cards:** Review stars (defer to PDP), spec icons (defer to PDP/quick view). The designer scanning a collection needs: what is it, what colors, what does it cost. Everything else lives one click deeper.

### 6. Image Ratios: Standardized

| Context | Ratio | Reason |
|---------|-------|--------|
| Product cards | 1:1 (square) | Clean uniform grid regardless of product type |
| PDP main image | 1:1 | Consistent with cards; gallery handles detail shots |
| Blog featured image | 3:2 | Editorial — the ratio of magazines and photography books |
| Blog card thumbnails | 3:2 | Matches featured ratio for consistency |

### 7. Cart: Slide-out drawer

Slide-out drawer as primary cart experience. 420px minimum width. Show product image large enough to see color. Show color name explicitly (not just a dot). Quantity adjuster, remove button, subtotal + checkout. One upsell slot ("Complete the look").

Full cart page as accessible fallback URL. Same content, page layout.

### 8. Color Swatches: The signature moment

| Context | Size | Behavior |
|---------|------|----------|
| Collection cards | 12px circles | Up to 5 visible + "+X more" overflow. No navigation on click. |
| PDP | 36-40px circles | Color name labels always visible below each swatch. Selected = 2px `#4A4A4A` ring with 2px white gap. Product image updates on selection. |
| Filter panel | 28px circles | Tooltip names on hover. Already established in product listing concept. |

Clicking a swatch on a collection card does NOT navigate — the entire card links to the PDP. Color selection happens on the PDP.

The PDP color selector is the most important interaction on the site. It should feel like choosing from a curated artist's palette.

### 9. Mobile Navigation: Full-screen overlay

Full-screen white overlay, not a sidebar. Centered navigation links at 24px+ size with generous vertical spacing. Animated entrance — links fade up with 50ms stagger between each.

**Contents (top to bottom):**
- Search field
- Close button (X) top-right
- Navigation links (centered, large)
- Account + Cart links
- "Join the Trade Program" CTA at bottom in orange

### 10. Announcement Bar: One message, not rotating

Single message, not rotating. Rotating feels promotional/discount. Dark gray (`#4A4A4A`) background, white text, orange accent on link. Dismissible (localStorage). Hides for logged-in trade customers.

Default: *"Interior designer or architect? Join the Trade Program →"*

Can be updated for seasonal moments (product launch, trade show) but always one message at a time.

---

## Phase 1: Foundation

**Goal:** Set up Dawn dev environment and port the design system into it. Nothing visible to customers yet.

### Deliverables

#### 1.1 — Dawn Development Setup
- [ ] Fork Shopify Dawn theme (latest stable version)
- [ ] Set up Shopify CLI for local development (`shopify theme dev`)
- [ ] Create a development store or use theme preview
- [ ] Establish git workflow (branch per phase, PR reviews)

#### 1.2 — Strip Dawn Defaults
- [ ] Remove Dawn's default CSS custom properties
- [ ] Remove Dawn's default color scheme system
- [ ] Remove Dawn's default typography settings
- [ ] Keep Dawn's Liquid architecture, section schema, and JS modules intact

#### 1.3 — Port Design Tokens
- [ ] Migrate `tokens.css` into Dawn's `assets/` directory
- [ ] Map Dutton Brown tokens to Dawn's CSS variable naming where possible (reduces Liquid refactoring)
- [ ] Set up font loading: Poppins via Google Fonts or self-hosted woff2 files
- [ ] **Decision required: self-host fonts (faster, no third-party dependency) or Google Fonts (easier)?**

#### 1.4 — Port Component Library
- [ ] Migrate button styles (primary, secondary, accent, white variants)
- [ ] Migrate form input styles (text, select, radio, checkbox, file upload)
- [ ] Migrate typography classes (display, h1-h4, body, caption, overline)
- [ ] Migrate layout utilities (container, grid, flex, section)
- [ ] Ensure all components use grays+orange only (no 13-color references in UI)

#### 1.5 — Base Settings Schema
- [ ] Configure Dawn's `settings_schema.json` with Dutton Brown color options
- [ ] Set default values matching your token palette
- [ ] Remove or hide color pickers for brand-controlled values (prevent staff from breaking the palette)

### Definition of Done
You can run `shopify theme dev` and see a blank Dawn theme with Dutton Brown typography, colors, spacing, and form elements rendering correctly. No page content yet.

---

## Phase 2: Site Chrome

**Goal:** Build the persistent elements that appear on every page — header, footer, announcement bar, color strip. These block everything else.

### Deliverables

#### 2.1 — Header / Navigation Section
- [ ] Port header from concepts (sticky, white background, 72px height, 1px border-bottom)
- [ ] Logo placement (left-aligned, 28px height, links to homepage)
- [ ] Navigation links: Lighting, Hardware, Our Story, Trade, Contact
- [ ] Account + Cart icons (right-aligned)
- [ ] **Mobile navigation panel — NEEDS CONCEPT** (see Decision #9)
- [ ] Search integration (icon in header? Separate search page? Predictive search drawer?)
- [ ] Active state on current page nav link
- [ ] Cart count badge (shows item count)
- [ ] Transparent header variant (for hero sections where header overlaps a dark background)

#### 2.2 — Announcement Bar Section
- [ ] Dark gray bar above header (`#4A4A4A`)
- [ ] Configurable message text via Shopify section settings
- [ ] Link support (e.g., "Join the Trade Program →")
- [ ] **Decision required: dismissible? rotating messages? conditional visibility for trade customers?**

#### 2.3 — Footer Section
- [ ] Port footer from concepts (dark gray background, 4-column grid)
- [ ] Column 1: Logo + brand tagline
- [ ] Columns 2-4: Shop, Company, Resources link groups
- [ ] Bottom bar: copyright + social icons (Instagram, Facebook, Pinterest)
- [ ] **Consider adding:** Newsletter signup in footer? (common for DTC, drives email list)
- [ ] Responsive: 4-col → 2-col → 1-col stacking

#### 2.4 — Color Strip Component
- [ ] 13-color strip as a reusable Liquid snippet
- [ ] Used between content and footer (or wherever appropriate)
- [ ] 6px height desktop, 4px mobile
- [ ] Include as a section that can be toggled per page template

### Definition of Done
Every page on the dev store shows the correct header, announcement bar, footer, and color strip. Mobile nav works. Cart icon shows count. Navigation highlights current page.

---

## Phase 3: Commerce Pages (Critical Path)

**Goal:** Build the pages where money changes hands. These must work before launch.

### Deliverables

#### 3.1 — Collection / Product Listing Page
- [ ] Port `product-listing-concept.html` into Dawn's `collection.liquid` template
- [ ] Breadcrumb navigation
- [ ] Collection header (title, count, description)
- [ ] Sticky filter toolbar (below sticky header)
- [ ] Filter drawer with groups: Type, Color (swatches), Finish, Price
- [ ] Active filter chips with clear-all
- [ ] Sort dropdown (Featured, Price Low-High, Price High-Low, Newest)
- [ ] View toggle (4-col / 3-col / 2-col grid)
- [ ] Product card component (see existing concept — fully designed)
- [ ] Pagination
- [ ] Trade CTA banner below grid
- [ ] Empty collection state ("No products match your filters")
- [ ] **Wire up Shopify's native filtering API** (Storefront Filtering)
- [ ] **Color swatch filter must map to actual Shopify product options**

#### 3.2 — Product Detail Page (PDP) — CONCEPT EXISTS

Concept at `product-page-concept.html`. Already on grays+orange palette. Two-column layout with sticky gallery left, product info right. Includes:
- [ ] Gallery with photo/3D tabs, 6-thumbnail grid, zoom on hover, badge system
- [ ] Color swatches (32px, tooltip names) — **verify against Decision #8:** increase to 36-40px, add always-visible color name labels below swatches (not just tooltips)
- [ ] Price block with trade pricing tag and locked-state for non-trade users
- [ ] Quantity selector + Add to Cart (full-width, `#4A4A4A`)
- [ ] "Made to order" lead time messaging
- [ ] Details accordion (Description, Specifications, Shipping, Downloads)
- [ ] Reviews section
- [ ] Related products carousel
- [ ] Trade-specific features: "Request a Sample" button, "Download Spec Sheet", CAD file access
- [x] **Verify font weights:** trimmed to 300/400/600 only — 500 and 700 removed from tokens and components
- [ ] **Verify border radius:** should be 4px on UI elements, 50% on swatches only

#### 3.3 — Cart Drawer
- [ ] Slide-out from right on "Add to Cart"
- [ ] Line items: image, title, color, quantity adjuster, price, remove
- [ ] Subtotal + "Checkout" button
- [ ] Continue shopping link
- [ ] Trade pricing reflected in line items (if logged in)
- [ ] **Upsell opportunity:** "Add a matching pull?" or related product suggestion
- [ ] Empty cart state with CTA to browse

#### 3.4 — Cart Page (Fallback)
- [ ] Full-page version of cart for accessibility and direct links
- [ ] Same line item format as drawer
- [ ] Order notes field
- [ ] Shipping estimate (optional)

#### 3.5 — Search Results
- [ ] Search bar (accessible from header)
- [ ] Predictive search dropdown (shows products + articles as you type)
- [ ] Full search results page reusing product card component
- [ ] Empty results state ("No results for 'xyz'. Try browsing our collections.")
- [ ] **Supports product and blog article results**

#### 3.6 — Checkout Customization (Limited)
Shopify controls checkout, but you can brand it:
- [ ] Logo on checkout
- [ ] Colors matching your palette
- [ ] Font (Poppins) if on Shopify Plus — otherwise Shopify defaults
- [ ] Thank you page customization

### Definition of Done
A customer can browse collections, filter by color, view a product, select options, add to cart, and reach checkout — all in a cohesive Dutton Brown experience.

---

## Phase 4: Brand Pages

**Goal:** Port your existing concept pages into Dawn sections/templates. This is where the site starts feeling like *your* brand, not a store.

### Deliverables

#### 4.1 — Homepage
- [ ] **Revise `index.html` concept** — replace pinkaboo/chalk gradient hero with grays+orange
- [ ] Hero section with headline, subline, CTAs (Shop Now + Trade Program)
- [ ] Stats bar (colors, products, years)
- [ ] Featured collections grid or product highlights
- [ ] Brand story section (text + image)
- [ ] Value propositions (what makes DB different)
- [ ] Testimonial
- [ ] Trade CTA section
- [ ] Color strip
- [ ] **Decision: does the homepage hero rotate/change seasonally? Or is it static?**
- [ ] **Decision: feature specific products on homepage? Or just collection links?**

#### 4.2 — Trade Program Page
- [ ] Port `trade-concept.html` into Dawn custom page template
- [ ] Hero, benefits grid, testimonial, application form, next steps
- [ ] **Form handling: keep Globo Form Builder or rebuild?**
  - Globo: Works now, has file upload, conditional logic. But adds third-party JS.
  - Custom Liquid form + app: Cleaner, but more work. Could use Shopify Flow or Klaviyo for processing.
  - *Recommendation: Keep Globo for now. Replace it later when the rest of the site is stable.*
- [ ] **Trade-specific account features (post-launch):**
  - Trade login → sees trade pricing
  - Trade dashboard (order history, saved specs, project boards)
  - This is a Phase 6 / future item

#### 4.3 — Blog / Articles
- [ ] Port `blog-concept.html` into Dawn blog template
- [ ] **Decision #3 applied** — Poppins-only (DM Serif removed from concept 2026-02-18)
- [ ] Blog index: featured post + card grid + archive list
- [ ] Category filtering (Design Tips, Color Stories, Studio News, Trade, Behind the Scenes)
- [ ] Individual article template (long-form content with images)
- [ ] Newsletter CTA within blog
- [ ] Related articles at bottom
- [ ] Author display (optional — depends on if multiple authors)

#### 4.4 — Rebates Page
- [ ] **Revise `rebates-concept.html`** — replace cobalt hero with `#4A4A4A`
- [ ] Port revised concept into Dawn custom page template
- [ ] Hero, how it works, rebate cards, CTA, terms

#### 4.5 — About / Our Story
- [ ] **NEEDS CONCEPT** — no concept exists
- [ ] Sections to include:
  - Hero with brand statement
  - Origin story (Minneapolis, made-to-order, why color)
  - Process / how it's made (if you can show assembly)
  - Team or founder section (optional — depends on brand comfort)
  - Values or philosophy
  - Trade CTA or shop CTA
- [ ] **Design direction:** This should feel editorial. Large imagery, generous whitespace, short paragraphs. Let photography carry the emotion. Text should be confident and brief.

#### 4.6 — Contact Page
- [ ] **NEEDS CONCEPT** — no concept exists
- [ ] Contact form (name, email, subject, message)
- [ ] Business info (address, phone, email, hours)
- [ ] Map embed (optional)
- [ ] FAQ link ("Check our FAQ first")
- [ ] Trade applicants redirect ("Looking for trade pricing? Apply here →")

#### 4.7 — FAQ Page
- [ ] **NEEDS CONCEPT** — no concept exists
- [ ] Accordion pattern (question → expand to reveal answer)
- [ ] Categories: Ordering, Shipping, Returns, Trade Program, Custom, Care & Maintenance
- [ ] Search within FAQ (nice to have, not required)
- [ ] CTA: "Still have questions? Contact us"

#### 4.8 — 404 Page
- [ ] **NEEDS CONCEPT** — no concept exists
- [ ] Brand moment: "This page doesn't exist, but your perfect fixture does."
- [ ] Search bar + links to popular collections
- [ ] Keep it light, keep it on-brand

### Definition of Done
All key pages are live in the Dawn theme with consistent branding. A visitor can arrive on the homepage, read about the brand, browse products, apply for trade, read the blog, and find answers to questions — all in one cohesive experience.

---

## Phase 5: Polish & QA

**Goal:** Everything works correctly across devices, performs well, and is ready for real traffic.

### Deliverables

#### 5.1 — Cross-Device Testing
- [ ] Desktop: Chrome, Firefox, Safari, Edge
- [ ] Tablet: iPad Safari, iPad Chrome
- [ ] Mobile: iPhone Safari, Android Chrome
- [ ] Test every page at 320px, 375px, 768px, 1024px, 1440px, 1920px

#### 5.2 — Performance
- [ ] Lighthouse score targets: Performance > 85, Accessibility > 90
- [ ] Lazy-load product images
- [ ] Font loading strategy: `font-display: swap` + preload critical weights
- [ ] Minimize third-party JS (audit Globo, review apps, analytics)
- [ ] Image optimization: WebP format, proper sizing via Shopify CDN
- [ ] Critical CSS inlined

#### 5.3 — Accessibility
- [ ] Keyboard navigation on all interactive elements
- [ ] Screen reader testing on key flows (browse → PDP → add to cart → checkout)
- [ ] Color contrast passes WCAG AA (your grays need checking — `#6B6B6B` on white is borderline)
- [ ] Alt text on all product images
- [ ] Form labels and error states are accessible
- [ ] Focus styles visible and on-brand

#### 5.4 — SEO Migration
- [ ] Map all existing URLs to new URLs
- [ ] Set up 301 redirects for any URL changes
- [ ] Verify structured data (Product, BreadcrumbList, Organization, FAQPage)
- [ ] Meta titles and descriptions on all pages
- [ ] Open Graph and Twitter Card meta tags
- [ ] Sitemap.xml generates correctly
- [ ] **Critical: Don't lose existing Google rankings during migration**

#### 5.5 — Content Migration
- [ ] All product data carries over (this lives in Shopify, not the theme)
- [ ] Blog posts migrated
- [ ] Page content migrated
- [ ] Navigation menus reconfigured
- [ ] Image assets verified

---

## Phase 6: Launch

### Pre-Launch
- [ ] Final visual review of every page template
- [ ] Test complete purchase flow (browse → add → cart → checkout → confirmation)
- [ ] Test trade application submission
- [ ] Test on slow connection (3G throttle)
- [ ] Backup current Impact theme (download as zip)
- [ ] Notify team of launch window

### Launch Day
- [ ] Publish Dawn theme as active theme
- [ ] Verify all redirects
- [ ] Monitor for 404s (check Shopify analytics and Google Search Console)
- [ ] Test one real purchase

### Post-Launch
- [ ] Monitor site speed (did it improve? It should.)
- [ ] Monitor conversion rates for 2 weeks
- [ ] Collect feedback from trade partners
- [ ] Address any edge cases discovered in production

---

## Future Considerations (Not In Scope Now)

These are valuable but should not delay launch:

- **Trade account portal** — logged-in trade customers see pricing, download CAD files, manage projects
- **Project boards** — trade customers save products to named projects (like Pinterest boards for specs)
- **Custom product configurator** — visual builder showing color/size combinations on the fixture
- **Wishlist / Save for Later** — requires app or custom metafield work
- **Multi-language** — if expanding beyond US/Canada
- **Dark mode** — probably not on-brand (you're a color/light brand), but worth noting

---

## Dependency Map

```
Phase 1 (Foundation)
  └── Phase 2 (Site Chrome)
        ├── Phase 3 (Commerce Pages)  ← CRITICAL PATH, do this first
        │     └── Phase 5 (Polish & QA)
        │           └── Phase 6 (Launch)
        └── Phase 4 (Brand Pages)  ← Can overlap with Phase 3
              └── Phase 5 (Polish & QA)
```

**What can run in parallel:**
- Phase 3 and Phase 4 can overlap once site chrome is done
- Within Phase 4, pages are independent — blog, about, FAQ, 404 can be built in any order
- Concept pages that need revision (homepage, rebates) can be revised during Phase 1

**What blocks everything:**
- Phase 1 must complete before anything else
- Phase 2 must complete before any page templates
- The PDP concept (3.2) blocks Phase 3 completion — this is the most urgent gap

---

## Email & Social Template Compliance Audit

The email templates and social templates were built before the grays+orange UI standard was established. Partial remediation completed 2026-02-18.

### Email Template Remediation Status

| Template | Status | Changes Applied (2026-02-18) |
|----------|--------|------------------------------|
| `product-launch.html` | FIXED | Orange gradient hero → `#4A4A4A` |
| `savings-event.html` | FIXED | Orange product placeholders → neutral gray gradients |
| `templates/email/index.html` | FIXED | Orange gradient hero → `var(--db-primary)` |
| `trade-program.html` | NEEDS WORK | Cobalt→lagoon hero gradient, pinkaboo testimonial bg, benefit circles, border-radius, font weights still violating |
| `brand-story.html` | NEEDS WORK | Pinkaboo hero, border-radius, font weights still violating |

### Remaining Violations in Unfixed Templates

**Border radius:** Hero sections (`12px 12px 0 0`), footer (`0 0 12px 12px`), product placeholders (`8px`) — should be `4px` max on standard UI.

**Font weight 700:** ~~Still present in `trade-program.html` and `brand-story.html`~~ — **Resolved.** Email templates now use 600 max. Token system trimmed to 300/400/600 only.

**Signature colors as backgrounds:** `trade-program.html` (cobalt, lagoon, python green, pinkaboo) and `brand-story.html` (pinkaboo) still use product colors as section backgrounds.

### Social Template Standards (New)

Social post image templates currently use signature colors as overlay gradients. Under the new standard:
- **Allowed overlay gradients:** `#4A4A4A` (dark gray), orange→dark orange (`#FF9912`→`#D97706`), transparent overlays on photography
- **Not allowed:** Cobalt, lagoon, python green, pinkaboo, slate blue, riding hood red as post overlays
- **Exception:** If the social post is specifically about a product color (e.g., "Meet Python Green"), the product's signature color can appear in that post. This is product storytelling, not UI.

---

## Immediate Next Steps

All 10 design decisions are locked. The design system (`tokens.css`, `components.css`) has been updated. Brand enforcement sweep completed 2026-02-18 across all concept pages and email templates.

1. ~~**Revise homepage concept**~~ — DONE (2026-02-18). Grays+orange UI, color strip added.
2. ~~**Revise rebates concept**~~ — DONE (2026-02-18). Hero → #4A4A4A, color strip + footer added.
3. ~~**Revise blog concept**~~ — DONE (2026-02-18). DM Serif removed, Poppins-only, border-radius updated.
4. ~~**Build missing concepts**~~ — DONE. About, Contact, FAQ, 404, Cart Drawer, Mobile Nav all exist.
5. **Review PDP concept** (`product-page-concept.html`) against locked decisions — verify swatch sizes, font weights, border radius.
6. **Fix remaining email templates** — `trade-program.html` and `brand-story.html` still have violations.
7. **Fork Dawn** and start Phase 1 — this can happen in parallel with remaining revisions.

---

*Last updated: 2026-02-18*
*Design decisions locked: 2026-02-18*