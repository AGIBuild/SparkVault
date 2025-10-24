# SparkVault

> Ideas are sparks; this vault preserves them until the right time, people, and resources converge.

## 1. Purpose
SparkVault is for:
- Capturing unbuilt ideas (tools, products, systemic or civic innovation concepts).
- Providing minimal structure beyond raw slogans.
- Letting contributors enrich, critique, and de-risk them.
- Helping future selection into a Prototype / Pilot phase.

## 2. Scope
This repository stores early-stage concepts that are:
- Not yet prioritized
- Potentially high-impact but resource constrained
- Needing clearer articulation or risk surfacing
- Candidates for future prototyping, pilots, or open collaboration

## 3. Repository Structure
```
/
├── ideas/                # Raw & evolving idea entries
├── prototypes/           # (Optional) Early technical or process experiments
├── pipeline/             # Selection artifacts (scorecards, shortlists)
├── docs/                 # Shared references, frameworks
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
└── IDEA-TEMPLATE.md
```

## 4. Idea Entry Template
Create each idea as a markdown file inside `ideas/` named: `YYYY-MM-DD-short-slug.md`.

Suggested content:
```
# Title
One-line summary

## Problem
The systemic / user pain this addresses and why it matters now.

## Insight
The non-obvious angle or leverage point.

## Concept
Core mechanism, actors, usage flow (MVP narrative).

## Potential Impact
Who benefits; levels (individual / community / sector / public systems); any quantitative hypothesis.

## Feasibility Notes
Early thoughts on tech stack / process / dependencies / blockers / key risks.

## Related
Links to research, comparable products, datasets, regulations.

## Evolution Ideas
Possible sub-experiments or validation steps.

## Status
draft | exploring | ready-for-prototype | archived

## Revision Notes
- YYYY-MM-DD: brief change log
```

Optional front-matter:
```
---
tags: [tool-dev, civic-innovation]
status: draft
author: YOUR_NAME
priority: low
impact_hypothesis: "If X then Y improves by Z%"
---
```

## 5. Tag Suggestions
- tool-dev
- civic-innovation
- system-reform
- data-platform
- ai-augment
- sustainability
- education
- experimental-policy
- protocol
- speculative

## 6. Evolution Flow
1. Capture
2. Enrich (context, precedents, risks)
3. Score (Impact, Feasibility, Novelty, Urgency, Alignment)
4. Select (shortlist for prototype)
5. Prototype (in `prototypes/` or separate repos)
6. Archive (obsolete, implemented elsewhere, deprioritized)

## 7. Evaluation Dimensions
| Dimension   | Question                                    | Scale Hint |
|-------------|---------------------------------------------|-----------|
| Impact      | Will this materially shift outcomes?        | Breadth + depth |
| Feasibility | Can we credibly build/validate near-term?   | Resources + clarity |
| Novelty     | Does it differ from existing solutions?     | Differentiation |
| Urgency     | Is timing critical now?                     | Time sensitivity |
| Alignment   | Does it fit SparkVault’s dual mission?      | Tool + societal synergy |

## 8. Contributing
- Fork & PR new idea file or improvements.
- Preserve original author’s intent—add extensions via sections or Revision Notes.
- Use evidence: cite sources, precedents, data.
- Mark speculative assumptions clearly.
- If proposing implementation, outline a Minimum Viability Experiment (MVE).

## 9. Code of Conduct
We encourage:
- Evidence-based critique
- Ethical awareness (privacy, equity, accessibility)
We reject:
- Personal attacks
- Unfounded absolutist claims

(Consider adopting [Contributor Covenant](https://www.contributor-covenant.org/).)

## 10. Roadmap (Draft)
- [ ] Add initial 5–10 ideas
- [ ] Introduce scoring helper (script or GitHub Action)
- [ ] Publish shortlist for prototype candidates
- [ ] Open community discussion (GitHub Discussions)
- [ ] Identify first prototype spin-off repo

## 11. Licensing
Recommended:
- Content (ideas, docs): CC BY 4.0
- Code / prototypes: MIT or Apache-2.0

## 12. FAQ
Q: Can I implement an idea immediately?  
A: Yes—open an issue or PR linking the source idea and outline your experiment plan.

Q: Why not jump straight to building everything?  
A: Intentional curation reduces waste and increases reuse, alignment, and timing effectiveness.

Q: How do we avoid stagnation?  
A: Quarterly review: update statuses, archive stale or merged concepts.

---

Welcome to SparkVault—help turn latent sparks into catalytic systems.