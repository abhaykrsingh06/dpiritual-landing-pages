# dpiritual-landing-pages

Static landing pages for digital products. Each product lives in its own
folder and is a single self-contained `index.html` with its images in
`assets/`. No build step. Host on GitHub Pages, Netlify, Vercel or any static
host.

| Page | Folder | Checkout / funnel |
|------|--------|-------------------|
| वशीकरण मंत्र PDF Guide (₹49) | [`vashikaran-mantra-pdf/`](vashikaran-mantra-pdf/) | https://superprofile.bio/vp/vashikaran-mantra-pdf-guide (SuperProfile, embedded) |
| Vivah Kundli PDF — शादी में देरी क्यों? (₹51) | [`vivah-kundli-pdf/`](vivah-kundli-pdf/) | https://jyoti.namaveda.in/vivah (NamaJyoti funnel, same-tab link) |

## Run locally

```bash
python3 -m http.server 8000
# open http://localhost:8000/vashikaran-mantra-pdf/
# or   http://localhost:8000/vivah-kundli-pdf/
```

## Two kinds of pages

- **Checkout pages** (`vashikaran-mantra-pdf/`) sell a fixed product through a
  SuperProfile checkout, embedded or in a new tab. See *Checkout: embedded vs
  redirect* below.
- **Funnel pre-sell pages** (`vivah-kundli-pdf/`) warm the visitor up and send
  them to a funnel page where they fill a form and pay. The funnel at
  `jyoti.namaveda.in` sends `X-Frame-Options: SAMEORIGIN`, so it cannot be
  embedded; every buy button is a plain link that opens the funnel in the
  **same tab** so mobile visitors keep momentum. The page's `CONFIG` block has
  `funnelUrl` and `defaultParams`. Any `utm_*`, `fbclid`, `gclid`, `ttclid` or
  `ref` parameter on the landing page URL is forwarded to the funnel so ad
  attribution survives the hop; `defaultParams` are added only when the
  visitor arrived with no `utm_*` of their own.

## Checkout: embedded vs redirect

Every page has a small `CONFIG` block at the top of its `<script>`:

```js
const CONFIG = {
  checkoutUrl: 'https://superprofile.bio/vp/...',
  checkoutMode: 'embed',   // 'embed' | 'redirect'
};
```

- `embed` opens the SuperProfile checkout inside the page in a modal
  (an `<iframe>`), so the buyer never leaves your site. The modal always
  shows an "open in new tab" fallback link.
- `redirect` opens the SuperProfile page in a new tab. Always works.

`embed` only works if SuperProfile permits its checkout to be framed from
your domain. Test once on the live domain: open the page, click the buy
button, and confirm the checkout form appears inside the modal and that a
test UPI/card payment completes. If the modal stays blank, switch to
`redirect`. You can also test either mode without editing the file by
appending `?checkout=redirect` or `?checkout=embed` to the page URL.

## Analytics

Paste a Meta Pixel or GA4 snippet into `<head>`. The buy buttons already
fire `InitiateCheckout` (Meta) / `begin_checkout` (GA4) when clicked. For a
funnel pre-sell page, use the same pixel ID as the funnel so the landing →
funnel → purchase path is attributed to one pixel.

## Deploy on GitHub Pages

Settings → Pages → Source: *Deploy from a branch* → branch `main`, folder `/`.
Pages are served at `https://<user>.github.io/dpiritual-landing-pages/<folder>/`,
e.g. `.../vashikaran-mantra-pdf/` or `.../vivah-kundli-pdf/`.
