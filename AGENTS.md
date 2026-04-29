# TradingAgents Lab Notes

This fork is a lab repo for experimenting with TradingAgents alongside Cortana.
Keep it isolated: no cron, no Mission Control integration, and no trade influence
until Cortana explicitly consumes a normalized artifact later.

## Local Setup

Use Python 3.13. Python 3.14 can force packages like `tiktoken` to build from
source and fail without Rust.

```bash
cd ~/Developer
git clone git@github.com:cortana-foundry/TradingAgents.git
cd TradingAgents
uv python install 3.13
uv sync --python 3.13
```

API keys are local only:

```bash
cp .env.example .env
# fill in OPENAI_API_KEY, ANTHROPIC_API_KEY, GOOGLE_API_KEY, etc.
```

Never commit `.env`.

## Smoke Checks

```bash
uv run --with pytest pytest -q
uv run python test.py
uv run tradingagents --help
```

Model-backed structured-output smoke, after keys are configured:

```bash
uv run python scripts/smoke_structured_output.py openai
```

Interactive CLI:

```bash
uv run tradingagents
```

## Experiment Rules

- Start with manual one-symbol runs such as `AAPL`, `NVDA`, or a Cortana BUY/WATCH candidate.
- Save outputs under `lab-runs/` or another ignored local folder.
- Treat results as second-opinion research only.
- Cortana remains the source of truth for freshness gates, lifecycle state, BUY readiness, Telegram alerts, and future execution boundaries.
- Do not add scheduled jobs or production integrations from this repo without a separate design doc.

## Useful Remotes

```bash
git remote -v
# origin   git@github.com:cortana-foundry/TradingAgents.git
# upstream https://github.com/TauricResearch/TradingAgents.git
```

Update from upstream manually when desired:

```bash
git fetch upstream
git checkout main
git merge upstream/main
```
