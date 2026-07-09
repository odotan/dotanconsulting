# Dr. Hilla Dotan — website

Static site (no build step) for GitHub Pages, at **dotanconsulting.com**.

```
/
├── index.html          English homepage
├── he/index.html        Hebrew homepage (RTL)
├── assets/
│   ├── css/style.css     shared design system
│   ├── css/rtl.css       Hebrew/RTL overrides (loaded only on he/)
│   ├── js/main.js        menu, scroll-reveal, back-to-top
│   └── images/
│       ├── hilla-portrait.jpg      (add this)
│       ├── clients/client-01.png … (add these)
│       └── press/tv-1.jpg …        (add these)
└── CNAME                 custom domain for GitHub Pages
```

Both language versions link to each other (top-right "עברית" / "English").

---

## 1. Publish on GitHub Pages

1. Create a new **public** GitHub repo, e.g. `hilladotan-site`.
2. Push these files to the `main` branch (the CNAME file must sit at the repo root).
3. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   branch `main`, folder `/ (root)`. Save.
4. GitHub will show a temporary URL like `https://<username>.github.io/hilladotan-site/` —
   confirm the site loads there before moving to the custom domain.

## 2. Point dotanconsulting.com at it

At your domain's DNS provider, add:

**Apex domain (`dotanconsulting.com`) — four A records:**
```
A   @   185.199.108.153
A   @   185.199.109.153
A   @   185.199.110.153
A   @   185.199.111.153
```

**`www` subdomain (optional but recommended) — one CNAME record:**
```
CNAME   www   <username>.github.io.
```

Then in **Settings → Pages → Custom domain**, enter `dotanconsulting.com` and save
(GitHub writes the CNAME file automatically after this — the one in this repo just
pre-seeds it). Tick **Enforce HTTPS** once the certificate is issued (can take up to
~24h after DNS propagates).

Verify DNS anytime with:
```
dig dotanconsulting.com +noall +answer
```

## 3. Add the Calendly scheduler

Both `index.html` and `he/index.html` already include the Calendly embed script.
Find `data-url="https://calendly.com/YOUR-CALENDLY-LINK..."` in the **Contact**
section of each file and replace `YOUR-CALENDLY-LINK` with the real scheduling
link (e.g. `hilladotan/intro-call`). No other change needed.

## 4. About the sample content

This version is filled in for presentation purposes — everywhere Hilla hasn't
supplied real material yet (Publications, Awards, Articles, Press mentions,
TV/Video/Podcast entries), the site shows realistic-looking placeholder
copy so the page reads and flows like a finished site. Each of those items
carries a small **"Sample"** tag so it's obvious which entries need to be
swapped for the real thing before anything goes live — none of it should be
published as-is.

Bio, About, Approach, Services, and Clients copy is real, from Hilla's
content brief (English + Hebrew) — no sample tag needed there. Her portrait
is in place at `assets/images/hilla-portrait.jpg`.

Still functional placeholders (not just copy, but things that need to work):
the phone/contact details and the **Calendly link** in the Contact section —
see step 3 above.

## 5. Add client logos

The client list (eBay, Wix, HP, Deloitte, BCG, EY, AIG, TASC Consulting,
Riskified, IDF, international intelligence agencies, Israeli Ministry of
Foreign Affairs, Israeli Ministry of Justice, Prime Minister's Office) is
already in both `index.html` and `he/index.html` inside `#clients`. Each
tile just needs a matching logo file dropped into `assets/images/clients/`:

```
ebay.png  wix.png  hp.png  deloitte.png  bcg.png  ey.png  aig.png
tasc.png  riskified.png  idf.png  intelligence.png  mfa.png  moj.png  pmo.png
```

PNG or SVG with a transparent background works best (tiles show them in
grayscale until hovered). If a logo file is missing, the tile still shows
the organization's name — nothing breaks. For government/defense/intelligence
clients, confirm with Hilla whether an official emblem is appropriate to
display publicly, or whether a text-only tile is preferred.

## 6. Local preview

No build tools needed. From the project folder:
```
python3 -m http.server 8000
```
then open `http://localhost:8000`.
