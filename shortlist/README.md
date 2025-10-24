# Shortlist Directory

This folder contains concise one-page summaries of ideas that have reached `status: ready-for-prototype` and have been formally shortlisted.

## Purpose
- Provide a quick-scannable artifact for steering meetings / review.
- Freeze the decision context (scores, rationale, next step) separate from the evolving original idea file.
- Reduce cognitive load when selecting first prototypes.

## Entry Criteria
An idea moves here when ALL are true:
1. Scores recorded (Impact, Feasibility, Novelty, Urgency, Alignment).
2. Impact OR Feasibility >= 4 (threshold adjustable).
3. Explicit resource outline drafted (people/timebox/high-level stack).
4. Risks enumerated with at least one mitigation each.
5. Issue label updated to `status:ready-for-prototype` and `decision:shortlisted`.

## File Naming
`<slug>-shortlist.md` (e.g. `cursor-voice-assistant-shortlist.md`).

## Recommended Summary Structure
```
# <Title>

## Snapshot
- Source Idea: ideas/YYYY-MM-DD-<slug>.md (Issue #<n>)
- Scores: impact=X feasibility=Y novelty=Z urgency=U alignment=A
- Rationale: 1–2 sentence justification of selection
- Primary Risks: <list>
- Mitigations: <list>
- Resource Sketch: people (roles) + timebox + key dependencies
- Next Step: e.g. "Prototype push-to-talk + transcript panel"

## Decision Notes
- YYYY-MM-DD: shortlisted after review session <name>
- YYYY-MM-DD: (future updates)
```

## Maintenance
- If prototype started: add line `Prototype: /prototypes/<folder>`.
- If deprioritized later: move file to a future `archived/` folder (not yet created) and update Issue to `status:archived`.

## Review Rhythm
Quarterly: verify relevance, update scores, remove outdated entries.

---
Keep this lean; avoid duplicating minute details from the original idea file.