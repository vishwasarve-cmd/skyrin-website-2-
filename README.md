# Skyrin Engineering website

A small static website made with plain HTML, CSS and JavaScript. There is no build step and nothing to install.

```
index.html        all the text and structure
css/styles.css    colours, layout, animations (numbered sections inside)
js/main.js        tabs, intro, form, tracking  (SETTINGS are at the top)
assets/           logo and project images
robots.txt        tells search engines what to crawl
sitemap.xml       list of pages for Google
vercel.json       hosting settings for Vercel
```

## How the site is organised

The site is one page with five tabs: **Home, Services, Projects, About, Contact**. Each tab fits on about one screen, so visitors scroll very little. On phones the tabs become a bar at the bottom of the screen.

- Services has seven sub-tabs (one per discipline).
- About has four sub-tabs (Who we are, Ways to work, Codes, FAQ).
- Contact has four office tabs and the quote form.
- Every tab has its own address, for example `yoursite.com/#services` or `yoursite.com/#services-piping`. The Back button works.

## 1. Try it on your computer

Double-click `index.html`. It opens in your browser.

## 2. Put it on GitHub

**Easiest way (no commands):**
1. Sign in at github.com, click **New repository**, name it `skyrin-website`, choose **Private**, click **Create repository**.
2. On the new page click **uploading an existing file**.
3. Unzip this folder, then drag **everything inside it** into the browser window.
4. Click **Commit changes**.

**With Git commands (inside this folder):**
```
git init
git add .
git commit -m "Skyrin website"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/skyrin-website.git
git push -u origin main
```

## 3. Deploy on Vercel

1. Sign in at vercel.com with your GitHub account.
2. Click **Add New**, then **Project**, and choose the `skyrin-website` repository.
3. Leave every setting as it is (Framework Preset: **Other**, no build command, no output directory). Click **Deploy**.
4. In about a minute you get a link like `skyrin-website.vercel.app`.

Every change you commit to GitHub is then published automatically.

## 4. Settings (top of `js/main.js`)

| Setting | What to do |
|---|---|
| `WEB3FORMS_KEY` | Get a free key at web3forms.com using the email that should receive enquiries, and paste it in. Until then the form opens the visitor's email app. |
| `GTM_ID` | Paste your Google Tag Manager ID (GTM-XXXXXXX). Add Google Analytics 4 and Microsoft Clarity inside Tag Manager. Leave empty for no tracking. |
| `WHATSAPP` | The WhatsApp number, digits only with country code. |
| `SHOW_CLIENT_NAMES` | Set to `false` to hide every client name until each client approves. |
| `INTRO_MS` | How long the intro plays (2400 = 2.4 seconds). |

**Intro:** it plays once per visit and has a Skip button. To turn it off completely, change `data-intro="on"` to `data-intro="off"` on the first line of `index.html` (the `<html>` tag).

## 5. Before going live on the real domain

- [ ] In `index.html`, delete the line `<meta name="robots" content="noindex, nofollow">` (it keeps Google away from the demo).
- [ ] Confirm the main address (www or non-www). It appears in the `canonical` link, the `og:url` tag and the schema block in `index.html`, and in `sitemap.xml` and `robots.txt`.
- [ ] In Vercel: **Settings, Domains**, and add the domain.
- [ ] Confirm the facts below.

## Content to confirm with the team

The wording was taken from the earlier demo. Please confirm before launch:
- The Home numbers: 100+ projects, 4+ years, 7 disciplines, 24 hour reply. (Edit the `data-count` values in `index.html`.)
- That each client may be named (or set `SHOW_CLIENT_NAMES` to `false`).
- The phone numbers, emails and office addresses.
- The "Ways to work" descriptions on the About tab.
- Add real client testimonials and certifications when you have permission.

## How enquiries and visits are tracked

When someone arrives from a tagged link (for example `?utm_source=whatsapp&utm_medium=message&utm_campaign=...`), the site remembers it for that visit and:
- sends the source, landing page and referrer with every quote request,
- adds the source to the WhatsApp message text,
- records these events in Tag Manager (only after the visitor accepts cookies): `virtual_pageview` (each tab opened), `quote_start`, `quote_submit`, `whatsapp_click`, `phone_click`, `email_click`, `project_view`, `project_filter`, `faq_open`.

Because the tabs live on one web address, Google Analytics would count only one page. The `virtual_pageview` event fixes this: in Tag Manager, create a GA4 event tag that fires on the custom event `virtual_pageview` and sends `page_path` and `page_title`. Then Analytics shows which tab each visitor looked at.

## A note on search ranking (SEO)

All the text is in the page, so Google can read it, but a one-address tabbed site gives Google fewer separate pages to rank than a site with a page per service. If search traffic becomes the main goal later, the Services tab can be split into one page per discipline.
