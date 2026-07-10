# Ars Festum — Website

Static website for **Ars Festum · The Art of Celebration** — event design house, Palma de Mallorca.

No build step. Plain HTML, CSS and assets, served as-is. Fonts load from Google Fonts CDN.

## Structure

```
index.html            Home page
assets/               Images, wordmark, sketch data
  h/                  Hero montage
  gallery/            Gallery plates
  blooms/             Bloom / petal imagery
legal/                Legal notice, privacy, cookie policy
catalogue/            Downloadable catalogue PDF (see below)
llms.txt, robots.txt  Crawler files
vercel.json           Clean URLs + cache headers
```

## The catalogue PDF

The catalogue is a compressed (~40 MB) PDF. Drop the file in at:

```
catalogue/ars-festum-catalogue.pdf
```

The home page links to `/catalogue/ars-festum-catalogue.pdf`.

> **Note on size:** 40 MB commits fine to GitHub (limit is 100 MB) and serves from
> Vercel's CDN. If the catalogue grows or you add more large files, move them to
> **Vercel Blob** or an **R2/S3 bucket** and point the link at that URL instead — keep
> heavy binaries out of Git. Never commit the original uncompressed (~400 MB) file.

## Deploy — GitHub + Vercel

### 1. Push to GitHub
```bash
cd arsfestum-site
git init
git add .
git commit -m "Ars Festum website"
git branch -M main
git remote add origin https://github.com/ELIAANSR/Ars-Festum.git
git push -u origin main
```

### 2. Import to Vercel
1. Go to vercel.com → **Add New → Project** → import the repo.
2. Framework preset: **Other** (it's a static site — no build command, no output dir).
3. Deploy. Vercel serves the files directly and applies `vercel.json`.

### 3. Custom domain
In the Vercel project → **Settings → Domains** → add `arsfestum.com` and `www.arsfestum.com`,
then point your DNS at Vercel (A record `76.76.21.21` for the apex, or the CNAME Vercel shows).
The canonical URL and Open Graph tags in `index.html` already use `https://arsfestum.com/`.

## Local preview
Any static server works, e.g.:
```bash
npx serve .
```
