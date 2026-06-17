# 🎨 IFF SmartDeck — AI-Powered Sales Presentation Engine

> **Transforming institutional knowledge into intelligent, real-time customer presentations across IFF's full product portfolio.**

![Status](https://img.shields.io/badge/Status-Prototype-orange) ![Phase](https://img.shields.io/badge/Phase-1%20MVP-blue) ![Departments](https://img.shields.io/badge/Departments-5-green) ![AI](https://img.shields.io/badge/AI-Copilot%20%2B%20GPT-purple)

---

## 📋 Table of Contents

1. [Why This Exists](#why-this-exists)
2. [The Problem We're Solving](#the-problem)
3. [Solution Overview](#solution)
4. [System Architecture](#architecture)
5. [Data Requirements by Department](#data-requirements)
6. [AI & Backend Workflow](#workflow)
7. [Department Coverage](#departments)
8. [Project Roadmap](#roadmap)
9. [Tech Stack](#tech-stack)
10. [Outcome & KPIs](#outcomes)

---

## 🎯 Why This Exists

IFF's Colors Solutions team and every commercial team across the company face the same problem: **the knowledge exists, but accessing and communicating it at scale is slow, inconsistent, and manual.**

When a food brand asks *"Can you help us replace Red 40 in our cereal?"*, the right IFF response requires:
- The correct color source from a 9 family portfolio
- Application-specific stability data
- Regional regulatory compliance
- A case study matching their product category
- A brand-consistent, visually compelling deck

Building that response takes **4–8 hours per pitch**. With hundreds of reformulation inquiries accelerating due to the FDA synthetic dye phase-out (2026 deadline), the team cannot scale manually.

**SmartDeck exists to close that gap.**

---

## 🔴 The Problem

```
CURRENT STATE

Customer RFQ arrives
        ↓
Sales rep emails R&D team for technical data     ← 1–2 day lag
        ↓
Marketing locates outdated slide library         ← inconsistent content
        ↓
Product manager assembles deck manually          ← 4–8 hours
        ↓
Regulatory checks done manually per region       ← error risk
        ↓
Deck goes out — sometimes wrong version          ← brand damage
        ↓
No feedback loop to improve next deck            ← no learning
```

**Impact:**
- Average pitch response time: 3–5 days
- Monthly deck capacity per commercial person: ~8–12
- Brand consistency errors: frequent (local teams create rogue versions)
- Institutional knowledge: locked in individuals, not systems

---

## ✅ Solution

**IFF SmartDeck** is a three-layer AI system:

```
LAYER 1 — STRUCTURED CONTENT DATABASE
   All product data, application specs, visuals, regulatory rules,
   case studies, and market intelligence — tagged, versioned, queryable

LAYER 2 — AI ORCHESTRATION ENGINE
   Reads the customer brief → selects the right content modules →
   applies regional rules → assembles the narrative logic

LAYER 3 — PRESENTATION GENERATION
   Microsoft 365 Copilot builds the branded deck from selected
   content → human reviews → exports in 30 minutes total
```

**Core outcome:** From customer brief to send-ready deck in **< 30 minutes**, consistently on-brand, technically accurate, regionally compliant.

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                        SMARTDECK PLATFORM                           │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌──────────────────┐     ┌──────────────────────────────────────┐  │
│  │  BRIEF INTAKE    │     │         DATA INGESTION LAYER         │  │
│  │  (Frontend)      │────▶│                                      │  │
│  │                  │     │  ┌──────────┐  ┌──────────────────┐  │  │
│  │  • Customer name │     │  │ R&D Feed │  │  Sales CRM Feed  │  │  │
│  │  • Category      │     │  │ (weekly) │  │  (real-time)     │  │  │
│  │  • Target shade  │     │  └──────────┘  └──────────────────┘  │  │
│  │  • Region        │     │  ┌──────────┐  ┌──────────────────┐  │  │
│  │  • Claim         │     │  │  Market  │  │   Regulatory     │  │  │
│  │  • Meeting type  │     │  │  Intel   │  │   Compliance DB  │  │  │
│  └──────────────────┘     │  └──────────┘  └──────────────────┘  │  │
│           │               └──────────────────────────────────────┘  │
│           ▼                              │                          │
│  ┌──────────────────────────────────────▼──────────────────────┐   │
│  │              CONTENT DATABASE (SharePoint / Azure)           │   │
│  │                                                              │   │
│  │  Products  │  Applications  │  Visuals  │  Case Studies      │   │
│  │  Regs      │  Market Data   │  Templates│  Win Stories       │   │
│  └──────────────────────────────────────────────────────────────┘   │
│           │                                                          │
│           ▼                                                          │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │              AI ORCHESTRATION ENGINE                         │   │
│  │                                                              │   │
│  │  ┌─────────────────┐   ┌──────────────┐   ┌─────────────┐  │   │
│  │  │ Content Selector│   │ Logic Engine │   │ NLG Module  │  │   │
│  │  │ (RAG / Vector   │   │ (Rule-based  │   │ (GPT-4o /   │  │   │
│  │  │  Search)        │   │ + ML ranking)│   │  Copilot)   │  │   │
│  │  └─────────────────┘   └──────────────┘   └─────────────┘  │   │
│  └──────────────────────────────────────────────────────────────┘   │
│           │                                                          │
│           ▼                                                          │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │         PRESENTATION GENERATION (PowerPoint Copilot)         │   │
│  │                                                              │   │
│  │  IFF Brand Template → Slide Assembly → Speaker Notes →       │   │
│  │  Compliance Check → Export (PPTX / PDF / Teams Live)         │   │
│  └──────────────────────────────────────────────────────────────┘   │
│           │                                                          │
│           ▼                                                          │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │              ANALYTICS & FEEDBACK LOOP                       │   │
│  │  Which slides used most → Win/loss tagging → Model improves  │   │
│  └──────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 📊 Data Requirements by Department

### How to read this section
Each department feeds the database differently. The table below defines **what data**, **in what format**, **from whom**, and **how frequently** it must be contributed.

---

### 🟠 1. Colors — Taste Division

**Why this department is the MVP focus:** Highest current commercial pressure (FDA synthetic dye ban). Most structured data. Clearest customer brief template.

| Data Type | Specific Fields | Source Owner | Format | Update Frequency |
|---|---|---|---|---|
| Product catalog | Color source, E-number, hue range, solubility, vegan Y/N | R&D / Product Management | Excel → SharePoint | Quarterly |
| Application matrix | Color × food segment × performance rating | Application Scientists | Structured spreadsheet | Monthly |
| Stability data | pH range, heat tolerance, light stability, shelf-life curve | R&D Lab | PDF reports + tabular | Per new trial |
| Shade library | Pantone/hex match, Delta-E to synthetic equivalent, photography | Lab + Marketing | Image files + metadata | Per product launch |
| Regulatory status | Approved regions, E-number, label declaration, restricted uses | Regulatory Affairs | Compliance database | Per regulation change |
| Usage levels | Min/max % by application, cost per kg, MOQ | Commercial / Supply Chain | Pricing database | Monthly |
| Case studies | Customer segment, challenge, color used, outcome, %improvement | Sales / Account Managers | Structured template | Per project close |
| Reformulation guides | Step-by-step by synthetic dye being replaced | Technical Marketing | Word docs → tagged | Per FDA update |

**Key dataset consideration:** Stability data is multi-dimensional (pH × temperature × time × light). Store as structured matrices, not PDF prose. This is the #1 data quality issue to solve first.

---

### 🟡 2. Flavours — Taste Division

**Why flavors need SmartDeck:** Flavor profiles are the most complex to communicate — masking, enhancement, and regional taste preferences all vary. Sales reps need to pair flavor and color solutions in combined pitches.

| Data Type | Specific Fields | Source Owner | Format | Update Frequency |
|---|---|---|---|---|
| Flavor catalog | Profile descriptor, category, application segment, regional preference score | Flavorists / R&D | Structured DB | Quarterly |
| Application pairing | Flavor × color × texture compatibility matrix | Application Scientists | Cross-reference table | Monthly |
| Sensory data | Consumer panel scores by region, preferred intensity levels | Consumer Insights | Anonymized dataset | Per study |
| Taste masking solutions | Off-note masked, protein system, recommended flavor partner | Technical Marketing | Tagged solution cards | Per innovation |
| Trend alignment | Top flavor trends by category and region (Mintel, proprietary) | Market Intelligence | API feed / report | Monthly |
| Regulatory | FEMA GRAS status, EU flavoring regulation, APAC approvals | Regulatory Affairs | Compliance DB | Per change |
| Win stories | Customer, category, challenge, solution, volume won | Sales | CRM-tagged | Per deal close |

---

### 🟣 3. Fragrance — Scent Division

**Use case in SmartDeck:** Consumer product companies (home care, personal care, beauty) need fragrance presentations that blend technical performance with emotional/sensory storytelling. Very different brief structure.

| Data Type | Specific Fields | Source Owner | Format | Update Frequency |
|---|---|---|---|---|
| Fragrance portfolio | Family, olfactory descriptor, key accords, mood profile | Perfumers / Creative | Structured catalog | Per collection launch |
| Consumer product application | Fragrance × end product (detergent, shampoo, candle) × region | Application Scientists | Matrix | Quarterly |
| Sustainability data | Natural origin %, biodegradable %, IFRA compliance, EWG rating | Sustainability / R&D | Certified data sheet | Annually |
| Sensory/emotional mapping | Scent → emotional association → target consumer profile | Consumer Insights | Research summary | Per study |
| LMR Naturals portfolio | Raw material origin, traceability certificate, sustainability story | LMR team | PDF + structured | Per crop season |
| Regulatory | IFRA standards, REACH (EU), California Prop 65 | Regulatory Affairs | Compliance DB | Per IFRA amendment |
| Trend data | Fine fragrance trends, consumer fragrance trends by region | Market Intelligence | Report summary | Quarterly |

---

### 🟢 4. Food Ingredients — Nourish Division

**Use case in SmartDeck:** Functional ingredients (emulsifiers, starches, proteins) need highly technical presentations — often for R&D and procurement audiences simultaneously. Data-heavy, regulatory-intensive.

| Data Type | Specific Fields | Source Owner | Format | Update Frequency |
|---|---|---|---|---|
| Ingredient catalog | Function, category, application, origin, clean label status | Product Management | Structured DB | Quarterly |
| Functional performance data | Emulsification efficiency, texture profile, water binding, heat behavior | R&D | Lab reports + tables | Per trial |
| Application test data | Ingredient × food system × process condition → performance outcome | Application Scientists | Structured results | Per study |
| Cost-in-use analysis | Ingredient cost vs. competitive benchmark, usage level required | Commercial | Excel model | Monthly |
| Clean label / label claims | Free-from list, organic certified, non-GMO verified, allergen status | Regulatory + Quality | Compliance DB | Per certification |
| Formulation guides | Dosage, order of addition, incompatibilities, synergies | Technical Marketing | Word → tagged cards | Per product |
| Market sizing | Category volume, reformulation trend data, customer pipeline | Market Intelligence | Mintel / Euromonitor | Quarterly |

---

### 🔵 5. Health & Bioscience — IFF Health Sciences Division

**Use case in SmartDeck:** This is the most specialized — clinical data, scientific publications, regulatory health claims. Presentations go to pharma-adjacent procurement, nutrition brands, and functional food companies.

| Data Type | Specific Fields | Source Owner | Format | Update Frequency |
|---|---|---|---|---|
| Probiotic portfolio (HOWARU®) | Strain ID, CFU, health endpoint, clinical trial reference | R&D / Medical Affairs | Scientific dossiers | Per study publication |
| Clinical data | Trial name, N size, endpoint, outcome, p-value, publication | Medical Affairs | Structured citations | Per paper |
| Botanical portfolio (CARE4U®) | Ingredient, standardization, health benefit, origin | Product Management | Structured catalog | Per launch |
| Health claim status | Approved claims by region (EU Article 13/14, FDA structure-function, EFSA) | Regulatory Affairs | Compliance DB | Per regulation update |
| Consumer research | Health concern by market, preferred delivery format, awareness levels | Consumer Insights | Report data | Biannually |
| Stability / formulation | Survival in food matrix, encapsulation technology, shelf-life | R&D | Lab reports | Per study |
| Competitor intelligence | Key probiotic brands, claim positioning, pricing | Market Intelligence | Analyst summary | Quarterly |

---

## 🔄 AI & Backend Workflow

### Step 1 — Brief Intake (30 seconds)

User fills the SmartDeck brief form:
```
FIELD               INPUT TYPE         EXAMPLE
─────────────────────────────────────────────
Company             Text               General Mills
Department          Dropdown           Colors | Flavours | Fragrance | Food Ingredients | Health
Category            Dropdown           Cereal & Confectionery
Target (optional)   Color picker / Text  Pink-red shade, replacing Red 40
Region              Multi-select       US / EU / APAC
Clean label claim   Checkbox           Clean label, No E-numbers, Vegan
Meeting type        Radio              Discovery / Technical / Commercial proposal
Urgency             Toggle             Standard (48h) / Urgent (2h) / Live (30 min)
```

---

### Step 2 — AI Orchestration Engine (the brain)

```python
# Pseudocode — what happens when the brief is submitted

def process_brief(brief):

    # 2a. INTENT CLASSIFICATION
    department = classify_department(brief)        # Colors, Flavours, etc.
    meeting_type = classify_meeting(brief)         # Discovery, Technical, Commercial
    complexity = assess_complexity(brief)          # Simple / Multi-color / Multi-region

    # 2b. CONTENT RETRIEVAL (RAG — Retrieval Augmented Generation)
    # Vector search over SharePoint content database
    products = retrieve_products(brief.target, brief.category, brief.region)
    case_studies = retrieve_case_studies(brief.category, brief.region)
    regulatory = retrieve_regulatory(products, brief.region)
    market_data = retrieve_market_context(brief.category, brief.region)
    visuals = retrieve_visuals(products, brief.category)

    # 2c. RULE ENGINE (deterministic guardrails)
    if brief.claim == "vegan":
        products = exclude(products, "carmine")   # Carmine not vegan
    if brief.region == "EU":
        regulatory_style = "E-number labeling"
    if brief.region == "US" and brief.category == "Food":
        include_slide("FDA_synthetic_dye_ban_context")
    if complexity == "multi-color":
        include_slide("color_system_overview")
        include_slide("color_matrix_by_application")

    # 2d. SLIDE MODULE SELECTION
    # Ranked by relevance score from retrieval + rule overrides
    slides = select_slide_modules(
        products, case_studies, regulatory,
        market_data, meeting_type, complexity
    )

    # 2e. NARRATIVE SEQUENCING
    # ACT structure: Context → Challenge → Solution → Proof → Action
    ordered_deck = apply_narrative_arc(slides)

    # 2f. CONTENT GENERATION
    # GPT-4o / Copilot writes headlines, transitions, speaker notes
    deck_content = generate_content(ordered_deck, brief, tone=meeting_type)

    return deck_content
```

---

### Step 3 — Content Database Query (what RAG searches)

Each piece of content in the database is tagged with metadata:

```json
{
  "content_id": "COL-ANT-BEV-US-001",
  "department": "Colors",
  "product": "Anthocyanins (grape-derived)",
  "application": "Beverage",
  "region": ["US", "EU"],
  "color_family": "Red / Purple",
  "vegan": true,
  "clean_label": true,
  "pH_stable_range": "3.0-4.5",
  "heat_stable": false,
  "claim_tags": ["clean-label", "natural", "plant-based"],
  "synthetic_replacement": ["Red 40", "Red 3"],
  "slide_type": "product_detail",
  "visual_asset": "anthocyanin_beverage_swatch.jpg",
  "last_updated": "2026-03-15",
  "approved_by": "R&D"
}
```

Semantic search on this metadata (using Azure AI Search or OpenAI embeddings) returns the most relevant content for any brief — not just keyword matching, but meaning-based retrieval.

---

### Step 4 — Presentation Generation

```
COPILOT PROMPT (auto-generated by SmartDeck engine):

"Create a [meeting_type] presentation for [company] using the following 
structured content. Apply IFF brand template. Department: [department].
Tone: [tone]. Slides selected: [slide_module_list].
Regional compliance: [region_rules]. Visual assets: [asset_list].
Add 3-sentence speaker notes to every slide. Total slides: [N]."
```

PowerPoint Copilot receives this instruction + content payload → generates the branded deck → saves to SharePoint → notifies the user.

---

### Step 5 — Analytics & Feedback Loop

Every deck generated logs:
```
- Which slides were selected
- Which slides were deleted by the human reviewer
- Whether the meeting resulted in a win/loss (CRM integration)
- Customer segment and region
- Time from brief to send
```

Over time, the model learns: *"For beverage customers in the US, the FDA regulatory slide + stability chart combination closes deals at 40% higher rate."* The system self-improves.

---

## 🏢 Department Coverage

| Department | Division | Brief Complexity | Data Volume | Priority |
|---|---|---|---|---|
| Colors | Taste | Medium | Large (stability matrices) | **Phase 1 — MVP** |
| Flavours | Taste | High | Very Large (sensory data) | Phase 2 |
| Food Ingredients | Nourish | Very High | Very Large (functional data) | Phase 2 |
| Fragrance | Scent | High | Large (LMR + consumer) | Phase 3 |
| Health & Bioscience | Health Sciences | Very High | Large (clinical data) | Phase 3 |

**Combined estimated database size at full scale:**
- ~2,000 product entries
- ~15,000 application data points
- ~500 case studies
- ~200 regulatory rules per region
- ~5,000 visual assets
- ~1,000 market intelligence data points

---

## 📅 Project Roadmap

### Phase 0 — Foundation (Weeks 1–6)
*"Know what you have before you build."*

```
MILESTONE                           OWNER           WEEK
─────────────────────────────────────────────────────
Audit existing slide libraries       Marketing        W1-2
Map all data sources per dept        Intern + R&D     W1-3
Define content tagging taxonomy      Intern + IT      W2-4
Design SharePoint folder structure   IT + Marketing   W3-5
Stakeholder alignment workshop       Marketing Lead   W4
Brief intake form v1 design          Intern           W5-6
```

**Deliverable:** Data architecture document + approved taxonomy + SharePoint structure skeleton

---

### Phase 1 — MVP: Colors Department (Weeks 7–14)
*"Prove it works on the highest-priority department."*

```
MILESTONE                           OWNER           WEEK
─────────────────────────────────────────────────────
Migrate Colors product catalog       R&D + Intern     W7-8
Build 9-color stability matrix       R&D + Intern     W7-9
Upload 50 visual assets (tagged)     Marketing        W8-10
Build 10 core slide modules          Intern           W9-11
Write IF/THEN rule set (v1)          Intern           W10-12
Connect Copilot to SharePoint        IT               W11-13
Test with 3 real customer briefs     Sales team       W13-14
```

**Deliverable:** Working SmartDeck prototype for Colors — generates a branded deck from a brief in < 30 minutes

**Success metric:** 3 test decks reviewed by Mathilde's team with >80% content accuracy

---

### Phase 2 — Expansion: Flavours + Food Ingredients (Weeks 15–24)
*"Scale the model to the next two departments."*

```
MILESTONE                           OWNER           WEEK
─────────────────────────────────────────────────────
Flavours data migration              R&D Flavours     W15-17
Food Ingredients data migration      R&D Food Ing.    W15-18
Cross-department brief (Color+Flavor)Intern           W17-19
RAG vector search implementation     IT / AI team     W18-21
Multi-region logic expansion         Intern + Legal   W19-22
Analytics dashboard v1               IT + Intern      W22-24
```

**Deliverable:** SmartDeck covering 3 departments, with semantic search + multi-region rules

---

### Phase 3 — Full Platform: Fragrance + Health & Bioscience (Weeks 25–36)
*"Complete the IFF product portfolio coverage."*

```
MILESTONE                           OWNER           WEEK
─────────────────────────────────────────────────────
Fragrance portfolio integration      Scent Marketing  W25-28
Health & Bioscience clinical data    Medical Affairs  W25-30
Feedback loop ML model (v1)          AI team          W28-32
CRM integration (win/loss tagging)   Sales Ops + IT   W30-34
Global rollout training              Marketing        W33-36
```

**Deliverable:** Full IFF SmartDeck platform — all 5 departments, self-improving feedback loop, CRM integration

---

### Phase 4 — Optimize & Scale (Month 10–12)
*"Make the system better than any single person."*

- Personalization: system learns per sales rep's style
- Real-time market data integration (Mintel API, Euromonitor API)
- Auto-translation for regional languages (FR, DE, ES, ZH, PT)
- Teams integration: deck auto-shared to meeting invite
- Customer portal: client-facing version with IFF-branded access

---

## 🛠️ Tech Stack

| Layer | Technology | Why |
|---|---|---|
| Content Database | Microsoft SharePoint + Azure Blob Storage | Enterprise-grade; integrates natively with Copilot; IFF likely already uses M365 |
| Search & Retrieval | Azure AI Search (vector + semantic) | Handles large unstructured data; scales to 15,000+ data points |
| AI Content Selection | GPT-4o via Azure OpenAI (private deployment) | No data leaves IFF's Azure tenant — critical for commercial confidentiality |
| Logic/Rules Engine | Microsoft Copilot Studio (Power Automate) | No-code rule building; can be maintained by marketing team without IT |
| Presentation Output | PowerPoint + Microsoft 365 Copilot | Native M365 integration; brand template support; no third-party dependency |
| Brief Intake Form | Microsoft Forms or Power Apps | Zero infrastructure cost; M365 native; easy to iterate |
| Analytics | Power BI | Native M365; connects to SharePoint + CRM data |
| CRM Integration | Salesforce API or Microsoft Dynamics | Pulls customer context; logs deck sends; tracks win/loss |
| Rapid Prototyping | Gamma AI | Fast iteration for new slide modules before formal database entry |
| Version Control | GitHub | Tracks rule set changes, taxonomy updates, prompt engineering iterations |

---

## 📈 Outcomes & KPIs

### Efficiency Outcomes

| Metric | Baseline | Target (Phase 1) | Target (Full Platform) |
|---|---|---|---|
| Deck build time | 4–8 hours | < 30 minutes | < 15 minutes |
| Decks per person/month | 8–12 | 40–50 | 80–100 |
| Brief-to-send time | 3–5 days | Same day | < 2 hours |
| Brand compliance errors | Frequent | Rare | Near-zero |
| Regulatory errors | Possible | Rule-enforced | Automated |

### Commercial Outcomes

| Metric | Current | Target |
|---|---|---|
| RFQ response rate | ~60% in time | >95% in time |
| Cross-sell in decks | Manual (inconsistent) | Automated (rule-based) |
| New product in deck | Weeks (manual) | Real-time (database) |
| Win rate (tracked) | Not tracked | Tracked + used to improve |

### Strategic Outcomes

- IFF's institutional knowledge moves from **individual brains → permanent, queryable system**
- Global teams (US, EU, APAC, LatAm) generate locally-accurate decks without Paris team involvement
- New sales reps become productive in **days, not months** (SmartDeck is their knowledge base)
- R&D innovation reaches sales 10x faster (new product → database → all decks overnight)

---

## 👩‍💻 Contribution Guide (Internal Departments)

### How R&D contributes data

1. Download the **IFF SmartDeck Data Template** from SharePoint: `[SmartDeck] > Templates > [Department]`
2. Complete required fields (marked with *) — optional fields improve AI accuracy
3. Upload completed template to: `[SmartDeck] > Incoming Data > [Department] > [Month]`
4. Marketing intern reviews + tags → promoted to live database within 48h

### How Sales contributes case studies

1. Complete the **Case Study Card** in Salesforce (SmartDeck custom object) immediately after project close
2. Fields: customer segment (anonymized), category, challenge, color/product used, outcome metrics, quotable result
3. Auto-synced to SmartDeck database — available in all future relevant decks within 24h

### How Marketing maintains the system

- Monthly: review incoming data submissions, tag and approve
- Quarterly: audit slide module performance (which slides are removed most → flag for improvement)
- Per product launch: add new product to database within 1 week of launch

---

## 🗒️ Intern Scope (6-Month Contribution)

| Month | Focus | Deliverable |
|---|---|---|
| 1 | Data audit + taxonomy design | Architecture document + SharePoint structure |
| 2 | Colors database migration | 9 color families fully tagged and loaded |
| 3 | Slide module library build | 30+ reusable slide modules for Colors |
| 4 | Rule engine v1 + Copilot connection | Working brief → deck prototype |
| 5 | Test + iterate with sales team | 10 real briefs tested; accuracy scorecard |
| 6 | Phase 2 prep + documentation | Flavours data template + handover system guide |

---

*IFF SmartDeck — Built by the Colors Solutions Marketing Team, Neuilly-sur-Seine*
*Version 0.1 — June 2026*
