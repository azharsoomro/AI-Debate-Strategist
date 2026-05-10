# Layer 5 — Final Strategy
**SCIPAB:** B (Benefit)

**Role given to the model:** "Senior debater synthesising both sides into a balanced verdict."

**Prompt-engineering technique:** Reflexion + LLM-as-judge self-grading; emits an observability bundle.

---

## System prompt

Combine Layers 2, 3, and 4 into a balanced final verdict.

1. Build a **verdict matrix**: criterion × era, with the era-winner per row.
2. Compose a **3-minute spoken brief** (~420 words).
3. Self-grade against the SCIPAB rubric, scoring each dimension 0–1.
4. Emit telemetry: `input_tokens`, `output_tokens`, `total_tokens`, `latency_ms`, `SCIPAB_score`, `self_consistency`.

## Output schema

```json
{
  "verdict_matrix": {"<criterion>": "1990s | 2020s"},
  "spoken_brief": "string",
  "cue_cards": ["string"],
  "scipab_scores": {"S": 0.0, "C": 0.0, "I": 0.0, "P": 0.0, "A": 0.0, "B": 0.0},
  "telemetry": {
    "input_tokens": 0,
    "output_tokens": 0,
    "total_tokens": 0,
    "latency_ms": 0,
    "SCIPAB_score": 0.0,
    "self_consistency": 0.0
  }
}
```

## Sample output

```
VERDICT MATRIX
  Melody              -> 1990s
  Lyricism            -> 1990s
  Vocal craft         -> 1990s
  Replay value        -> 1990s
  Production quality  -> 2020s
  Genre diversity     -> 2020s
  Cultural reach      -> 2020s
  Modern relevance    -> 2020s

SPOKEN BRIEF (excerpt)
"1990s gave Hindi cinema melodies that hold a wedding hall. 2020s took Hindi music
to the world - Naatu Naatu Oscar, Pasoori 300M+, Kesariya #1 Spotify Global India.
Verdict: 1990s win on craft, 2020s win on impact, the listener wins overall."

SCIPAB self-grade: 0.89  (post-optimization: 0.94)
```
