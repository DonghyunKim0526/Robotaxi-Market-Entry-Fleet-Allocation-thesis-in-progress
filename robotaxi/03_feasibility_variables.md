# Robotaxi City-Entry Feasibility Variables

This document summarizes variables that determine whether a robotaxi service can legally, technically, and operationally enter and operate in a city.

## Scope

\[
	ext{Demand prediction}

ightarrow
	ext{City feasibility filtering}

ightarrow
	ext{Fleet allocation}
\]

The question addressed here is:

> Even if a city has sufficient potential demand, can a robotaxi service legally and technically operate there?

---

# 1. *A Framework for Automated Driving System Testable Cases and Scenarios*

**Institution:** U.S. Department of Transportation / National Highway Traffic Safety Administration  
**Document type:** Federal technical framework  
**Document link:** [NHTSA PDF](https://www.nhtsa.gov/sites/nhtsa.gov/files/documents/13882-automateddrivingsystems_092618_v1a_tag.pdf)  
**Evidence level:** **Official federal evidence on ADS operating conditions**

This document does not estimate the probability that a robotaxi company will enter a particular city. Instead, it defines the elements of the **Operational Design Domain (ODD)**, meaning the conditions under which an automated driving system is designed to operate.

## Feasibility variables identified in the document

| Robotaxi feasibility variable | Source content and relevance | Expected role in city feasibility | Official measurement data | Official data link |
|---|---|---|---|---|
| Geographic operating area | The ODD includes the geographic area in which the ADS is designed to operate. A robotaxi system cannot be assumed to provide the same performance outside its validated and authorized area. | Areas outside the approved geofence are not serviceable. **Hard constraint** | Company service-area maps and state deployment permits | [California DMV AV Programs](https://www.dmv.ca.gov/portal/vehicle-industry-services/autonomous-vehicles/) |
| Roadway type | The ODD includes supported roadway types such as freeways, arterials, and local streets. | Trips requiring unsupported roadway types are infeasible or require detours. | FHWA HPMS functional classification | [FHWA HPMS](https://www.fhwa.dot.gov/policyinformation/hpms.cfm) |
| Speed range | An ADS may be designed to operate only within a specified speed range. | Roads outside the supported speed range cannot be served. | HPMS or local DOT speed-limit GIS | [FHWA HPMS](https://www.fhwa.dot.gov/policyinformation/hpms.cfm) |
| Environmental and weather conditions | Weather and environmental conditions are core ODD elements. | Rain, snow, fog, ice, or other conditions may reduce operating time or available fleet capacity. | NOAA hourly weather observations | [NOAA Climate Data Online](https://www.ncei.noaa.gov/cdo-web/) |
| Lighting and time of day | The ODD may restrict operation by daylight, nighttime, or lighting conditions. | Determines feasible operating hours and daily vehicle productivity. | Sunrise/sunset data and company ODD or permit conditions | [NOAA Solar Calculator](https://gml.noaa.gov/grad/solcalc/) |
| Traffic and operational constraints | Traffic conditions and other operational limitations may define the ADS operating envelope. | Certain traffic conditions may limit service availability or require operational restrictions. | Local DOT traffic counts, FHWA data, and NPMRDS | [FHWA Operations](https://ops.fhwa.dot.gov/) |
| Temporary road configuration and work zones | Temporary road layouts, including construction zones, are relevant ADS test scenarios. | Active work zones can reduce route availability and reliability. | Local DOT work-zone feeds and WZDx | [USDOT Work Zone Data Exchange](https://www.transportation.gov/av/data/wzdx) |

## Other relevant findings

- The ODD is not a single score. It is a combination of geography, roadway type, speed, weather, lighting, traffic, and temporary operating conditions.
- A single, researcher-created “ODD suitability score” may conceal important differences among these components.
- Different parts of the same city can have different feasibility.
- The appropriate unit of analysis is often the **road segment or proposed service zone**, not the city as a whole.

## Document conclusion

> Robotaxi city-entry feasibility must be evaluated against the specific ODD supported by the ADS. Geographic area, roadway type, speed range, weather, lighting, traffic, and temporary road conditions should therefore be represented as explicit feasibility conditions rather than general demand predictors.

---

# 2. California DMV Autonomous Vehicle Programs and CPUC Passenger Service Programs

**Institutions:** California Department of Motor Vehicles; California Public Utilities Commission  
**Source links:**  
- [California DMV Autonomous Vehicles](https://www.dmv.ca.gov/portal/vehicle-industry-services/autonomous-vehicles/)  
- [CPUC Autonomous Vehicle Programs](https://www.cpuc.ca.gov/regulatory-services/licensing/transportation-licensing-and-analysis-branch/autonomous-vehicle-programs)  
**Evidence level:** **Official regulatory evidence on legal and commercial robotaxi entry**

## Regulatory feasibility variables

| Robotaxi feasibility variable | Source content and relevance | Expected role | Official measurement method | Official data link |
|---|---|---|---|---|
| Driverless testing legally permitted | A separate permit is required to test without a safety driver on public roads. | Without authorization, driverless testing is infeasible. **Hard constraint** | Permit held by operator: 0/1 | [California DMV AV Programs](https://www.dmv.ca.gov/portal/vehicle-industry-services/autonomous-vehicles/) |
| Driverless deployment legally permitted | Deployment authorization is separate from testing authorization. | Without deployment authorization, public driverless deployment is infeasible. | Deployment permit held: 0/1 | [California DMV AV Programs](https://www.dmv.ca.gov/portal/vehicle-industry-services/autonomous-vehicles/) |
| Paid passenger service authorized | Paid passenger service requires separate passenger-service authorization. | Commercial robotaxi service is infeasible without authorization. | Paid-service authorization: 0/1 | [CPUC AV Programs](https://www.cpuc.ca.gov/regulatory-services/licensing/transportation-licensing-and-analysis-branch/autonomous-vehicle-programs) |
| Authorized geography | Permits may restrict geographic operating areas. | Vehicles cannot be allocated outside authorized geography. | Permit geography and service-area GIS overlap | DMV permit documentation |
| Authorized operating conditions | Permits may specify hours, road types, speed limits, or other restrictions. | Limits route coverage and effective operating time. | Permit-specific restrictions | DMV permit documentation |
| Reporting requirements | CPUC requires operational reporting and publishes quarterly data. | Affects compliance burden and data availability. | Reporting frequency and required fields | [CPUC Quarterly Reporting](https://www.cpuc.ca.gov/regulatory-services/licensing/transportation-licensing-and-analysis-branch/autonomous-vehicle-programs/quarterly-reporting) |
| Insurance and safety-plan requirements | Passenger-service programs impose insurance and safety obligations. | Adds entry cost and compliance requirements. | Required insurance and safety-plan submission | CPUC AV Programs |

## Other relevant findings

\[
R_i^{test},\quad R_i^{deploy},\quad R_i^{paid}
\]

where:

- \(R_i^{test}\): driverless testing is permitted;
- \(R_i^{deploy}\): driverless deployment is permitted;
- \(R_i^{paid}\): paid passenger service is permitted.

## Source conclusion

> Regulatory feasibility should be represented through explicit permissions for testing, deployment, and paid passenger service. These variables are better modeled as binary or categorical eligibility constraints than as continuous demand predictors.

---

# 3. Waymo Flooded-Road Recall and Weather-Related Operating Restrictions

**Source:** Reuters, based on Waymo and NHTSA recall information  
**Article link:** [Reuters report](https://www.reuters.com/legal/litigation/waymo-recall-nearly-3800-robotaxis-over-self-driving-software-issue-2026-05-12/)  
**Evidence level:** **Direct operational evidence that weather and flooding can restrict robotaxi operations**

## Feasibility variables supported by the incident

| Robotaxi feasibility variable | Observed operational evidence | Expected effect | Official measurement data | Official data link |
|---|---|---|---|---|
| Heavy-rain frequency | Intense rain contributed to operational restrictions. | More heavy-rain exposure may increase weather-related downtime. | Hourly precipitation and heavy-rain days | [NOAA Climate Data Online](https://www.ncei.noaa.gov/cdo-web/) |
| Flash-flood exposure | Access to flash-flood-prone areas was restricted. | Reduces route availability and service-area coverage. | Flash-flood events, warnings, and hazard zones | [NOAA Storm Events Database](https://www.ncei.noaa.gov/access/monitoring/storm-events/) |
| Flood-exposed road share | A flooded roadway contributed to the recall and operating-scope restrictions. | A larger exposed road network may reduce usable road capacity. | FEMA flood layers combined with road GIS | [FEMA National Flood Hazard Layer](https://www.fema.gov/flood-maps/national-flood-hazard-layer) |
| Weather-related operating restriction | Operating scope was narrowed during severe weather. | Reduces effective fleet availability. | Service interruption or restricted-operating hours | Operator incident and service logs |
| Map and route updates | Hazard areas were restricted while a permanent remedy was developed. | Changes dynamic route feasibility and geofence. | Proprietary map data; public substitute is road-closure data | Local DOT and 511 feeds |

\[
a_{i,t}^{\omega}\in[0,1]
\]

\[
x_{i,t}^{effective,\omega}
=
a_{i,t}^{\omega}x_{i,t}
\]

## Source conclusion

> The Waymo recall provides direct operational evidence that intense rainfall, flooded roads, and flash-flood exposure can narrow a robotaxi system’s operating scope. These variables should be represented as scenario-dependent operational-availability factors, not merely as demand covariates.

---

# 4. FHWA Highway and Work-Zone Data

**Source links:**  
- [FHWA Highway Performance Monitoring System](https://www.fhwa.dot.gov/policyinformation/hpms.cfm)  
- [USDOT Work Zone Data Exchange](https://www.transportation.gov/av/data/wzdx)  

| Variable | What the official data can measure | Expected relevance | Data source |
|---|---|---|---|
| Functional road class | Interstate, freeway, arterial, collector, and local road | Compatibility with ADS-supported roadway types | FHWA HPMS |
| Traffic volume | Annual average daily traffic and related measures | Congestion and route exposure | FHWA HPMS |
| Road mileage by class | Composition of the city or service zone | Freeway dependency and local-road share | FHWA HPMS |
| Work-zone presence | Active work zone, lane closure, temporary geometry | Temporary route availability and ODD complexity | WZDx |
| Lane closure | Location and duration | Reduces road capacity and routing options | WZDx |
| Work-zone duration | Start and end time | Determines time-varying service feasibility | WZDx |

\[
	ext{Freeway feasibility}
=
	ext{city freeway dependence}
	imes
	ext{ADS freeway capability}
\]

\[
C_{r,t}
=
egin{cases}
1,&	ext{road segment }r	ext{ is affected by construction at }t\
0,&	ext{otherwise}
\end{cases}
\]

## Source conclusion

> Road type, freeway dependence, traffic volume, and active construction should be measured at the road-segment or service-zone level. Their effects depend on the capabilities of the specific ADS and should not be assigned a universal positive or negative sign.

---

# 5. FEMA and NOAA Hazard Data

**Source links:**  
- [FEMA National Risk Index](https://hazards.fema.gov/nri/)  
- [FEMA National Flood Hazard Layer](https://www.fema.gov/flood-maps/national-flood-hazard-layer)  
- [NOAA Storm Events Database](https://www.ncei.noaa.gov/access/monitoring/storm-events/)  
- [NOAA Climate Data Online](https://www.ncei.noaa.gov/cdo-web/)  

| Variable | Official measurement | Expected role | Limitation |
|---|---|---|---|
| Heavy-rain days | Number of observations above a threshold | Weather-related service reduction | Actual ADS rainfall threshold is proprietary |
| Snow and ice days | Snowfall, snow depth, freezing temperatures | May reduce operating hours and route availability | Company ODDs differ |
| Low-visibility hours | Station-level visibility | Exposure to sensor and operating limitations | Does not fully capture urban microclimates |
| Flash-flood events | Recorded NOAA events | Frequency of service-interruption scenarios | Past events do not equal future risk |
| Floodplain road share | Overlap between FEMA flood layers and road networks | Fraction of road network exposed to flooding | Actual flooding depends on rainfall and drainage |
| Hazard-related expected annual loss | FEMA risk indicators | Long-run hazard exposure | Not robotaxi-specific |

## Source conclusion

> FEMA and NOAA data can quantify the frequency and spatial exposure of weather and flood hazards, but they do not independently establish an ADS’s operating limit. They should be combined with company-specific ODD thresholds whenever those thresholds are available.

---

# 6. DOE Alternative Fuels Data Center

**Source links:**  
- [Alternative Fueling Station Locator](https://afdc.energy.gov/stations/)  
- [AFDC Data Downloads](https://afdc.energy.gov/data_download)  

| Variable | Official measurement | Expected role in feasibility | Limitation |
|---|---|---|---|
| Public charging-station count | Station locations | General EV-infrastructure availability | Does not equal robotaxi depot capacity |
| DC fast-charger count | Charger type by station | Availability of faster charging | Does not capture access rights or congestion |
| Connector count | Number of simultaneous connectors | Proxy for concurrent charging capacity | Private fleet reservation is unknown |
| Charger power | Charger level and power | Helps estimate charging duration | Vehicle-specific charging curves are needed |
| Distance to service area | Station coordinates relative to geofence | Charging deadhead time | Private depots are omitted |

## Source conclusion

> AFDC data provides a nationwide measure of general EV charging infrastructure. It should be treated as a proxy for local charging readiness, not as direct evidence of proprietary robotaxi depot capacity.

---

# Feasibility Variables: Final Classification

| Variable | Direct source support | Measurement feasibility | Recommended model role |
|---|---:|---:|---|
| Driverless deployment permission | Strong | High | Hard constraint |
| Paid passenger-service permission | Strong | High | Hard constraint |
| Authorized geographic area | Strong | Medium | Hard constraint |
| Supported roadway type | Strong | Medium | Hard constraint or coverage ratio |
| Supported speed range | Strong | Medium | Hard constraint |
| Weather-compatible hours | Strong conceptually | Medium | Effective availability |
| Heavy-rain frequency | Strong operational evidence | High | Scenario variable |
| Flood-exposed road share | Strong operational evidence | High | Scenario availability |
| Work-zone exposure | Strong operational relevance | Medium | Time-varying route capacity |
| Freeway dependency | Conditional evidence | High | Interaction with ADS capability |
| Traffic congestion | Strong operational relevance | Medium | Vehicle productivity |
| Public charging capacity | Moderate | High | Infrastructure proxy |
| Private depot capacity | Strong operational need | Low | Capacity or entry-cost parameter |
| HD-map availability | Operationally relevant | Low | Exclude unless company data are available |
| Public trust | Relevant but difficult to isolate | Low–medium | Separate adoption or regulatory analysis |

---

# Final Research Variables

1. Driverless deployment legally allowed  
2. Paid passenger service legally allowed  
3. Authorized geographic service area  
4. Supported roadway-type share  
5. Supported speed-range share  
6. Weather-compatible operating hours  
7. Heavy-rain frequency  
8. Flood-exposed road share  
9. Work-zone exposure  
10. Freeway dependence × freeway capability  
11. Charging capacity  
12. Depot availability and cost  

## Suggested feasibility constraints

\[
y_i\le R_i^{legal}
\]

\[
	ext{service}_{r,t}
\le
R_{r}^{road}
R_{r}^{speed}
R_{r,t}^{weather}
R_{r,t}^{construction}
\]
