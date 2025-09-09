## Inventory Policy (Synthetic)

### Targets
- **Service level**: 98% for critical security materials; 95% for others.
- **Safety stock**: Based on demand and lead time variability.

### Calculations
- **Average daily demand (ADD)**: historical usage / days.
- **Demand during lead time (DLT)** = ADD × lead_time_days.
- **Safety stock (SS)** = z × σ_dlt, where z reflects service level.
- **Reorder point (ROP)** = DLT + SS.

### Practices
- **Cycle counting**: A-items weekly, B monthly, C quarterly.
- **Quality holds**: Segregate and exclude from available-to-promise.
- **Shelf life**: FEFO for items with shelf-life constraints.

### Triggers
- **Expedite** if projected on-hand before next receipt < SS.
- **Re-qualify** if recurring quality holds > 2 incidents/quarter.
