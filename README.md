# Mikevisuals link page

The Instagram link-in-bio page: a 3D rangefinder over a mashup reel of the films, with the
email up top and the links underneath. One static folder, no build step.

| File | What it is |
|---|---|
| `index.html` | The whole page. Links are the `LINKS` array near the top of the first `<script>`. |
| `media/reel.mp4` | The 17-shot background reel (18 s, 2.1 MB): Emirates Finland and Australia, Sony, and behind-the-camera shots. `media/reel_poster.jpg` is a frame from its first shot. |
| `og.jpg` | 1200×630 preview shown when the link is shared in WhatsApp, iMessage or X. |
| `favicon.svg`, `favicon-32.png`, `apple-touch-icon.png` | Browser tab and iPhone home-screen icons. |
| `CNAME` | The address GitHub Pages serves it at: `links.mikevisuals.com`. |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are. |

three.js (0.160.0) and the two fonts load from jsDelivr and Google Fonts; everything else is here.

## Hosting plan: GitHub Pages at links.mikevisuals.com

1. Create a **public** repo `mikevisuals-links` on the `mickeyg5287-spec` account and push this folder
   (free GitHub Pages needs a public repo; nothing in here is private, the page itself is public).
2. Turn on Pages for the `main` branch, root folder. The `CNAME` file sets the custom domain.
3. Add one DNS record for mikevisuals.com (see below), wait for it to resolve, then tick
   **Enforce HTTPS** in the repo's Pages settings once GitHub has issued the certificate.

| Type | Host | Value |
|---|---|---|
| CNAME | `links` | `mickeyg5287-spec.github.io` |

To put the page on the bare domain instead (mikevisuals.com, since the Squarespace site has expired),
change `CNAME` to `mikevisuals.com`, change the three `links.mikevisuals.com` URLs in the `<head>` of
`index.html`, and replace the root `A` records with GitHub's four: `185.199.108.153`,
`185.199.109.153`, `185.199.110.153`, `185.199.111.153`, plus `www` CNAME → `mickeyg5287-spec.github.io`.

## Where the DNS lives, and what must not be touched

- Registrar: **GoDaddy** (renews 2027-12-11). Nameservers: **Squarespace DNS**, so records are edited in
  Squarespace → Domains → mikevisuals.com → DNS, not in GoDaddy.
- The Squarespace **website** subscription has expired (mikevisuals.com shows "Website Expired").
  If Squarespace no longer lets you edit DNS because of that, the fallback is switching GoDaddy back
  to its own nameservers, and that switch drops every record below unless they are re-created first.

Records in place on 2026-11-02 (email for @mikevisuals.com depends on these):

| Type | Host | Value |
|---|---|---|
| MX | `@` | 1 `aspmx.l.google.com`, 5 `alt1.aspmx.l.google.com`, 5 `alt2.aspmx.l.google.com`, 10 `aspmx2.googlemail.com`, 10 `aspmx3.googlemail.com` |
| TXT | `@` | `v=spf1 include:_spf.google.com ~all` |
| TXT | `@` | `google-site-verification=ndoAshv6BkSw9JisqCZ628-ToI-YaaYFlZrLtzCvCvU` |
| A | `@` | Squarespace: `198.185.159.144`, `198.185.159.145`, `198.49.23.144`, `198.49.23.145` |
| CNAME | `www` | `ext-sq.squarespace.com` |

## Changing the page later

- **Links:** edit `LINKS` in `index.html`. An entry with `url: null` shows its `soon` message instead.
- **Email:** the `<a class="mail">` right under the header. Tapping it opens the mail app and copies the
  address, because Instagram's in-app browser sometimes ignores `mailto:`.
- **Share image:** `og.jpg` was rendered from this page with headless Chrome at 2×, then scaled to
  1200×630. Re-render it if the wordmark, bio or email change, since they are baked into the image.
- After pushing, GitHub Pages updates within a minute or two; link previews in apps can stay cached
  for days.
