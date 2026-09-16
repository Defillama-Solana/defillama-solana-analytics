# DeFiLlama Scraper - Apify CLI examples

Client-side usage of the hosted Actor **[logiover/defillama-scraper](https://apify.com/logiover/defillama-scraper)** via the Apify CLI.

## Install & log in

```bash
npm install -g apify-cli
apify login   # paste your Apify API token
```

## All protocols by TVL (default, empty input)

```bash
apify call logiover/defillama-scraper
```

## Ethereum protocols above $1M TVL

```bash
apify call logiover/defillama-scraper --input '{
  "mode": "protocols",
  "chainFilter": "Ethereum",
  "minTvl": 1000000
}'
```

## Yield pools on Arbitrum

```bash
apify call logiover/defillama-scraper --input '{
  "mode": "yields",
  "chainFilter": "Arbitrum",
  "maxResults": 1000
}'
```

## Protocol detail (TVL history by slug)

```bash
apify call logiover/defillama-scraper --input '{
  "mode": "protocolDetail",
  "slugs": ["aave", "uniswap-v3", "curve-dex"]
}'
```

## Stablecoins market overview

```bash
apify call logiover/defillama-scraper --input '{ "mode": "stablecoins" }'
```

## Per-chain TVL

```bash
apify call logiover/defillama-scraper --input '{
  "mode": "chains",
  "minTvl": 10000000
}'
```

## Save output to a file

```bash
apify call logiover/defillama-scraper \
  --input '{"mode":"protocols","minTvl":5000000}' \
  --output-dataset > defi-protocols.json
```

See also: [api-curl.md](api-curl.md) · [javascript.md](javascript.md) · [python.md](python.md)
