# Hillstrom Dataset — Column Definitions

## Pre-treatment features (X)

| Column | Definition |
|---|---|
| `recency` | Months since the customer's last purchase |
| `history_segment` | Binned version of `history` (a categorical bucket, e.g. "$100-$200") |
| `history` | Dollar amount spent by the customer in the past year |
| `mens` | 1 if the customer purchased men's merchandise in the past year |
| `womens` | 1 if the customer purchased women's merchandise in the past year |
| `zip_code` | Customer's zip code classified as `Urban`, `Suburban`, or `Rural` |
| `newbie` | 1 if the customer became a customer in the last 12 months |
| `channel` | Channels the customer purchased from in the past year: `Phone`, `Web`, or `Multichannel` |

## Treatment

| Column | Definition |
|---|---|
| `segment` | Which email campaign the customer was randomly assigned to: `Mens E-Mail`, `Womens E-Mail`, `No E-Mail` |
| `treatment` | Derived: 1 if `segment` is either email arm, 0 if `No E-Mail` (collapses the two email arms per project scope) |

## Outcomes (post-treatment — never use as features)

| Column | Definition |
|---|---|
| `visit` | 1 if the customer visited the website in the two weeks following the campaign (outcome used in this project) |
| `conversion` | 1 if the customer made a purchase in the two weeks following the campaign (not used — see below) |
| `spend` | Dollar amount spent by the customer in the two weeks following the campaign |

**Why `visit` and not `conversion`:** `conversion`'s base rate (~0.9%) is too rare to reliably detect uplift at the segment level (Radcliffe & Surry's volume rule: uplift × segment size ≥ 500 — conversion clears only ~100 at plausible segment sizes). `visit` (~15% base rate) clears the threshold comfortably (~1,000+).

## Derived columns (added during analysis)

| Column | Definition |
|---|---|
| `customer_id` | Row position, used as a stand-in ID since the dataset has none natively |
