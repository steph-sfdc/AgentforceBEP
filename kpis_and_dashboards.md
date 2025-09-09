## KPIs and Dashboards (Synthetic)

### Core KPIs
- **Vendor On-Time %** = on_time_deliveries / total_deliveries
- **OTIF** (On Time In Full) = deliveries_on_time_and_full / total_deliveries
- **Lead Time Variance** = σ(PO_actual_lead_time)
- **Quality Defect Rate** = defective_units / received_units
- **Inventory Turns** = annualized_usage / average_inventory
- **Coverage (days)** = on_hand_qty / average_daily_usage

### Dashboard Views
- **Supplier Performance**: On-time %, quality, risk score trend.
- **PO Pipeline**: Open vs delayed vs received by material category.
- **Inventory Health**: Items below ROP, quality holds, aging stock.
- **Capacity & Demand**: Facility capacity vs planned consumption.

### Thresholds
- **Alert** if on-time % < 90% for critical suppliers.
- **Alert** if coverage < safety stock days for M0002/M0004/M0003.
- **Alert** if quality holds > 1% of receipts by category.
