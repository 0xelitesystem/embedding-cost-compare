# embedding-cost-estimator

Estimate embedding costs across 11 providers before you commit to a RAG strategy.

**Live demo:** https://0xelitesystem.github.io/embedding-cost-estimator/

Browser-only, single HTML file. No API calls, no telemetry, no upload.

## What it does

Plug in:
- Number of documents in your corpus
- Average tokens per document
- Re-embed frequency (one-time, quarterly, monthly, weekly, daily)
- Search query volume per month

Get a sorted cost matrix showing:
- Per-1M-token rate
- Backfill cost (one full pass)
- Total annual cost
- Cheapest vs most expensive multiplier

## Providers covered

| Provider | Models included |
|---|---|
| OpenAI | text-embedding-3-small, text-embedding-3-large |
| Voyage | voyage-3, voyage-3-large |
| Cohere | embed-english-v3, embed-multilingual-v3 |
| Jina | jina-embeddings-v3 |
| Mistral | mistral-embed |
| Google | text-embedding-004 |
| BGE | M3 (self-hosted, $0 token cost) |
| Nomic | Embed v1.5 (self-hosted, $0 token cost) |

Self-hosted entries show $0 token cost. Add your own GPU/inference cost on top to compare apples to apples.

## Use

1. Enter the number of documents and the average tokens per document.
2. Pick a re-embed frequency: one-time, quarterly, monthly, weekly or daily.
3. Enter search queries per month and the average tokens per query.
4. Read the cost matrix, sorted by cost. It updates as you type.

## Why this exists

Picking an embedding provider for RAG is a decision you make once and pay for forever. Pricing is fragmented across docs, dimensions vary, and re-indexing costs can dominate query costs depending on how often your corpus changes. Most cost comparison content online is stale within a quarter.

This estimator is a single static file so it loads instantly, runs locally, and the math is auditable in the source.

## Caveats

- Prices are based on each provider's published documentation as of model launch. Verify current rates before commitment for procurement.
- Self-hosted estimates exclude infrastructure cost. A 7B-param embedding model on a single A10G is roughly $0.50/hour; estimate your throughput separately.
- This compares cost only. Recall quality differences between models matter and aren't captured here. Run your own eval on a representative sample before committing.

## Use cases

- Scoping a RAG project: "is this affordable at our corpus size?"
- Provider switch analysis: "what would we save moving from X to Y?"
- Architecture review: "is daily re-embedding the right cadence?"

## Privacy

Everything runs in your browser. The numbers you enter stay on your machine; the page makes no API calls and no network requests, and the prices are embedded in the file. If you use the theme toggle, your light or dark choice is saved in your browser's localStorage under the key `theme`. Nothing you paste or type is stored.

## Run locally

```
git clone https://github.com/0xelitesystem/embedding-cost-estimator
cd embedding-cost-estimator
```

Open `index.html` in a browser. Or serve the folder with `python -m http.server` and visit http://localhost:8000.

## Build

No build. Open `index.html` in a browser, or deploy via GitHub Pages.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT.

## Related

- [llm-pricing-data](https://github.com/0xelitesystem/llm-pricing-data): inference cost data
- [prompt-cost-calculator](https://github.com/0xelitesystem/prompt-cost-calculator): per-call cost estimator
- [rag-chunk-visualizer](https://github.com/0xelitesystem/rag-chunk-visualizer): visualize chunking strategies
- [rag-evaluation-rubrics](https://github.com/0xelitesystem/rag-evaluation-rubrics): how to measure RAG quality
