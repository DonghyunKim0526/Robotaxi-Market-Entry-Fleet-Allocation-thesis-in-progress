# Robotaxi-Market-Entry-Fleet-Allocation (thesis in progress)

## Research problem

**Which candidate cities should a robotaxi operator enter, and how many vehicles should it allocate before uncertain demand is known?** The operator has a limited fleet, pays to enter markets, and faces both unused service capacity and demand it cannot serve. A useful deployment decision must account for city differences and demand uncertainty rather than treating one demand forecast as certain.

This research develops that question in stages: first establish a transparent entry/fleet model; then learn demand from observable city characteristics and examine protection against distributional uncertainty; finally extend the model so that operating decisions can themselves affect choice and demand. The numerical experiments test those modeling and learning mechanisms, rather than seeking a definitive real-city fleet recommendation.

> [!NOTE]
> **Current research progress.** The current main model is **contextual two-stage ER-DRO**, with a revised formulation and synthetic numerical experiments. Baseline verification provides its foundation; real-data validation and decision-dependent demand remain planned extensions.

## Repository map

| Folder / document | Role |
|---|---|
| [1. model](1.%20model/README.md) | Earlier ideas, baseline formulation/verification, current ER-DRO model, and Korean companions |
| [2. driving factors](2.%20driving%20factors/README.md) | Demand evidence → candidate M/p factors → selection criteria and proposed input construction |
| [3. References](3.%20References/README.md) | Cost-component rationale, parameter evidence/assumptions, model-structure guideline, and supporting literature |

## How the model develops

| Stage | What changes | Files and status |
|---|---|---|
| **Former model ideas** | Compares newsvendor, cost, profit, and multiple-penalty formulations; defines served demand, surplus, shortage, and possible double counting | [Earlier formulations](1.%20model/A.%20former_model%20ideas/former_models.pdf) — development record |
| **Baseline** | Joint binary city entry and integer fleets with fixed market scale and specified demand scenarios; minimizes entry + annual vehicle cost + expected surplus/shortage cost | [Formulation](1.%20model/B.%20baseline_model/1%29%20baseline/baseline%28main%29.pdf) · [Guide](1.%20model/B.%20baseline_model/README.md) · [Verification experiments](1.%20model/B.%20baseline_model/2%29%20numerical_experiments/README.md) — implemented and independently checked |
| **ER-DRO with exogenous context — current** | Fits logit choice probabilities from city characteristics, builds empirical-residual scenarios, and replaces average recourse cost with a CVaR-type robust criterion | [Revised formulation and experiments](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf) · [Guide](1.%20model/C.%20ER-DRO_model/README.md) · [Notebook](1.%20model/C.%20ER-DRO_model/ER-DRO%28non%20decision-dependent%29.ipynb) — synthetic learning/optimization evaluation available |
| **ER-DRO with decision-dependent service context/demand — planned** | Retains exogenous city traits but also learns how fare, waiting time, or service features affect choice; fleet decisions may affect waiting time and hence demand | [Choice-variable roles](2.%20driving%20factors/C.%20Selection/Factors_of_p.pdf) · [Model-structure comparison](3.%20References/%E2%80%BB%20translation/C.%20Model%20Structure%20Guidelines.pdf) · [Decision-dependent EV-location reference](3.%20References/%E2%80%BB%20papers/C.%20contextual_stochastic_optimization/EV_charging_station.pdf) — response estimation and optimization extension still to develop |

The last stage does not make fixed demographics into decision variables. It adds decision-dependent service attributes/demand to exogenous city context; it is not already implemented in the current notebook.

## Demand inputs: how M and p are defined, selected, and estimated

```math
D_c^s=M_cp_c^s.
```

$M_c$ is potential trip opportunities over the evaluation period. $p_c^s$ is the probability of choosing robotaxi **before capacity shortages**, under specified service conditions. The denominator of p must match the definition of M. Evidence, screening decisions, and assumptions are documented in [driving factors](2.%20driving%20factors/README.md), not inferred from a final fleet solution.

