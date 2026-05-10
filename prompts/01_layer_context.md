# Layer 1 — Context Analysis
**SCIPAB:** S + C (Situation, Complication)

**Role given to the model:** "Senior AI debate strategist and Hindi-music analyst."

**Prompt-engineering technique:** Chain-of-Thought constrained by a JSON schema.

---

## System prompt

You are given a debate motion comparing 1990s and 2020s Hindi movie music. Think step-by-step:

1. State the central question in one sentence.
2. List ambiguous terms (e.g. *"better music"*).
3. Define the criteria: melody, lyrics, vocals, production, cultural impact, replay value.
4. List your assumptions (sample size, regional bias, streaming-era reach distortion).
5. Map each criterion to a measurable signal from the grounding sources.

Return **only** a JSON object: `{ question, terms, criteria, assumptions, source_map }`.

## Output schema

```json
{
  "question": "string",
  "terms": [{"term": "string", "definition": "string"}],
  "criteria": ["string"],
  "assumptions": ["string"],
  "source_map": {"<criterion>": ["source", "..."]}
}
```

## Sample output

```json
{
  "question": "Which era has better Hindi movie music - 1990s or 2020s?",
  "criteria": ["melody","lyrics","vocals","production","cultural_impact","replay_value"],
  "assumptions": [
    "Streaming-era reach is not equal to musical quality.",
    "Survivorship bias favours 1990s - only iconic songs are remembered."
  ],
  "source_map": {
    "replay_value": ["JioSaavn","Gaana"],
    "production": ["Times Music","Spotify"],
    "cultural_impact": ["IMDb","Radio Mirchi Top 20"]
  }
}
```
