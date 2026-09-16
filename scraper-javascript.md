# DeFiLlama Scraper - JavaScript (apify-client) examples

Call the hosted Actor **[logiover/defillama-scraper](https://apify.com/logiover/defillama-scraper)** from Node.js with the official [`apify-client`](https://www.npmjs.com/package/apify-client).

## Install

```bash
npm install apify-client
```

## All protocols, sorted by TVL

```js
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_TOKEN' });

const run = await client.actor('logiover/defillama-scraper').call({
  mode: 'protocols',
  minTvl: 1000000,
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.sort((a, b) => (b.tvl ?? 0) - (a.tvl ?? 0));
console.table(items.slice(0, 10).map((p) => ({ name: p.name, tvl: p.tvl, category: p.category })));
```

## Top yield pools above 10% APY on Arbitrum

```js
const run = await client.actor('logiover/defillama-scraper').call({
  mode: 'yields',
  chainFilter: 'Arbitrum',
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
const highApy = items
  .filter((p) => (p.apy ?? 0) >= 10)
  .sort((a, b) => b.apy - a.apy);
console.log(`${highApy.length} pools ≥ 10% APY`);
```

## Stablecoin supply change vs. previous day

```js
const run = await client.actor('logiover/defillama-scraper').call({ mode: 'stablecoins' });
const { items } = await client.dataset(run.defaultDatasetId).listItems();
for (const s of items) {
  const delta = (s.circulating ?? 0) - (s.circulatingPrevDay ?? 0);
  console.log(s.name, s.pegType, 'Δ', delta.toFixed(0));
}
```

## Export to CSV buffer

```js
import { writeFileSync } from 'node:fs';
const csv = await client.dataset(run.defaultDatasetId).downloadItems('csv');
writeFileSync('defillama.csv', csv);
```

See also: [cli.md](cli.md) · [api-curl.md](api-curl.md) · [python.md](python.md)
