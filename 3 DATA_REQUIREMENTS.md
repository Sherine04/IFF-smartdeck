# 📊 IFF SmartDeck — Data Requirements by Department

> This document defines exactly what data is needed, in what format, from which team, and how it feeds the AI engine. Every field listed here becomes a queryable attribute in the SmartDeck content database.

---

## How the Database Is Structured

Every piece of content stored in SmartDeck has two layers:

**Layer 1 — The Content** (what gets put in the deck)
> Product spec, case study text, regulatory rule, market statistic, visual asset

**Layer 2 — The Metadata Tags** (what the AI uses to find and select it)
```json
{
  "content_id":     "COL-ANT-BEV-US-001",
  "department":     "Colors",
  "product":        "Anthocyanins (grape-derived)",
  "application":    "Beverage",
  "region":         ["US", "EU"],
  "vegan":          true,
  "clean_label":    true,
  "synthetic_replaces": ["Red 40", "Red 3"],
  "meeting_type":   ["discovery", "technical", "commercial"],
  "slide_type":     "product_detail",
  "data_owner":     "R&D Colors",
  "last_reviewed":  "2026-03-15"
}
```

---

## Department 1: Colors (Taste Division)
**Priority: Phase 1 — MVP**
**Brief complexity: Medium | Data volume: Large**

### Why first
Highest commercial pressure due to the FDA synthetic dye phase-out. Most structured data type (stability matrices are quantitative). Clearest brief template from sales team.

### Required Datasets

#### 1A. Product Catalog
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Color name + E-number | Official name and EU designation | Text | R&D | Quarterly |
| Hue range | Min–max hex or Pantone range | Color codes | R&D + Marketing | Per launch |
| Solubility | Water-soluble / oil-dispersible / emulsion | Dropdown | R&D | Per product |
| Vegan status | Yes / No / Conditionally | Boolean | Regulatory | Per product |
| Clean label | Yes / No | Boolean | Regulatory | Per product |
| Synthetic equivalents | Which synthetic dyes this replaces | Multi-select | R&D | Per product |

#### 1B. Stability Matrix (the most critical dataset)
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| pH stability range | Min–max pH where color holds | Numeric range | R&D | Per trial |
| Heat tolerance | Max °C before degradation | Numeric | R&D | Per trial |
| Light stability | Low / Medium / High | Rating | R&D | Per trial |
| Shelf-life curve | % intensity at 3 / 6 / 12 months | Time-series table | R&D | Per trial |
| Food matrix | Which food system tested in | Multi-select | Application Scientists | Per trial |

**Critical note:** This data currently lives in PDF lab reports. It must be extracted into structured tables — this is the #1 data quality task for Phase 1. An Excel template will be provided to R&D for submission.

#### 1C. Application Matrix
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Color × segment performance | Rating per application (dairy, bakery, etc.) | Structured matrix | Application Scientists | Monthly |
| Recommended usage level | % min–max by application | Numeric | R&D | Per product |
| Processing compatibility | Extrusion / panning / UHT / fermentation | Checkbox | Application Scientists | Per study |
| Cost-in-use | EUR/kg at standard usage level | Numeric | Commercial | Monthly |

#### 1D. Shade Library
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Product photography | Studio shot of color in application | .jpg/.png (min 3MB) | Marketing | Per launch |
| Shade comparison visual | Natural vs synthetic side-by-side | .jpg/.png | R&D + Marketing | Per product |
| Delta-E value | Color difference vs synthetic target | Numeric | R&D | Per trial |
| Mood board | Lifestyle/brand imagery for that color | .jpg set | Marketing | Per collection |

#### 1E. Regulatory Database
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| FDA status | Approved / Petition pending / Not approved | Status | Regulatory Affairs | Per regulation |
| EFSA status | E-number assigned / Under review | Status | Regulatory Affairs | Per regulation |
| APAC approvals | Japan / China / ASEAN status | Per-country table | Regulatory Affairs | Annually |
| Label declaration | Exact label text required per region | Text | Regulatory Affairs | Per change |
| Restricted uses | Any application or level restrictions | Text | Regulatory Affairs | Per change |

#### 1F. Case Studies
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Customer segment | Anonymized (e.g. "Global beverage brand") | Text | Sales | Per project close |
| Category | Beverage / Dairy / Bakery / Confectionery etc. | Dropdown | Sales | Per close |
| Challenge | What synthetic they were replacing | Text | Account Manager | Per close |
| Color solution | Which IFF color(s) used | Multi-select | Technical | Per close |
| Outcome | Quantified result (e.g. "18% shelf premium") | Text + metric | Account Manager | Per close |
| Timeline | Brief to commercial launch duration | Weeks | Sales | Per close |

