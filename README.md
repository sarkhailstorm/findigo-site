# findigo-site

The "Launching soon" page that findigo.in shows until the Findigo app goes live. One plain HTML file, no build step.

## Changing the page

Edit `index.html` and push to `main`. GitHub Pages republishes it in a minute or two (a phone may need a reload).

- **Headline words** ("Find **a photographer** near you."): the `words` list in the `<script>` at the bottom. "a photographer" is the longest that fits a small phone.
- **Countdown**: set `data-launch` on `<main>`, for example `data-launch="2026-12-01T10:00:00+05:30"` (India time). Empty means no countdown.
- **Share message**: `MESSAGE` in the script, and the same words in the WhatsApp link on the `#share` button.
- **Link preview** (WhatsApp, Instagram, X): the `og:` tags in `<head>` and `share-card.png`.

Preview on your machine: `python3 -m http.server 8080`, then open http://localhost:8080.

## Setup

1. **Settings → Pages → Build and deployment**: Source **Deploy from a branch**, branch **main**, folder **/ (root)**, Save.
2. The custom domain comes from the `CNAME` file (`findigo.in`). Once the DNS check passes, tick **Enforce HTTPS**.
3. At the domain registrar, remove any other records on `@` and `www`, then add:

| Type | Name | Value |
| --- | --- | --- |
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |
| CNAME | www | sarkhailstorm.github.io |

## Launch day

1. A day before, lower the TTL of the `@` and `www` records to 300 seconds.
2. Point `@` and `www` at the app's server. Replace **all** of GitHub's `A` **and** `AAAA` records; a leftover `AAAA` keeps showing this page to people on IPv6, which is most mobile users in India.
3. In this repo's **Settings → Pages**, remove the custom domain and **Unpublish site**, then archive or delete the repo.
