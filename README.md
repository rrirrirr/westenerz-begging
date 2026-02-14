# Westenerz Mixtape Vol. 1 - Pre-Order Landing Page

An indie aesthetic pre-order landing page for Westenerz Mixtape Vol. 1 cassette release.

![Westenerz Mixtape](images/sticker-waifu.png)

## Features

- 🎵 **Crowdfunding Progress Bar** - Shows current funding vs 2000 SEK goal
- 💳 **Stripe Integration** - Ready for card payments
- 📱 **Swish Backup** - Manual Swish payment option for Swedish customers
- 🎨 **80s/90s Indie Aesthetic** - Glitch effects, vaporwave colors, CRT scanlines
- 🎌 **Exclusive Waifu Sticker** - AI-generated anime mascot design
- 📼 **Animated Vinyl** - Spinning record animation
- 📱 **Mobile Responsive** - Works on all devices

## Price & Goal

- **Price:** 150 SEK per cassette
- **Goal:** 2000 SEK (~13-14 orders needed)
- **Release:** Ships when goal is reached

## Setup & Deployment

### 1. Local Development

```bash
# Clone or navigate to the project
cd westenerz-mixtape

# Serve locally (Python 3)
python3 -m http.server 8000

# Or with Node.js
npx serve

# Or simply open index.html in your browser
```

Visit `http://localhost:8000` to view the site.

### 2. Stripe Integration Setup

1. **Create a Stripe Account**
   - Go to [stripe.com](https://stripe.com)
   - Sign up and complete verification

2. **Get Your API Keys**
   - Dashboard → Developers → API Keys
   - Copy your **Publishable key** (starts with `pk_test_` or `pk_live_`)
   - Copy your **Secret key** (starts with `sk_test_` or `sk_live_`)

3. **Update index.html**
   ```javascript
   const stripe = Stripe('pk_test_YOUR_PUBLISHABLE_KEY');
   ```

4. **Create a Payment Intent** (Backend required for production)
   ```javascript
   // Example checkout flow
   stripe.redirectToCheckout({
       lineItems: [{
           price_data: {
               currency: 'sek',
               product_data: {
                   name: 'Westenerz Mixtape Vol. 1',
                   description: 'Limited edition cassette + sticker'
               },
               unit_amount: 15000, // 150 SEK in öre
           },
           quantity: 1,
       }],
       mode: 'payment',
       successUrl: 'https://yourdomain.com/success',
       cancelUrl: 'https://yourdomain.com/cancel',
   });
   ```

5. **For Simple Integration**
   - Use [Stripe Payment Links](https://dashboard.stripe.com/payment-links)
   - Create a product → Get payment link → Replace button with link

### 3. Swish Setup

1. Update the Swish number in `index.html`:
   ```javascript
   // Find this line and replace with your number
   <code class="swish-number">07X-XXX XX XX</code>
   ```

2. Optional: Generate a Swish QR code
   - Use [Swish QR Generator](https://developer.swish.nu/documentation/guides/create-a-qr-code)
   - Add the QR code image to the modal

### 4. Deploy to GitHub Pages

1. **Create a GitHub Repository**
   ```bash
   # Initialize git
git init
   git add .
   git commit -m "Initial commit - Westenerz Mixtape landing page"
   
   # Create repo on GitHub, then:
   git remote add origin https://github.com/YOUR_USERNAME/westenerz-mixtape.git
   git push -u origin main
   ```

2. **Enable GitHub Pages**
   - Go to repository Settings → Pages
   - Source: Deploy from a branch
   - Branch: main → / (root)
   - Click Save

3. **Access Your Site**
   - Your site will be at: `https://YOUR_USERNAME.github.io/westenerz-mixtape/`
   - May take a few minutes to propagate

### 5. Update Progress Tracking

Currently, the progress bar uses simulated data. To make it dynamic:

**Option A: Google Sheets + Apps Script (Free)**
1. Create a Google Sheet with order tracking
2. Add Apps Script to serve as JSON API
3. Fetch data in JavaScript

**Option B: Static Site with GitHub Actions**
1. Store order count in a JSON file
2. Update via GitHub Actions workflow
3. Rebuild site on each order

**Option C: Simple Backend (e.g., Vercel, Netlify Functions)**
```javascript
// Example API endpoint
fetch('/api/orders')
    .then(res => res.json())
    .then(data => updateProgress(data.totalAmount));
```

## File Structure

```
westenerz-mixtape/
├── index.html          # Main landing page
├── style.css           # Styles with indie aesthetic
├── README.md           # This file
└── images/
    └── sticker-waifu.png   # AI-generated waifu sticker
```

## Customization

### Colors
Edit CSS variables in `style.css`:
```css
:root {
    --color-accent: #ff006e;        /* Hot pink */
    --color-accent-secondary: #8338ec;  /* Purple */
    --color-cyan: #00f5d4;          /* Cyan */
    --color-yellow: #fee440;        /* Yellow */
}
```

### Content
- Update band name: Search/replace "WESTENERZ"
- Update pricing: Change `PRICE_PER_UNIT` in JavaScript
- Update goal: Change `GOAL_AMOUNT` in JavaScript
- Update tracklist: Edit the `<ol class="tracks">` section
- Update Swish number: Find `swish-number` class

### Sticker Image
The waifu sticker was generated using Pollinations AI. To regenerate:
```bash
# Using the pollinations script
./skills/pollinations/scripts/image.sh "your new prompt" --output images/sticker-waifu.png
```

## Browser Support

- Chrome/Edge 80+
- Firefox 75+
- Safari 13+
- Mobile browsers (iOS Safari, Chrome Mobile)

## License

For Westenerz band use only. Art and design elements are property of the band.

## Credits

- Fonts: [Syne](https://fonts.google.com/specimen/Syne) & [Space Mono](https://fonts.google.com/specimen/Space+Mono) via Google Fonts
- Sticker Art: Generated with [Pollinations AI](https://pollinations.ai)
- Icons: Native emoji + CSS styling

---

**Questions?** Contact the band or check the Stripe/Swish documentation for payment integration help.