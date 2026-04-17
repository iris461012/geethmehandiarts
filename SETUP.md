# SETUP — GeethMehaniArts Mehandi Portfolio

A complete, production-ready portfolio built on React + Vite + Tailwind.
This guide walks you through personalising content, wiring up Cloudinary
& Formspree, deploying, and uploading new photos yourself.

---

## 1. Personalise content (5 minutes)

Open **`src/lib/site.ts`** and replace every value marked `// TODO`:

```ts
whatsapp: "919999999999",       // your full number, no + or spaces
instagram: "HANDLE",             // your handle without the @
mapsUrl: "https://maps.app.goo.gl/...",
yearsExperience: 8,
email: "hello@geethmehaniarts.com",
```

Also update `index.html`:
- The `<title>` and `<meta name="description">` tags
- The JSON-LD `telephone`, `sameAs` URLs, and `geo` coordinates
- The canonical `<link rel="canonical">` once your domain is live

Update `public/sitemap.xml` and `public/robots.txt` with your final domain.

Update testimonials in **`src/components/site/Testimonials.tsx`** with real
client quotes when you have them.

---

## 2. Cloudinary setup (live gallery — optional but recommended)

This lets you upload new mehandi photos from your phone and have them
appear on the site automatically — no developer needed.

1. Create a free account at https://cloudinary.com
2. Copy your **Cloud name** from the dashboard.
3. In Cloudinary → **Settings → Security**, scroll to "Restricted media types"
   and **uncheck "Resource list"**. (This allows the public `/list/{tag}.json`
   endpoint the site uses.)
4. Open **Media Library** and upload your photos.
5. For each photo, add **one tag**: `bridal`, `arabic`, `traditional`, or `festive`.
6. In `src/lib/site.ts`, set:
   ```ts
   cloudinary: {
     cloudName: "your_cloud_name_here",
     tags: ["bridal", "arabic", "traditional", "festive"],
   }
   ```
7. Save and redeploy. The gallery will fetch live photos.

If `cloudName` is left empty, the site shows the bundled fallback images.

### Uploading new photos going forward

1. Open the Cloudinary mobile app (or web).
2. Tap **Upload** → choose your photo.
3. Add the tag matching the category: `bridal`, `arabic`, `traditional`, or `festive`.
4. Done — the photo appears on the live site within minutes (no rebuild needed).

---

## 3. Formspree setup (booking form)

1. Sign up at https://formspree.io (free plan = 50 submissions/month).
2. Create a new form. Choose where you want submissions emailed.
3. Copy the form endpoint, it looks like `https://formspree.io/f/abcd1234`.
4. Paste it into `src/lib/site.ts`:
   ```ts
   formspreeEndpoint: "https://formspree.io/f/abcd1234",
   ```
5. (Optional) In Formspree dashboard → **Settings → Spam** turn on reCAPTCHA.
   The site already includes a hidden honeypot field for basic spam protection.

---

## 4. Cloudflare Pages deployment

This site is a Vite static build — no server needed.

1. Push the project to a GitHub repo (use Lovable's GitHub sync).
2. Go to https://dash.cloudflare.com → **Workers & Pages → Create → Pages → Connect to Git**.
3. Select your repo. Configure build:
   - **Framework preset:** Vite
   - **Build command:** `npm run build`
   - **Build output directory:** `dist`
   - **Node version:** `20`
4. Click **Save and Deploy**. Your site goes live at `your-project.pages.dev`.
5. (Optional) Add a **custom domain** in Pages → *Custom domains*.
   Cloudflare handles SSL automatically.

> Lovable's built-in **Publish** button also deploys to a `.lovable.app` domain
> with one click — both options work.

---

## 5. Personalisation checklist

Before going live, confirm:

- [ ] `src/lib/site.ts` — name, location, WhatsApp, Instagram, maps URL, years
- [ ] `index.html` — title, description, canonical URL, JSON-LD phone & geo
- [ ] `public/sitemap.xml` — replace `geethmehaniarts.com` with your domain
- [ ] `public/robots.txt` — sitemap URL
- [ ] `src/components/site/Testimonials.tsx` — real client quotes
- [ ] Cloudinary cloudName set (or leave blank to use bundled images)
- [ ] Formspree endpoint set
- [ ] Test the booking form end-to-end
- [ ] Test the WhatsApp button on a real phone
- [ ] Replace `public/og-cover.jpg` with a 1200×630 social-share image

---

## 6. Performance & SEO notes baked in

- Hero image uses `fetchpriority="high"` for fastest LCP.
- All gallery images are `loading="lazy"` with explicit width/height (CLS = 0).
- Cloudinary URLs use `f_auto, q_auto, w_700` for thumbnails and `w_1600` for lightbox.
- Fonts loaded with `display=swap` and preconnect hints — no FOIT.
- IntersectionObserver for reveal animations (no scroll polling).
- `prefers-reduced-motion` honoured site-wide.
- Skip-to-content link, focus-visible styles, ARIA labels on every interactive element.
- LocalBusiness JSON-LD for rich Google results.

Lighthouse target: **95+** across Performance, Accessibility, Best Practices, SEO.

---

Questions? Open the project in Lovable and ask in chat — Geeth's site is
designed to evolve with her practice.
