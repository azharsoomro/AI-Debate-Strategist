# AI Debate Strategist with Observability
### Hindi Movie Music — 1990s vs 2020s &nbsp;·&nbsp; SCIPAB framework &nbsp;·&nbsp; 5 reasoning layers

A multi-layer reasoning system that debates whether 1990s Hindi movie music is better than 2020s music. The pipeline anchors every step in the **SCIPAB** rhetorical framework, grounds claims in eight top Indian music sites (JioSaavn, Gaana, Spotify India, Bollywood Hungama, Filmfare, Radio Mirchi, Times Music, IMDb), emits per-layer telemetry, and ships with one telemetry-driven optimization that cut Layer 3 latency by 60% and hallucination risk by 67%.

![Flowchart](assets/flowchart.png)

---

## 📦 Required deliverables (graded)

| # | Deliverable | File |
|---|---|---|
| 1 | **Prompt Design PDF** | [`docs/01_prompt_design.pdf`](docs/01_prompt_design.pdf) |
| 2 | **AI Outputs + Telemetry PDF** | [`docs/02_outputs_and_telemetry.pdf`](docs/02_outputs_and_telemetry.pdf) |
| 3 | **Reflection** | [`docs/03_reflection.md`](docs/03_reflection.md) |
| 4 | **Flowchart** | [`assets/flowchart.svg`](assets/flowchart.svg) (vector) · [`assets/flowchart_ppt_hires.png`](assets/flowchart_ppt_hires.png) (3200 × 4730 PNG for slide decks) |
| 5 | **Video demo (≤5 min)** | [`docs/04_video_demo.mp4`](docs/04_video_demo.mp4) — recorded walk-through |

## 📚 Supporting material

| File | What it is |
|---|---|
| [`app/index.html`](app/index.html) | Live interactive 5-layer demo. No server, no API key. Each layer renders a plain-English summary + Strengths + Weaknesses + telemetry. Click **Apply L3 optimization** to see the bottleneck fix in place. |
| [`docs/05_video_demo_script.md`](docs/05_video_demo_script.md) | Time-coded script + storyboard for the video. |
| [`docs/06_summary_deck.pptx`](docs/06_summary_deck.pptx) | 3-slide PowerPoint summary (topic · prompt design · telemetry insights). |
| [`docs/07_deck_talking_points.md`](docs/07_deck_talking_points.md) | Speaker notes for the 3-slide deck. |
| [`prompts/`](prompts/) | One Markdown file per reasoning layer plus the master orchestrator preamble. |
| [`assets/flowchart_4k.png`](assets/flowchart_4k.png) | 3840 × 5677 PNG for 4K slide decks. |
| [`assets/flowchart_1920.png`](assets/flowchart_1920.png) | 1920 × 2838 PNG for standard projectors. |
| [`assets/flowchart_transparent.png`](assets/flowchart_transparent.png) | Transparent-background variant for coloured slide backgrounds. |
| [`scripts/build_pdfs.py`](scripts/build_pdfs.py) | Regenerates the two PDFs from the SVG and inline content. |
| [`scripts/init_git.sh`](scripts/init_git.sh) | One-shot helper to push this repo to GitHub. |

---

## 🚀 Architecture at a glance

```
USER INPUT  (motion · side · audience · grounding sources)
   │
   ▼
SCIPAB · Situation · Complication · Implication · Position · Action · Benefit
   │
   ▼
L1 Context Analysis     ──►  tokens · latency · schema_validity
   │
   ▼
L2 Argument Builder (1990s) ──►  tokens · latency · argument_strength
   │
   ▼
L3 Counter Argument (2020s) ──►  tokens · latency · hallucination_risk  ⚠ bottleneck
   │
   ▼
L4 Self-Critique         ──►  tokens · latency · bias_caught
   │
   ▼
L5 Final Strategy        ──►  tokens · latency · SCIPAB_score
   │
   ▼
DEBATE PACKAGE  (verdict matrix · spoken brief · cue cards · telemetry bundle)
```

Each layer has **one job**, a **typed JSON schema**, and instrumentation hooks. Layer N's output becomes Layer N+1's input — the pipeline behaves like a typed function chain.

---

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

---

## 🛠️ Run it locally

### View the live demo (zero setup)
```bash
git clone https://github.com/azharsoomro/ai-debate-strategist.git
cd ai-debate-strategist
open app/index.html        # macOS
xdg-open app/index.html    # Linux
start app/index.html       # Windows
```

### Rebuild the PDFs
```bash
pip install -r requirements.txt
python scripts/build_pdfs.py
```

---

## 📁 Repo layout

```
ai-debate-strategist/
├── README.md
├── LICENSE                   (MIT)
├── .gitignore
├── requirements.txt
├── app/
│   └── index.html            (interactive 5-layer demo)
├── docs/
│   ├── 01_prompt_design.pdf
│   ├── 02_outputs_and_telemetry.pdf
│   ├── 03_reflection.md
│   ├── 04_video_demo.mp4
│   ├── 05_video_demo_script.md
│   ├── 06_summary_deck.pptx
│   └── 07_deck_talking_points.md
├── prompts/
│   ├── 00_master_orchestrator.md
│   ├── 01_layer_context.md
│   ├── 02_layer_argument.md
│   ├── 03_layer_counter.md
│   ├── 04_layer_critique.md
│   └── 05_layer_final.md
├── assets/
│   ├── flowchart.svg
│   ├── flowchart.png
│   ├── flowchart_4k.png
│   ├── flowchart_ppt_hires.png
│   ├── flowchart_1920.png
│   └── flowchart_transparent.png
└── scripts/
    ├── build_pdfs.py
    └── init_git.sh
```

---

## License

MIT — see [LICENSE](LICENSE).

## Author

**Azhar Soomro** &nbsp;·&nbsp; 10 May 2026
