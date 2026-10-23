# GenAI FinOps — code and reproducibility pack

**CAS ETH in Machine Learning in Finance and Insurance · Innovation Project**
Albert Escriche · October 2026

---

## What this is, and what it is not

The Innovation Project is a **framework study**, not a software product. Its contribution is a
method for forecasting the total cost of ownership of GenAI inference infrastructure before the
infrastructure is chosen, and a comparison of four infrastructure models under that method.

The code in this pack exists for one reason: so that every figure in the report can be checked
rather than taken on trust. It is working material, not a deliverable in its own right, and
nothing here is intended for production use.

There is no training code. The project is scoped to inference only (Chapter 1.2), and no model
is trained or fine-tuned anywhere in it. There is no dataset either: the inputs are published
list prices, published salary medians and the coefficients of a diffusion model, all fixed in
the annexes of the report and restated in the code as constants with their annex reference
beside them.

---

## Files

| File | What it is |
|---|---|
| `GenAI_FinOps_reproduce.ipynb` | Jupyter notebook. Recomputes every figure in the report and the presentation from the annex constants, then asserts each one against the published value. |
| `GenAI_FinOps_estimator.html` | The estimator, as an offline single file. Opens from disk — no account, no key, no network request of any kind. |
| `GenAI_FinOps_TCO_audit.xlsx` | The same cost model as a spreadsheet with live formulas, one assumption per row with its annex source. For checking by cell rather than by code. |

---

## Running them

**Notebook.** `jupyter lab GenAI_FinOps_reproduce.ipynb`, then run all cells. It needs only
`numpy` and `matplotlib`. The outputs are saved in the file, so it can also just be read.

The last cell checks 29 published figures — phase lengths, server counts, the four three-year
totals and their service, infrastructure and workforce lines, the per-million token costs, the
17× crossover and the three use-case results. It raises if any one of them disagrees. If the
notebook runs to the end, every number in the report has been reproduced from first principles.

**Estimator.** Double-click `GenAI_FinOps_estimator.html`. Pick one of the three use cases from
the report and press Estimate.

All arithmetic in that page is JavaScript operating on the static tables from the annexes. A
language model does exactly one thing in the online version — it reads a free-text description
of an application and sets the parameters from it — and it computes nothing. For the three
report use cases those parameters are pinned to the report, so the offline copy carries them,
and their commentary, in the file itself and needs no model at all. Describing an application of
your own is therefore the only feature that is unavailable offline.

**Workbook.** Open in Excel or LibreOffice. Blue cells are inputs, black are formulas, green are
cross-sheet references, and a yellow fill marks an assumption rather than a sourced price.

---

## How the figures relate to the report

| Report | Notebook |
|---|---|
| Annex F — adoption S-curve, phase boundaries | §2 |
| Annexes D and G — hardware tiers, rented against owned | §3 |
| Chapter 4 — the four infrastructure models | §4 |
| Chapter 5.3 — the underwriting assistant | §5 |
| Annex H — workforce, pensum by phase, switching threshold | §6 |
| Chapter 5.5 — the three use cases and their recommendations | §7 |
| Chapter 6.4 — economy of scale and the crossover | §8 |
| Chapter 6.3 — the blended path across adoption phases | §9 |

---

## Caveats

The figures are assumptions, not quotations, and the report says so in each annex:

- Salaries are market medians with a 15% employer loading, not an employer's own payroll.
- The staff fractions and the one-time build effort are estimates.
- The adoption coefficients are the average values from the diffusion literature, not values
  fitted to an observed rollout.
- Dell does not publish APEX prices for GPU servers, so the owned cost is built from component
  prices plus a subscription uplift rather than from a quote.
- Azure prices are pay-as-you-go list for Switzerland North. Reservations and negotiated
  discounts lower them, and the report keeps the list price deliberately, as the conservative
  reading.

The model shows how the decision behaves. It does not claim to show what the decision would
cost a particular insurer.
