# Layer 3 — Counter Argument (defends 2020s)
**SCIPAB:** P (Position, opposing)

**Role given to the model:** "Adversarial debate strategist defending the 2020s side."

**Prompt-engineering technique:** ReAct loop with retrieval over JioSaavn / Spotify charts; explicit steel-man directive.

> ⚠ **Bottleneck layer.** This layer drives 38 % of total wall-clock and the highest hallucination risk. After applying the optimization, it is split into **L3a** (retrieval-only) and **L3b** (narration), with cached responses from the eight Indian music sites in Redis for 24 h.

---

## System prompt

Build the **strongest possible** 2020s case. Do **not** weaken it.

Cover:
1. Production quality — Dolby Atmos, AI-assisted mastering, global mixing engineers.
2. Genre diversity — hip-hop, indie, sufi-pop fusion, electro.
3. Streaming reach — *Naatu Naatu* (RRR, Oscar), *Pasoori* (300M+ streams), *Kesariya* (Brahmastra virality).
4. Modern relevance — short-form video, Reels, Spotify Wrapped behaviour.

Each claim **must** carry a `citation_id` from the grounding sources.

If the retrieval tool returns empty, write `"value": "unknown"` rather than guessing.

## Output schema

```json
{
  "thesis": "string",
  "reasons": [
    {"claim": "string", "warrant": "string", "evidence": "string", "citation_id": "string"}
  ],
  "citation_ids": ["string"]
}
```

## Sample output

```json
{
  "thesis": "2020s Hindi movie music is better - it overtakes the 1990s on production, genre, reach, and global recognition while preserving melodic skill.",
  "reasons": [
    {"claim": "Atmos / global mixing standards", "evidence": "Animal (2023), Pathaan (2023)", "citation_id": "TM-PROD-2023"},
    {"claim": "Naatu Naatu won Best Original Song, 95th Academy Awards (2023)", "citation_id": "SP-CHARTS-2023"}
  ]
}
```