### M: separate market scale from choice

| Use | How M is constructed | Evidence / reference |
|---|---|---|
| Proposed real-data construction | Group-specific NHTS trip rates × ACS city populations, summed over population groups such as vehicle availability/income | [Factors_of_M.pdf](2.%20driving%20factors/C.%20Selection/Factors_of_M.pdf) explains the method, units, geography, sparse cells, and local-survey validation; actual city calculations remain to be checked |
| Current ER-DRO synthetic experiment | Actual ACS household totals ×10 for candidate-county proxies | [Revised ER-DRO, synthetic-data design](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf); the multiplier is a toy assumption, not the completed NHTS/ACS calculation |
| Annual baseline experiment | Reference 770,544,140 opportunities/year with city multipliers 0.75/1/1.25 | [Parameter rationale](3.%20References/B.%20parameter_rationale_baseline.pdf) derives a scale proxy from reported TNC trips / 5% mode share and states source-scope mismatches; [experiment guide](1.%20model/B.%20baseline_model/2%29%20numerical_experiments/large_case/README.md) records implemented inputs |

The proposed population-group construction is

```math
M_c=\sum_{g\in G}N_{c,g}r_g.
```

Here $N_{c,g}$ is the population in group g and $r_g$ its annual per-person trip rate. Person/household conversion, eligible trips, year, and city/tract boundaries must align. Variables considered for M regression may also explain p; fixing a transparently constructed scale helps separate those roles. See [the M selection rationale](2.%20driving%20factors/C.%20Selection/Factors_of_M.pdf) for the alternatives and limitations.

### p: learn choice rather than treating every demand association as a choice effect

The preliminary exogenous priorities are **zero-vehicle household share and age composition**. The current ER-DRO synthetic implementation uses **zero-vehicle share only**. Relative own fare, waiting time, and support features are candidates for the decision-dependent extension, requiring matched service/choice response data. Permission and ODD compatibility are treated separately as operating feasibility.

The selection checks evidence scope, common measurement across cities, interpretability/redundancy, availability before the decision, training-range overlap, and residual behavior. See [Factors_of_p.pdf](2.%20driving%20factors/C.%20Selection/Factors_of_p.pdf) and [the selection guide](2.%20driving%20factors/C.%20Selection/README.md) for why candidates were selected, deferred, or assigned a different role.

In the current model, regress the logit-scale observations and attach empirical residuals to candidate-city context:

```math
\ln\left(\frac{p^k}{1-p^k}\right)=\beta_0+\beta_1x^k+\varepsilon^k,
\qquad \hat\varepsilon^k=\ln\left(\frac{p^k}{1-p^k}\right)-\hat\beta_0-\hat\beta_1x^k,
```

```math
p_c^s=\sigma(\hat\beta_0+\hat\beta_1x_c+\hat\varepsilon^s),\quad
D_c^s=M_cp_c^s,\quad \sigma(z)=\frac1{1+e^{-z}}.
```

One residual produces one joint scenario, so the training sample size equals the scenario count. In real data, completed robotaxi trips divided by M may reflect supply shortages rather than unconstrained choice; request/rejection adjustment or an explicit censoring assumption is needed. These are open validation issues, explained in [the choice-input document](2.%20driving%20factors/C.%20Selection/Factors_of_p.pdf) and [the revised real-data plan](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf).

**Where the demand evidence comes from:** Loa, Lee & Circella's observed SF robotaxi study supports considering zero-vehicle share; its reported relationship informs the synthetic coefficient but is not a calibrated cross-city logit estimate. Conventional ride-hailing papers inform other city candidates, while stated-choice studies motivate fare/wait/features. The [paper-to-use map](2.%20driving%20factors/A.%20Background_Research/1%29%20Research/README.md) and [demand-evidence review](2.%20driving%20factors/A.%20Background_Research/1%29%20Research/02_demand_variables.pdf) distinguish those evidence types. The [residual SAA](3.%20References/%E2%80%BB%20papers/C.%20contextual_stochastic_optimization/C3_Kannan_Data-Driven%20Sample%20Average%20Approximation%20with%20Covariate%20Info.pdf) and [residual DRO](3.%20References/%E2%80%BB%20papers/C.%20contextual_stochastic_optimization/C4_Kannan_Residuals-based%20distributionally%20robust%20optimization.pdf) papers explain the learning/scenario methodology; [the concept-classified literature guide](3.%20References/%E2%80%BB%20papers/README.md) separates these methods from decision-dependent learning.

