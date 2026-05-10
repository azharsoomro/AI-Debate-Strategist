# Layer 4 — Self-Critique
**SCIPAB:** A (Action — stress-test)

**Role given to the model:** "Red-team analyst attacking Layer 2's case."

**Prompt-engineering technique:** Reflexion loop with an explicit bias-naming directive.

---

## System prompt

Critique the 1990s-first argument from Layer 2:

- Identify **nostalgia bias** and **survivorship bias**.
- Surface missing dimensions: indie scene (Prateek Kuhad, Ritviz), short-form video virality (Reels, YouTube Shorts), Spotify Wrapped behaviour, Gen-Z listening habits, evolving production tooling.
- Flag any unfair comparisons (e.g. comparing chart-toppers of the 1990s with mid-tier 2020s tracks).

Return a weakness ledger with **at least 4 entries** and a recommended fix per entry.

## Output schema

```json
{
  "weaknesses": [
    {"name": "string", "severity": "low|medium|high", "fix": "string"}
  ],
  "unfair_assumptions": ["string"]
}
```

## Sample output

```json
{
  "weaknesses": [
    {"name": "Nostalgia bias",         "severity": "high",   "fix": "compare like-for-like chart-toppers"},
    {"name": "Survivorship bias",      "severity": "high",   "fix": "sample full decade catalogues"},
    {"name": "Indie scene ignored",    "severity": "medium", "fix": "add non-film tier (Kuhad, Ritviz)"},
    {"name": "Reels criterion missing","severity": "medium", "fix": "add short-form virality dimension"}
  ],
  "unfair_assumptions": [
    "Lyrical density framed as a 1990s-only strength - Amitabh Bhattacharya / Varun Grover ignored.",
    "Vocal craft framed as live-only - modern multi-mic capture is also high fidelity."
  ]
}
```
