# Baseline numerical experiments

Two synthetic instances test implementation correctness and parameter sensitivity.

- Small case: independent exhaustive enumeration. Large case: annual-scale inputs and an independent dynamic-programming reference.
- Inputs are experimental assumptions and literature-informed proxies, not calibrated forecasts for actual cities.

## Run in Colab

| Notebook | Launch |
|---|---|
| [baseline_largecase.ipynb](large_case/baseline_largecase.ipynb) | [Open in Colab](https://colab.research.google.com/drive/1eLKtC6O0tr65SM1JkziHM24RaPbEDo3_) |
| [baseline_smallcase.ipynb](small_case/baseline_smallcase.ipynb) | [Open in Colab](https://colab.research.google.com/drive/1xJvXZokBwrCa2vabDtKB1izIU3fAevtx) |

Colab opens the original Drive notebook; the GitHub file is a saved snapshot. Sign in with an account that can access the original.

## Folders

- [large_case](large_case/README.md) — Annual synthetic instance with three cities, ten demand scenarios, and a fleet limit of 1,000 vehicles.
- [small_case](small_case/README.md) — Three-city, ten-scenario instance for checking the MILP against exhaustive enumeration.


---

[Parent folder](../README.md) · [Project overview](../../../README.md)
