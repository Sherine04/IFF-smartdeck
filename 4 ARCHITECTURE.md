# 🏗️ IFF SmartDeck — System Architecture

> Technical design of the AI backend, data pipeline, and presentation generation engine.

---

## Architecture Principles

1. **Enterprise-first** — Built on Microsoft 365 stack. No data leaves IFF's Azure tenant.
2. **Human-in-the-loop** — AI generates, humans approve. No deck sends without review.
3. **Modular** — Each department's data is isolated. A bug in Fragrance data doesn't affect Colors.
4. **Self-improving** — Win/loss feedback trains the model over time.
5. **Auditable** — Every deck is logged: what content was selected, who reviewed it, when it was sent.

---

## Full System Architecture

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                          IFF SMARTDECK PLATFORM                            ║
╠══════════════════════════════════════════════════════════════════════════════╣
║                                                                              ║
║  ┌─────────────────────────────────────────────────────────────────────┐    ║
║  │                    LAYER 1 — DATA INGESTION                        │    ║
║  │                                                                     │    ║
║  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐           │    ║
║  │  │  R&D DB  │  │  CRM     │  │  Market  │  │Regulatory│           │    ║
║  │  │ (weekly  │  │(Salesforce│  │Intel API │  │Compliance│           │    ║
║  │  │  export) │  │real-time)│  │(Mintel)  │  │   DB     │           │    ║
║  │  └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘           │    ║
║  │       └─────────────┴──────────────┴──────────────┘                │    ║
║  │                              │                                      │    ║
║  │                     ETL Pipeline (Power Automate)                   │    ║
║  │                    Validate → Tag → Normalize                       │    ║
║  └─────────────────────────────┬───────────────────────────────────────┘    ║
║                                │                                            ║
║                                ▼                                            ║
║  ┌─────────────────────────────────────────────────────────────────────┐    ║
║  │                LAYER 2 — CONTENT DATABASE                          │    ║
║  │                                                                     │    ║
║  │  SharePoint + Azure Blob Storage                                    │    ║
║  │                                                                     │    ║
║  │  ┌──────────────────────────────────────────────────────────────┐  │    ║
║  │  │  Azure AI Search Index (vector + keyword + semantic)         │  │    ║
║  │  │  ~15,000 data points │ ~4,700 visual assets │ ~580 cases    │  │    ║
║  │  └──────────────────────────────────────────────────────────────┘  │    ║
║  │                                                                     │    ║
║  │  Colors    │  Flavours   │  Food Ing.  │  Fragrance  │  Health     │    ║
║  │  (Phase 1) │  (Phase 2)  │  (Phase 2)  │  (Phase 3)  │  (Phase 3)  │    ║
║  └─────────────────────────────┬───────────────────────────────────────┘    ║
║                                │                                            ║
║                                ▼                                            ║
║  ┌─────────────────────────────────────────────────────────────────────┐    ║
║  │               LAYER 3 — AI ORCHESTRATION ENGINE                   │    ║
║  │                                                                     │    ║
║  │  ┌──────────────────┐  ┌─────────────────┐  ┌─────────────────┐   │    ║
║  │  │ Brief Parser     │  │ RAG Retrieval   │  │ Rule Engine     │   │    ║
║  │  │ (intent + tags)  │→ │ (GPT-4o embeds) │→ │ (Power Automate)│   │    ║
║  │  └──────────────────┘  └─────────────────┘  └────────┬────────┘   │    ║
║  │                                                        │            │    ║
║  │                                              ┌─────────▼────────┐  │    ║
║  │                                              │ Narrative Sequencer│  │    ║
║  │                                              │ (ACT structure)   │  │    ║
║  │                                              └─────────┬────────┘  │    ║
║  │                                                        │            │    ║
║  │                                              ┌─────────▼────────┐  │    ║
║  │                                              │ NLG Module        │  │    ║
║  │                                              │ (GPT-4o via Azure │  │    ║
║  │                                              │  OpenAI — private)│  │    ║
║  │                                              └─────────┬────────┘  │    ║
║  └────────────────────────────────────────────────────────┼────────────┘    ║
║                                                           │                 ║
║                                                           ▼                 ║
║  ┌─────────────────────────────────────────────────────────────────────┐    ║
║  │               LAYER 4 — PRESENTATION GENERATION                   │    ║
║  │                                                                     │    ║
║  │  PowerPoint Copilot receives:                                       │    ║
║  │  • Ordered slide module list                                        │    ║
║  │  • Generated text content per slide                                 │    ║
║  │  • Selected visual asset paths                                      │    ║
║  │  • IFF brand template reference                                     │    ║
║  │  • Speaker notes per slide                                          │    ║
║  │                                                                     │    ║
║  │  Output: .pptx draft saved to SharePoint review folder              │    ║
║  └─────────────────────────────┬───────────────────────────────────────┘    ║
║                                │                                            ║
║                                ▼                                            ║
║  ┌─────────────────────────────────────────────────────────────────────┐    ║
║  │               LAYER 5 — HUMAN REVIEW (15 min)                     │    ║
║  │  Marketing → Product Mktg → R&D → Regulatory → APPROVED           │    ║
║  └─────────────────────────────┬───────────────────────────────────────┘    ║
║                                │                                            ║
║                                ▼                                            ║
║  ┌─────────────────────────────────────────────────────────────────────┐    ║
║  │               LAYER 6 — ANALYTICS & FEEDBACK LOOP                 │    ║
║  │  Power BI dashboard │ CRM win/loss log │ Model retraining signal   │    ║
║  └─────────────────────────────────────────────────────────────────────┘    ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