---

## Department 2: Flavours (Taste Division)
**Priority: Phase 2**
**Brief complexity: High | Data volume: Very Large**

### Why flavors require special handling
Flavor is the most subjective category — regional taste preferences vary enormously (sweet profiles differ between US, EU, and APAC). Sensory data is qualitative by nature and requires careful structuring.

### Required Datasets

#### 2A. Flavor Catalog
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Flavor descriptor | e.g. "Sweet strawberry with jammy base note" | Text | Flavorists | Per launch |
| Flavor family | Fruit / Dairy / Savory / Sweet / Bitter | Taxonomy | Product Mgmt | Per launch |
| Application segment | Beverage / Dairy / Bakery / Confectionery | Multi-select | Application Scientists | Per launch |
| Regional preference score | 1–5 by region (US, EU, APAC, LatAm) | Numeric matrix | Consumer Insights | Per study |
| Kosher / Halal | Certified Y/N | Boolean | Regulatory | Per product |

#### 2B. Sensory & Consumer Data
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Consumer panel scores | Liking score by country and age group | Numeric dataset | Consumer Insights | Per study |
| Preferred intensity | Optimal usage level by application | Numeric | Consumer Insights | Per study |
| Off-note profile | What negative notes exist if over-dosed | Text | Flavorists | Per product |

#### 2C. Masking Solutions
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Off-note masked | e.g. "Protein bitterness", "HMO sweetness" | Text | Technical Marketing | Per solution |
| Recommended flavor partner | Which IFF flavor masks the noted off-note | Product reference | Flavorists | Per solution |
| Protein system | Works with / Against (soy, pea, whey) | Matrix | Application Scientists | Per trial |

#### 2D. Trend Alignment
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Top flavor trend | e.g. "Yuzu, Tajín, Pistachio" by category+region | Ranked list | Market Intelligence | Monthly |
| Source | Mintel report / Euromonitor / PANOPTIC | Citation | Market Intelligence | Monthly |
| Trend maturity | Emerging / Growing / Mainstream / Declining | Status | Market Intelligence | Monthly |

---

## Department 3: Food Ingredients (Nourish Division)
**Priority: Phase 2**
**Brief complexity: Very High | Data volume: Very Large**

### Critical distinction
Food Ingredients presentations often go simultaneously to R&D and Procurement audiences — meaning the same deck needs a technical layer AND a commercial layer. SmartDeck must handle this dual audience logic.

### Required Datasets

#### 3A. Ingredient Catalog
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Ingredient name + function | e.g. "GRINDSTED® Pectin — gelation / texture" | Text | Product Mgmt | Quarterly |
| Category | Emulsifier / Hydrocolloid / Protein / Enzyme / Starch | Taxonomy | Product Mgmt | Per launch |
| Clean label status | Natural / Organic / Non-GMO / Allergen-free | Multi-flag | Regulatory + Quality | Per certification |
| Origin | Plant-derived / Microbial / Animal | Category | R&D | Per product |

#### 3B. Functional Performance Data
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Emulsification efficiency | % oil-in-water stability at standard dose | Numeric | R&D | Per trial |
| Texture profile | Firmness / Viscosity / Gel strength at dose | Numeric table | R&D | Per trial |
| Water binding capacity | g water per g ingredient | Numeric | R&D | Per trial |
| Heat behavior | Thermal stability profile | Chart data | R&D | Per trial |
| Synergy / Incompatibility | Works with / Against other ingredients | List | Application Scientists | Per study |

#### 3C. Cost-in-Use Model
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Ingredient cost per kg | EUR/kg at standard commercial volume | Numeric | Commercial | Monthly |
| Usage level required | % in finished product | Numeric range | R&D | Per product |
| Cost vs competitor benchmark | % premium or discount vs leading alternative | Index | Commercial | Quarterly |

---

## Department 4: Fragrance (Scent Division)
**Priority: Phase 3**
**Brief complexity: High | Data volume: Large**

### What makes fragrance different
Fragrance presentations must balance technical performance with emotional/sensory storytelling. The brief includes a "mood" dimension not present in other departments — and the visual assets (mood boards, lifestyle photography) are as important as the data.

### Required Datasets

#### 4A. Fragrance Portfolio
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Fragrance name | Internal and commercial name | Text | Perfumers | Per launch |
| Olfactory family | Floral / Woody / Fresh / Oriental / Gourmand | Taxonomy | Perfumers | Per launch |
| Key accords | e.g. "bergamot, cedar, musk" | Comma-separated | Perfumers | Per launch |
| Mood profile | Emotion this scent evokes | Tag list | Creative | Per launch |
| Target consumer | e.g. "25–40F, premium household, EU" | Audience profile | Consumer Insights | Per launch |

