# Photo Vibe Matcher

A client-side photo color-grading tool. Upload a photo, upload a reference whose look you want to match, click a button. Everything runs in the browser — no uploads, no accounts, no server.

## What's in this folder

- `index.html` — the whole app in one file (~31 KB).
- `README.md` — this file.

## How it works (briefly)

1. Converts both images to CIE Lab color space.
2. Builds a luminance histogram match LUT so the source's exposure curve adopts the reference's contrast shape.
3. Computes Gaussian-weighted chroma statistics for shadows, midtones, and highlights separately, then transfers those per tier so the source picks up the reference's split-toning (e.g. teal shadows + orange highlights).
4. Post-correction: shifts mean luminance back to the source's to prevent over/under-exposure, applies a soft highlight knee and shadow lift.
5. Reads EXIF orientation so iPhone portraits don't appear sideways.
6. Lazy-loads `heic2any` from a CDN only if a HEIC file is dropped.

## Deploying to GitHub Pages

There are two common setups. Pick whichever matches your existing repo.

### Option A — `yourname.github.io` user site

If you have a repo named `yourname.github.io`, drop `index.html` at the repo root and push. Your site is already live at `https://yourname.github.io/`.

```bash
cp index.html /path/to/yourname.github.io/
cd /path/to/yourname.github.io/
git add index.html
git commit -m "Add Photo Vibe Matcher"
git push
```

### Option B — a project repo

If it's a regular repo, you can serve it from the `main` branch. In the repo settings: **Settings → Pages → Source: Deploy from a branch → Branch: `main` → `/` (root) → Save**.

```bash
cp index.html /path/to/your-repo/
cd /path/to/your-repo/
git add index.html
git commit -m "Add Photo Vibe Matcher"
git push
```

It'll be live at `https://yourname.github.io/your-repo/` within about a minute.

If you'd rather serve from a subfolder, put `index.html` in `docs/` and point Pages at the `docs/` folder in settings. That's a good pattern if the repo has other things in it.

### Custom path (optional)

If you want it at something like `yourname.github.io/vibe/` without cluttering the repo root, create a `vibe/` folder, drop `index.html` there, and point Pages at the branch root. The URL becomes `yourname.github.io/your-repo/vibe/`.

## Testing locally before deploying

GitHub Pages serves over `https://`, but opening this file over `file://` also works — CORS restrictions don't affect it because all images are user-supplied and loaded via blob URLs. You can just double-click `index.html` to verify the deploy version works as expected.

## Updating copy / branding

- Page title and Open Graph preview: search for `<title>` and the `og:` meta tags near the top of `index.html`.
- The app title and intro paragraph are in the `<header>` section.
- Favicon is an inline SVG data URL on the `<link rel="icon">` line — edit the SVG directly or replace with a `favicon.png` file.