## Current main model: two-stage contextual ER-DRO

The authoritative specification is [ER-DRO(revised).pdf](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf). Demand scenarios are computed before solving and do not yet depend on the deployment decision.

### Stage 1: enter cities and allocate fleet

```math
\begin{aligned}
\min_{y,q}\quad &\sum_{c\in C}F_cy_c+\mathcal R_\zeta(q)\\
\text{s.t.}\quad &0\le q_c\le\bar q_cy_c &&\forall c\in C,\\
&\sum_{c\in C}q_c\le Q,\\
&y_c\in\{0,1\},\quad q_c\in\mathbb Z_{\ge0} &&\forall c\in C.
\end{aligned}
```

$y_c$ is entry and $q_c$ is integer fleet, common to all scenarios. $F_c$ is fixed entry cost; $\bar q_c$ and Q are city and total fleet limits. Scenario costs enter through the revised document's CVaR term:

```math
\mathcal R_\zeta(q)=\min_{\tau\in\mathbb R}
\left\{\tau+\frac1{|S|(1-\zeta)}\sum_{s\in S}\big(H(q,D^s)-\tau\big)^+\right\},
\qquad 0\le\zeta<1.
```

At risk level zero this becomes the empirical mean, ER-SAA. Larger risk levels emphasize expensive scenarios. The interpretation is distributional robustness over the existing residual scenarios, not moving their demand locations or guaranteeing OOS improvement.

### Stage 2: scenario-specific surplus and unmet demand

For the fixed first-stage fleet and scenario demand:

```math
\begin{aligned}
H(q,D^s)=\min_{O^s,U^s}\quad
&\sum_{c\in C}(c_c^+O_c^s+c_c^-U_c^s)\\
\text{s.t.}\quad
&\kappa_cq_c-D_c^s=O_c^s-U_c^s &&\forall c\in C,\\
&O_c^s,U_c^s\ge0 &&\forall c\in C.
\end{aligned}
```

```math
O_c^s=\left(\kappa_cq_c-D_c^s\right)^+,\qquad
U_c^s=\left(D_c^s-\kappa_cq_c\right)^+.
```

The superscript plus denotes the positive part. Productivity $\kappa_c$ converts vehicles to trip capacity; $c_c^+,c_c^-$ price surplus and unmet demand. Recourse separates by scenario/city and does not transfer capacity between cities. The extensive-form MILP embeds both stages and linearizes CVaR with the document's threshold/excess-cost variables; “two-stage” describes decisions/outcomes, not two independent one-pass solves. Full constraints and the entry-budget variant are in [the revised specification](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf).

### Cost and resource assumptions: which evidence supports them?

[A. Cost-component rationale](3.%20References/A.%20cost_selection_rationale.pdf) explains **why a cost term is included**; [B. Parameter rationale](3.%20References/B.%20parameter_rationale_baseline.pdf) explains **how an experimental number was obtained**. Structural support, observations, derived proxies, and designed assumptions are different evidence levels.

