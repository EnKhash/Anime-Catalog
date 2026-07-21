# Mabel's Anime Library — Custom Catalog Addon

Full anime catalog for Nuvio, built from scratch, backed by Kitsu's public API (no account/login needed).
Outputs `kitsu:{id}` IDs so it plugs directly into your existing AIOStreams HTTP + P2P instances —
no ID mismatch, no dead third-party backend.

## What it gives you
- Trending Anime
- Popular Anime
- Top Rated Anime
- Airing Now
- Anime Movies (separate catalog, correctly typed)
- Search across all of the above

## Deploy — Option A: Vercel (simplest, ~2 minutes)

1. Go to https://vercel.com → sign up/log in (GitHub login is easiest)
2. Click **Add New → Project**
3. Choose **Deploy without Git** → drag the whole `anime-catalog-addon` folder in
   (or push it to a new GitHub repo first, then import that repo — either works)
4. Leave build settings as default — `vercel.json` handles it
5. Click **Deploy**
6. Once live, your manifest URL is:
   `https://<your-project-name>.vercel.app/manifest.json`
7. Paste that into Nuvio → Addons → Add Addon

## Deploy — Option B: Railway (you already know this from Dizipal)

1. Go to https://railway.app → New Project → Deploy from GitHub repo
   (push this folder to a new GitHub repo first)
2. Railway auto-detects Node.js and runs `npm install && npm start`
3. Once deployed, go to Settings → Networking → **Generate Domain**
4. Your manifest URL:
   `https://<your-railway-domain>/manifest.json`
5. Paste into Nuvio → Addons → Add Addon

## Important — test before trusting it

This was built and syntax-checked locally, but **not tested against a live network call**
(no internet access in the build environment). Two things to verify once deployed:

1. Open `https://<your-domain>/manifest.json` in a browser first — should return JSON,
   not an error page.
2. Open `https://<your-domain>/catalog/series/kitsu-trending.json` — should return a
   `metas` array with real anime entries and poster URLs. If this is empty or errors,
   send me the response and I'll debug it.

## Why kitsu: IDs specifically

Your AIOStreams HTTP and P2P manifests both declare `kitsu` and `kitsu:` in their
`idPrefixes`. That means once this catalog shows a title and you tap it, AIOStreams
will actually know how to look up streams for it — unlike Anime Catalogs (baby-beamup)
which is dead, or AniSync which needs a MAL/AniList login you don't have.

## Extending this later (not built yet, easy to add if you want)

- RPDB ratings-on-poster overlay (you already have a free key)
- Genre filtering
- Seasonal catalog (current anime season specifically)
- Dub-only filter
