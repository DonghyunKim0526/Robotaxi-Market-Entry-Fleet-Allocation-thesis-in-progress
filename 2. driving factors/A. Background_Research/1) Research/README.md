# Market and demand evidence

## What each document contributes

- **Companies and markets:** separates current public-rider markets from announced expansion, testing, and rollout stages for Waymo, Zoox, and Tesla. It supports candidate screening, not a verified universal feasibility set.
- **Demand-variable review:** distinguishes direct robotaxi trip evidence, conventional ride-hailing evidence, and stated-choice/acceptance studies. The SF robotaxi study covers 194 tracts over September 2023–August 2024; its local trip associations are not automatically between-city choice effects.
- **Entry conditions:** separates confirmed prerequisites/enablers, operational events demonstrating risk, and public-data proxies. ODD includes geography, road types, weather, lighting, speed, and traffic conditions.

## Main papers and where they inform the research

The [demand-variable review](02_demand_variables.pdf) records the findings and source links. The main references below serve different roles; using a paper to screen variables does not mean its coefficients have been fitted or transferred to all candidate cities.

| Paper | What is taken from it | Where it is used / current status |
|---|---|---|
| **Loa, Lee & Circella — Just another ride-hailing?** | Observed SF robotaxi trip associations, especially zero-vehicle households and demographic/urban characteristics | Supports the zero-vehicle context in the current ER-DRO demand model and the candidate/selection discussion. Its reported slope informs a synthetic coefficient; it is not a calibrated city-level robotaxi choice model |
| **Elkhouly & Alhadidi — Ride-sharing Determinants** | Chicago conventional ride-hailing associations with population, economic activity, income, and vehicle availability | Informs the M/p candidate pool and screening of measurable urban characteristics. Indirect robotaxi evidence; current M design uses trip generation rather than transferring this regression |
| **Zhang et al. — Examining spatial heterogeneity of ridesourcing demand determinants with explainable machine learning** | Built-environment/accessibility variables and their nonlinear, spatially varying relationships with usage | Informs candidate urban-form variables and cautions against fixing one universal sign; these variables are not all included in the current ER-DRO toy model |
| **Cats et al. — Beyond the dichotomy** | Ride-hailing can substitute for or complement public transport depending on travel-time competitiveness | Informs alternative-service/public-transport candidates and their interpretation; not a direct robotaxi choice coefficient |
| **Yin & Cherchi — Willingness to pay for automated taxis** | Choice responses to fare, waiting time, support features, and customer reviews | Supports service-variable screening and the planned decision-dependent extension. Fare/waiting-time responses are not yet embedded in the current fleet-independent demand model |
| **Wei et al. — Using the Extended Unified Theory of Acceptance and Use of Technology** | Survey evidence on acceptance, perceived value, and habits | Helps interpret candidate acceptance mechanisms and measurement requirements. Latent survey scores are not directly used as city context; this study does not include a trust construct |
| **Yin, Cherchi & Nettle — Living in a City Where Automated Taxis are Operating and Using Them** | Distinguishes operating-area exposure and individual use experience when explaining preferences | Informs experience/awareness candidates and transfer cautions; no uniform positive experience effect or ready-made city predictor is assumed |

**Additional background:** papers 8–12 in the review cover SAV adoption with pilot experience (Etminani-Ghasrodashti et al.), SAV preferences (Krueger et al.), AV preferences (Haboucha et al.), a stated-choice review (Gkartzonikas & Gkritza), and SAV pilot-user/ridership evaluation (Khan et al.). They broaden the evidence for demographic, attitudinal, service, and experience candidates, with SAV/AV and individual-to-city transfer limitations; they are not all implemented regressors.

**How this connects to the current work:** [Candidates](../../B.%20Candidates/README.md) assembles the literature-backed pool; [Selection](../../C.%20Selection/README.md) defines the roles of fixed M and uncertain p and prioritizes measurable variables; the [current ER-DRO model](../../../1.%20model/C.%20ER-DRO_model/README.md) presently uses only zero-vehicle household share as context in its synthetic experiment. Age and service variables remain screening/extension directions, not completed real-data estimation.

## Evidence-to-input rules

| Evidence | What it can support | What it cannot establish alone |
|---|---|---|
| Observed robotaxi trips | Local associations with actual use | Unconstrained demand or separate effects on $M$ and $p$ |
| Conventional ride-hailing | Candidate scale/access variables | Direct robotaxi effect sizes |
| Stated-choice experiment | Fare/wait/support trade-offs | Realized city-level market shares |
| Public data (ACS, SLD, GTFS, NOAA) | Consistent variable measurement | Causality or a predetermined coefficient sign |

![Operator-market illustration from the project background review; operating status is a source-dated snapshot.](images/robotaxi_market.png)

Operator-market illustration from the project background review; operating status is a source-dated snapshot.

The market image illustrates the inventory described in the accompanying document; it is a snapshot, not live operating coverage. Use comparable geography and service conditions when turning this research into candidate-city inputs.

## Documents and their contents

- **[02_demand_variables.pdf](02_demand_variables.pdf)** — Separates observed robotaxi, conventional ride-hailing, and stated-choice evidence; maps candidate variables to comparable measurement data.
- **[01_robotaxi_companies_markets.pdf](01_robotaxi_companies_markets.pdf)** — Operator-specific market inventory with public-service versus announced/testing/rollout distinctions; document snapshot rather than live coverage.
- **[03_city_entry_conditions_variables.pdf](03_city_entry_conditions_variables.pdf)** — Distinguishes operating prerequisites, demonstrated operational risks, and constructed public-data proxies for entry feasibility.

---

[Parent guide](../README.md) · [Project overview](../../../README.md)
