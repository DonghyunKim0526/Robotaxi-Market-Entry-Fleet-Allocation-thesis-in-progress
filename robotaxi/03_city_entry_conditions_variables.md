# Observable Conditions for Robotaxi City Entry

This document reorganizes robotaxi city-entry conditions into three evidence categories:

1. **Publicly confirmed prerequisites or enabling factors**
2. **Operational risks demonstrated by actual events**
3. **Variables that can be constructed from public datasets**

The purpose of this classification is to separate:

- conditions that are explicitly required or publicly confirmed;
- operational risks that have been observed in real robotaxi service;
- researcher-constructed variables that can be measured across cities but are not publicly confirmed corporate city-selection criteria.

---

# 1. Publicly Confirmed Prerequisites or Enabling Factors

These variables are supported by official regulatory documents, company service structures, or publicly disclosed operating arrangements.

They should not be interpreted as a complete list of the internal criteria used by robotaxi companies when selecting cities. They are conditions that are publicly confirmed as necessary or enabling for deployment.

## 1.1 Driverless testing authorization

**Meaning:** Whether an operator is legally permitted to test autonomous vehicles on public roads without a human safety driver.

**Why it matters:** A company cannot complete local driverless validation without the relevant authorization.

**Recommended variable form:**

- `driverless_testing_allowed = 1` if legally permitted and authorized
- `driverless_testing_allowed = 0` otherwise

**Evidence:** California DMV separates testing with a safety driver, driverless testing, and deployment into distinct authorization categories.

