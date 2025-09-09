## BEP Supply Chain Knowledge Set (Synthetic)

- **Purpose**: Seed data and concise knowledge for spinning up an Agent in Agentforce to answer questions about Bureau of Engraving and Printing (BEP) supply chain operations.
- **Scope**: Vendors, materials, facilities, inventory, and purchase orders; SOPs, policies, KPIs, disruption playbooks, FAQs.
- **Disclaimer**: This content and data are entirely synthetic and for testing/training. They do not represent official US Government information.

### Files
- The folder provides:
  - Knowledge docs for RAG grounding, policies, KPIs, SOPs, and test prompts.
  - CSV datasets for vendors, materials, facilities, inventory, and POs with defined join keys for analytics and decisioning.
- Knowledge: Markdown articles in `Agentforce/Knowledge`.
- Data: CSVs in `Agentforce/Data`.


### What each Knowledge doc is for
- **`Knowledge/00_readme.md`**: Project purpose, quick start, and suggested agent settings (semantic chunking, citations, guardrails).
- **`Knowledge/data_dictionary.md`**: Canonical schema for all CSVs, join keys, and common calculations. Use this to ground structured queries and enforce correct joins.
- **`Knowledge/disruption_playbooks.md`**: Step-by-step mitigation guidance for specific disruptions. Use for recommendation/action-oriented responses when a delay/shortage is detected.
- **`Knowledge/faq.md`**: Short factual answers the agent can cite for common questions (critical materials, ROP formula pointer, etc.).
- **`Knowledge/inventory_policy.md`**: Service-level targets and formulas (ADD, DLT, SS, ROP). Use for on-the-fly calculations or to justify recommendations.
- **`Knowledge/kpis_and_dashboards.md`**: KPI definitions and alert thresholds. Use to compute and explain metrics, and to justify when to alert/escalate.
- **`Knowledge/sample_queries.md`**: Ready-made prompts to validate the agent’s end-to-end behavior.
- **`Knowledge/scm_overview_bep.md`**: High-level operational context (sites, logistics, risks, controls) for grounding.
- **`Knowledge/vendor_management_sop.md`**: SOPs for onboarding, performance mgmt, sourcing, and escalation. Use when the user asks “what should we do?” beyond pure data lookup.

All Knowledge content is synthetic and safe for testing. Index these for retrieval-augmented answers and citations.

### What each Data CSV is for
- **`Data/bepscm_facilities.csv`**: Master data for sites (type, capacity, timezone). Join via `facility_id`.
- **`Data/bepscm_materials.csv`**: Materials master (safety stock, lead time, primary/secondary vendors, cost). Join via `material_id`; link to vendors.
- **`Data/bepscm_vendors.csv`**: Suppliers (criticality, on-time %, quality, risk, terms). Join via `vendor_id`.
- **`Data/bepscm_inventory.csv`**: Current stock by facility/material with holds and last count date. Composite key (`facility_id`, `material_id`).
- **`Data/bepscm_purchase_orders.csv`**: PO pipeline (qty, price, incoterms, dates, ship method, status including Delayed). Join to vendors and materials.

Use the `data_dictionary.md` “Join Keys” section for the correct relationships and the “Common Calculations” for coverage, ROP, OTIF, etc.

### How to use this to build/test your agent
- **Index unstructured knowledge**: Chunk and embed all `Knowledge/*.md` for RAG responses, grounding explanations and recommended actions.
- **Load structured data**: Ingest `Data/*.csv` into a dataframe/SQL/feature store. Implement tools/functions for the agent to:
  - Fetch inventory, facilities, POs, vendors, materials by keys
  - Compute ROP/coverage using `inventory_policy.md`
  - List delayed POs and assess impact using `disruption_playbooks.md`
  - Calculate KPIs using `kpis_and_dashboards.md`
- **Test flows using `sample_queries.md`**:
  - Risk summary with mitigations (joins across delayed POs, critical materials; cite playbooks).
  - Delayed security thread POs and facility coverage impact (POs + inventory + materials).
  - ROP calculation for a material (materials + policy formulas).
  - Vendors under 90% on-time with corrective actions (vendors + SOP/KPIs).
  - Items below safety stock with expedite proposals (inventory + policy + playbooks).

### Typical joins you’ll need
- **PO → Vendor/Material**: `purchase_orders.vendor_id` → `vendors.vendor_id`; `purchase_orders.material_id` → `materials.material_id`
- **Inventory → Facility/Material**: `inventory.facility_id` → `facilities.facility_id`; `inventory.material_id` → `materials.material_id`
- **Material → Suppliers**: `materials.primary_vendor_id`/`secondary_vendor_id` → `vendors.vendor_id`

### Minimal validation checklist
- Retrieval returns cited sections from the correct Knowledge file.
- Structured tools return accurate rows (spot-check a delayed PO and a coverage calc).
- Calculations (ROP, coverage) match formulas in `inventory_policy.md`.
- KPI thresholds match `kpis_and_dashboards.md`.
- Recommendations align with `disruption_playbooks.md` and `vendor_management_sop.md`.


### Recommended Agent Settings
- **Retrieval**: Enable semantic chunking (max 500 tokens per chunk).
- **Citations**: Prefer quoting the nearest line/section.
- **Guardrails**: Remind users data is synthetic when asked for official figures.

### Quick Start
- Load CSVs into your data store or attach as knowledge.
- Index Markdown articles for retrieval-augmented responses.
- Test with prompts in `sample_queries.md`.
