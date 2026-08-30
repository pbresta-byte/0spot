# Internal Operating System

This is Pedro's personal knowledge base, skill library, and project index. Read this file at the start of every session opened at this root — it explains what lives where and how to use each folder, so context doesn't need to be re-explained each time.

## Folder structure

```
internal-os/
  knowledge/
    me/            personal history, preferences, values, experiences
    frameworks/    reusable mental models, methodologies, decision frameworks
    audience/      notes on the people this work is for (readers, clients, users)
    raw/           unprocessed ingested material — articles, transcripts, notes
  skills/
    _template/     starting point for any new skill
    improve-system/  self-updating skill — run after a session to fold lessons back in
    ingest-resource/ brings a new external resource into knowledge/
  projects/
    dashboard/     pointer to the live trading dashboard project (oanda-command-center)
    muhurta-app/   pointer to the Muhūrta Gauge / PL0 Jyotish app
    personal-site/ placeholder for the personal site project
  pipelines/       ICM (Interpretable Context Methodology) staged workspaces — see below
  .claude/
    skills/        junction to skills/ above, so slash commands work in this project
    agents/        statistical-analysis subagents (see below) — Claude Code invokes these directly
```

## knowledge/

The durable memory layer. Four subfolders, each with a distinct role:

- **me/** — who Pedro is: background, preferences, working style, values, and `me/experiences/` for specific stories/lessons he's shared that are worth remembering verbatim (not just summarized into a preference). Read this before drafting anything in his voice or making a judgment call on his behalf.
- **frameworks/** — reusable models and methodologies he uses to think or decide — not project-specific facts, but the lens applied across projects (e.g. how he evaluates a trade, how he structures a decision, a named mental model). A framework file should be usable on a totally different question than the one that produced it.
- **audience/** — who specific pieces of work are *for* — readers of the personal site, users of the dashboard, whoever the output serves. Separate from `me/` because the audience's needs aren't Pedro's own preferences.
- **raw/** — unprocessed capture of ingested material (full article text, video transcript, meeting notes) with source metadata. This is the ledger `ingest-resource` writes to before anything gets distilled into `frameworks/`, `audience/`, or `me/`. Treat `raw/` as an archive, not something to edit — corrections happen in the distilled file, not the source capture.

## skills/

Custom skills for this personal system, mirrored into `.claude/skills/` (via a directory junction — same files, both paths) so they're invocable as slash commands in any session opened here.

- **_template/SKILL.md** — copy this when starting a new skill. Keep the frontmatter (`name`, `description`) and the structure; don't invent a different shape per skill.
- **improve-system/** — `/improve-system`. Run this at the end of a session (or any time) to fold what just happened back into this knowledge base: skill corrections become skill edits, shared stories become `knowledge/me/experiences/` entries, stale/duplicate material gets flagged (not silently deleted).
- **ingest-resource/** — `/ingest-resource`. Bring a new external resource (article URL, YouTube video, transcript, notes, attachment) into this system: captures it in `raw/`, then distills and files it into the right knowledge subfolder.
- **Trading skills (2026-08-25)** — `pivot-points/`, `price-action/`, `price-levels/`, `moving-averages/`, `technical-analysis/`, `trading-strategies/`, `risk-management/`. Each teaches a specific technique, anchored on real, confirmed ForexToday videos where a matching one exists (see each SKILL.md's frontmatter description for the exact source video), general correct methodology where it doesn't — never presented as more sourced than it is. `technical-analysis` and `trading-strategies` are synthesis skills that sequence the narrower ones; `risk-management` hands the actual pip/lot arithmetic to `fx-calculator` in `oanda-command-center`. Individually globally-junctioned into `C:\Users\drrag\.claude\skills\`, same pattern as `ingest-resource` (see below) — invocable as slash commands in ANY Claude Code session, not just ones opened at this root.
- **dispatch-integrity/** (2026-08-26) — not a task skill, an operational one: how to avoid two recurring failures when delegating to Hermes/opencode async — a long prompt silently truncating to its first sentence, and a job coming back "lost" while its on-disk checkpoint survived (causing accidental duplicate work). Load this before any large async dispatch or redispatch. Globally junctioned like the others.

## .claude/agents/ — statistical-analysis + trading-knowledge + jyotish subagents

Fifteen Claude-Code-invoked subagents, purpose-built to turn either a hypothesis into a rigorous finding, the ingested trading knowledge base into applied guidance, or the 1,437-book jyotish/tropical corpus scan into applied jyotish technique — all `knowledge/frameworks/`-ready, not vibes. Each is scoped to not overlap the others — see each file's own "what you explicitly do not do" for the exact handoffs.

**Statistical-methodology lens (tests a hypothesis against data):**
- **correlation-analyst** — do two time-indexed variables actually move together (strength, lag, spuriousness)?
- **backtest-statistician** — does a stated entry/exit rule actually beat chance historically (win rate vs. base rate, overfitting/lookahead checks)? Formalizes what pl0-app's own Commodities backtest page already does informally.
- **distribution-regime-analyst** — how does a series actually behave (volatility regime, tails, outliers), and does another agent's finding survive across regimes or is it outlier-driven?
- **time-series-seasonality-analyst** — does a series have a genuine recurring cycle, calendar or astronomical/jyotish-period — the natural bridge between FX seasonality work and jyotish's inherently cyclical timing systems.

**Trading-knowledge lens (synthesizes the ingested corpus into applied guidance):**
- **general-trading-strategist** — market-agnostic principles: risk philosophy, psychology, process, market structure — synthesized from the ingested knowledge base with sources named.
- **technical-analysis-specialist** — chart/indicator/pattern knowledge as taught by the ingested sources — mechanics, application, known failure modes.
- **currency-strength-analyst** — operationalizes the TRADARS QuantBox+TradeOurs workflow: turns an 8-currency economic scorecard into ranked pair selection, with seasonality overlay and divergence detection against price. Anchored on the 28-pair matrix/RSI math also used in the Pine Script conversion below and on two named TRADARS videos (QuantBox Part 1/2 — video IDs in the file's Source Anchoring section, useful for the still-pending Tradars transcription work).

**Jyotish-knowledge lens (2026-08-26, from the completed book-scan pipeline — see `knowledge/synthesis/jyotish-muhurta/`):**
- **dasha-timing-analyst** — Vimshottari/Yogini/Char/conditional dasa period timing; "when will X happen."
- **nadi-cuspal-analyst** — Nadi-system cuspal interlinks and KP sub-lord analysis.
- **ashtakavarga-strength-analyst** — Ashtakavarga/Shadbala/Bhavabala quantitative planetary strength scoring.
- **medical-astrology-analyst** — health-indication astrology; always descriptive, never diagnostic (hard boundary in the file itself).
- **electional-timing-analyst** — muhurta/electional timing; formalizes and extends pl0-app's own `NEWMUHURTA` R1-R24 rules.
- **varshaphal-analyst** — annual/solar-return (Tajik) year-ahead forecasting.
- **mundane-event-analyst** — national/world-event jyotish, the jyotish-side counterpart to the statistical seasonality agents.
- **jyotish-history-specialist** — source-tracing, edition/variant comparison, OCR-risk flagging — resolves "which classical text actually says this" before another agent cites it.

All three lenses are source-disciplined: the statistical agents test claims against real data, the knowledge agents (trading and jyotish alike) ground claims in named ingested material — none of them invent plausible-sounding numbers or sources. Where a knowledge-lens claim is worth testing statistically (an FX-jyotish correlation, a mundane-astrology market claim), it hands off to the statistical lens rather than asserting it's proven.

**How these fit the wider escalation ladder** (see `knowledge/frameworks/working-with-opencode-and-hermes.md`): Claude Code invokes these subagents directly for the analysis itself (that's a judgment-heavy step that stays with Claude Code, not delegated blind). Their structured output is meant to be hand-off-ready: paste straight into a new `knowledge/frameworks/` entry, or hand to Hermes (with a `workdir` pointing here) to file and cross-link — e.g. into the `ask-the-board` Jyotish panel or pl0-app's Currency Significators where the finding bridges astrology and trading. Don't ask Hermes or opencode to run these subagents themselves — they're Claude-Code-native; Hermes's role is filing/cross-linking the finished output, not producing it.

## pipelines/

Numbered-stage folder workspaces for recurring, sequential, human-reviewed work — the "current run" layer, as
opposed to `knowledge/`, which is the durable "what Pedro knows" layer. Based on Interpretable Context
Methodology (ICM): each pipeline has its own root `CLAUDE.md`/`CONTEXT.md` (routing) and numbered stage folders,
each with a `CONTEXT.md` contract (Inputs/Process/Outputs), a `references/` folder (stable, Layer 3), and an
`output/` folder (per-run, Layer 4). See `knowledge/frameworks/interpretable-context-methodology-icm.md` for
the framework and `knowledge/synthesis/tooling/icm-adoption-plan.md` for which of this OS's existing workflows
(jyotish book-scan, forex/FX ingestion, currency-strength filing) are candidates and how to migrate one safely.
`pipelines/_template/` is the copy-and-fill starting point for a new one.

## projects/

Pointers into the actual project folders elsewhere in the workspace — this directory holds short indexes, not duplicated code. Open the linked project directly to do real work; come back here only to update the index entry.

Pedro's two currently-built apps are both explicitly in scope of this Internal Operating System — treat them as part of "the system," not separate side projects:

- **dashboard/** — points at `oanda-command-center` (the live PySide6 OANDA trading app) as the active dashboard project. `market-dashboard` is an earlier static-HTML iteration, kept for reference. This project has its own `.claude/skills/ask-the-board/` (the FX + Jyotish Board of Advisors) — a project-local skill, separate from the ones in this OS's `skills/`.
- **muhurta-app/** — points at the Muhūrta Gauge / PL0 Jyotish app. Referenced elsewhere in this OS (e.g. `/ask-the-board`'s Jyotish panel draws on PL0's live Currency Significators when available).
- **personal-site/** — placeholder; no project exists yet.

## How to use this at session start

1. Skim this file and `knowledge/me/` for who Pedro is and how he wants to work.
2. Check `knowledge/frameworks/` if the task looks like it should follow an established model rather than being reasoned from scratch.
3. If the session touches a specific project, open `projects/<name>/` first for the pointer to where the real work lives.
4. At a natural stopping point, consider running `/improve-system` so lessons from this session don't stay trapped in one conversation.

## Token economy (OWNER DIRECTIVE — overrides any earlier Opus/high-effort request)
The token budget burns out instantly at scale (934-work corpus, daily council re-runs). Therefore, for ALL Jyotish corpus / skill-refresh / verification work in this OS:
- **DO NOT use Opus or any high-effort/expensive model.** Use the cheapest FREE model (opencode-free / hy3-free / a free openrouter model).
- **Minimize token spend:** reuse `knowledge/frameworks/jyotish/nav_index.json` to locate nodes; do NOT re-read full PDFs or re-extract text. Bulk-verify via grep / short targeted reads. Cap council outputs to a concise reconciliation summary.
- Parallel-dispatch verification councils as LEAF agents on FREE models only; never upgrade effort.
- This applies to the 4:25 AM daily council re-run and any ad-hoc corpus task. Paid models are reserved ONLY for explicit owner-approved high-judgment work, and even then keep it lean.
