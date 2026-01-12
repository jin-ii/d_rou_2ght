# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## Project Overview

**NEWS-ADAN NEXUS** is a web-based agricultural drought management system that integrates Water-Energy-Food (WEF) resource management. The project is a static HTML/CSS/JavaScript website with a modern, animated interface.

### Key Technologies
- **Frontend**: HTML5, CSS3 (minified, single-line format), Vanilla JavaScript
- **Animations**: GSAP (GreenSock Animation Platform) with ScrollTrigger
- **Media**: Swiper.js for carousel/slider functionality
- **Fonts**: Pretendard (CDN-hosted)
- **Icons**: Font Awesome 6.4.0

---

## Project Structure

```
nexus-drought/
├── index.html                 # Main landing page
├── login.html                 # Login page
├── reset.css                  # Global CSS reset (shared across pages)
├── style.css                  # Main page styles (index.html)
├── css/
│   └── style.css             # Login page styles (separate from main)
├── images/
│   ├── main_nexus_img[1-5].jpg    # Hero section images
│   ├── video/                     # MP4 and MOV video files
│   │   ├── intro-box-*.mp4       # Hero media animations
│   │   ├── circle-*.mp4           # Main background animations
│   └── *.svg, *.png               # Icons and diagrams
├── .cursor/                   # Cursor IDE configuration
├── .claude/                   # Claude Code settings
└── PRD.md                     # Project requirements & CSS guidelines
```

---

## HTML/CSS Guidelines (From PRD.md)

### Critical Rules - MUST Follow

#### 1. **CSS Coding Format** (Non-negotiable)
All CSS must use **single-line, minified format**:

```css
/* CORRECT */
.header .logo{font-weight:700;font-size:22px}
.navbar .nav-links{display:flex;gap:60px;list-style:none}
.nav-links a:hover::after{transform:scaleX(1)}

/* WRONG - Multi-line or spaced */
.header .logo {
    font-weight: 700;
    font-size: 22px;
}
```

**Rules**:
- Each selector and all properties on ONE line
- NO spaces after colons (`:`) or semicolons (`;`)
- NO trailing semicolon on last property
- NO trailing spaces

#### 2. **CSS Selector Hierarchy** (Critical)
Always include parent context for reusable class names to avoid conflicts:

```css
/* CORRECT - Parent context included */
.header .logo{font-weight:700;font-size:22px}
.navbar .nav-links{display:flex;gap:40px}
.nav-actions .btn-login{font-size:15px}

/* WRONG - No parent context */
.logo{font-weight:700}
.nav-links{display:flex}
.btn-login{font-size:15px}
```

**Exception**: Unique section classes don't need parent context
- `.vision-section` ✅ (unique name, no parent needed)
- `.btn-login` ❌ (reusable, must have parent like `.nav-actions .btn-login`)

#### 3. **HTML Naming Conventions**
- Sections: `class="[name]-section"` and `id="[name]-section"`
- Buttons: `class="btn-[type]"` (e.g., `.btn-login`, `.btn-share`)
- Components: `class="container-[type]"` (e.g., `.container-fluid`)
- Always use **kebab-case** (lowercase with hyphens)

#### 4. **@media Queries** (Exception to single-line rule)
@media blocks are formatted with each selector on new lines:

```css
@media(max-width:768px){
    .hero-title{font-size:48px}
    .hero{padding-top:90px}
    .navbar .nav-links{display:none}
}
```

#### 5. **Design Constraints**
- Do NOT add `border-radius` or `box-shadow` unless explicitly requested
- Do NOT add shadows, rounded corners, or decorative effects beyond what's in the design

#### 6. **Root Variables** (Fixed)
Keep these CSS variables consistent across all stylesheets:

```css
:root{
    --bg-white:#ffffff;
    --text-black:#111111;
    --text-grey:#666666;
    --accent-blue:#0044cc;
    --border-light:#e5e7eb;
    --font-main:'Pretendard',...
}
```

---

## Page Architectures

### Index.html (Main Landing Page)
**Structure** (from top to bottom):
1. **Header** - Fixed navigation bar (90px height)
   - Logo: "NEWS-ADAN"
   - Nav links: NEXUS 소개, 대시보드, 가뭄현황, 보고서
   - Share button + popup menu
   - Login button
   - Hamburger menu (mobile)

2. **Hero Section** - Full viewport height
   - Center-aligned title + subtitle with GSAP animations
   - Three media boxes (WATER, ENERGY, FOOD) with video backgrounds
   - Staggered reveal animations on scroll

3. **Gallery Section** - Full width, scrollable
   - Gallery container with custom layout

4. **Vision Section** - Two-column layout
   - Left column: Section title
   - Right column: Lead text + statistics grid

5. **Solutions Section** (implied structure)
   - Multiple solution cards (Water, Energy, Food)

6. **NEXUS System Section** - System overview

7. **Footer** - Contact and navigation links

**Styling**: `style.css` (root-level)

### Login.html (Authentication Page)
**Structure**:
- **Left side (40%)**: Visual carousel with Swiper.js
  - 3 slides with background images + overlay text
  - Pagination dots
  - Auto-rotating effect