#### 4B. Sustainability & Compliance
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Natural origin % | % of formula from natural sources | Numeric | Sustainability | Per formula |
| Biodegradable % | Biodegradability rating | Numeric | Sustainability | Per formula |
| IFRA compliance | Compliant / Under review / Restricted | Status | Regulatory | Per IFRA update |
| EWG rating | Score 1–10 | Numeric | Regulatory | Per formula |

#### 4C. LMR Naturals Specifics
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Raw material origin | Country + farm partner | Text | LMR team | Per crop season |
| Traceability certificate | Audit trail document | PDF link | LMR team | Per harvest |
| Sustainability story | Farmer partnership narrative | Text | Sustainability + LMR | Annually |

---

## Department 5: Health & Bioscience (Health Sciences Division)
**Priority: Phase 3**
**Brief complexity: Very High | Data volume: Large**

### Critical compliance note
Health & Bioscience data includes clinical trial results and health claims. **All content in this department requires sign-off from Medical Affairs before it is uploaded to the database.** No clinical claim goes into a deck without this approval gate.

### Required Datasets

#### 5A. Probiotic Portfolio (HOWARU®)
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Strain ID | ATCC/NCIMB designation | Text | R&D | Per strain |
| CFU at end of shelf life | Colony forming units at expiry | Numeric | R&D | Per batch |
| Health endpoint | e.g. "Gut barrier function", "Immune response" | Taxonomy | Medical Affairs | Per study |
| Clinical trial reference | Study name, DOI, N size, outcome | Citation | Medical Affairs | Per publication |
| Delivery format | Capsule / powder / food matrix | Multi-select | R&D | Per format |

#### 5B. Health Claims Database
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Claim text | Exact approved claim wording | Text | Regulatory | Per approval |
| Claim type | EU Article 13 / EU Article 14 / FDA structure-function | Category | Regulatory | Per approval |
| Region approved | US / EU / APAC specific | Multi-select | Regulatory | Per change |
| Supporting study | DOI / Publication | Citation | Medical Affairs | Per paper |
| Restrictions | Any dosage, population, or format restrictions | Text | Regulatory | Per approval |

#### 5C. Consumer Health Research
| Field | Description | Format | Owner | Frequency |
|---|---|---|---|---|
| Health concern by market | Top 5 concerns by country | Ranked list | Consumer Insights | Biannually |
| Preferred delivery format | Consumer preference for supplement vs food | % breakdown | Consumer Insights | Biannually |
| Awareness level | % aware of probiotic/prebiotic category by market | Numeric | Consumer Insights | Biannually |

---

## Data Quality Standards (applies to all departments)

### Acceptance Criteria
A content submission is accepted into SmartDeck only if:
- [ ] All required fields (*) are completed
- [ ] Data owner is identified
- [ ] Regulatory/quality sign-off obtained (for claims and clinical data)
- [ ] Visual assets meet resolution minimum (3MB, RGB, 16:9 crop available)
- [ ] Content has been reviewed within the last 12 months

### Rejection Criteria (will not be uploaded)
- Data in PDF prose format — must be extracted to structured tables
- Claims without regulatory approval citation
- Stability data not linked to a specific product + application combination
- Case studies with identifiable customer names (must be anonymized)

### Update Protocol
```
New data submitted
       ↓
Marketing Intern reviews within 48h
       ↓
Dept head spot-check (weekly batch)
       ↓
Uploaded to SharePoint with metadata tags
       ↓
Live in SmartDeck within 5 business days
       ↓
Quarterly full database review by Marketing Lead
```

---

## Database Scale Projection

| Department | Products | App Data Points | Case Studies | Regulatory Rules | Visual Assets |
|---|---|---|---|---|---|
| Colors | ~200 | ~2,500 | ~150 | ~80 | ~1,500 |
| Flavours | ~800 | ~5,000 | ~200 | ~60 | ~800 |
| Food Ingredients | ~400 | ~4,000 | ~100 | ~120 | ~600 |
| Fragrance | ~500 | ~2,000 | ~80 | ~100 | ~1,500 |
| Health & Bioscience | ~100 | ~1,500 | ~50 | ~150 | ~300 |
| **TOTAL** | **~2,000** | **~15,000** | **~580** | **~510** | **~4,700** |

**Estimated Azure AI Search index size:** ~50–80GB structured + unstructured content
**Query response time target:** < 2 seconds per brief

---

*IFF SmartDeck Data Requirements · v0.1 · June 2026*
*Owner: Marketing Intern — Colors Solutions, Neuilly-sur-Seine*