| Item | Rationale and boundary | Reference |
|---|---|---|
| Entry / vehicle / unmet-loss terms | EV-location and SAV/fleet-planning literature motivate the structure; shortage loss is foregone contribution, not gross fare. Extra idle penalty is a study assumption and should not duplicate vehicle costs | [Cost-component rationale](3.%20References/A.%20cost_selection_rationale.pdf) |
| Annual capacity 8,760 | Rounded 24 daily trips ×365, motivated by public trip/fleet scale reports; not observed maximum vehicle capacity | [Parameter rationale](3.%20References/B.%20parameter_rationale_baseline.pdf) |
| Baseline entry 3.5M and vehicle 7,972/year | Facility-project estimates plus an assumed preparation allowance, and selected personal-vehicle ownership-cost components; proxies rather than calibrated robotaxi city costs | [Parameter derivations and limitations](3.%20References/B.%20parameter_rationale_baseline.pdf) |
| ER-DRO toy costs/resources | Surplus cost normalized to 1, shortage ratio tested at 1/5/10; entry cost scaled with shortage loss; fleet/city caps designed for the synthetic study | [Revised experiment settings](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf) |
| Revised versus baseline vehicle cost | Revised omits separate vehicle cost. Its coefficient-absorption identity is exact in expectation under the stated adjustment, but only approximate inside general CVaR | [Revised section 1.6](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf) · [Model-structure guideline](3.%20References/%E2%80%BB%20translation/C.%20Model%20Structure%20Guidelines.pdf) |

The baseline dollar objective and the normalized ER-DRO costs should therefore not be compared as if they measured the same policy under identical assumptions. [Entry-condition research](2.%20driving%20factors/A.%20Background_Research/1%29%20Research/03_city_entry_conditions_variables.pdf) also separates permission/ODD prerequisites from demand predictors.

## Numerical experiments: what was checked and learned?

### 1. Baseline: independent verification and economic mechanisms

| Question | Setting / check | What the experiments show |
|---|---|---|
| Does the implementation match the equations? | Small case: 3 cities, 10 fixed scenarios, fleet 4, city cap 2; all 60 feasible entry/fleet pairs. Annual case: fleet 1,000, city cap 500; independent exact dynamic program | Reported MILP/reference checks agree; objective, integrality, balance, and limits are recomputed independently |
| Do boundary conditions behave correctly? | Eight edge cases per case, adapted to each scale | Zero demand/fleet, no service incentive, prohibitive entry, and exact capacity balance give interpretable behavior; fleet availability is an upper bound |
| Why does a city become worth entering? | Small-case entry-cost and productivity sweeps | Extra service need not cover fixed entry cost; the marginal third-city contribution is 8, creating the common-entry-cost switch at 8 |
| Do assumptions expose meaningful allocation choices? | Annual demand compared with maximum city capacity | Probability levels were deliberately chosen to straddle capacity; universal shortage would mask demand-sensitive allocation |
| What do stable fleets and multiple optima mean? | Track costs, service, and complete tied solution sets | Performance can change while a representative vector stays fixed; annual equal marginal values generate 72 tied allocations |

![Small-case entry-cost sensitivity: an independently interpretable switch rather than merely a reported optimal fleet.](1.%20model/B.%20baseline_model/2%29%20numerical_experiments/small_case/figures/smallcase/06_F_zoom.png)

The small experiment traces a change in entry decisions to additional service value versus fixed cost. Coarse penalty tests can miss a switch: expanding the idle-penalty sweep identifies the compared alternatives meeting at 15. Mean-preserving dispersion also changes costs/ties without necessarily changing a representative fleet. See [small-case design and conclusions](1.%20model/B.%20baseline_model/2%29%20numerical_experiments/small_case/README.md) and [the full report](1.%20model/B.%20baseline_model/2%29%20numerical_experiments/small_case/small_case.pdf).

![Annual demand scale versus maximum city capacity: designed to reveal both shortage and idle-capacity regimes.](1.%20model/B.%20baseline_model/2%29%20numerical_experiments/large_case/figures/annual/01_scale.png)

At the annual reference capacity of 4.38M trips per city, demand exceeds the cap in 5/10, 5/10, and 8/10 scenarios. Earlier larger probability levels made every city universally capacity-constrained. The revised synthetic setting tests demand effects instead of that artifact. Common proportional changes in M and p are equivalent through their product; city-specific costs can resolve ties that common changes leave intact. See [annual input rationale and sensitivity](1.%20model/B.%20baseline_model/2%29%20numerical_experiments/large_case/README.md).

