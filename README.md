# Vriezenveen Woningmarkt — Data Journalism Project

An interactive data journalism visualization of housing, demographics, and affordability for Vriezenveen / Twenterand (Overijssel, NL). Published as a static site on Cloudflare Pages.

## Live site

**https://vjenne.pages.dev** (Cloudflare Pages, auto-deployed from `main`)

- `/` — scrollytelling article with 17 charts (home page)
- `/kaart` → redirects to `/map.html` — interactive MapLibre map
- `/analyse` → redirects to `/index.html`

## What's in it

### `index.html` — Article (home page)
15 sections covering:
- Regional price history 1995–2035 (actual + CBS/PBL prognosis)
- Neighbour municipality price comparison (Almelo, Wierden, Hellendoorn, Tubbergen)
- Housing tenure breakdown (koop / corporatiehuur / vrije huur)
- Household composition trends
- Affordability: income vs. mortgage capacity vs. prices
- 4-persona stories (starter, gezin, gepensioneerd, arbeidsmigrant)
- New build plans and 8-party political positions (GR2026)
- Migration flows (10 arc routes, origin fixed to Vriezenveen)
- WOZ-value development
- Income distribution by quintile
- 2026–2035 prognosis (CBS PBL mid-scenario: +3%/yr prices, +3.5%/yr income)

### `map.html` — Interactive map
- 6,683 BAG building dots from PDOK/Kadaster
- Color-coded by bouwjaar (construction year)
- Hover tooltips with address and year
- MapLibre GL JS (CDN)

## Data sources

| Dataset | Source | File |
|---|---|---|
| House prices 2003–2024 | CBS Statline | `data/cbs/twenterand_tijdreeks_2003_2025.csv` |
| Neighbour municipality prices | Kadaster/CBS | `data/cbs/verkoopprijzen_alle_regioos_raw.json` |
| Building addresses (BAG) | PDOK / Kadaster | `data/kadaster/adressen_compact.js` |
| Migration flows | CBS | `data/cbs/verhuizingen_twenterand.json` |
| Prognosis 2026–2035 | CBS PBL mid-scenario | Embedded in `index.html` |
| News corpus | RTV Oost, Tubantia | `data/news/` (30 articles) |

## News corpus (`data/news/`)

30 archived articles (2021–2026) covering:

- **Woningbouw** — nieuwbouwprojecten, bestemmingsplannen, bezwaarprocedures
- **Sociale huur** — Mijande Wonen, ontruimingen, Oale Bouw vervanging Westerhaar
- **Betaalbaarheid** — starters, woonlasten, OZB, ravijnjaar 2026
- **Vluchtelingen & arbeidsmigranten** — Oekraïense opvang, statushouders, registratieproblematiek
- **Kanaaldrama** — woningschade langs Kanaal Almelo-De Haandrik, provincie Overijssel
- **Bestuur** — wethouder vertrek, burgemeester Broekhuizen, GR2026 lijsttrekkers
- **Leefbaarheid** — schoolsluitingen, pur-huizen, buurtconflicten

## Tech stack

- **Vanilla HTML/CSS/JS** — no build tooling, no framework, no npm install needed
- **[MapLibre GL JS](https://maplibre.org/)** — interactive map (CDN)
- **[Chart.js](https://www.chartjs.org/)** — all charts (CDN)
- **Google Fonts** — Playfair Display, JetBrains Mono (CDN)
- **Cloudflare Pages** — static hosting, no build step

## Design

NYT dark editorial aesthetic:
- Background `#08080e`
- Playfair Display serif for headings
- JetBrains Mono for data labels and numbers
- Accent `#e8c96d` (gold)

## Run locally

```bash
npm run dev
# or
python3 -m http.server 8765
```

Then open `http://localhost:8765`

## Deploy

Connected to Cloudflare Pages (`vjenne` project). Every push to `main` triggers a deploy.

- **Build command:** none (static files)
- **Output directory:** `.` (root)
- **Config:** `wrangler.toml`, `_headers`, `_redirects`

Manual deploy:
```bash
npx wrangler pages deploy . --project-name vjenne
```

## Prognosis methodology

Prices 2026–2035: CBS PBL mid-scenario, +3%/yr compound from 2025 baseline.  
Income 2026–2035: +3.5%/yr compound from 2025 median (CBS loonontwikkeling mid).  
Mortgage capacity calculated at 4.5% 30-year annuity, 4× gross annual income NHG limit.

## Repository

`github.com/leanderrj/vjenne` — branch `main`
