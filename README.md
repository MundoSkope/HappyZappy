# HappyZappy Explorer

An interactive companion web app for the paper *Quality of Life Adjusted GDP per
Capita: Methodology, Web App, and Impact on Happiness* (Marcus [Marktanner]).

It prices **happiness zappers** — costs no household chose to pay (conflict,
pollution, disease, forced saving against risk) — in dollars per person, so
they sit next to GDP on equal terms, and lets a reader explore which zappers
hit which countries hardest, how that reshapes GDP-per-capita rankings, and
how zappers have moved over time.

## Live app

Static site, no build step: `index.html` + two data files (`data.json`,
`world-topo.json`), all loaded via relative `fetch()`. Deploying to Netlify
needs no configuration beyond pointing it at this repo — `netlify.toml` sets
the publish directory to the repo root.

## What's in this repo

- `index.html` — the whole app (HTML/CSS/JS). Charts/map use D3, topojson,
  and Chart.js from CDN; no local build tooling required.
- `data.json` — the country-year zapper panel (2011–2025, 153 countries,
  unbalanced), plus pre-aggregated World/region averages.
- `world-topo.json` — TopoJSON world map (country boundaries) for the map view.
- `netlify.toml` — zero-config static-site deploy settings.

## Zapper methodology, in brief

Each zapper is priced one of three ways:

- **Direct** — actual spending or observed damage (e.g. military expenditure,
  disaster-reconstruction cost, out-of-pocket health spending).
- **Life-years-reducing** — mortality/morbidity burden priced via the Value
  of a Statistical Life (e.g. conflict deaths, air pollution, malnutrition).
- **Implicit** — estimated from life-satisfaction regressions (inflation,
  unemployment, the GNI–GDP gap); shown for context, not summed into the
  priced total.

Two adjusted measures, not one, depending on which zappers are cumulated:

- **Resource-adjusted GDP** = GDP − direct costs only. A same-economy
  counterfactual: that spending could mechanically have gone elsewhere.
- **Welfare-equivalent income** = GDP − direct costs − life-years-reducing
  costs. A welfare measure (VSL-priced), not a claim about a bigger or
  smaller economy.

Full methodology detail (data sources, construction of each zapper field,
inclusion/exclusion decisions) belongs in this repo as it's written up —
see the paper for the current canonical description in the meantime.

## Status

Web app in active development; this repo currently holds the deployable
app only. Methodology notes and the replication pipeline (raw data →
`data.json`) to follow.