---

## The AI Engine — Detailed

### Component 1: Brief Parser

Converts the sales rep's form input into a structured JSON object the system can reason over.

```json
Input (from sales rep):
{
  "customer": "General Mills",
  "category": "Cereal & Confectionery",
  "target": "Pink-red shade, replacing Red 40",
  "region": ["US"],
  "claims": ["clean-label", "no-artificial-colors"],
  "meeting_type": "commercial_proposal",
  "urgency": "standard"
}

Parsed output (SmartDeck internal):
{
  "department": "Colors",
  "color_family": ["red", "pink"],
  "application": "confectionery",
  "regions": ["US"],
  "exclude": ["carmine_not_needed_check: vegan=false → carmine allowed"],
  "regulatory_focus": ["FDA", "clean-label"],
  "slide_tone": "commercial",
  "narrative_arc": "ACT_commercial",
  "urgency": "48h",
  "context_tags": ["FDA_dye_ban", "reformulation", "confectionery_coating"]
}
```

---

### Component 2: RAG Retrieval (Retrieval-Augmented Generation)

The system converts the parsed brief into an embedding vector and runs semantic search across the Azure AI Search index.

```
Query embedding: "pink-red natural color, confectionery, US clean label"
           ↓
Semantic search over 15,000+ indexed content chunks
           ↓
Top-N results returned with relevance scores:

RESULT 1 — Score: 0.94
  Product: Carmine (E120) — confectionery application, US FDA approved
  Type: product_detail

RESULT 2 — Score: 0.91
  Product: Anthocyanins (grape) — confectionery, pink-red, clean label
  Type: product_detail

RESULT 3 — Score: 0.88
  Case Study: "Global confectionery brand, Red 40 replacement, US launch"
  Type: case_study

RESULT 4 — Score: 0.85
  Data: Carmine stability in panning at 120°C — 97% retention
  Type: technical_data

RESULT 5 — Score: 0.82
  Regulatory: FDA synthetic dye phase-out timeline and compliance steps
  Type: regulatory_context
```

---

### Component 3: Rule Engine (Deterministic Guardrails)

After RAG retrieval, rules are applied to filter, add, or reorder content. Rules cannot be overridden by the AI.

```python
RULE LIBRARY v1 (Colors Department)

# Vegan filter
IF brief.claims includes "vegan":
    REMOVE all content tagged product="carmine"
    ADD content tagged product="anthocyanins" OR product="beetroot"

# FDA context injection
IF brief.region includes "US" AND brief.department == "Colors":
    FORCE_INSERT slide_module="FDA_synthetic_dye_ban_2025"
    POSITION = slide 2 (after title)

# Multi-color complexity
IF brief.target mentions ">1 color" OR brief.category == "confectionery":
    ADD slide_module="multi_color_system_overview"
    ADD slide_module="color_matrix_by_application"

# EU E-number compliance
IF brief.region includes "EU":
    SWAP regulatory_module="US_FDA" FOR "EU_EFSA_Enumber"
    FLAG all products WITHOUT E-number for review

# Commercial vs Technical tone
IF brief.meeting_type == "technical":
    INCREASE weight of stability_data slides
    DECREASE weight of market_trend slides
    ADD slide_module="formulation_deep_dive"

IF brief.meeting_type == "discovery":
    PRIORITIZE market_opportunity slides
    ADD slide_module="portfolio_overview_visual"
    REMOVE technical_detail slides (move to appendix)

# Cross-sell trigger
IF brief.department == "Colors" AND brief.category in ["dairy","beverage","bakery"]:
    ADD slide_module="flavour_solutions_crosssell"
    POSITION = second-to-last (before next steps)
```

