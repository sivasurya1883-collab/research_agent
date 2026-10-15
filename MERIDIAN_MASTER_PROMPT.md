# MASTER PROMPT: Meridian FinSight v3.0 (Production-Ready Edition)
## Institutional Equity Research Cockpit for Middle-Market Insurance Brokerage

---

### 1. Executive Role & Platform Objective
**Role:** You are an elite AI Solutions Architect and Full-Stack Quantitative Systems Engineer. Your objective is to build **Meridian FinSight v3.0**, an institutional-grade, production-ready equity research and fundamental analysis platform for the investment firm **Meridian**.

**Firm Mandate:** Growth at a Reasonable Price (GARP) with strict Free Cash Flow (FCF) yield floors ($\ge 4.0\%$), defensive balance sheets ($\text{Debt/EBITDA} < 2.5\text{x}$), and secular tailwinds in middle-market property & casualty (P&C) insurance brokerage, risk advisory, and specialty binding programs.

**Core Objective:** Empower senior business analysts and investment committees to select a coverage company from our 8-broker universe (or input custom theses), run a one-click fundamental analysis (**"Analyze ME"**), verify audited SEC EDGAR regulatory evidence with live accession hyperlinks, benchmark performance against public and private rivals in an interactive **Peer Comps Cockpit**, explore relational market dynamics in a **3 Core Pillars Strategic Intelligence Network**, generate institutional research memoranda, and consult with **"Business Buddy"**, an interactive floating plug-out advisor.

---

### 2. Coverage Universe: 8 Middle-Market Commercial P&C Brokers
The system must come pre-configured with the official 8 middle-market insurance brokers:

1. **Brown & Brown, Inc. (`BRO`):** Public market leader (NYSE: BRO, CIK 0000079282). Middle-market commercial P&C, National Programs MGA binding authority.
2. **Lockton Companies (`PRIV-LOCK`):** Largest independent, privately owned global broker; high organic growth, low leverage.
3. **NFP Corp. (`NFP`):** Mid-market corporate benefits, wholesale specialty, and P&C advisory (acquired by Aon).
4. **TIH / Truist Insurance Holdings (`PRIV-TIH`):** Wholesale broking and MGA specialty programs (CRC Group, Stone Point / CD&R).
5. **Alliant Insurance Services (`PRIV-ALLI`):** High-growth national specialty brokerage (Construction, Agribusiness, Public Entity; Stone Point / CDPQ).
6. **Acrisure LLC (`PRIV-ACRI`):** Rapid programmatic retail brokerage roll-up and AI fintech platform.
7. **USI Insurance Services (`PRIV-USI`):** Middle-market commercial brokerage and risk consulting (USI ONE Advantage; KKR / CDPQ).
8. **AssuredPartners (`PRIV-AP`):** High-volume middle-market programmatic agency consolidator (GTCR).

---

### 3. Production Tech Stack & Architecture
* **Frontend:** Next.js 14 (App Router) + React 18 + TypeScript + Tailwind CSS.
  - Iconography: `lucide-react`.
  - Design Philosophy: Dark mode Bento Grid, frosted-glass backdrop blur, atmospheric glows, high-chroma semantic badges.
* **Backend:** Python 3.12+ FastAPI running asynchronously on `http://127.0.0.1:8000`.
* **Graph Engine:** NetworkX (Python-based local graph engine) for relational 3-pillar entity and risk factor modeling.
* **Regulatory Data Pipeline:** Local bulk SEC EDGAR parser reading directly from unzipped `Resources/companyfacts/CIK*.json` files (490+ US-GAAP concepts per issuer).
* **Storage & Caching:** SQLite database (`meridian_research.db`) caching corporate fundamentals, research runs, and entity schemas.
* **Language Model & Inference:** Gemini 2.5 Pro via enterprise API gateway (`https://genailab.tcs.in/v1`) with corporate proxy SSL handling (`verify=False`), paired with an **Interactive Context-Aware Business Analyst Fallback Engine** guaranteeing dynamic, non-repetitive responses.

---

### 4. 3 Core Pillars Knowledge Graph Schema
The NetworkX relational graph must strictly aggregate data across three institutional pillars:

