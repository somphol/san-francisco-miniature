# San Francisco Miniature

A single self-contained HTML file: one interactive 3D miniature of San Francisco with eight
landmarks, traffic, boats and day/night lighting. No build step, no server, no network calls.

## Publish on GitHub Pages

1. Create a repository and push `index.html` to the default branch.
2. Settings > Pages > Source: *Deploy from a branch*, branch `main`, folder `/ (root)`.
3. The page appears at `https://<user>.github.io/<repo>/`.

## URL options

- `?lang=zh-CN` — Simplified Chinese (English is the default)
- `?embed=1` — chrome-free layout for iframes
- `?quality=low|high` — force a rendering tier

## Embed

```html
<iframe src="https://<user>.github.io/<repo>/?embed=1" width="345" height="345"
        style="border:0" loading="lazy"></iframe>
```

Prefer the raw `index.html` URL from Pages, not `raw.githubusercontent.com` (served as text/plain).
