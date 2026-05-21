# Cyan Outlaw — Website Documentation

A handcrafted e-commerce website for Cyan Outlaw, a cyanotype apparel and accessories brand based in Delhi, India. Built as a single-file HTML template with no dependencies beyond Google Fonts.

---

## Project Structure

```
cyan_outlaw.html        Main website file — self-contained, no build step required
README.md               This file
```

---

## Tech Stack

| Layer | Choice | Reason |
|---|---|---|
| Framework | Vanilla HTML/CSS/JS | Zero dependencies, instant load |
| Fonts | Google Fonts (Cormorant Garamond + Jost) | Loaded via CDN link in `<head>` |
| Icons | None — CSS only | Keeps file lean |
| Payments | Not yet integrated | See Integrations section below |

---

## Sections

| Section | ID | Description |
|---|---|---|
| Navigation | — | Fixed top bar with logo, links, cart |
| Hero | — | Full-height split layout with cyanotype art |
| Care Banner | — | Sticky strip with 5 key care rules |
| Process | `#process` | 3-step cyanotype process walkthrough |
| Products | `#products` | 6-item grid — apparel and accessories |
| Care Instructions | `#care` | Full care guide with 4 cards + warning block |
| About | `#about` | Brand story with stats |
| Newsletter | — | Email capture form |
| Footer | — | Links, contact, copyright |

---

## Design System

### Colours

```css
--cyan:        #0D7A8A   /* Primary brand colour */
--cyan-light:  #B8E4EA   /* Accents and highlights */
--cyan-pale:   #EAF7F9   /* Background surfaces */
--ink:         #1A1A18   /* Primary text and dark backgrounds */
--paper:       #F8F5F0   /* Main background */
--cream:       #EDE9E2   /* Secondary surfaces */
--muted:       #7A7570   /* Secondary text */
--rust:        #8A4A2F   /* Reserved for future use */
```

### Typography

```css
--font-display: 'Cormorant Garamond', serif   /* Headings, brand name */
--font-body:    'Jost', sans-serif             /* Body text, labels, buttons */
```

### Spacing

- Section padding: `100px 48px` (desktop)
- Card padding: `48px 40px`
- Component gaps: `24px` (grid), `16px` (inline)

---

## Customisation Guide

### 1. Updating Product Listings

Each product card follows this structure in the `#products` section:

```html
<div class="product-card">
  <div class="product-new">New</div>           <!-- Remove if not new -->
  <div class="product-image cyan-bg">          <!-- Change background class -->
    <!-- SVG art or <img> tag goes here -->
    <div class="product-overlay">
      <a href="#">Add to Cart</a>              <!-- Link to product or cart action -->
    </div>
  </div>
  <div class="product-info">
    <p class="product-tag">Apparel</p>         <!-- Category label -->
    <p class="product-name">Product Name</p>   <!-- Product name -->
    <p class="product-price">₹1,800 — Status</p>
  </div>
</div>
```

**Background colour classes available:**
- `cyan-bg` — medium teal `#1A6B7A`
- `pale-bg` — light cyan `#C8E8ED`
- `deep-bg` — dark teal `#0D4A55`
- `sand-bg` — warm sand `#D8D0C2`
- `ink-bg` — near black `#1A1A18`
- `teal-bg` — mid teal `#2A8A9A`

**To use a real product photo instead of SVG art:**

```html
<div class="product-image">
  <img src="your-image.jpg" alt="Product name" style="width:100%; height:100%; object-fit:cover;">
  <div class="product-overlay">
    <a href="#">Add to Cart</a>
  </div>
</div>
```

---

### 2. Updating Care Instructions

Care cards are in the `#care` section. Each card:

```html
<div class="care-card">
  <div class="care-icon">〜</div>              <!-- Symbol or character -->
  <h3 class="care-card-title">Washing</h3>
  <p class="care-card-desc">
    <strong>Key rule highlighted here.</strong>
    Supporting detail follows.
  </p>
</div>
```

The wash lifespan warning block:

```html
<div class="care-warning">
  <div class="care-warning-icon">!</div>
  <div class="care-warning-text">
    <strong>Title</strong>
    Body text with <strong style="color:var(--cyan-light)">highlighted figure</strong>.
  </div>
</div>
```