![Annual scenario sampling: judge sampled decisions under one common original demand distribution.](1.%20model/B.%20baseline_model/2%29%20numerical_experiments/large_case/figures/annual/17_sampling.png)

With 50 sampled scenarios, some seeds incur about 1.73M additional evaluated cost; with 500, all five tested seeds incur zero. Mean-demand-optimal decisions cost about 0.39M–8.14M more under the original ten scenarios. Both comparisons use a common evaluation distribution; neither validates actual robotaxi demand or a universal sample-size rule. Detailed caveats are in [the annual report](1.%20model/B.%20baseline_model/2%29%20numerical_experiments/large_case/large_case.pdf).

**Reference outputs only:** small fleet (0,2,2), cost 858; annual representative (132,368,500), cost about 166.264M with 72 optima. Their role is reproducibility, not a real-city recommendation or cross-scale cost ranking.

### 2. Contextual ER-DRO: learning, information value, and tail protection

**Design.** Use actual ACS zero-vehicle shares for 18 candidate-county proxies, household totals ×10, and a known synthetic logit model with intercept −3.5, slope 0.8, error standard deviation 0.3. Train on 15 or 200 observations; compare contextual ER-SAA, contextual ER-DRO, and no context across risk/cost-ratio settings. Score fixed decisions on 1,000 separate common true-model scenarios; OOS tail cost always means the worst 10%. Settings and tables are from [the revised ER-DRO report](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf), not a new experiment run.

| Validation question | Evidence and lesson |
|---|---|
| Does the learner recover the intended signal? | With 200 observations, estimated slope 0.665 and residual spread 0.298 are near truth 0.8/0.3. Low test R² ≈0.143 reflects the intentionally weak signal; compare with −0.013 for no context |
| Is the conclusion specific to one cost ratio? | Contextual expected-cost gains persist at surplus:shortage ratios 1:1, 1:5, 1:10; this is robustness to assumptions, not cost calibration |
| What does context contribute separately from DRO? | At matched risk levels, context reduces OOS expected cost; increasing risk aversion within a model exchanges mean performance for tail protection |
| What happens with scarce training data? | At risk 0.9, contextual expected costs for 15/200 observations differ about 0.8–3.1% across tested ratios; this is not a general small-sample guarantee |
| Which conditions matter most? | Resource scarcity, context strength, noise, costs, sample size, and risk can change the relative value of the methods |

![Demand-learning diagnostics: fitted signal, residual distribution/patterns, and independent test predictions.](1.%20model/C.%20ER-DRO_model/figures/fig1_f_diagnostics.png)

The plots support checking residual reuse in the synthetic setting; they do not prove independence, homoscedasticity, or cross-city transfer for actual observations. Those are explicit prerequisites to validate later. See [the ER-DRO validation-question guide](1.%20model/C.%20ER-DRO_model/README.md).

![Independent expected and worst-10% costs versus optimization risk level: separate information gains from the cost of tail protection.](1.%20model/C.%20ER-DRO_model/figures/toy_oos_vs_zeta.png)

| Contextual model, training 200, surplus 1 / shortage 5 | Risk 0: ER-SAA | Risk 0.5 | Risk 0.9 |
|---|---:|---:|---:|
| OOS expected cost, million normalized units | 12.46 | 12.67 | 14.22 |
| OOS worst-10% cost, same units | 22.79 | 22.29 | 21.62 |

**Risk trade-off:** endpoints give about 14% higher expected cost and 5.1% lower tail cost. **Information contribution:** expected-cost gains over matched-risk no context are about 1–3%, 3–15%, and 4–19% at risks 0, 0.5, and 0.9 across the reported settings. **Important failure case:** with only 15 observations and no context, tail cost can worsen as risk grows (22.79M→23.20M at shortage 5). In-sample robustness alone is not an OOS guarantee. The source is [the revised analysis of results](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf).

