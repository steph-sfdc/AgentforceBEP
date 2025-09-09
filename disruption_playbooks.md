## Supply Disruption Playbooks (Synthetic)

### Security Thread Delay (M0002)
- **Signal**: PO `status = Delayed` or ETA slip > 3 days.
- **Immediate**: Check on-hand coverage at `FDC01` and `FTW01`; freeze non-critical consumption.
- **Supplier**: Engage `V0002` and backup `V0008` for split shipments; request partial air freight.
- **Logistics**: Switch to fastest customs clearance; pre-file documents.
- **Production**: Re-sequence jobs to consume lower thread volumes first.

### Holographic Foil Shortage (M0004)
- **Signal**: On-hand < safety stock and open PO ETA > 10 days.
- **Immediate**: QA re-test quality hold lots; release if acceptable.
- **Supplier**: Expedite from `V0004` and `V0012` with premium air.
- **Packaging**: Optimize foil usage; reduce spoilage.

### Ink Quality Hold (M0003)
- **Signal**: `quality_hold_qty > 0` after receipt.
- **Immediate**: Quarantine lots; open CAPA with `V0003`.
- **Lab**: Accelerated tests; approve rework if within spec window.
- **Production**: Use alternative approved ink for non-security layers if possible.
