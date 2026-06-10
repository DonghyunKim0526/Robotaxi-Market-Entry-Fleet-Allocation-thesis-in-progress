# Demand-Side Variables for Robotaxi Deployment Research

## Key Principles

- Only Paper 1 directly analyzes **observed robotaxi demand**.
- Papers 2–4 analyze conventional **ride-sharing/ridesourcing demand** and therefore provide only indirect evidence for robotaxi demand.
- When a paper does not establish a single directional effect, no positive or negative sign is assigned.
- “Official measurement data” refers to public datasets that can be used to construct comparable variables across U.S. cities. These datasets do **not** by themselves establish that the variable affects demand.

---

# 1. *Just another ride-hailing? Examining the determinants of robotaxi demand in San Francisco*

**Authors:** Patrick Loa, Yongsung Lee, and Giovanni Circella  
**Journal:** *Transportation* (2026)  
**Paper link:** [Springer DOI](https://doi.org/10.1007/s11116-026-10751-9)  
**Study scope:** Monthly observed robotaxi trip productions and attractions across 194 San Francisco census tracts from September 2023 through August 2024  
**Evidence level:** **Direct empirical evidence on observed robotaxi demand**

## Robotaxi Demand Variables

All significance levels below are based on Table 3 of the paper. `***` indicates \(p<0.01\), while `**` indicates \(p<0.05\).

| Variable associated with robotaxi demand | Estimated direction and significance | Official measurement data | Official data link |
|---|---|---|---|
| Population density | **Negative (-)** for both trip productions and trip attractions, \(p<0.01\). Census tracts with higher population density had lower observed robotaxi demand. | U.S. Census ACS population combined with Census TIGER/Line area, or EPA Smart Location Database population density | [ACS](https://www.census.gov/programs-surveys/acs), [ACS B01003 Total Population](https://api.census.gov/data/2024/acs/acs5/groups/B01003.html), [EPA Smart Location Database](https://www.epa.gov/smartgrowth/smart-location-mapping) |
| Employment density | **Positive (+)** for trip attractions, \(p<0.01\). It was not retained in the final trip-production model. | Census LEHD LODES Workplace Area Characteristics or EPA SLD employment density | [LEHD/LODES](https://lehd.ces.census.gov/data/), [EPA SLD](https://www.epa.gov/smartgrowth/smart-location-mapping) |
| Land-use mix | **Positive (+)** for both trip productions and trip attractions, \(p<0.01\). | EPA Smart Location Database five-tier employment entropy or related land-use-mix indicators | [EPA Smart Location Database](https://www.epa.gov/smartgrowth/smart-location-mapping) |
| Evening peak transit-service frequency per capita | **Positive (+)** for both trip productions and trip attractions, \(p<0.01\). | EPA SLD transit-frequency variables or official GTFS feeds from local transit agencies | [EPA Smart Location Database](https://www.epa.gov/smartgrowth/smart-location-mapping), [GTFS Documentation](https://gtfs.org/documentation/overview/) |
| National Walkability Index | **Positive (+)** for both trip productions and trip attractions, \(p<0.01\). | EPA National Walkability Index | [EPA Smart Location Mapping](https://www.epa.gov/smartgrowth/smart-location-mapping) |
| Density of art, entertainment, and recreation POIs | **Positive (+)** for both trip productions and trip attractions, \(p<0.01\). | The paper uses OpenStreetMap. A federal nationwide POI dataset is limited, but Census County Business Patterns can be used to measure establishments by NAICS category. | [Census County Business Patterns](https://www.census.gov/programs-surveys/cbp.html), [OpenStreetMap](https://www.openstreetmap.org/) |
| Density of restaurant POIs | **Positive (+)** for trip productions, \(p<0.01\). The trip-attraction model uses a combined restaurant-and-bar variable rather than restaurant density alone. | Census County Business Patterns food-service and drinking-place establishments or OpenStreetMap | [Census CBP](https://www.census.gov/programs-surveys/cbp.html), [OpenStreetMap](https://www.openstreetmap.org/) |
| Density of restaurant and bar POIs | **Positive (+)** for trip attractions, \(p<0.01\). | Census CBP NAICS 722 and related subcategories, or OpenStreetMap | [Census CBP](https://www.census.gov/programs-surveys/cbp.html), [OpenStreetMap](https://www.openstreetmap.org/) |
| Share of residents aged 18–34 | **Positive (+)** for both trip productions and trip attractions, \(p<0.01\). | ACS age-by-sex population tables | [ACS B01001 Sex by Age](https://api.census.gov/data/2024/acs/acs5/groups/B01001.html) |
| Share of residents identifying as female | **Negative (-)** for trip productions, \(p<0.01\), and trip attractions, \(p<0.05\). | ACS sex-by-age population tables | [ACS B01001](https://api.census.gov/data/2024/acs/acs5/groups/B01001.html) |
| Median household income | **Positive (+)** for both trip productions and trip attractions, \(p<0.01\). | ACS B19013 Median Household Income | [ACS B19013](https://api.census.gov/data/2024/acs/acs5/groups/B19013.html) |
| Share of zero-vehicle households | **Positive (+)** for trip productions, \(p<0.01\). It was not retained in the final trip-attraction model. | ACS B08201 Household Size by Vehicles Available | [ACS B08201](https://api.census.gov/data/2024/acs/acs5/groups/B08201.html) |
| Disadvantaged or equity-priority community designation | **Negative (-)** for both trip productions and trip attractions, \(p<0.01\). | California OEHHA CalEnviroScreen and MTC Equity Priority Communities. The same definition cannot be transferred directly to nationwide comparisons. | [CalEnviroScreen](https://oehha.ca.gov/calenviroscreen), [MTC Equity Priority Communities](https://mtc.ca.gov/planning/transportation/access-equity-mobility/equity-priority-communities) |

## Other Findings from the Paper

### Spatial and Temporal Characteristics of Observed Demand

- Mean monthly robotaxi trip productions per census tract increased from approximately 241 trips in September 2023 to approximately 1,410 trips in August 2024.
- Demand was concentrated in downtown San Francisco and areas popular with tourists.
- Trip productions and trip attractions exhibited statistically significant positive spatial autocorrelation in every month of the study period.
- Because neighboring census tracts were not independent, the study estimated pooled spatial lag models.

### Findings Related to Trip Purpose

The densities of art, entertainment, recreation, restaurant, and bar POIs were positively associated with demand. The authors interpret these results as evidence that robotaxis tend to be used for **discretionary activities**, including leisure, dining, and entertainment.

### Findings Related to Public Transit

Transit-service frequency was positively associated with robotaxi demand. However, this result alone does not establish a causal complementary relationship between transit and robotaxis. Areas with frequent transit service may also be downtown, employment, commercial, and entertainment centers.

### Main Limitations

- The study examines one city and one period.
- The dataset is aggregated at the census-tract level, so individual user characteristics cannot be observed.
- The one-year study period is insufficient to identify stable long-term or seasonal demand patterns.
- Supply-side changes, service-area expansion, prices, and waiting times could not be fully controlled.
- The results describe differences across census tracts **within San Francisco**. The estimated coefficients are not guaranteed to explain demand differences across cities.

## Paper Conclusion

> Observed robotaxi demand in San Francisco was positively associated with land-use mix, walkability, transit-service frequency, median household income, and leisure- and dining-related POI density. In contrast, population density and disadvantaged or equity-priority community designation were associated with lower demand. Among the studies reviewed here, this paper provides the strongest direct empirical evidence on robotaxi demand determinants.

---

# 2. *Ride-sharing Determinants: Spatial and Spatio-temporal Bayesian Analysis for Chicago Service in 2022*

**Authors:** Mohamed Elkhouly and Taqwa Alhadidi  
**Paper link:** [arXiv](https://arxiv.org/abs/2406.11590)  
**Study scope:** Ride-sharing demand across Chicago’s 77 community areas in 2022  
**Evidence level:** **Indirect ride-sharing evidence; not direct robotaxi evidence**

The study analyzes demographic, socioeconomic, transportation, and land-use variables using spatial and spatiotemporal Bayesian models. The reported squared correlation between observed and fitted values in the spatiotemporal model was 0.95.

## Ride-Sharing Demand Variables

| Variable associated with ride-sharing demand | Estimated direction and paper result | Official measurement data | Official data link |
|---|---|---|---|
| Population size | **Positive (+)**. Reported in the abstract as a primary demographic determinant. | Census ACS B01003 | [ACS B01003](https://api.census.gov/data/2024/acs/acs5/groups/B01003.html) |
| Crime incidence | **Positive (+)**. Reported with population as a primary demographic determinant. | FBI Crime Data Explorer or official city police open data | [FBI Crime Data Explorer](https://cde.ucr.cjis.gov/) |
| Median income or income level | **Positive (+)**. Higher-income areas were associated with greater ride-sharing demand. | ACS B19013 | [ACS B19013](https://api.census.gov/data/2024/acs/acs5/groups/B19013.html) |
| Share of economically active residents | **Positive (+)**. A larger economically active population was associated with greater demand. | ACS B23025 Employment Status | [ACS B23025](https://api.census.gov/data/2024/acs/acs5/groups/B23025.html) |
| Share of car-free residents or households | **Positive (+)**. A larger car-free population was associated with greater demand. | ACS B08201 or B25044 | [ACS B08201](https://api.census.gov/data/2024/acs/acs5/groups/B08201.html), [ACS B25044](https://api.census.gov/data/2024/acs/acs5/groups/B25044.html) |
| Public-transit availability | Reported as an important determinant, but the abstract alone does not support assigning one universal coefficient direction. | EPA SLD transit-frequency and accessibility variables, National Transit Database, and local GTFS feeds | [EPA SLD](https://www.epa.gov/smartgrowth/smart-location-mapping), [FTA National Transit Database](https://www.transit.dot.gov/ntd), [GTFS](https://gtfs.org/documentation/overview/) |
| Walkability | Reported as an important determinant, but the abstract alone does not support assigning one universal coefficient direction. | EPA National Walkability Index | [EPA Smart Location Mapping](https://www.epa.gov/smartgrowth/smart-location-mapping) |

## Other Findings from the Paper

- The spatial model accounts for spatial correlation across community areas.
- The spatiotemporal model captures both geographic differences and temporal variation.
- The authors identify population and crime as the most important demographic factors.
- Income, economic activity, and car-free households were associated with higher demand.
- Public-transit availability and walkability were also important, but the abstract does not establish a single coefficient direction that can be applied consistently across all model specifications.

### Caution for Robotaxi Research

This paper examines ride-sharing demand in Chicago. It supports the following statement:

> Prior ride-sharing research reports that population, income, economic activity, and car-free households are associated with demand.

It does **not** support the stronger statement:

> These variables increase robotaxi demand.

For a robotaxi model, these variables should be labeled as **candidate contextual variables supported by proxy evidence**.

## Paper Conclusion

> Chicago ride-sharing demand was associated with demographic and socioeconomic characteristics, including population, crime, income, economic activity, and car-free households. Whether these effects have the same direction for robotaxi demand must be tested separately.

---

# 3. *Examining spatial heterogeneity of ridesourcing demand determinants with explainable machine learning*

**Authors:** Xiaojian Zhang, Xiang Yan, Zhengze Zhou, Yiming Xu, and Xilei Zhao  
**Paper link:** [arXiv](https://arxiv.org/abs/2209.07980)  
**Study scope:** Chicago ridesourcing trips, divided into airport, downtown, and neighborhood spatial contexts  
**Evidence level:** **Indirect ridesourcing evidence; not direct robotaxi evidence**

This study uses explainable machine learning to examine how the importance and nonlinear effects of ridesourcing-demand determinants differ across spatial contexts.

## Ridesourcing Demand Variables

The central finding is not that each variable has one universal positive or negative effect. Instead, the effects are **nonlinear and context-dependent** across airport, downtown, and neighborhood trips.

| Variable associated with ridesourcing demand | Estimated direction and paper result | Official measurement data | Official data link |
|---|---|---|---|
| Land-use mix | **Nonlinear and spatially heterogeneous.** It contributes to ridesourcing-demand prediction as part of the built-environment variable group, but the paper does not establish one universal positive linear effect across all contexts. | EPA SLD land-use entropy | [EPA Smart Location Database](https://www.epa.gov/smartgrowth/smart-location-mapping) |
| Walkability | **Nonlinear and spatially heterogeneous.** It is an important built-environment factor, but should not be assigned one universal directional effect. | EPA National Walkability Index | [EPA Smart Location Mapping](https://www.epa.gov/smartgrowth/smart-location-mapping) |
| Intersection density and street connectivity | **Nonlinear and spatially heterogeneous.** | EPA SLD intersection-density measures | [EPA Smart Location Database](https://www.epa.gov/smartgrowth/smart-location-mapping) |
| Population and employment density | **Nonlinear and spatially heterogeneous.** | ACS population, Census LEHD LODES employment, and EPA SLD | [ACS](https://www.census.gov/programs-surveys/acs), [LEHD/LODES](https://lehd.ces.census.gov/data/), [EPA SLD](https://www.epa.gov/smartgrowth/smart-location-mapping) |
| Destination accessibility and commercial activity | **Nonlinear and spatially heterogeneous.** | EPA SLD destination-accessibility measures and Census CBP establishment data | [EPA SLD](https://www.epa.gov/smartgrowth/smart-location-mapping), [Census CBP](https://www.census.gov/programs-surveys/cbp.html) |
| Public-transit accessibility | **Nonlinear and spatially heterogeneous.** | EPA SLD, FTA NTD, and local GTFS feeds | [EPA SLD](https://www.epa.gov/smartgrowth/smart-location-mapping), [National Transit Database](https://www.transit.dot.gov/ntd) |
| Airport spatial context | The built-environment variable group collectively had the **largest predictive importance** for airport trips. This is not an estimated coefficient for airport passenger volume. | FAA annual passenger enplanements | [FAA Passenger Boarding Data](https://www.faa.gov/airports/planning_capacity/passenger_allcargo_stats/passenger) |

## Other Findings from the Paper

- The importance of the built environment differed across airport, downtown, and neighborhood contexts.
- Collectively, built-environment variables had the greatest predictive importance for airport-trip demand.
- In contrast, ridesourcing demand was generally most responsive to built-environment changes for downtown trips, followed by neighborhood trips and airport trips.
- Therefore, “the built environment is most important for airport trips” and “airport demand is most responsive to built-environment changes” are not equivalent statements:
  - The first refers to relative predictive importance.
  - The second refers to the magnitude of demand response.
- Because the study uses explainable machine learning, it does not estimate one fixed positive or negative regression coefficient for every variable.

### Correct Interpretation of Airport Passenger Volume

The study treats airport trips as a separate spatial context. It does **not** estimate a relationship of the form:

> A given increase in FAA enplanements causes a specific increase in citywide ridesourcing demand.

FAA enplanements can therefore be used as:

- an official indicator of the size of the airport-related travel market; and
- a potential measure of an airport demand anchor.

However, this paper does not justify assigning airport passenger volume a universally positive linear coefficient.

## Paper Conclusion

> The relationship between the built environment and ridesourcing demand is nonlinear and varies across airport, downtown, and neighborhood contexts. A demand model should therefore distinguish spatial contexts rather than impose one identical coefficient across an entire city.

---

# 4. *Beyond the Dichotomy: How Ride-hailing Competes with and Complements Public Transport*

**Authors:** Oded Cats, Rafał Kucharski, Santosh Rao Danda, and Menno Yap  
**Paper link:** [arXiv](https://arxiv.org/abs/2104.04208)  
**Published version:** [PLOS ONE DOI](https://doi.org/10.1371/journal.pone.0262496)  
**Study scope:** Uber trips in six U.S. and European cities, compared with the best available public-transport alternative for each trip  
**Evidence level:** **Indirect ride-hailing evidence; not direct robotaxi evidence**

The paper concludes that the relationship between ride-hailing and public transport cannot be described as universally competitive or universally complementary.

## Ride-Hailing Demand Variables

| Variable associated with ride-hailing demand | Estimated direction and paper result | Official measurement data | Official data link |
|---|---|---|---|
| Relative travel-time competitiveness of ride-hailing versus public transport | Ride-hailing demand share was higher when ride-hailing was relatively faster. Ride-hailing demand share was lower when public-transport travel time was competitive. | Official transit-agency GTFS Schedule, GTFS Realtime, and road travel-time data | [GTFS Documentation](https://gtfs.org/documentation/overview/), [FTA National Transit Database](https://www.transit.dot.gov/ntd) |
| Availability of a viable public-transport alternative | Trips without a viable transit alternative were associated with the complementary, gap-filling role of ride-hailing. The study reported that approximately 20%–40% of ride-hailing trips lacked a viable public-transport alternative, depending on the city. | Official GTFS data used to calculate routing, travel time, transfers, and service availability | [GTFS](https://gtfs.org/documentation/overview/) |
| Public-transport service accessibility | Adding ride-hailing increased overall service accessibility, and the increase was larger in the analyzed U.S. cities than in the European cities. | EPA SLD transit accessibility, FTA NTD, and Census LEHD LODES job-accessibility measures | [EPA SLD](https://www.epa.gov/smartgrowth/smart-location-mapping), [FTA NTD](https://www.transit.dot.gov/ntd), [LEHD/LODES](https://lehd.ces.census.gov/data/) |
| Relative monetary cost of public transport and ride-hailing | Monetary cost was part of the comparison, but the paper’s main conclusion emphasizes relative travel-time competitiveness. A single independent cost direction should not be assigned based on the abstract alone. | Official transit fare data and GTFS fare files | [GTFS Schedule Reference](https://gtfs.org/documentation/schedule/reference/) |

## Other Findings from the Paper

- Most ride-hailing trips had a formally available public-transport alternative.
- Depending on the city, approximately 20%–40% of trips lacked a viable public-transport alternative.
- When public-transport travel time was competitive with ride-hailing, ride-hailing demand share was lower.
- When public transport was relatively slow or did not provide a viable alternative, ride-hailing demand share was higher.
- Ride-hailing increased accessibility more in the analyzed U.S. cities than in the European cities.
- Ride-hailing therefore competes with public transport for some trips while filling service gaps for others.

### Caution for Robotaxi Research

These findings do not directly measure a robotaxi-specific technology effect. However, because robotaxis are also on-demand, point-to-point mobility services, the evidence supports testing variables such as:

\[
\text{Transit competitiveness}
=
\text{Transit travel time}
-
\text{Robotaxi travel time}
\]

In a candidate city without existing robotaxi service, actual robotaxi travel times and prices are unavailable. Early-stage analysis may therefore require conventional ride-hailing travel times, prices, or operational estimates as proxies.

## Paper Conclusion

> Ride-hailing and public transport are neither universally competitive nor universally complementary. Ride-hailing demand share declines when public transport is competitive in travel time, while ride-hailing fills accessibility gaps when viable public-transport alternatives are unavailable.

---

# Final Variables that may be considered for Research

## A. Variables with Direct Empirical Evidence from Observed Robotaxi Demand

Among the studies reviewed here, only Paper 1 provides direct empirical evidence.

- Population density: negative
- Employment density: positive for trip attractions
- Land-use mix: positive
- Transit-service frequency: positive
- Walkability: positive
- Art, entertainment, and recreation POI density: positive
- Restaurant and bar POI density: positive
- Share of residents aged 18–34: positive
- Share of female residents: negative
- Median household income: positive
- Share of zero-vehicle households: positive for trip productions
- Disadvantaged or equity-priority community designation: negative

These findings describe variation **across census tracts within San Francisco**. They should not automatically be treated as city-level causal effects.

## B. Variables Supported Only by Indirect Ride-Sharing or Ridesourcing Evidence

- City population size
- Crime incidence
- Share of economically active residents
- Airport, downtown, and neighborhood spatial context
- Nonlinear effects of intersection density
- Relative public-transport versus ride-hailing travel time
- Availability of a viable transit alternative
- Public-transport disruptions and service gaps

These variables can be included as candidate predictors in a robotaxi-demand model, but they should be labeled:

> Evidence from conventional ride-sharing or ridesourcing demand, not from observed robotaxi demand.

## C. Interpretation Cautions

- **Population density is not necessarily positive.** The observed robotaxi study found a negative association.
- **Public-transit accessibility is not necessarily negative.** Transit-service frequency was positively associated with robotaxi demand in San Francisco, while the six-city ride-hailing study found that competition or complementarity depends on relative travel time and service availability.
- **The reviewed papers do not establish a direct robotaxi-demand coefficient for airport passenger volume.**
- **Intersection density and other built-environment effects may be nonlinear and spatially heterogeneous.**
- Associations should not be described as causal effects unless a study explicitly identifies causality.