![One-parameter OOS expected-cost sensitivity: contextual ER-DRO, contextual ER-SAA, and no-context ER-DRO.](1.%20model/C.%20ER-DRO_model/figures/fig2_sensitivity.png)

| Sensitivity mechanism | What was learned in the tested settings |
|---|---|
| Fleet and productivity | More resources reduce cost; at fleet ratio 0.2, costs nearly coincide because severe scarcity dominates method differences |
| City cap | Effects plateau above about 100 for ER-SAA and 150 for ER-DRO in this instance; relaxing a nonbinding limit has no further value |
| Context strength | At zero signal the compared costs coincide; reported context gains reach about 25%/41% at slopes 3/5. Changing the true slope requires refitting |
| Entry cost and noise | Larger values raise evaluated expected cost; these assumptions materially affect policy evaluation |
| Training size | Across tested 10–200 observations, contextual ER-SAA varies within about 1.4%, while ER-DRO fluctuates about 13.19M–14.24M; one realized experiment need not improve monotonically |
| Shortage loss and risk | Cost scale and risk preference matter; interpret mean-cost curves together with tail performance rather than declaring a mean-cost winner universally best |

These are one-input-at-a-time comparisons around training 200, surplus 1, shortage 5, risk 0.9. They are not confidence bands or universal comparative-statics claims. [The revised report](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf) and [notebook](1.%20model/C.%20ER-DRO_model/ER-DRO%28non%20decision-dependent%29.ipynb) document the settings; the [ER-DRO guide](1.%20model/C.%20ER-DRO_model/README.md) explains their interpretation.

### 3. Solving the two-stage model: one MILP or decomposition?

The extensive form solves all scenarios together. L-shaped decomposition alternates a first-stage master with scenario subproblems connected by cuts and bound updates. At training 15, shortage 5, risk 0.9, the document reports:

| Setting | Extensive form | L-shaped | Interpretation |
|---|---|---|---|
| Entry cost in objective | 1.5 s | 54.5 s, 38 iterations; feasible cost +0.43% | Decomposition stops at a 1% bound tolerance, not exact equality |
| City-count budget 3, entry cost removed | 0.4 s | 29.5 s, 38 iterations; feasible cost +0.65% | Different objective from the row above; compare methods within a row |

Subsequent experiments use the extensive form because the piecewise-linear recourse is compact in these toy instances. This is not a general result about large or decision-dependent instances. Timings, objectives, and stopping rules are from [the revised solution comparison](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf); enable `RUN_COMPARE=True` in the notebook to reproduce the optional comparison.

## Code and Colab

