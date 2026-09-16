# DeFiLlama Scraper - Python (apify-client) examples

Call the hosted Actor **[logiover/defillama-scraper](https://apify.com/logiover/defillama-scraper)** from Python with the official [`apify-client`](https://pypi.org/project/apify-client/).

## Install

```bash
pip install apify-client
```

## All protocols into a pandas DataFrame

```python
import pandas as pd
from apify_client import ApifyClient

client = ApifyClient("YOUR_TOKEN")

run = client.actor("logiover/defillama-scraper").call(run_input={
    "mode": "protocols",
    "minTvl": 1000000,
})

items = list(client.dataset(run["defaultDatasetId"]).iterate_items())
df = pd.DataFrame(items)

# Top 10 protocols by TVL
print(df.sort_values("tvl", ascending=False)[["name", "tvl", "category", "chain"]].head(10))

# TVL by category
print(df.groupby("category")["tvl"].sum().sort_values(ascending=False))
```

## High-APY yield pools

```python
run = client.actor("logiover/defillama-scraper").call(run_input={
    "mode": "yields",
    "chainFilter": "Ethereum",
})
items = list(client.dataset(run["defaultDatasetId"]).iterate_items())
high = [p for p in items if (p.get("apy") or 0) >= 10]
high.sort(key=lambda p: p["apy"], reverse=True)
for p in high[:20]:
    print(p["project"], p["name"], f'{p["apy"]:.2f}%')
```

## Stablecoin monitoring

```python
run = client.actor("logiover/defillama-scraper").call(run_input={"mode": "stablecoins"})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    delta = (item.get("circulating") or 0) - (item.get("circulatingPrevDay") or 0)
    print(item["name"], item.get("pegType"), "price", item.get("price"), "delta", round(delta))
```

## Export the dataset to CSV

```python
with open("defillama.csv", "wb") as f:
    f.write(client.dataset(run["defaultDatasetId"]).download_items(item_format="csv"))
```

See also: [cli.md](cli.md) · [api-curl.md](api-curl.md) · [javascript.md](javascript.md)
