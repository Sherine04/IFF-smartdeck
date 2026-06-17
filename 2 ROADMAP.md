# 📅 IFF SmartDeck — Project Roadmap

> From intern prototype to enterprise-scale AI presentation platform across all IFF divisions.

---

## Roadmap at a Glance

```
PHASE 0          PHASE 1          PHASE 2          PHASE 3          PHASE 4
Foundation    →  MVP: Colors   →  Expand Depts  →  Full Platform →  Scale & Learn
Weeks 1–6        Weeks 7–14       Weeks 15–24      Weeks 25–36      Month 10–12
```

---

## Phase 0 — Foundation (Weeks 1–6)
### Theme: *"Know what you have before you build"*

**Goal:** Audit existing assets, design the data architecture, and get stakeholder buy-in before writing a single line of logic.

### Milestones

| # | Milestone | Owner | Week | Done When |
|---|---|---|---|---|
| 0.1 | Audit existing slide libraries across all departments | Marketing Intern | W1–2 | Full inventory list with quality scores |
| 0.2 | Map all data sources by department | Intern + R&D leads | W1–3 | Data source register completed |
| 0.3 | Define content tagging taxonomy | Intern + IT | W2–4 | Taxonomy approved by 3 dept heads |
| 0.4 | Design SharePoint folder structure | IT + Marketing | W3–5 | Folder skeleton live in SharePoint |
| 0.5 | Stakeholder alignment workshop | Marketing Lead | W4 | All 5 dept owners committed to data contribution |
| 0.6 | Brief intake form v1 design | Intern | W5–6 | Form tested by 2 sales reps |

### Deliverable
> Data architecture document + approved taxonomy + SharePoint skeleton + signed stakeholder charter

---

## Phase 1 — MVP: Colors Department (Weeks 7–14)
### Theme: *"Prove it works on the highest-priority use case"*

**Why Colors first:** Maximum commercial urgency (FDA 2026 deadline), most structured data, clearest brief template. Success here justifies the full platform investment.

### Milestones

| # | Milestone | Owner | Week | Done When |
|---|---|---|---|---|
| 1.1 | Migrate Colors product catalog (9 families) | R&D + Intern | W7–8 | All 9 color sources tagged in SharePoint |
| 1.2 | Build stability data matrix (pH × heat × shelf-life) | R&D + Intern | W7–9 | Structured table, not PDFs |
| 1.3 | Upload 50+ tagged visual assets | Marketing | W8–10 | All assets tagged with product + application metadata |
| 1.4 | Build 30 core slide modules | Intern | W9–11 | Modules peer-reviewed by Mathilde's team |
| 1.5 | Write IF/THEN rule set v1 | Intern | W10–12 | Covers all 9 colors × 7 applications × 4 regions |
| 1.6 | Connect PowerPoint Copilot to SharePoint | IT | W11–13 | Copilot can query asset library |
| 1.7 | End-to-end test: 3 real customer briefs | Sales team | W13–14 | >80% content accuracy rated by product manager |

### Deliverable
> Working SmartDeck prototype for Colors — brief → deck in < 30 minutes

### Success Metrics
- 3 test decks reviewed, >80% accuracy
- Deck build time: 4 hours → <30 minutes
- Zero regulatory errors in test decks

---

## Phase 2 — Expansion: Flavours + Food Ingredients (Weeks 15–24)
### Theme: *"Scale the model, deepen the intelligence"*

**Why these two next:** Both sit in the Taste/Nourish division — close to the Colors team, overlapping customer base. Many briefs will require cross-department content (color + flavor combined pitch).

### Milestones