| Experiment | English notebook / execution | Korean notebook / execution |
|---|---|---|
| Small baseline | [Notebook](1.%20model/B.%20baseline_model/2%29%20numerical_experiments/small_case/baseline_smallcase.ipynb) · [Colab](https://colab.research.google.com/drive/1xJvXZokBwrCa2vabDtKB1izIU3fAevtx) | [노트북](1.%20model/%E2%80%BB%20translation/B.%20baseline_model/numerical_experiments/smallcase/baseline_smallcase%28%ED%95%9C%EA%B8%80%29.ipynb) · [Colab](https://colab.research.google.com/drive/1VT-cDsVp_YqmNhzPgUUk2LuJHBpc97tK) |
| Annual baseline | [Notebook](1.%20model/B.%20baseline_model/2%29%20numerical_experiments/large_case/baseline_largecase.ipynb) · [Colab](https://colab.research.google.com/drive/1eLKtC6O0tr65SM1JkziHM24RaPbEDo3_) | [노트북](1.%20model/%E2%80%BB%20translation/B.%20baseline_model/numerical_experiments/smallcase/baseline_largecase%28%ED%95%9C%EA%B8%80%29.ipynb) · [Colab](https://colab.research.google.com/drive/1YsArFdKTv3LFnlhcAC__o0PlrfRD-eEx) |
| Contextual ER-DRO, decision-independent | [Notebook](1.%20model/C.%20ER-DRO_model/ER-DRO%28non%20decision-dependent%29.ipynb) · [Colab](https://colab.research.google.com/drive/1dz5QtiAnYBBmKfDLi95xfjFirqg2fcAT) | [노트북](1.%20model/%E2%80%BB%20translation/C.%20ER-DRO_model/ER-DRO%28non%20decision-dependent%20%ED%95%9C%EA%B8%80%29.ipynb) · [Colab](https://colab.research.google.com/drive/17iILpKgogewmOCaTxgyWJqE7_LOHQ_7o) |

Run cells top to bottom. Notebooks use NumPy, pandas, SciPy `milp`/HiGHS, and Matplotlib; setup details and export steps are in each experiment guide. The ER-DRO notebook exports comparison/budget/sensitivity CSVs and diagnostics; the annual baseline exports checks and sampling tables. Colab opens permission-controlled Drive originals; GitHub notebooks are saved snapshots, not automatically synchronized copies. [Korean model guides](1.%20model/%E2%80%BB%20translation/README.md) mirror the English guides' structure.

## Next development and validation

1. **Build comparable real-data M and p.** Check tract/city geography, eligible trips, periods, person/household units, sample weights, and supply censoring before fitting. Validate the NHTS/ACS scale against local travel surveys. Basis: [M construction](2.%20driving%20factors/C.%20Selection/Factors_of_M.pdf), [p measurement/selection](2.%20driving%20factors/C.%20Selection/Factors_of_p.pdf), and [revised real-data plan](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf).
2. **Validate spatial transfer and residual reuse.** The revised plan learns on operating-city tracts (e.g. SF), aggregates candidate-tract demand, and proposes testing on another operating city (e.g. LA). Check prediction errors, residual mean/spread, dependence, and support overlap; distinguish an illustrative example from completed data validation. Basis: [real-data procedure and assumptions](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf) and [residual SAA](3.%20References/%E2%80%BB%20papers/C.%20contextual_stochastic_optimization/C3_Kannan_Data-Driven%20Sample%20Average%20Approximation%20with%20Covariate%20Info.pdf) / [residual DRO foundations](3.%20References/%E2%80%BB%20papers/C.%20contextual_stochastic_optimization/C4_Kannan_Residuals-based%20distributionally%20robust%20optimization.pdf).
3. **Calibrate and test risk choices.** Compare risk settings with repeated training/evaluation samples and suitable held-out validation, rather than selecting solely on training cost or one seed. Revisit noise, cost ratios, resource scarcity, and cost-definition consistency. Basis: [synthetic findings](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf), [parameter limitations](3.%20References/B.%20parameter_rationale_baseline.pdf), and [ambiguity-sizing/validation reference](3.%20References/%E2%80%BB%20papers/C.%20contextual_stochastic_optimization/C4_Kannan_Residuals-based%20distributionally%20robust%20optimization.pdf).
4. **Develop decision-dependent service learning.** Obtain choices linked to fare, fleet/waiting-time changes, and service features; separate exogenous city traits from decision responses, then connect them to optimization. Formulation, estimation, and tractability still need development. Basis: [selected service variables](2.%20driving%20factors/C.%20Selection/Factors_of_p.pdf), [structure guideline](3.%20References/%E2%80%BB%20translation/C.%20Model%20Structure%20Guidelines.pdf), and [EV-location learning framework](3.%20References/%E2%80%BB%20papers/C.%20contextual_stochastic_optimization/EV_charging_station.pdf).
5. **Reassess computation and evidence at the extended scale.** Recompare extensive form/decomposition with explicit gaps and timing conditions after the model changes. If multiple biased sources are combined, source-reliability models are additional research options, not existing features. Basis: [current solution comparison](1.%20model/C.%20ER-DRO_model/ER-DRO%28revised%29.pdf) and [classified methodological references](3.%20References/%E2%80%BB%20papers/README.md).