**Source:**  
[California DMV — Autonomous Vehicles](https://www.dmv.ca.gov/portal/vehicle-industry-services/autonomous-vehicles/)

---

## 1.2 Driverless deployment authorization

**Meaning:** Whether an operator is legally permitted to deploy driverless vehicles beyond the testing stage.

**Why it matters:** Testing authorization does not automatically permit commercial or general driverless deployment.

**Recommended variable form:**

- `driverless_deployment_allowed = 1` if deployment is legally authorized
- `driverless_deployment_allowed = 0` otherwise

**Evidence:** California DMV treats deployment as a separate authorization category from testing.

**Source:**  
[California DMV — Autonomous Vehicles](https://www.dmv.ca.gov/portal/vehicle-industry-services/autonomous-vehicles/)

---

## 1.3 Paid passenger-service authorization

**Meaning:** Whether the operator is authorized to provide paid passenger service.

**Why it matters:** A company may be allowed to test or deploy vehicles but still lack authority to carry paying passengers.

**Recommended variable form:**

- `paid_passenger_service_allowed = 1`
- `paid_passenger_service_allowed = 0`

**Evidence:** The California Public Utilities Commission manages autonomous passenger-service programs separately from DMV vehicle-deployment authorization.

**Source:**  
[CPUC — Autonomous Vehicle Passenger Service Programs](https://www.cpuc.ca.gov/regulatory-services/licensing/transportation-licensing-and-analysis-branch/autonomous-vehicle-programs)

---

## 1.4 Authorized geographic service area

**Meaning:** The geographic area in which the operator is authorized and technically prepared to operate.

**Why it matters:** Robotaxi deployment is generally geofenced. Vehicles cannot be assumed to operate throughout an entire metropolitan area simply because service exists in one part of the city.

**Recommended variable forms:**

- authorized service-area size in square miles;
- share of the target market covered by the authorized geofence;
- number of population or employment centers inside the geofence.

**Evidence:** Regulatory permits and company service-area announcements define or limit where vehicles may operate.

**Sources:**  
[California DMV — Autonomous Vehicles](https://www.dmv.ca.gov/portal/vehicle-industry-services/autonomous-vehicles/)  
[Waymo — Where Waymo Operates](https://waymo.com/rides/)

---

## 1.5 Operational Design Domain compatibility

**Meaning:** Whether the proposed roads, speeds, environmental conditions, lighting conditions, and operating situations are inside the ADS's supported Operational Design Domain.

**Why it matters:** An ADS is designed for a specified operating domain rather than every possible roadway and environmental condition.

**Publicly identified ODD components include:**

- geographic area;
- roadway type;
- speed range;
- weather and environmental conditions;
- lighting conditions;
- traffic and operational conditions.

**Recommended variable forms:**

- share of proposed service roads supported by the ADS;
- share of proposed operating hours inside the ADS weather and lighting limits;
- share of required routes compatible with supported speed ranges.

**Evidence:** NHTSA identifies roadway, geographic, speed, weather, lighting, and operational conditions as core ODD dimensions.

**Source:**  
[NHTSA — A Framework for Automated Driving System Testable Cases and Scenarios](https://www.nhtsa.gov/sites/nhtsa.gov/files/documents/13882-automateddrivingsystems_092618_v1a_tag.pdf)

---

## 1.6 Prior local testing and operational validation

**Meaning:** Whether the operator has already accumulated testing and validation experience in the target city or service area.

**Why it matters:** Commercial deployment generally follows local mapping, simulation, road testing, safety validation, and gradual service expansion.

**Recommended variable forms:**

- months or years of prior local testing;
- local autonomous miles driven;
- whether driverless testing has occurred in the city;
- whether public-rider pilots have already operated.

**Evidence level:** Public company announcements and regulatory records often confirm testing or pilot activity before commercial rollout.

**Potential sources:**

- company press releases;
- DMV permit-holder records;
- local pilot announcements;
- company safety reports.

**Example sources:**  
[Waymo — Latest Updates](https://waymo.com/blog/)  
[California DMV — Autonomous Vehicles](https://www.dmv.ca.gov/portal/vehicle-industry-services/autonomous-vehicles/)

---

## 1.7 Local operating or platform partnership

**Meaning:** Whether the robotaxi operator has a local ride-hailing, fleet-management, or service-distribution partner.

**Why it matters:** A partner may provide customer access, fleet operations, cleaning, charging, maintenance, or local market infrastructure.

**Recommended variable forms:**

- `local_platform_partnership = 1/0`;
- type of partnership;
- partner-operated versus operator-operated service.

**Evidence:** Waymo service in Austin and Atlanta is provided through Uber, demonstrating that platform and fleet-operation partnerships can enable market entry.

**Source:**  
[Waymo — Where Waymo Operates](https://waymo.com/rides/)

---

## 1.8 Feasible initial geofence

**Meaning:** Whether the city contains a limited, operationally manageable area in which initial service can be launched.

**Why it matters:** Many robotaxi services begin in a restricted area rather than covering an entire city.

**Recommended variable forms:**

- size of feasible initial service area;
- number of major destinations inside the initial geofence;
- road-network connectivity within the geofence;
- ability to avoid unsupported road types.

**Evidence:** Company service rollouts are commonly organized around defined service areas and gradual geographic expansion.

**Sources:**  
[Waymo — Where Waymo Operates](https://waymo.com/rides/)  
[Zoox — Where to Ride](https://zoox.com/where-to-ride)

---

## 1.9 Charging and depot feasibility

**Meaning:** Whether the operator can establish sufficient charging, parking, cleaning, dispatch, and maintenance capacity.

**Why it matters:** Even when public-road operations are legally and technically feasible, fleet service cannot scale without supporting facilities.

**Recommended variable forms:**

- feasible depot site available: 1/0;
- estimated depot construction or lease cost;
- charging stalls available;
- vehicles serviceable per hour;
- average distance between depot and service area.

**Evidence level:** This is an operational prerequisite, but robotaxi companies generally do not disclose complete city-selection thresholds for depot and charging capacity.

**Potential official measurement source:**  
[U.S. Department of Energy — Alternative Fueling Station Locator](https://afdc.energy.gov/stations/)

**Important limitation:** Public chargers do not directly measure proprietary robotaxi depot capacity.

---

# 2. Operational Risks Demonstrated by Actual Events

These factors have been shown to affect real robotaxi operations through recalls, operating restrictions, service pauses, or route limitations.

They are not necessarily publicly confirmed ex ante city-selection criteria. They are demonstrated risks that can reduce service availability after entry.

## 2.1 Flooded roads

**Observed evidence:** Waymo recalled approximately 3,800 robotaxis after a vehicle entered a flooded lane during extreme weather. Operating restrictions were strengthened while the software issue was addressed.

**Operational effect:**

- routes may become unusable;
- geofences may be temporarily narrowed;
- vehicles may be removed from service;
- unmet demand may increase.

**Possible variable forms:**

- flood-exposed road share;
- number of flood-related road closures;
- frequency of flooded-road events;
- share of the service area inside flood hazard zones.

**Source:**  
[Reuters — Waymo recall over flooded-road risk](https://www.reuters.com/legal/litigation/waymo-recall-nearly-3800-robotaxis-over-self-driving-software-issue-2026-05-12/)

---

## 2.2 Heavy rain and severe weather

**Observed evidence:** Weather-related operating restrictions were strengthened following the flooded-road incident.

**Operational effect:**

- fewer serviceable hours;
- lower effective fleet availability;
- reduced operating speed;
- temporary service suspension.

**Possible variable forms:**

- heavy-rain hours per year;
- severe-weather days;
- hours exceeding an operator-defined rainfall threshold;
- weather-related service suspension hours.

**Sources:**  
[Reuters — Waymo recall over flooded-road risk](https://www.reuters.com/legal/litigation/waymo-recall-nearly-3800-robotaxis-over-self-driving-software-issue-2026-05-12/)  
[NOAA Climate Data Online](https://www.ncei.noaa.gov/cdo-web/)

---

## 2.3 Flash-flood exposure

**Observed evidence:** Access to areas with flash-flood risk was restricted as part of the operating response.

**Operational effect:**

- loss of route connectivity;
- service-area fragmentation;
- temporary exclusion of high-risk zones.

**Possible variable forms:**

- flash-flood events per year;
- share of roads inside flash-flood-prone areas;
- number of flash-flood warnings affecting the proposed geofence.

**Sources:**  
[Reuters — Waymo recall over flooded-road risk](https://www.reuters.com/legal/litigation/waymo-recall-nearly-3800-robotaxis-over-self-driving-software-issue-2026-05-12/)  
[NOAA Storm Events Database](https://www.ncei.noaa.gov/access/monitoring/storm-events/)

---

## 2.4 Construction zones and temporary road configurations

**Observed relevance:** Construction zones alter lane geometry, markings, traffic control, and expected road behavior.

**Operational effect:**

- routes may become temporarily unsupported;
- detours and travel times may increase;
- service reliability may decline;
- additional remote assistance or fallback behavior may be required.

**Possible variable forms:**

- active work zones per road mile;
- work-zone duration;
- lane-closure hours;
- percentage of major routes affected by construction.

**Official data source:**  
[USDOT — Work Zone Data Exchange](https://www.transportation.gov/av/data/wzdx)

---

## 2.5 Unsupported freeway operations

**Observed relevance:** If freeway operations are paused, restricted, or unsupported, some airport, suburban, and cross-city trips cannot be served efficiently.

**Operational effect:**

- reduced trip coverage;
- longer detours;
- longer passenger travel time;
- lower vehicle productivity;
- smaller practical service area.

**Possible variable forms:**

- share of target OD trips requiring freeway use;
- freeway miles inside the proposed service region;
- airport-to-downtown routes requiring freeway access;
- operator freeway capability: 1/0.

**Official data source:**  
[FHWA — Highway Performance Monitoring System](https://www.fhwa.dot.gov/policyinformation/hpms.cfm)

**Important limitation:** Freeway dependence is not inherently negative. Its effect depends on whether the specific ADS supports freeway operation.

---

## 2.6 Route closures and temporary service interruptions

**Observed relevance:** Weather, construction, incidents, and regulatory actions can temporarily remove routes or zones from service.

**Operational effect:**

- reduced road-network capacity;
- increased deadheading;
- more unmet demand;
- need for dynamic rebalancing.

**Possible variable forms:**

- road-closure hours;
- service-zone closure frequency;
- percentage of fleet unavailable during disruptions;
- average duration of service interruptions.

**Potential sources:**

- state and local 511 feeds;
- local DOT closure data;
- operator service-status announcements.

---

# 3. Variables That Can Be Constructed from Public Datasets

The following variables can be built from official datasets to compare candidate cities.

These are **researcher-constructed proxies**. Public evidence does not establish that robotaxi firms use these exact measures or thresholds in their internal city-selection process.

## 3.1 Regulatory eligibility variables

| Constructed variable | Measurement | Data source | Evidence status |
|---|---|---|---|
| Driverless testing allowed | Binary indicator | State DMV or transportation agency | Confirmed prerequisite |
| Driverless deployment allowed | Binary indicator | State DMV or transportation agency | Confirmed prerequisite |
| Paid passenger service allowed | Binary indicator | PUC or equivalent regulator | Confirmed prerequisite |
| Number of active AV permit holders | Count | State regulator | Researcher-constructed market-readiness proxy |
| Reporting burden | Number or type of required reports | State regulator | Researcher-constructed compliance proxy |

---

## 3.2 ODD and road-network variables

| Constructed variable | Measurement | Data source | Evidence status |
|---|---|---|---|
| Supported roadway share | Share of target roads belonging to ADS-supported functional classes | FHWA HPMS and company ODD information | Directly linked to ODD compatibility |
| Supported speed-range share | Share of target roads inside the supported speed range | HPMS or local speed-limit GIS | Directly linked to ODD compatibility |
| Freeway dependence | Freeway share of road miles or target OD routes | FHWA HPMS | Researcher-constructed conditional proxy |
| Intersection density | Intersections per square mile | EPA Smart Location Database or road-network GIS | Researcher-constructed complexity proxy |
| Work-zone exposure | Active work zones or closure hours per road mile | WZDx or local DOT | Researcher-constructed operational-risk proxy |
| Traffic volume | AADT or vehicle flow | FHWA HPMS | Researcher-constructed operational-load proxy |
| Travel-time reliability | Planning Time Index or travel-time variability | NPMRDS or local MPO | Researcher-constructed productivity proxy |

**Sources:**  
[FHWA HPMS](https://www.fhwa.dot.gov/policyinformation/hpms.cfm)  
[USDOT WZDx](https://www.transportation.gov/av/data/wzdx)  
[EPA Smart Location Mapping](https://www.epa.gov/smartgrowth/smart-location-mapping)

---

## 3.3 Weather and hazard variables

| Constructed variable | Measurement | Data source | Evidence status |
|---|---|---|---|
| Heavy-rain days | Days or hours above a rainfall threshold | NOAA CDO | Proxy for demonstrated weather risk |
| Snow and ice days | Snowfall, snow depth, freezing days | NOAA CDO | ODD exposure proxy |
| Low-visibility hours | Hours below a visibility threshold | NOAA weather observations | ODD exposure proxy |
| Flash-flood frequency | Historical event count | NOAA Storm Events | Proxy for demonstrated flood risk |
| Flood-exposed road share | Road miles overlapping FEMA flood zones | FEMA NFHL + road GIS | Proxy for demonstrated flood risk |
| Hazard expected annual loss | FEMA risk estimate | FEMA National Risk Index | General hazard proxy, not robotaxi-specific |

**Sources:**  
[NOAA Climate Data Online](https://www.ncei.noaa.gov/cdo-web/)  
[NOAA Storm Events Database](https://www.ncei.noaa.gov/access/monitoring/storm-events/)  
[FEMA National Flood Hazard Layer](https://www.fema.gov/flood-maps/national-flood-hazard-layer)  
[FEMA National Risk Index](https://hazards.fema.gov/nri/)

---

## 3.4 Charging and depot-readiness variables

| Constructed variable | Measurement | Data source | Evidence status |
|---|---|---|---|
| Public charging-station density | Stations per square mile or per 100,000 residents | DOE AFDC | General EV-readiness proxy |
| DC fast-charger count | Number of DC fast chargers | DOE AFDC | Charging-readiness proxy |
| Connector count | Number of simultaneous charging connectors | DOE AFDC | Public-capacity proxy |
| Distance to charging | Mean distance from proposed geofence to public chargers | DOE AFDC + GIS | Deadheading proxy |
| Commercial land or warehouse cost | Lease or property cost | Local property or commercial real-estate data | Depot-cost proxy |
| Potential depot-site availability | Number or area of suitable parcels | Local zoning and parcel data | Researcher-constructed depot proxy |

**Source:**  
[DOE Alternative Fueling Station Locator](https://afdc.energy.gov/stations/)

**Important limitation:** These measures do not reveal whether a company has access to a private robotaxi depot.

---

## 3.5 Prior deployment-readiness variables

| Constructed variable | Measurement | Data source | Evidence status |
|---|---|---|---|
| Prior AV testing activity | Presence, duration, or number of operators testing locally | Company announcements and state records | Enabling-factor proxy |
| Existing robotaxi pilot | Binary indicator | Company or local-government announcement | Confirmed local readiness |
| Public-rider pilot history | Binary indicator or duration | Company announcement | Confirmed local validation |
| Local platform partnership | Binary indicator | Company announcement | Confirmed enabling factor |
| Existing service-area size | Square miles | Company map or permit | Confirmed operating footprint |

---

# 4. Final Variables That Can Be Used

The variables below are recommended for the empirical city-entry analysis.

They are separated by evidence strength.

## 4.1 Confirmed prerequisite variables

1. Driverless testing legally allowed  
2. Driverless deployment legally allowed  
3. Paid passenger service legally allowed  
4. Authorized geographic service area  
5. Supported roadway-type share  
6. Supported speed-range share  
7. Prior local testing or pilot activity  
8. Local operating or platform partnership  
9. Feasible initial geofence  
10. Feasible depot and charging plan  

## 4.2 Demonstrated operational-risk variables

1. Heavy-rain exposure  
2. Flood-exposed road share  
3. Flash-flood frequency  
4. Construction-zone exposure  
5. Temporary road-closure exposure  
6. Freeway dependence conditional on ADS freeway capability  
7. Weather-related service interruption rate  

## 4.3 Researcher-constructed proxy variables

1. Intersection density  
2. Traffic volume  
3. Travel-time reliability  
4. Public fast-charger density  
5. Distance from proposed service area to charging infrastructure  
6. Commercial land or warehouse cost  
7. Number of active AV permit holders  
8. Historical AV testing duration  
9. Share of roads inside FEMA flood zones  
10. Annual hours of severe weather or low visibility  

---

# 5. Suggested Use in the Model

The recommended approach is to avoid combining every factor into one subjective city score.

Instead, use three stages.

## 5.1 Stage 1: Legal eligibility filter

A city can be considered only if the required legal authorizations are available.

$$
y_i \leq R_i^{legal}
$$

where:

- \(y_i = 1\) if the model enters city \(i\);
- \(R_i^{legal} = 1\) if driverless deployment and paid passenger service are legally permitted.

---

## 5.2 Stage 2: ODD and infrastructure feasibility

A city should be excluded or constrained when its proposed service area is not sufficiently compatible with the ADS or when minimum operational infrastructure cannot be established.

$$
y_i \leq R_i^{ODD}
$$

$$
y_i \leq R_i^{infrastructure}
$$

where:

- \(R_i^{ODD}\) represents whether the proposed service area satisfies minimum roadway, speed, weather, and geographic requirements;
- \(R_i^{infrastructure}\) represents whether minimum depot and charging requirements can be met.

These indicators should be based on explicitly defined thresholds rather than subjective judgment.

---

## 5.3 Stage 3: Risk-adjusted effective operating capacity

Operational risks should reduce effective capacity rather than automatically eliminate every high-risk city.

$$
Q_{i,t}^{effective,\omega}
=
a_{i,t}^{\omega} Q_i
$$

where:

- \(Q_i\) is the nominal fleet capacity assigned to city \(i\);
- \(a_{i,t}^{\omega}\in[0,1]\) is the fraction of capacity available under weather, flooding, construction, or closure scenario \(\omega\).

---

## 5.4 Integrated city-entry formulation

A simplified entry model can be written as:

$$
\min
\sum_i
\left(
f_i y_i
+
c_i^{entry} y_i
\right)
+
\mathbb E_{\omega}
\left[
\sum_{i,t}
c_{i,t}^{risk}
\left(
1-a_{i,t}^{\omega}
\right)
Q_i
\right]
$$

subject to:

$$
y_i \leq R_i^{legal}
$$

$$
y_i \leq R_i^{ODD}
$$

$$
y_i \leq R_i^{infrastructure}
$$

where:

- \(f_i\) is the fixed market-entry cost;
- \(c_i^{entry}\) includes depot, charging, mapping, testing, and compliance costs;
- \(a_{i,t}^{\omega}\) represents scenario-dependent operational availability;
- \(c_{i,t}^{risk}\) is the cost associated with unavailable capacity.

---

# Final Interpretation

The strongest defensible conclusion is not:

> Robotaxi firms publicly select cities using rainfall, floodplain share, intersection density, and charger counts.

The defensible conclusion is:

> Public evidence identifies legal authorization, ODD compatibility, prior validation, service-area feasibility, and operating partnerships as prerequisites or enabling factors. Actual events demonstrate that flooding, severe weather, construction, freeway limitations, and route closures can reduce service availability. Official datasets can then be used to construct city-level proxies for these publicly documented conditions and risks.
