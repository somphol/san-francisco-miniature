# Agent notes — San Francisco Miniature

This repository is **output only**: `index.html` is a generated, self-contained 3D diorama served by
GitHub Pages. There is no build step here and nothing to install.

Live: <https://somphol.github.io/san-francisco-miniature/>

## Editing

The source lives outside this repository, at `~/san-francisco-miniature`. Never edit `index.html` by
hand — it is a 1 MB inlined bundle and will be overwritten.

```sh
cd ~/san-francisco-miniature
npm run build:single
cp dist-single/index.html ~/sf-site/index.html
cd ~/sf-site && git add -A && git commit -m "…" && git push
```

GitHub Pages rebuilds automatically; check the deployment under the repository's Actions or Pages
settings if the live page lags.

## Verification

Run in the source project, before copying:

```sh
node tests/run.mjs        # geometry, traffic, diversity, planning
node scripts/verify.mjs   # 20 driven checks, frame-rate independent
```

`npm run shoot` is the deeper pixel harness, but it needs GPU-backed headless Chrome. On this Mac
headless Chrome falls back to SwiftShader at ~2.5 fps and its wall-clock waits time out — that is an
environment limit, not a scene defect. Report `verify.mjs` results instead.

## What is in the file

A React + three.js scene inlined into one document: a compressed San Francisco peninsula with a
rotated downtown grid and Market Street, eight landmark models (Golden Gate, Transamerica, Salesforce,
Ferry Building, Coit Tower, Painted Ladies, City Hall, Alcatraz), traffic, boats and day/night
lighting. Roughly 200 parcels, ~600 road edges.

URL parameters: `?lang=zh-CN` (Simplified Chinese), `?embed=1` (chrome-free layout for iframes),
`?quality=low|high`, `?capture=1` (deterministic stepping). No network calls at runtime.

## Constraints

- Keep it one self-contained file: no external scripts, fonts, images or fetches.
- Pages serves no response headers, so the sandbox CSP from `_headers` applies only on hosts that
  support headers (Netlify, Cloudflare Pages). That is expected, not a bug.
- `_headers` is inert on Pages; keep it for other hosts.
- The layout is artistically compressed. Do not treat it as a map.

## Known issues

- The bridge's city end stops above the Presidio without an approach viaduct.
- Blocks whose streets failed to route are empty.
- The full `npm run shoot` suite is unverified on GPU hardware.

## Attribution

Derived from the Manhattan Miniature 0.2.0 sample by SandBase Lab. Reused: scene mechanism, building
families, build pipeline. New: geography, landmarks, copy, roofs, bridge traffic, verification. The
original brand mark is not redistributed — `src/skill-config.ts` uses a neutral identity. State this
in any public description; attribution is not a licence, and the original archive carried none.

## Continuity

- Source project: `~/san-francisco-miniature` (not a git repository).
- Reusable skill that produced it: <https://github.com/somphol/city-miniature>.
- Session transcripts are archived **locally only** in `~/opencode-transcripts`; they are deliberately
  not published.
