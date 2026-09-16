# DeFiLlama Scraper - API & cURL examples

Call the hosted Actor **[logiover/defillama-scraper](https://apify.com/logiover/defillama-scraper)** over the Apify REST API. Replace `YOUR_TOKEN` with your Apify API token.

## Run synchronously and get dataset items

```bash
curl -X POST \
  "https://api.apify.com/v2/acts/logiover~defillama-scraper/run-sync-get-dataset-items?token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"mode":"protocols","minTvl":1000000,"maxResults":500}'
```

## Yield pools on Ethereum

```bash
curl -X POST \
  "https://api.apify.com/v2/acts/logiover~defillama-scraper/run-sync-get-dataset-items?token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"mode":"yields","chainFilter":"Ethereum","maxResults":1000}'
```

## Stablecoins overview

```bash
curl -X POST \
  "https://api.apify.com/v2/acts/logiover~defillama-scraper/run-sync-get-dataset-items?token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"mode":"stablecoins"}'
```

## Get results as CSV

```bash
curl -X POST \
  "https://api.apify.com/v2/acts/logiover~defillama-scraper/run-sync-get-dataset-items?token=YOUR_TOKEN&format=csv" \
  -H "Content-Type: application/json" \
  -d '{"mode":"chains","minTvl":10000000}' \
  -o chains.csv
```

## Start an async run (large yields sweep)

```bash
curl -X POST \
  "https://api.apify.com/v2/acts/logiover~defillama-scraper/runs?token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"mode":"yields"}'
```

## Poll status, then fetch items

```bash
curl "https://api.apify.com/v2/actor-runs/RUN_ID?token=YOUR_TOKEN"
curl "https://api.apify.com/v2/datasets/DATASET_ID/items?token=YOUR_TOKEN&format=json"
```

See also: [cli.md](cli.md) · [javascript.md](javascript.md) · [python.md](python.md)
