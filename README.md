## BEP Supply Chain Knowledge Set (Synthetic)

- **Purpose**: Seed data and concise knowledge for spinning up an Agent in Agentforce to answer questions about Bureau of Engraving and Printing (BEP) supply chain operations.
- **Scope**: Vendors, materials, facilities, inventory, and purchase orders; SOPs, policies, KPIs, disruption playbooks, FAQs.
- **Disclaimer**: This content and data are entirely synthetic and for testing/training. They do not represent official US Government information.

### Files
- Data: CSVs in `Agentforce/Data`.
- Knowledge: Markdown articles in `Agentforce/Knowledge`.

### Recommended Agent Settings
- **Retrieval**: Enable semantic chunking (max 500 tokens per chunk).
- **Citations**: Prefer quoting the nearest line/section.
- **Guardrails**: Remind users data is synthetic when asked for official figures.

### Quick Start
- Load CSVs into your data store or attach as knowledge.
- Index Markdown articles for retrieval-augmented responses.
- Test with prompts in `sample_queries.md`.
