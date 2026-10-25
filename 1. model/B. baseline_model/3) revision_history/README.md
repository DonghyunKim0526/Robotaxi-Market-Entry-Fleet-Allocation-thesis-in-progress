# Baseline revision history

This log records changes visible in the archived baseline versions and the current formulation. Dates identify the archived files; the current file has no revision date in its filename. Reasons below distinguish explicit revision notes from modeling implications inferred from the equations.

## 2026-09-21 → 2026-09-30: simplify the baseline

| Part changed | Before → after | Reason / consequence |
|---|---|---|
| Unmet-demand loss | The earlier marked-up document retains separate human-taxi-switching and other-loss terms alongside the compact formulation; the later document keeps only $c_c^-U_c^s$ | Consolidates the baseline around one shortage coefficient. With a fixed switching share, the earlier split can be combined into an effective shortage cost; this is a mathematical rationale, not a recorded statement of author intent |
| Operational outcome variables | Removed struck-out throughput/fallback variables and their equations; retained $O_c^s=(\kappa_cq_c-D_c^s)_+$ and $U_c^s=(D_c^s-\kappa_cq_c)_+$ | Makes clear that surplus and shortage follow from demand and deployment rather than requiring separate datasets |
| Constraints | Removed obsolete struck-out feasibility and throughput/decomposition rows; retained entry/fleet linking, total fleet, and capacity balance | Aligns the explanation table with the compact active formulation; removal of already struck-out text is cleanup, not a newly imposed relaxation |
| Market scale | Removed old scenario-indexed market notation and explicitly stated that baseline $M_c$ is fixed | Keeps uncertainty in the choice scenarios while holding market scale constant |
| Document structure | Moved demand/outcome explanations before the notation table; removed obsolete comments and deletion markup | Presents the active equations and their meanings together |
| Driving-factor material | Marked the factor discussion as moved to the Candidates document, while retaining a greyed copy | The move is explicitly noted in the archived document; separates factor research from the mathematical formulation |

## 2026-09-30 → current baseline: clarify demand scope

| Part changed | Before → after | Reason / consequence |
|---|---|---|
| Definition of $M_c$ | Potential ride-hailing opportunities → potential travel opportunities **across all modes**, with an annual interpretation | Makes the denominator consistent with the stated non-robotaxi alternatives, including other modes; this is the interpretation implied by the revised definitions |
| Definition of $p_c^s$ | General robotaxi choice probability → probability under specified service conditions **before fleet-capacity constraints** | Separates unconstrained choice demand from completed trips affected by shortages |
| Factor appendix | Removed the greyed driving-factor copy after the earlier relocation note | Leaves the baseline document focused on equations, notation, and demand/capacity interpretation |

The core entry + vehicle + expected surplus/shortage objective and city/total fleet constraints remain in the current baseline. The changes above do not document a switch to ER-DRO; that later model has its own formulation folder.

## Versions to compare

- [2026-09-21 marked-up baseline](09_21_2026_baseline.pdf): preserves proposed removals, alternative shortage decomposition, and relocation notes.
- [2026-09-30 baseline](09_30_2026_baseline.pdf): compact active formulation, fixed market scale, and greyed relocated factor material.
- [Current baseline](../1%29%20baseline/baseline%28main%29.pdf): all-mode opportunity definition and pre-capacity choice probability.

[Baseline guide](../README.md)