```yaml
Target_Schema:
  Core_Pillars:
    - Business_News:
        sub_categories: [Events, Sentiment, Market Dynamics]
        metrics: [Commercial rate hardening, client renewal retention (94%+), M&A cadence, surplus lines property adequacy]
    - Tech:
        sub_categories: [Tech Architecture, IP, Innovation, Tech Risks]
        metrics: [Digital agency management APIs, catastrophe loss analytics IP, cyber broking automation, carrier binding interfaces]
    - Finance_Operations:
        sub_categories: [Financial Metrics, FCF, Balance Sheet, Cost Drivers]
        metrics: [Gross commission revenue, EBITDAC margins, Debt/EBITDA multiple, FCF yield, producer compensation inflation]
```

**Relational Graph Mapping:**
- Bidirectional nodes and edges connecting: `Target Company` $\leftrightarrow$ `Strategy Rules` $\leftrightarrow$ `Pillar Nodes` $\leftrightarrow$ `Peers` $\leftrightarrow$ `Financial Metrics` $\leftrightarrow$ `Risk Factors`.
- Export clean JSON payloads (`nodes`, `links`, `core_pillars`, `connections_summary`) consumable by frontend interactive visualizers.

---

### 5. UI/UX & Production-Ready Language Standards
* **Strict Business Analyst Tone:** **Zero developer or technical jargon across the entire application.**
  - ❌ *Banned terms:* "FastAPI", "NetworkX DiGraph", "Agent Swarm", "Multi-Agent Swarm", "Orchestrator Pipeline", "Research Synthesis Pipeline", "SSL Bypass", "LangChain".
  - ✅ *Required terms:* "Fundamental Research", "Institutional Research Platform", "Strategic Intelligence Network", "Audited SEC EDGAR Data", "GARP & FCF Compounding Strategy", "Peer Comps & Benchmarking", "Business Buddy".
* **Visual Palette:**
  - Background: Deep canvas (`#0B0E14` / `#0F172A`).
  - Cards: Translucent glass (`bg-surface-card/85 backdrop-blur-xl border border-surface-border`).
  - Accents: Electric Sky Cyan (`#38BDF8`), Mint Emerald (`#10B981`), High-Chroma Magenta (`#E879F9`), Vivid Amber (`#F59E0B`), Rose Coral (`#F43F5E`).

---

### 6. Five Core Dashboard Modules

#### Module 1: Thesis Studio & Execution
- **Input Controls:** Company preset selector (8 brokers), customizable investment thesis, portfolio holdings context, investment horizon (`4Q`, `8Q`, `12Q`), and mandate mode.
- **Action Button:** Single prominent, full-width button labeled **`"Analyze ME"`** (transitions to animated **`"Analyzing ME..."`** during execution).
- **Meridian Compatibility Bento Tile:**
  - Overall Compatibility Score ($0–100\%$).
  - High-chroma verdict badge: **Strong Buy** (Emerald), **Hold** (Amber), **Pass** (Rose).
  - 3 Core Pillar breakdown cards showing individual scores, alignment statuses, and investment rationale.
  - 4 Mandate rule checks: FCF Yield ($\ge 4.0\%$), Debt/EBITDA ($< 2.5\text{x}$), Middle-Market P&C Tailwinds, and GARP Margin Discipline.
- **4 Bento Metric Cards:**
  - Revenue, Adjusted EBITDA Margin, Debt/EBITDA Multiple, Free Cash Flow Yield.
  - **Explicit Source Provenance Badges:** Each card must state its audited source (e.g., `SOURCE: SEC Form 10-Q | CIK 0000079282`).
- **Bull vs. Bear Catalyst Matrix:**
  - Bull Case (Emerald high-chroma): Catalysts, target upside price, and probability.
  - Bear Case (Rose high-chroma): Downside vectors, risk stop price, and probability.

#### Module 2: Structured Investment Memorandum with Clickable Evidence
- **Audited Regulatory Sources & Filing Evidence Table:**
  - Extracts audited line items directly from local XBRL files (`us-gaap:Revenues`, `us-gaap:NetCashProvidedByUsedInOperatingActivities`, `us-gaap:LongTermDebtNoncurrent`, `us-gaap:OperatingIncomeLoss`, `us-gaap:Assets`, `us-gaap:StockholdersEquity`).
  - Lists audited reported values, forms (`10-Q`, `10-K`), reporting periods, filing dates, and accession numbers (`0001193125-26-318251`).
  - **Clickable URLs:** Every accession number and CIK is an active hyperlink opening the official SEC EDGAR repository.
- **Scraped Web Intelligence & Industry Source Evidence Panel:**
  - Aggregates verified trade journalism (Insurance Journal, Business Insurance, AM Best).
  - Each item displays publication name, date, snippet, and a **clickable web URL** (`<a href="..." target="_blank">`) with an external link icon.
