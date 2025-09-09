## Data Dictionary: Synthetic BEP SCM Datasets

All fields are strings unless noted. Dates are ISO (YYYY-MM-DD). Quantities are integers, prices are decimals.

### bepscm_vendors.csv
- **vendor_id**: Unique vendor code (e.g., V0001)
- **vendor_name**: Supplier legal or trade name
- **category**: Primary supply category (Paper Substrate, Security Thread, Security Ink, etc.)
- **criticality**: Vendor criticality to production (High/Medium/Low)
- **status**: Vendor status (Active/Inactive)
- **country**: Country of origin/ship-from
- **duns**: Synthetic DUNS-like identifier
- **on_time_pct** (int): Percent of POs delivered on/before promise
- **quality_score** (int): 0–100 internal vendor quality score
- **risk_score** (int): 0–100 composite risk (higher = riskier)
- **contract_id**: Master contract reference
- **incoterms**: Primary Incoterms used
- **payment_terms**: e.g., Net30/Net45

### bepscm_materials.csv
- **material_id**: Unique material code (e.g., M0002)
- **material_name**: Material description
- **category**: Material category (Raw Fiber, Security Thread, etc.)
- **spec**: Internal spec/reference code
- **unit_of_measure**: EA, LB, KG, ROLL, L
- **safety_stock_qty** (int): Minimum buffer stock target
- **lead_time_days** (int): Average total lead time to receipt
- **primary_vendor_id**: Preferred vendor
- **secondary_vendor_id**: Approved backup supplier (optional)
- **unit_cost_usd** (decimal): Standard cost per UoM
- **shelf_life_days** (int): If applicable; metals/parts may be long (3650)
- **active** (bool): Material active/inactive

### bepscm_facilities.csv
- **facility_id**: Unique facility code (e.g., FDC01)
- **facility_name**: Site name
- **location_city/location_state**: US location fields
- **type**: Printing or Distribution
- **timezone**: Olson TZ for scheduling
- **capacity_units_per_day** (int): Nominal capacity in bill units/day
- **operating_days_per_week** (int)
- **dock_doors** (int): Inbound/outbound combined
- **status**: Active/Inactive

### bepscm_inventory.csv
- **facility_id**: FK to facilities
- **material_id**: FK to materials
- **on_hand_qty** (int): Book quantity on hand
- **on_order_qty** (int): Open PO quantity
- **allocated_qty** (int): Reserved to production orders
- **quality_hold_qty** (int): Not available due to QA
- **last_count_date** (date): Last cycle-count date

### bepscm_purchase_orders.csv
- **po_id**: Purchase order identifier
- **vendor_id**: FK to vendors
- **material_id**: FK to materials
- **order_qty** (int)
- **uom**: Unit of measure
- **unit_price_usd** (decimal)
- **incoterms**: Incoterms agreed on PO
- **ship_from_country**: Country of shipment origin
- **ship_method**: Air/Truck/Sea
- **order_date/need_by_date/promised_date** (date)
- **status**: Open/Delayed/Received

### Join Keys
- Vendors: `vendor_id`
- Materials: `material_id`, link to vendors by `primary_vendor_id` and `secondary_vendor_id`
- Inventory: (`facility_id`, `material_id`)
- POs: `vendor_id` and `material_id`

### Common Calculations
- **On-hand coverage (days)** = on_hand_qty / average_daily_usage
- **Reorder point (ROP)** = demand_during_lead_time + safety_stock
- **Vendor OTIF** = on_time_and_in_full_deliveries / total_deliveries
