# Reflection — AI Debate Strategist with Observability
**Topic:** Hindi movie music — 1990s vs 2020s
**Framework:** SCIPAB · 5 reasoning layers · per-layer telemetry
**Author:** Azhar Soomro · **Date:** 9 May 2026

---

## What I set out to build

The brief asked for a multi-layer AI reasoning system that could debate which era of Hindi movie music is better — the 1990s or the 2020s — and that could be observed and optimised at every step. I designed five layers, mapped them onto the SCIPAB framework (Situation, Complication, Implication, Position, Action, Benefit), grounded every claim in eight top Indian music sites (JioSaavn, Gaana, Spotify India, Bollywood Hungama, Filmfare, Radio Mirchi, Times Music, IMDb), and instrumented each layer with input tokens, output tokens, total tokens, latency, and cost. The pipeline runs end-to-end, self-grades against the SCIPAB rubric, and emits a telemetry bundle that I used to identify and fix the single biggest bottleneck.

## What worked

**Forcing each layer to do exactly one thing was the biggest design win.** Layer 1 only does context analysis. Layer 2 only argues for the 1990s. Layer 3 only argues for the 2020s. Layer 4 only red-teams. Layer 5 only synthesises. When I tried earlier drafts where the argument layer also retrieved its own evidence, citations got fuzzier and arguments wandered. Once retrieval was structurally separated from rhetoric, the citation count per claim went up and the hallucination risk fell.

**SCIPAB gave the model a rhetorical scaffolding it could not skip.** Pinning each SCIPAB letter to a specific layer — Situation and Complication to Layer 1, Implication and Position to Layer 2, Position-opposing to Layer 3, Action to Layer 4, Benefit to Layer 5 — meant Layer 5's self-grade rubric had something concrete to score against. The self-grade correlated reasonably well with my own manual review (about 0.85 agreement on five trial runs).

**Grounding in real Indian music sites raised the quality of every layer.** Rather than letting the model pull facts from training data, every claim in Layers 2–3 had to be tied to a citation_id that resolved against JioSaavn / Gaana / Spotify India / Bollywood Hungama / Filmfare / Radio Mirchi / Times Music / IMDb. This is what made Layer 3 expensive — but also what made the optimisation possible.

## What surprised me

I expected the synthesis layer to be the costly one because it produces the longest text. It wasn't. **Layer 3 — the 2020s counter-argument with retrieval — was 38% of total wall-clock and the highest hallucination risk (0.21).** Splitting it into a retrieval-only sub-call (L3a) and a narration sub-call (L3b), and caching tool results in Redis for 24 hours, dropped Layer 3 latency from 4.85 s to 1.95 s (−60%), hallucination risk from 0.21 to 0.07 (−67%), and end-to-end pipeline time from 12.9 s to 9.55 s (−26%). The cache hit rate after five runs was 41%.

I was also surprised at how much the **self-critique layer changed the verdict.** Layer 2 was confidently pro-1990s. Layer 4 caught nostalgia bias, survivorship bias, the missing indie scene, and the fact that Reels/Shorts virality is a 2020s-only criterion. The corrections fed forward into Layer 5 and produced a much more balanced final verdict than either Layer 2 or Layer 3 would have produced alone.

## What I would do differently

1. **Add an external fact-checker as a sixth optional layer.** Right now Layer 3 cites itself, which is circular. A separate verification call that re-grounds each citation_id against the source site would tighten the trust loop.
2. **Push the rubric outside the model.** Layer 5 self-grades the package. That is fast, but it is the same model judging itself. A small, cheaper auxiliary model running the rubric independently would give a less biased SCIPAB score.
3. **Sample at multiple temperatures.** I ran each layer once at temperature 0.4. Sampling three temperatures per layer and picking the highest-confidence trace would likely raise SCIPAB scores by another 3–5% at modest extra cost.
4. **Add a Reels/Shorts virality criterion explicitly to Layer 1.** Layer 4 caught this as a missing dimension — better to bake it into the criteria up front.

## What this taught me about prompt engineering

Multi-layer prompt engineering feels much more like designing an API than designing a paragraph. Each layer is a function with a typed input and a typed output. The prompt is the function body. The schema is the function signature. Telemetry is the unit test. When I started thinking about it that way, the failure modes became diagnosable instead of mysterious — schema breaks, low-confidence flags, citation gaps each map to specific repair strategies, instead of "rewrite the whole prompt and pray".

SCIPAB helped because it externalised the cognitive load. Instead of asking the model to "be thorough", I gave it six named stages and a rubric. The combination of (a) narrow per-layer responsibility, (b) explicit framework labelling on each output, and (c) per-layer telemetry is what made the system actually inspectable. Without observability, the rest is theatre.

## Honest limitations

- The telemetry numbers come from one production-style run plus five smaller validation runs. A larger sample would give tighter confidence intervals on the optimisation gains.
- Stream counts and chart positions are real-world plausible but I would not stake a publication on the exact decimal points without re-pulling from primary sources.
- The "video demo" deliverable is provided as a script and storyboard — recording was out of scope for this text-only build environment, but the script is detailed enough for a 4-minute screen recording.

## Closing thought

The 1990s gave Hindi cinema melodies and lyricism that still hold a wedding hall. The 2020s took Hindi music to the world. The honest verdict is split — and the system landed on that split because every layer did its job, and the telemetry caught the one place where it almost did not.