- **5-Section Institutional Structure:**
  1. Executive Summary & Thesis Validation (with confidence score)
  2. Strategic Fit with Meridian Mandate
  3. Regulatory Disclosures & SEC Filing Evidence (Item 1A Risk Factors & Item 7 MD&A)
  4. Earnings Commentary & Management Sentiment
  5. Final Recommendation & Portfolio Action
- **Export Controls:** One-click **Print / PDF** and **Copy Markdown**.

#### Module 3: Strategic Intelligence Network
- Visual interactive node graph categorized by the 3 Core Pillars (`Business_News`, `Tech`, `Finance_Operations`).
- Interactive filter bar to isolate individual pillars.
- Entity detail inspector showing node category, connected edges, and financial metadata.

#### Module 4: Peer Comps & Quantitative Benchmarking Cockpit
- Dedicated navigation access via the floating vertical dock (`BarChart3` icon) and header nav.
- **4 Industry Median Benchmark Cards:** Compares target company metrics against peer medians for EBITDAC Margin, Leverage, FCF Yield, and Organic Growth.
- **Sortable, Filterable Universe Matrix:**
  - Covers all 8 brokers with structure tags (`Public Listed`, `Private Equity Backed`, `Private Independent`).
  - Sort dynamically by Revenue, Organic Growth, EBITDAC Margin, Debt/EBITDA, FCF Yield, or Meridian Score.
  - Compliant vs. non-compliant color coding against mandate hurdles.
  - Click any row to dynamically switch the active target company.

#### Module 5: "Business Buddy" Floating Plug-Out Advisor
- Floating launch pill anchored at the bottom-right of the viewport.
- Slide-out glassmorphic drawer widget.
- **Universal, Generic Greeting:** Welcomes the analyst to commercial P&C brokerage advisory without hardcoding any single company name.
- **Adaptive Quick Prompt Chips:**
  - *"How does this broker's FCF yield compare to the 4% mandate?"*
  - *"Is the Debt/EBITDA multiple safely below the 2.5x ceiling?"*
  - *"Compare this company with peer roll-ups and competitors"*
  - *"What are the key risk factors and bear vectors?"*
  - *"What is our Price Target & valuation upside?"*
- **Dynamic, Non-Repetitive Response Engine:**
  - Evaluates the user's specific query intent (leverage, cash flow, peer comps, valuation, risks, catalysts, SEC filings).
  - Injects real figures from the active broker's financial model and compares them directly to mandate hurdles.
  - Zero canned boilerplate or identical repeated text.

---

### 7. Backend API Specification
The FastAPI backend must provide the following documented endpoints:

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/health` | Service health, SQLite database status, and SEC resources availability. |
| `GET` | `/api/presets` | List of the 8 official middle-market insurance brokers with fundamentals. |
| `GET` | `/api/sec-evidence/{target_id}` | Detailed audited SEC EDGAR line items, accession numbers, and XBRL concepts from local companyfacts. |
| `GET` | `/api/knowledge-graph/{target_id}` | NetworkX 3-pillar graph payload (nodes, edges, summary). |
| `POST` | `/api/research/analyze` | Executes complete fundamental research analysis; returns scores, pillar alignment, financial facts, scenarios, memo markdown, and SEC evidence. |
| `POST` | `/api/chat-copilot` | Business Buddy interactive conversational advisory endpoint. |

---

### 8. Verification & Acceptance Criteria
1. **Zero Technical Jargon:** Dashboard passes a full audit for business analyst readability.
2. **Action Button:** The primary analysis button is clearly labeled `"Analyze ME"`.
3. **Audited SEC Evidence:** For public issuers (e.g. Brown & Brown), figures must reconcile with local `Resources/companyfacts/CIK0000079282.json` and display clickable SEC EDGAR links.
4. **Clickable Web Sources:** Scraped market news must provide live, clickable web URLs to industry news publications.
5. **Peer Comps:** The side panel and header nav include the Peer Comps icon opening the quantitative benchmarking cockpit.
6. **Business Buddy:** Floating plug-out launches cleanly, greets generically, and provides dynamic, interactive, question-specific answers without repeating static phrases.
7. **Test Suite:** Automated tests (`pytest tests/test_meridian_system.py`) pass at 100% with zero regressions.
8. **Execution:** Runs locally with FastAPI (`port 8000`) and Next.js (`port 3000`).
