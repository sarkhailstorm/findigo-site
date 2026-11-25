# findigo-site

The "Launching soon" page at soon.findigo.in, while the Findigo app runs on findigo.in. One plain HTML file, no build step.

## Changing the page

Edit `index.html` and push to `main`. GitHub Pages republishes it in a minute or two (a phone may need a reload).

- **Headline words** ("Find **a new iPhone** near you."): the `words` list in the `<script>` at the bottom, and the first one also in the `#rotator` span so it shows before the script runs. Keep each about as short as "a bridal lehenga" or "a makeup artist", the longest that fit a 320 px phone; "a wedding planner" is already too wide.
- **Countdown**: set `data-launch` on `<main>`, for example `data-launch="2026-12-01T10:00:00+05:30"` (India time). Empty means no countdown.
- **Share message**: `MESSAGE` in the script, and the same words in the WhatsApp link on the `#share` button.
- **Link preview** (WhatsApp, Instagram, X): the `og:` tags in `<head>` and `share-card.png`.

Preview on your machine: `python3 -m http.server 8080`, then open http://localhost:8080.

## Setup

1. **Settings → Pages → Build and deployment**: Source **Deploy from a branch**, branch **main**, folder **/ (root)**, Save.
2. The custom domain comes from the `CNAME` file (`soon.findigo.in`). Once the DNS check passes, tick **Enforce HTTPS**.
3. At the domain registrar, remove any other records on `@` and `www`, then add:

| Type | Name | Value |
| --- | --- | --- |
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | sarkhailstorm.github.io |

GitHub's `AAAA` (IPv6) records are optional and left out on purpose: phones and networks on IPv6 still reach the page over IPv4, and there is nothing extra to remove on launch day.

## Launch day

1. A day before, lower the TTL of the `@` and `www` records to 300 seconds.
2. Point `@` and `www` at the app's server: replace all four of GitHub's `A` records and the `www` `CNAME`. If any `AAAA` record was added for GitHub, delete it too, or people on IPv6 keep seeing this page.
3. In this repo's **Settings → Pages**, remove the custom domain and **Unpublish site**, then archive or delete the repo.
