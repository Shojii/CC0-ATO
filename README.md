# ATO — *Permanent Loading*

An interactive installation piece. A single ever-growing diagram: every visitor
inherits what came before, adds up to three points, and each point is fixed to
the archive by exactly three lines of triangulation. Nothing can be erased.

Rotate with the mouse wheel held down (or a right-drag, or a touch drag), zoom
with the wheel, and open **Settings** in the corner to tune rotation speed, 3D
depth, mouse inertia, placement depth, and how fast old traces fade.

Old traces lose opacity as the archive grows, but never fall below 5% — they
recede, they never leave.

## Contents

| File | |
| --- | --- |
| `index.html` | The entire piece. One self-contained file: no build step, no dependencies, no bundler. |
| `og.png` | Social preview image. |

The only external request is Google Fonts (Fraunces, Archivo, Space Mono).
Everything else — the 3D engine, the triangulation, the rendering — is vanilla
JS on a 2D canvas.

## Put it on GitHub

```bash
cd living-archive-site
git init
git add .
git commit -m "Living Archive"
git branch -M main
git remote add origin git@github.com:<you>/living-archive.git
git push -u origin main
```

## Put it on Vercel

**From the dashboard** — the path with nothing to configure:

1. vercel.com → **Add New… → Project** → import the GitHub repo.
2. Framework preset: **Other**. Leave build command and output directory empty.
3. **Deploy.**

Vercel serves `index.html` from the repository root as-is. There is no build
step to get wrong, and every later `git push` to `main` redeploys.

**Or from the CLI:**

```bash
npm i -g vercel
vercel          # preview URL
vercel --prod   # production
```

## One thing to know before it goes public

Traces are stored in the visitor's own browser (`localStorage`), which was the
right call for a prototype and is still the right call for an installation
running on one screen: that screen accumulates every visitor's contribution,
and it survives a refresh or a reboot.

On a public URL it means something different. Each visitor gets their *own*
private archive, seeded from the same genesis diagram — two people opening the
link never see each other's points. If the piece needs to be genuinely
collective across visitors, it needs somewhere shared to write to: a small
Vercel Function plus a hosted store (Vercel KV, Postgres, Supabase) holding the
list of contributions, with the page fetching it on load and posting to it on
confirm. That is a real change, not a config flag — worth deciding before the
link goes out.

## Licence

CC0 — as the piece says in its own corner.
