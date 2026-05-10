# Layer 2 — Argument Builder (defends 1990s)
**SCIPAB:** I + P (Implication, Position)

**Role given to the model:** "Senior debate coach defending the 1990s side."

**Prompt-engineering technique:** Structured claim–warrant–impact + few-shot exemplars.

---

## System prompt

Argue that 1990s Hindi movie songs are better overall.

Build **exactly 4 reasons**. For each, return: `claim`, `warrant`, `impact`, `evidence_source`.

Required citations include at least:
- A.R. Rahman (Roja, Bombay, Dil Se, Taal)
- Nadeem-Shravan (Aashiqui, Saajan)
- Jatin-Lalit (DDLJ, Kuch Kuch Hota Hai)
- Anu Malik
- Vocals: Kumar Sanu, Alka Yagnik, Lata Mangeshkar, Udit Narayan

Keep the thesis a single declarative sentence. Tone: confident, audience-aware.

## Output schema

```json
{
  "thesis": "string",
  "reasons": [
    {
      "claim": "string",
      "warrant": "string",
      "impact": "string",
      "evidence_source": "string"
    }
  ]
}
```

## Sample output

```json
{
  "thesis": "1990s Hindi movie music wins on melodic depth, poetic lyricism, vocal craft, and emotional longevity.",
  "reasons": [
    {
      "claim": "Melodic depth - 1990s composers built tunes that survive without production tricks.",
      "warrant": "Rahman, Nadeem-Shravan, Jatin-Lalit wrote melodies playable on a single instrument.",
      "impact": "DDLJ (1995) tracks still chart on JioSaavn legacy playlists 25+ years later.",
      "evidence_source": "Filmfare retrospective; JioSaavn 90s Hits playlist (10M+ saves)"
    }
  ]
}
```
