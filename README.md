# dpiritual-landing-pages

Static landing pages for digital products sold through SuperProfile.
Each product lives in its own folder and is a single self-contained `index.html`
with its images in `assets/`. No build step. Host on GitHub Pages, Netlify,
Vercel or any static host.

| Page | Folder | Checkout |
|------|--------|----------|
| वशीकरण मंत्र PDF Guide (₹49) | [`vashikaran-mantra-pdf/`](vashikaran-mantra-pdf/) | https://superprofile.bio/vp/vashikaran-mantra-pdf-guide |

## Run locally

```bash
python3 -m http.server 8000
# open http://localhost:8000/vashikaran-mantra-pdf/
```

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
fire `InitiateCheckout` (Meta) / `begin_checkout` (GA4) when clicked.

## Deploy on GitHub Pages

Settings → Pages → Source: *Deploy from a branch* → branch `main`, folder `/`.
The page will be served at `https://<user>.github.io/dpiritual-landing-pages/vashikaran-mantra-pdf/`.