- **Right side (60%)**: Login form
  - Form fields: Username, Password
  - Password toggle button
  - Remember me checkbox
  - Forgot password link
  - Submit button
  - Home navigation button

**Styling**: `css/style.css` (separate from main page)
**Note**: Login uses separate CSS file with fully qualified selectors (e.g., `.login-container .login-visual`)

---

## Key CSS Files

### reset.css
- Global HTML/CSS reset
- Form element styling (inputs, selects)
- Utility classes (`.flex`, `.txtc`, `.w100`, etc.)
- Animation base classes (`.animate`)
- Shared variable definitions

### style.css (Main - index.html)
**Sections covered**:
- Header & navbar styling
- Hero animations with GSAP integration
- Vision section layouts
- Gallery section
- Impact cards with grid layout
- Responsive design (@media rules)

**Key considerations**:
- Uses GSAP for scroll-triggered animations
- Container max-width: 1400px
- Header is position: fixed with 90px height
- Navbar has hover effect with bottom border animation

### css/style.css (Login - login.html)
**Features**:
- Two-column layout (visual + form)
- Swiper pagination styling
- Form input styling with icon support
- Password visibility toggle
- Responsive breakpoints: 1024px, 768px, 480px

---

## Common Development Tasks

### Adding a New Section
1. Create HTML structure in index.html with `class="[name]-section" id="[name]-section"`
2. Add CSS to style.css following single-line format
3. Include parent selector context for all reusable classes
4. Add @media queries for responsive design (1024px, 768px, 480px)
5. Update navigation href in header to match section ID

### Modifying CSS
1. Locate the selector following the hierarchy (e.g., `.header .navbar .nav-links`)
2. Edit on single line: `.header .navbar .nav-links{display:flex;...}`
3. Add @media overrides if needed (maintain new-line format inside @media)
4. Test responsive behavior at 1024px, 768px, 480px breakpoints

### Working with Login Page
- CSS is in `css/style.css` (separate from main page)
- Uses fully qualified selectors: `.login-container .login-form-section .form-wrapper`
- Swiper.js handles carousel on left side
- Form validation JavaScript in `<script>` tag at bottom of HTML

### Updating Animations
- GSAP animations are inline in index.html `<script>` tags
- ScrollTrigger is used for scroll-based animations
- Timeline animations controlled via `.to()` and `.from()` methods
- Check hero section animations for element reference examples

---

## Responsive Design Strategy

### Breakpoints (Mobile-first approach)
```css
/* Desktop (default) */
/* All styles written for desktop first */

/* Tablet & Small Desktop */
@media(max-width:1024px){
    /* Reduce padding, adjust font sizes, reduce gaps */
}

/* Tablet & Mobile */
@media(max-width:768px){
    /* Stack layouts, hide desktop-only elements */
    /* Adjust header height if needed */
    /* Reduce font sizes further */
}

/* Mobile only */
@media(max-width:480px){
    /* Single column layouts, mobile-optimized spacing */
    /* Hamburger menu becomes primary navigation */
}
```

### Key Responsive Considerations
- Container width remains flexible (100% with max-width)
- Hero section text scales down at each breakpoint
- Navigation links hide/show based on breakpoint
- Gallery and cards adjust grid layout responsively

---

## Special Notes

### CSS Specificity
- Avoid `!important` except for overrides in @media queries (e.g., `!important` in Swiper pagination)
- Class-based selectors only (no ID selectors in CSS)
- Parent context prevents specificity issues

### Performance Considerations
- CSS is minified to single-line format for file size reduction
- GSAP scripts are loaded via CDN
- Images are optimized and lazy-loaded where possible
- Videos use `preload="auto"` and `autoplay` with muted for performance

### Known Issues / Edge Cases
- Hamburger menu icon (btn-menu) styling may conflict on mobile - check @media overrides
- Share popup z-index is set high (1001) to overlay other elements
- Hero media animations require specific z-index stacking - do not modify without testing

---

## External Dependencies

### CDN Resources
- Pretendard Font: `https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/static/pretendard.min.css`
- Font Awesome 6.4.0: `https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css`
- GSAP 3.12.2: `https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js`
- GSAP ScrollTrigger: `https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js`
- GSAP TextPlugin: `https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/TextPlugin.min.js`
- Swiper.js 11: `https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.js`

All CDN links are loaded in HTML `<head>` or end of `<body>`.

---

## File Organization Best Practices

1. **CSS files**: Keep all CSS in either root `style.css` or `css/` folder
2. **HTML files**: Root level (index.html, login.html, etc.)
3. **Images**: Organized in `images/` folder with subdirectories (`video/`, etc.)
4. **Never create**: Separate JS files - keep scripts inline in HTML for now

---

## Testing & Quality Checklist

- [ ] All CSS follows single-line minified format
- [ ] Parent selectors included for all reusable classes
- [ ] No `!important` outside @media queries
- [ ] Responsive design works at 480px, 768px, 1024px, 1400px+
- [ ] No border-radius or shadows added without explicit request
- [ ] Animation performance is smooth (use GSAP Timeline for complex animations)
- [ ] Images are optimized for web
- [ ] Mobile navigation (hamburger menu) functions correctly
- [ ] All navigation links point to correct section IDs