---

### 3. Brand Name and Logo

Find and replace all instances of `Cyan Outlaw` and `CyanOutlaw` in the HTML. The nav logo splits across two elements:

```html
<a href="#" class="nav-logo">Cyan<span>Outlaw</span></a>
```

The `<span>` renders in `--cyan`. Adjust as needed.

---

### 4. Navigation Links

Add your real page URLs to the nav:

```html
<ul class="nav-links">
  <li><a href="/shop">Shop</a></li>
  <li><a href="/process">Process</a></li>
  <li><a href="/care">Care</a></li>
  <li><a href="/about">About</a></li>
</ul>
```

---

## Integrations

### Payment — Razorpay (Recommended for India)

1. Sign up at [razorpay.com](https://razorpay.com)
2. Add the Razorpay script in `<head>`:

```html
<script src="https://checkout.razorpay.com/v1/checkout.js"></script>
```

3. Replace each "Add to Cart" link with a button that triggers checkout:

```javascript
const options = {
  key: 'YOUR_RAZORPAY_KEY',
  amount: 180000,           // Amount in paise (₹1800 = 180000)
  currency: 'INR',
  name: 'Cyan Outlaw',
  description: 'Koi Ribbed Tank',
  handler: function(response) {
    alert('Payment successful: ' + response.razorpay_payment_id);
  }
};
const rzp = new Razorpay(options);
rzp.open();
```

### Alternatively — Move to Shopify

This HTML template can be converted to a Shopify theme. The design system (CSS variables, section structure) maps cleanly to Shopify's Liquid templating. Recommended for anyone wanting a full cart, inventory management, and order tracking without custom backend code.

---

### Newsletter — Mailchimp or Brevo

Replace the newsletter form action with your Mailchimp embedded form URL:

```html
<form action="YOUR_MAILCHIMP_URL" method="POST">
  <input type="email" name="EMAIL" placeholder="Your email address">
  <button type="submit">Notify Me</button>
</form>
```

---

### Instagram Feed

To embed a live Instagram feed in the footer or a dedicated section, use [Behold](https://behold.so) — free tier available, no backend required.

---

## SEO Basics

Add these tags inside `<head>` before going live:

```html
<meta name="description" content="Handcrafted cyanotype apparel and accessories. Made slowly, in Delhi, one piece at a time.">
<meta property="og:title" content="Cyan Outlaw">
<meta property="og:description" content="Wear the art of light.">
<meta property="og:image" content="URL_TO_YOUR_HERO_IMAGE">
<meta property="og:url" content="https://cyanoutlaw.in">
<link rel="canonical" href="https://cyanoutlaw.in">
```

---

## Deployment

The site is a single HTML file — no build step, no Node, no dependencies.

**Quickest options:**

| Platform | Cost | Steps |
|---|---|---|
| GitHub Pages | Free | Push to repo → enable Pages |
| Netlify | Free tier | Drag and drop the HTML file |
| Hostinger | ₹69/month | Upload via File Manager |
| Shopify | ₹1,994/month | Convert to Liquid theme |

For a brand at early stage, **Netlify free tier** is the fastest path to a live URL.

---

## Browser Support

Tested on Chrome, Firefox, Safari, and Edge. Uses CSS custom properties and CSS Grid — supported in all modern browsers. No IE11 support (not required for India market in 2024).

---

## Known Limitations

- Cart functionality is visual only — no backend or state management
- Product images are SVG placeholders — replace with real photography
- Newsletter form submits but has no backend — connect to Mailchimp or Brevo
- No mobile responsive breakpoints yet — add media queries for screens below 768px

---

## Next Steps

- [ ] Replace SVG placeholders with real product photography
- [ ] Add mobile responsive CSS (`@media (max-width: 768px)`)
- [ ] Integrate Razorpay or migrate to Shopify
- [ ] Connect newsletter form to Mailchimp or Brevo
- [ ] Add SEO meta tags
- [ ] Register domain `cyanoutlaw.in` and deploy

---

*Built for Cyan Outlaw, Delhi. Single file, no framework, no fuss.*
