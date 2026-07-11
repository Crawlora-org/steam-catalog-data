# Steam Catalog Dataset — State of Steam 2026

Open aggregate data behind [**The State of Steam 2026**](https://crawlora.net/blog/state-of-steam-2026),
a study of the **top 10,000 Steam games by owner estimate**. Every field is a public storefront /
third-party-estimate fact — no personal data.

Built by [Crawlora](https://crawlora.net) by dogfooding its own APIs: the game universe is seeded from
SteamSpy's owner-ranked `all` pages and enriched with the public Steam storefront (`appdetails`). The full
dataset is queryable live at `https://api.crawlora.net/api/v1/datasets/steam-games/search` (and via the
`datasets_steam_games_*` MCP tools).

## What's inside

| File | Description |
|---|---|
| `data/summary.json` | The full aggregate rollups behind the study — pricing by year, review-tier & price-tier distributions, top genres, ownership concentration (Pareto), platform-support trends by year, review sentiment by genre. |
| `data/sample.jsonl` | 200 sample game records (top by owner estimate), one JSON object per line — the shape of the queryable dataset. |
| `data/pricing-by-year.csv` | Titles, free-to-play share, median/mean paid price by release year (2006–2026). |
| `data/platform-by-year.csv` | Native Linux and Mac support share by release year. |
| `data/review-tiers.csv` | Games per Steam review tier (Overwhelmingly Positive … Very Negative). |
| `data/genres.csv` | Games carrying each Steam genre tag (multi-tag; shares add past 100%). |
| `data/categories.csv` | Games carrying each Steam category (Family Sharing, Single-player, …). |
| `data/price-tiers.csv` | Games per list-price tier (free, under $5, … $30+). |
| `data/release-years.csv` | Games per release year. |
| `data/review-by-genre.csv` | Titles, median review score, free share per genre. |
| `data/ownership-concentration.csv` | Owner share held by the top 1/5/10/25% of games. |

The CSVs are flat cuts of the same rollups in `data/summary.json` — pick JSON for programmatic use,
CSVs for a quick load into a spreadsheet or `pandas.read_csv`.

### Sample record fields

`appid`, `name`, `developer`, `publisher`, `is_free`, `price_cents`, `initial_price_cents`, `discount_pct`,
`price_tier`, `owners_min`/`owners_max`/`owners_midpoint` (SteamSpy estimate range), `owners_bucket`, `ccu`
(peak concurrent), `positive`/`negative`/`total_reviews`, `review_score`, `review_tier` (Steam's
volume-gated bands), `average_forever_min`/`median_forever_min` (playtime), `genres`, `categories`,
`metacritic`, `recommendations`, `required_age`, `release_date`/`release_year`, `coming_soon`,
`platform_windows`/`platform_mac`/`platform_linux`, `language_count`.

## Headline findings

- **Ownership is wildly concentrated.** The top 1% of games hold ~33% of all estimated owners, the top 10%
  hold ~65%, the top 25% hold ~81% — of ≈9.2 billion estimated owner-copies.
- **New-game prices are climbing and free-to-play is retreating.** Median paid new-game price rose from
  $4.99 (2012–2016) to $9.99 (2024); free-to-play's share of new releases peaked ~32% (2019–2020) and fell
  to ~8% (2024). *(2025–2026 have small samples and are caveated in the study.)*
- **Mac and Linux support is collapsing despite the Steam Deck.** Among top games, native Linux support fell
  from ~44% (2013) to ~11% (2024) and Mac from ~51% to ~20% — Proton makes native builds unnecessary.
- **Top games skew overwhelmingly positive.** ~73% land in a positive review tier, only ~2% negative.
- **Indie dominates.** ~59% of top games carry the Indie tag.

## Methodology & caveats

- **Universe:** the top 10,000 games by SteamSpy owner estimate (of ~10,900 tracked at capture). The head of
  Steam, not the full ~90k+ long tail.
- **Owner counts are SteamSpy public *estimates* (ranges), not exact sales.** We keep min/max/midpoint;
  concentration figures use midpoints.
- **`review_tier`** follows Steam's own volume-gated algorithm ("Very Positive" needs 50+ reviews,
  "Overwhelmingly" 500+), so it matches the store label rather than raw ratio.
- Recent release years (2025–2026) have small samples; the robust price/platform trends run 2012→2024.
- Snapshot date: 2026-07-11.

## License

[**CC BY 4.0**](LICENSE) — free to use with attribution. Cite as:

> Crawlora (2026). *Steam Catalog Dataset — State of Steam 2026.* https://github.com/Crawlora-org/steam-catalog-data

See [`CITATION.cff`](CITATION.cff).
