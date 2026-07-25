# MedAkcess Website

A modern, single-page static website for the MedAkcess telemedicine platform. Healthcare, One Message Away.

## Features

- **Single-page scrolling design** with smooth scroll navigation
- **Dark/Light mode toggle** with system preference detection and localStorage persistence
- **Fully responsive** — mobile-first design with hamburger menu
- **Scroll animations** using Intersection Observer API
- **Interactive FAQ accordion**
- **Feature tab toggle** (For Patients / For Doctors)
- **Animated phone mockup** with WhatsApp chat interface
- **WhatsApp CTA integration** linking to `wa.me/260979040735`

## Tech Stack

- **HTML5** — semantic markup
- **Tailwind CSS** — via CDN, no build step required
- **Vanilla JavaScript** — no frameworks, no dependencies
- **Google Fonts** — Inter
- **SVG** — custom logo and phone mockup illustrations

## File Structure

```
website/
├── index.html          # Main page (all sections)
├── assets/
│   ├── favicon.svg     # MedAkcess logo icon
│   └── logo.svg        # Full logo for navbar
└── README.md           # This file
```

## Local Development

No build step required. Simply open `index.html` in a browser:

```bash
# Using Python
python3 -m http.server 8000

# Using Node.js (npx)
npx serve .

# Using PHP
php -S localhost:8000
```

Then visit `http://localhost:8000`.

## GitHub Pages Deployment

### Option 1: Deploy from Main Branch

1. Push this `website/` directory to a GitHub repository
2. Go to **Settings > Pages**
3. Under **Source**, select **Deploy from a branch**
4. Set branch to `main` (or `master`) and folder to `/ (root)` or `/docs`
5. Click **Save**

If the website is in a subdirectory (e.g., `website/`), set the folder to `/docs` or move the files to the repository root.

### Option 2: GitHub Actions (Recommended)

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
    paths:
      - 'website/**'

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Pages
        uses: actions/configure-pages@v5
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: 'website'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### Option 3: gh-pages Branch

```bash
# Install gh-pages
npm install -g gh-pages

# Deploy the website directory
gh-pages -d website
```

## WhatsApp Integration

All "Get Started" and "Chat with a Doctor" buttons link to:

```
https://wa.me/260979040735
```

To change the WhatsApp number, search and replace `260979040735` in `index.html`.

## Customization

### Colors

Edit the Tailwind config in the `<script>` tag at the top of `index.html`:

```javascript
tailwind.config = {
  theme: {
    extend: {
      colors: {
        'med': {
          'accent': '#6366f1',       // Muted indigo (primary)
          'accent-light': '#818cf8', // Dark mode variant
          'green': '#25D366',        // WhatsApp green
          'green-dark': '#1ebe57',   // WhatsApp hover
          // ...
        }
      }
    }
  }
}
```

### Content

All content is in `index.html`. Sections are clearly commented with `<!-- ===== SECTION NAME ===== -->` markers.

## Browser Support

- Chrome 80+
- Firefox 78+
- Safari 14+
- Edge 80+
- Mobile Safari (iOS 14+)
- Chrome for Android

## License

© 2026 MedAkcess. All rights reserved.
