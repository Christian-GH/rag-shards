# Distributed RAG (Filesystem Shards)

## Quick start (host mode)
```bash
bash ./run_local.sh
curl -s http://127.0.0.1:8001/health
curl -s "http://127.0.0.1:9000/search?q=cap%20theorem" | python -m json.tool
```

## Experiments
```bash
python experiments/run_load.py "what is consensus?" 100
python experiments/plot_results.py
```
- Slow shard (EU +500ms): restart EU with `LATENCY_MS=500` and re‑run the two commands above.
- Failure (APAC down): `kill $(lsof -ti:8003)` and re‑run.

## Notes
- MiniLM embeddings; FAISS if available, otherwise sklearn cosine.
- Shard folders: `data/us`, `data/eu`, `data/apac`.
- Env knobs: per‑shard `LATENCY_MS`; router `TOPK_PER_SHARD`, `TOPK_FINAL`.
