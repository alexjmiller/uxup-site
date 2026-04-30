# UXup Brighton (demo site)

One-page static site for UXup Brighton — built as a feedbakkr demo
target for the 2026-04-30 UX-designers presentation. Every nav link
is a deliberate **fake door**: clicking them rewrites to
`/coming-soon.html` so we can capture which sections people expect
the most.

## Layout

- `index.html` — single page with hero, "what happens at a UXup",
  past themes (sticky-note treatment), audience columns, get-involved
  + newsletter fake-door form, footer.
- `coming-soon.html` — destination for every fake-door click.
- `styles.css` — full visual identity per the UXup brand brief
  (cyan + coral + sticky-note motif, Inter / Space Grotesk).
- `feedbakkr.iife.js` — vendored vanilla SDK build, captures feedback
  in-context.
- `netlify.toml` — no-build config + cache headers for the SDK bundle.
- `_redirects` — fake-door rewrites (every "real" nav slug →
  coming-soon.html, status 200 so the URL bar stays).

## feedbakkr embed

The SDK script tag in `index.html` and `coming-soon.html` carries a
placeholder `data-site-id="REPLACE_WITH_UXUP_SITE_PUBLIC_KEY"`.
Once the UXup site is provisioned in admin.feedbakkr.io, swap that
literal for the real `fbk_pk_…` key.

For tonight's presentation, configure the new site in **gated
launcher mode** so the feedback button only renders for visitors who
arrive via the review link the host shares (e.g. share
`https://uxup-site.netlify.app/?fbk=1&fbk_group=ux-night-2026-04-30`
in the room). Reviewers then leave feedback on the page they're
looking at, the host can flip to admin.feedbakkr.io filtered by
`group=ux-night-2026-04-30` to see it land in real time.

## Deploy

Static, no build. Netlify drops this directory directly. To push
updates after committing:

```
git push origin main
# Netlify auto-deploys
```

## Local preview

```
python3 -m http.server 8000
open http://localhost:8000
```
