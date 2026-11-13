# BCS702 — Parallel Computing (VTU Scheme 2022)

Promotional site for the free module-wise video lecture series.

Built from the same design system as the BCS703 site, so both courses look and
behave like one series.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole site — one self-contained file (inline CSS + JS) |
| `dr_lokesh_professor_new.png` | Portrait used in the hero and the teacher section |
| `render.yaml` | Render Blueprint (static site + cache/security headers) |
| `robots.txt` | Search-engine crawl rules |

Keep `index.html` and `dr_lokesh_professor_new.png` side by side — the HTML
references the photo as `./dr_lokesh_professor_new.png`.

## Run locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Open it through a server, not by double-clicking the file: YouTube refuses to
embed video on `file://` pages. (The player detects this and opens YouTube in a
new tab instead, but the in-page player only works over http/https.)

## Where the content lives

Everything you are likely to edit is in one place, at the top of the `<script>`
block:

```js
const MODULES = [ { id:1, title:"…", hours:8, co:"CO1", lectures:[ … ] }, … ];
const PLANNER = { multiplier: 3, perModuleBaseHours: [8,8,8,8,8], … };
```

| What | How |
| --- | --- |
| Add or fix a lecture | edit that lecture's `{code, topic, url}` in `MODULES` |
| Publish a pending lecture | fill its empty `url:""` — the **Coming soon** badge disappears by itself |
| Change planner maths | `PLANNER.multiplier` (3 = watch + notes + practise) |
| Change the featured video | the two `data-video-id` attributes, and the `/youtu.be/…` link beside the hero player |
| Anything else | search the HTML for `[Add` — those are deliberate placeholders |

## Current data

- 5 modules · **41 lectures** (M1–M3, M5 have 8 each; M4 has 9, because
  "Producers and consumers" is published in two parts, M4-L6A / M4-L6B)
- 40 lectures have a video; **M3-L7 (Performance evaluation of MPI programs)**
  has none yet and renders as *Coming soon*
- 8 hours per module · Scheme 2022 · 3 credits · CO1–CO5

## Deploy to Render

See `DEPLOY-RENDER.md` in the parent folder. In short — **static site**:

| Field | Value |
| --- | --- |
| Root Directory | *(empty)* |
| Build Command | *(empty)* |
| Publish Directory | `.` |

`render.yaml` is a Blueprint, not a publish directory. If Render says
`Publish directory 'render.yaml' does not exist`, that is the mistake — put
`.` in Publish Directory.

## Placeholders to fill before sharing widely

| Placeholder | Where | What to supply |
| --- | --- | --- |
| `[Add institution]` | teacher section, footer | college / university name |
| `[Add BCS702 repo URL]` | Resources → GitHub card | the Parallel Computing repo link |
| canonical / `og:url` | `<head>` | the real deployed URL — currently `https://video-lectures-parallel-computing.onrender.com/` as a guess |