| # | Milestone | Owner | Week | Done When |
|---|---|---|---|---|
| 2.1 | Flavours data migration (catalog + sensory + application) | R&D Flavours + Intern | W15–17 | Flavor catalog tagged and queryable |
| 2.2 | Food Ingredients data migration | R&D Food Ing. + Intern | W15–18 | Functional performance data structured |
| 2.3 | Cross-department brief logic (Color + Flavor) | Intern | W17–19 | Combined brief generates multi-dept deck |
| 2.4 | RAG vector search implementation | IT / AI team | W18–21 | Semantic search replaces keyword matching |
| 2.5 | Multi-region regulatory logic expansion | Intern + Regulatory | W19–22 | All 4 regions: US, EU, APAC, LatAm |
| 2.6 | Analytics dashboard v1 (Power BI) | IT + Intern | W22–24 | Tracks deck usage, slide performance |

### Deliverable
> SmartDeck covering 3 departments, semantic RAG search, multi-region rules, analytics dashboard

---

## Phase 3 — Full Platform: Fragrance + Health & Bioscience (Weeks 25–36)
### Theme: *"Complete the IFF portfolio. Close the feedback loop."*

**Note:** Fragrance and Health & Bioscience have distinct data types (sensory/emotional data; clinical evidence). Their brief structures are different — handled by specialist rule sets.

### Milestones

| # | Milestone | Owner | Week | Done When |
|---|---|---|---|---|
| 3.1 | Fragrance portfolio integration | Scent Marketing + Intern | W25–28 | LMR + consumer fragrance catalog live |
| 3.2 | Health & Bioscience clinical data structured | Medical Affairs + IT | W25–30 | HOWARU® + CARE4U® data in compliant format |
| 3.3 | Feedback loop ML model v1 | AI team | W28–32 | Win/loss data improves slide selection |
| 3.4 | CRM integration (Salesforce win/loss tagging) | Sales Ops + IT | W30–34 | Every deck send logged; outcomes tracked |
| 3.5 | Global rollout training (US, EU, APAC) | Marketing | W33–36 | All regional teams trained and using SmartDeck |

### Deliverable
> Full IFF SmartDeck — all 5 departments, self-improving feedback loop, CRM integration, global rollout

---

## Phase 4 — Optimize & Scale (Month 10–12)
### Theme: *"Make the system smarter than any individual"*

| Feature | What it does | Priority |
|---|---|---|
| Per-rep personalization | System learns each rep's preferred style and client relationship context | High |
| Real-time market data | Mintel API + Euromonitor live feed → decks always cite current market numbers | High |
| Auto-translation | Decks auto-translated to FR, DE, ES, ZH, PT for regional teams | Medium |
| Teams integration | Deck auto-shared to Teams meeting invite 1 hour before meeting | Medium |
| Customer portal | Client-facing version — customer receives interactive, branded deck link | Low (future) |

---

## Dependency Map

```
0.1 Audit ──────────────────────────────────────────────────────────────────────┐
0.2 Data sources ────────────────────────────────────────────────────────────┐  │
0.3 Taxonomy ──────────────────────────────────────────────────────────────┐ │  │
0.4 SharePoint structure ──────────────────────────────────────────────┐   │ │  │
                                                                        ↓   ↓ ↓  ↓
                                                            1.1 Colors catalog
                                                                    ↓
                                                            1.2 Stability data
                                                                    ↓
                                                            1.3 Visual assets
                                                                    ↓
                                                            1.4 Slide modules
                                                                    ↓
                                                            1.5 Rule set v1
                                                                    ↓
                                                            1.6 Copilot connect
                                                                    ↓
                                                            1.7 Live test ──→ Phase 2
```

---

## Risk Register

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| R&D teams don't contribute data on schedule | High | Critical | Assign data steward per department; monthly contribution deadline |
| Data quality poor (PDFs instead of structured) | High | High | Provide Excel templates; Intern reviews before upload |
| Copilot licence not available at IFF | Medium | High | Gamma as fallback; PowerPoint manual assembly still 60% faster |
| Clinical data (Health & Bioscience) requires extra compliance review | Medium | Medium | Flag Phase 3 data for Medical Affairs sign-off before upload |
| Scope creep (too many departments at once) | High | Medium | Strict phasing — Phase 1 = Colors only; no exceptions |

---

*IFF SmartDeck Roadmap · v0.1 · June 2026*
