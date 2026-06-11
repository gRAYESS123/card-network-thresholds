# Card Network Monitoring-Program Thresholds

Machine-readable, source-cited thresholds for the card networks' merchant monitoring programs — **Visa VAMP** and **Mastercard ECP (ECM / HECM)** — including fine schedules and a dated changelog of every threshold change.

**Last verified: 2026-06-10.** Every figure links to a primary network document or an acquirer/processor's official documentation. No vendor-blog sourcing. Re-verified quarterly.

- [`data/thresholds.json`](data/thresholds.json) — full dataset (programs, tiers, ratios, counts, regions, fine schedules, per-figure citation)
- [`data/thresholds.csv`](data/thresholds.csv) — flat CSV export
- [`CHANGELOG.md`](CHANGELOG.md) — dated record of threshold changes, each row cited

Maintained by [Georges Rayess](https://www.georgesrayess.com/about) (payments-fraud consultant; ran fraud ops for a 200K-user subscription app). Canonical human-readable reference: [Payment Compliance Thresholds](https://www.georgesrayess.com/fraud/payment-program-thresholds) · interactive check: [VAMP & ECM Risk Calculator](https://www.georgesrayess.com/fraud/payment-risk-calculator).

## Visa VAMP (Visa Acquirer Monitoring Program)

Ratio = count of (TC40 fraud reports + TC15 disputes) ÷ count of settled card-not-present transactions (TC05), monthly. Count-based, not dollar-based. Disputes resolved via pre-dispute tools (RDR/CDRN) and TC40s qualified under Compelling Evidence 3.0 are excluded. ([Visa fact sheet, PDF][visa])

| Level | Tier | Threshold | Activity floor | Effective |
|---|---|---|---|---|
| Merchant | Excessive (only merchant tier) | **≥ 1.5%** (AP, Canada, EU, US — reduced from 2.2%; LAC already 1.5%; **CEMEA remains 2.2%**) | ≥ 1,500 fraud+dispute transactions/month (CEMEA: ≥ 150 and ≥ US$75,000) | 2026-04-01 |
| Acquirer | Above Standard | ≥ 0.5% | — | 2025-06-01 |
| Acquirer | Excessive | ≥ 0.7% | — | 2025-06-01 |
| Merchant | Enumeration monitoring | ≥ 20% enumeration ratio AND ≥ 300,000 enumerated authorizations | — (no fines assessed) | 2025-06-01 |

Notes: merchant thresholds apply only when the merchant's acquirer is itself below Above Standard (< 0.5%). There is no merchant "Above Standard" tier. Per-transaction non-compliance assessments (~US$8 at Excessive, US$4 at acquirer Above Standard, 3-month grace on first identification) are reported by processors ([NMI][nmi]) but are not enumerated in Visa's public fact sheet — treat as processor-reported.

## Mastercard ECP (Excessive Chargeback Program)

ECP is the program; its tiers are ECM and HECM. Ratio = current-month chargeback count ÷ **preceding month's** captured transaction count. ([Stripe docs][stripe])

| Tier | Trigger | Fine schedule (per month in program) |
|---|---|---|
| ECM (Excessive Chargeback Merchant) | 100–299 chargebacks AND 1.5%–2.99% | Mo 1: $0 · Mo 2–3: $1k · Mo 4–6: $5k · Mo 7–11: $25k · Mo 12–18: $50k · Mo 19+: $100k |
| HECM (High Excessive Chargeback Merchant) | ≥ 300 chargebacks AND ≥ 3.0% | Mo 1: $0 · Mo 2: $1k · Mo 3: $2k · Mo 4–6: $10k · Mo 7–11: $50k · Mo 12–18: $100k · Mo 19+: $200k |

Plus the **Issuer Recovery Assessment**: US$5 per chargeback above 300, from month 4 onward, in both tiers.

## Retired programs (historical)

**VDMP** and **VFMP** were retired 2025-03-31 (Standard tiers at 0.9% + 100 disputes / 0.9% fraud + US$75k respectively) and replaced by VAMP, effective 2025-06-01 with enforcement from 2025-10-01.

## Sources

- [Visa Acquirer Monitoring Program fact sheet (PDF, primary)][visa]
- [Stripe — Dispute & fraud monitoring programs (acquirer/processor docs)][stripe]
- [Adyen — Dispute and fraud monitoring (acquirer docs)][adyen]

## Update policy & contributions

Re-verified quarterly against the sources above; every change lands as a dated row in [CHANGELOG.md](CHANGELOG.md). If a network publishes a change before we catch it, please open an issue **with a link to the primary or acquirer document** — vendor blog posts are not accepted as sources.

## License

Data and documentation: [CC BY 4.0](LICENSE) — free to use with attribution (a link to this repo or to [the canonical page](https://www.georgesrayess.com/fraud/payment-program-thresholds)).

[visa]: https://corporate.visa.com/content/dam/VCOM/corporate/visa-perspectives/security-and-trust/documents/visa-acquirer-monitoring-program-fact-sheet-2025.pdf
[stripe]: https://docs.stripe.com/disputes/monitoring-programs
[adyen]: https://docs.adyen.com/risk-management/dispute-and-fraud-monitoring/
[nmi]: https://www.nmi.com/blog/vamp-what-you-need-to-know-about-visas-acquirer-monitoring-program/
