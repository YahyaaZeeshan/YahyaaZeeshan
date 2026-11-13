# PSX Signal Desk

A single-page app, published as a private Claude artifact, that scores liquid Pakistan Stock
Exchange stocks and shows the data behind every score.

- `index.html` is the whole app: markup, styles and script. It is published with the Artifact tool,
  which wraps it in a document skeleton, so the file has no `<html>`, `<head>` or `<body>` tags.

## What it does

- Buy / Sell / Watchlist switch over a grid of scored cards.
- A research note per stock: every input, its rank and weight, price chart, returns, dividends,
  reported accounts, recent headlines, and an optional AI analyst and broker-desk review.
- A watchlist with per-holding amounts and a projected value range from day 1 to day 20,000.

## Where the data comes from

All data is fetched in the viewer's browser through their Nimble connector:

| Data | Source |
| --- | --- |
| Daily closes, 1 year, all stocks | Yahoo Finance `v8/finance/spark` (tickers `SYMBOL.KA`, index `^KSE`) |
| Reported accounts | Yahoo Finance `fundamentals-timeseries` |
| 5-year weekly history, dividends | Yahoo Finance `v8/finance/chart` |
| Headlines | Nimble news search |

The PSX data portal (`dps.psx.com.pk`) is not used as a data source: it blocks automated access
from outside its region and its terms prohibit robots. The app only links to it.

Fetched data is cached in the artifact's database (`cache/*`, `fund/*`, `detail/*`); the watchlist
is stored per viewer under `data/users/<id>/watchlist`.

## Limits

The scores are model output from public data. They are not investment advice, no licensed analyst
or broker has reviewed them, and no model predicts share prices reliably. The stock list is
hand-picked and should be checked against current PSX listings.
