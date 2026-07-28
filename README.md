# Abode Appeal — Broward County DIY MVP

An interactive prototype for a self-service ("DIY") property-tax appeal product, built for the Abode Money operations case study. A homeowner who already has an evidence package uses Abode to file their own Value Adjustment Board (VAB) petition in Broward County, Florida — with the exact deadline, copy-ready form answers, a hearing-ready evidence PDF, a personalized hearing script, and a clear boundary around what Abode does and does not do.

The entire product is a single, dependency-light HTML file. Open it and it runs.

## Run it

- **Fastest:** double-click `index.html` (or `abode-appeal-broward.html`) to open it in any modern browser.
- **GitHub Pages:** this repo is structured so `index.html` serves automatically. In the repo, go to **Settings → Pages → Deploy from branch → `main` / root**, and the live URL appears in a minute or two.

No build step, no install, no server. The evidence-package PDF uses jsPDF loaded from a CDN, so that one feature needs an internet connection; with no connection it falls back to a text file.

## What to look at

The app has two views, toggled top-right:

- **Homeowner** — the end-to-end journey: create an account, match a property (add more than one — each files as its own petition), confirm the DIY path, review a copy-ready worksheet, download the evidence PDF and the official DR-486, file through the county portal, capture the receipt, prepare for the hearing, and record the result.
- **Operator** — the case answers behind the product: why DIY, why Broward first, how it scales county-to-county and to 50 states, and the metrics that matter, plus verified sources.

An "Ask Abode" assistant (bottom-right) answers procedural questions from a fixed, source-tagged knowledge base and generates a hearing script from the user's own answers.

Use the **Reset demo** button (top-right) to wipe everything and return to the sign-up page for a fresh run.

## Design decisions worth noting

- **DIY is a distinct product, not thin full-service.** The homeowner remains the filer; Abode never signs, submits, pays, represents, or stores county credentials. Every exception (late filing, multi-parcel petitions, exemption/classification/portability, ownership mismatch) is routed to a human queue instead of improvised.
- **The county configuration is the scalable unit.** The common workflow is built once; per-county rules (deadline, fee, portal, allowed petition types, hearing rules, exception routing) live in a configuration record with a source list, a last-verified date, an owner, and a pause switch. Broward lowering its filing fee from \$25 to \$15 mid-research is the working example of why that record needs an owner and a verification date.
- **Metrics measure completion, not traffic.** Marketing already acquired the paid user; operations succeeds when an eligible customer files an accepted petition on time. The north-star is accepted, on-time petitions ÷ eligible paid DIY customers, verified by confirmation capture rather than a button click.

## Data & honesty notes

- All property and value data is **synthetic** — no live county parcels are queried.
- Passwords are never saved or transmitted in this demo; uploaded files (receipt, hearing notice) record only the file name.
- Records persist in the browser (`localStorage`) and export to CSV in place of a production database, which would write each event to an `appeals` table via API, keyed by account and property.
- County rules and portals change; the prototype displays a last-verified date (July 27, 2026) and links official-first sources.

Not legal, tax, or appraisal advice. This is an interview prototype.