---

### Component 4: Narrative Sequencer

Arranges selected slide modules into a coherent story arc before passing to Copilot.

```
ACT STRUCTURE — Commercial Proposal (13 slides)

ACT 1 — CONTEXT (Why now)
  [01] Title + customer name
  [02] Market moment (FDA / trend data)
  [03] Consumer signal (stats)

ACT 2 — CHALLENGE (Why this is hard)
  [04] Reformulation challenges
  [05] Customer-specific complexity

ACT 3 — SOLUTION (What IFF offers)
  [06] Portfolio overview
  [07] Technical proof
  [08] Regulatory coverage
  [09] IFF vs generic supplier

ACT 4 — PROOF + JOURNEY (Why trust us)
  [10] Reformulation roadmap
  [11] Case study
  [12] Innovation context (SmartDeck meta-slide)

ACT 5 — ACTION
  [13] Next steps — single, specific CTA
```

---

### Component 5: NLG Module (Natural Language Generation)

The GPT-4o model (running on IFF's private Azure OpenAI instance) receives the ordered slide modules and writes:
- Headline for each slide (max 12 words, declarative, active voice)
- Body text (max 5 lines, no bullet overload)
- Data callouts (key numbers formatted for visual emphasis)
- Slide transitions (connects consecutive slides narratively)
- Speaker notes (3–5 sentences per slide for the presenter)

**Prompt template sent to GPT-4o:**
```
You are a B2B marketing writer for IFF, a global ingredients company.
Write the content for a [meeting_type] presentation to [customer], 
a [category] manufacturer in [region].

Tone: [tone_profile]
Meeting context: [meeting_objective]

For each slide module below, write:
1. HEADLINE (max 12 words, declarative)
2. BODY (max 5 lines, no nested bullets)
3. DATA_CALLOUT (if numerical data present — format for visual emphasis)
4. SPEAKER_NOTE (3–5 sentences, conversational, includes a question 
   the presenter can ask the customer)

Slide modules: [ordered_module_list_with_content_payloads]

Brand voice: Consultative, science-backed, specific over generic.
Never use filler phrases like "innovative solutions" or "best-in-class."
Every claim must be backed by data already present in the module.
```

---

## Technology Decisions

### Why Azure OpenAI (not public ChatGPT)
IFF's customer brief data is commercially confidential. Product formulation data is proprietary. Using public ChatGPT API means that data could be used to train OpenAI's models.

Azure OpenAI provides the same GPT-4o capability in a **private, IFF-controlled Azure tenant** — data never leaves IFF's environment.

### Why SharePoint (not a custom database)
IFF is almost certainly already on Microsoft 365. SharePoint gives:
- Zero new infrastructure cost
- Native Copilot integration
- IT team familiarity
- Granular permission controls (Regulatory data access ≠ Marketing data access)
- Version history on every content update

### Why Copilot Studio for rules (not custom code)
The rule engine must be maintained by the **Marketing team**, not IT. Copilot Studio's no-code interface means Mathilde's team can update IF/THEN rules when a new product launches or a regulation changes — without raising an IT ticket.

### Why Power BI for analytics
Same M365 ecosystem. Connects directly to SharePoint + Salesforce data. No new tool to learn.

---

## Security & Permissions Model

| Data Type | Access Level | Who Can Edit | Who Can Read |
|---|---|---|---|
| Product catalog | Internal | R&D + Product Mgmt | All SmartDeck users |
| Stability data | Internal | R&D only | All SmartDeck users |
| Regulatory database | Restricted | Regulatory Affairs only | All SmartDeck users |
| Clinical data (Health) | Highly Restricted | Medical Affairs only | Health dept users only |
| Customer brief data | Confidential | Sales rep only | Sales + Marketing |
| Pricing data | Restricted | Commercial only | Sales + Product Mgmt |
| Win/loss data | Internal | Sales Ops | Marketing + Leadership |

---

## Performance Targets

| Operation | Target | Stretch |
|---|---|---|
| Brief submission → content retrieved | < 10 seconds | < 5 seconds |
| Full deck assembled by Copilot | < 3 minutes | < 90 seconds |
| Human review cycle | < 15 minutes | < 10 minutes |
| Total: brief → send-ready deck | < 30 minutes | < 20 minutes |
| Database query (semantic search) | < 2 seconds | < 1 second |
| System uptime | 99.5% | 99.9% |

---

*IFF SmartDeck Architecture · v0.1 · June 2026*
*Technical Design: Marketing Intern — Colors Solutions*
