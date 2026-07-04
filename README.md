# Attentive.io — Architecture

**A live, open multi-agent research instrument for market news.**
Built by [Relight Labs](https://relightlabs.ai) · Live at [attentive.io](https://attentive.io)

## What this is

Attentive.io runs delayed market news through a pipeline of specialized AI agents and publishes every step of the reasoning — including the outcomes that went nowhere. It is a research instrument, not a signal service. Nothing it produces is investment advice, and we make no performance claims.

This repo documents the architecture. The implementation is private; the reasoning it produces is public at the live site.

## Why it exists

Signals are everywhere. Knowing which to believe is the hard part. Most tools in this space show you their hits. This instrument was built to answer a harder question: **when a system looks like it has an edge, how do you know the edge is real** — and not a leak, an overfit, or beta wearing a costume?

The answer we arrived at: the measurement apparatus *is* the product. The signal generator is ordinary. The part that tells you the truth is not.

## The pipeline

Four specialized agents, each with one job, each leaving its work on the record:

INGEST → EXTRACT → REASON → ADJUDICATE → RECORD

**01 · Scout (ingest).** Pulls delayed news and market-moving events across feeds, extracts the facts — what happened, who's involved — and filters noise before anything else runs.

**02 · Analyst (context).** Reads the market and technical context around the event and assembles the structured picture the adjudicator will weigh. Its read is shown, not hidden.

**03 · Judge (adjudicate).** Weighs the inputs and issues an internal confidence — the model's own read on conviction, labeled plainly for what it is: an internal score, not a signal, not advice.

**04 · Ledger (record).** Logs every output and what actually happened next, tracked to close. The misses stay on the record, not just the hits. The accumulated outcome record is the calibration and learning substrate for everything upstream — the asset that compounds.

The separation is deliberate: signal generation (creativity) is quarantined from risk adjudication (discipline). No single agent both proposes and disposes.

## The measurement methodology

The part we consider the actual contribution:

- **Verified entry basis.** An outcome only counts if its entry price has auditable provenance. No retroactive fills.
- **Look-ahead exclusion.** As-of joins throughout; the leakage controls are exercised by adversarial tests designed to prove the barriers fire, not assume they do.
- **Everything tracked to close.** Wins and losses alike feed the public record.
- **Provisional vs. clean, side by side.** When we enforced verified entry basis and stripped look-ahead, an apparent positive edge went negative. We lead with the clean number. That gap — between the flattering figure and the defensible one — is the entire point of the instrument.

## Stack

Python 3.12 / asyncio · Gemini via Vertex AI · TimescaleDB + pgvector · Cloud Run / Cloud SQL (GCP) · Docker. Built AI-natively — agentic coding tools are part of the daily workflow.

## Status

Live, in active development, operated by a single engineer. Current work: per-source evaluation, calibration analysis of adjudicator confidence, and exit-rule variants — all under the same leakage-safe methodology.

## Related

- **calibration-harness** *(forthcoming)* — post-hoc confidence calibration of LLM outputs: elicitation, proper scoring rules (Brier/CRPS), reliability diagnostics, frozen held-out validation.

## License / contact

Architecture documentation only; implementation is proprietary to Relight Labs. Questions: cjdeschenes@relightlabs.ai · [@Chris_Deschenes](https://x.com/Chris_Deschenes)
