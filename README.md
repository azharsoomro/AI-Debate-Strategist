# AI Debate Strategist with Observability
### Hindi Movie Music — 1990s vs 2020s &nbsp;·&nbsp; SCIPAB framework &nbsp;·&nbsp; 5 reasoning layers

A multi-layer reasoning system that debates whether 1990s Hindi movie music is better than 2020s music. The pipeline anchors every step in the **SCIPAB** rhetorical framework, grounds claims in eight top Indian music sites (JioSaavn, Gaana, Spotify India, Bollywood Hungama, Filmfare, Radio Mirchi, Times Music, IMDb), emits per-layer telemetry, and ships with one telemetry-driven optimization that cut Layer 3 latency by 60% and hallucination risk by 67%.


## 🔬 SCIPAB → Layer mapping

| Letter | Stage | What it forces the system to do | Layer |
|:-:|---|---|:-:|
| **S** | Situation | Frame the era comparison (charts, streams, criticism) | L1 |
| **C** | Complication | Surface the tension: nostalgia vs reach | L1 |
| **I** | Implication | State what is at stake | L2 |
| **P** | Position | Take a stance, then steel-man the other | L2 + L3 |
| **A** | Action | Stress-test the position; identify biases | L4 |
| **B** | Benefit | Deliver a balanced, criterion-by-criterion verdict | L5 |

---

## ⚡ Telemetry-driven optimization (headline)

The dashboard surfaced **Layer 3** as the single bottleneck — 38% of total wall-clock and the highest hallucination risk. Splitting L3 into retrieval-only (L3a) plus narration (L3b), and caching the eight music-site responses in Redis for 24 hours, produced:

| Metric | Before | After | Change |
|---|---|---|:-:|
| L3 latency | 4.85 s | 1.95 s | **−60%** |
| L3 hallucination risk | 0.21 | 0.07 | **−67%** |
| End-to-end pipeline | 12.90 s | 9.55 s | **−26%** |
| Cost per run | $0.0505 | $0.0381 | **−25%** |
| SCIPAB rubric score | 0.89 | 0.94 | **+0.05** |

---

## 🏆 Final verdict (Layer 5)

| Criterion | Era winner |
|---|:-:|
| Melody · Lyricism · Vocal craft · Replay value | **1990s** |
| Production · Genre diversity · Cultural reach · Modern relevance | **2020s** |

**1990s win on craft. 2020s win on impact. The listener wins overall.**
