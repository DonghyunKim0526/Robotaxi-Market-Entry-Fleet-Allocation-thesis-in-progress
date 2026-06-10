# Observable Conditions for Robotaxi City Entry

This document organizes robotaxi city-entry conditions into three evidence categories:

1. **Publicly Confirmed Prerequisites or Enabling Factors** 
2. **Operational Risks Demonstrated by Actual Events**
3. **Variables That Can Be Constructed from Public Datasets**

For part 2 and 3, 
the sources are news and datasets, so the variables are not official regulations for a robotaxi to be operated within a city; just derived variables that may be considered.

For each source, the structure is:

1. Paper, official document, or dataset and link  
2. Summary of the source and its main findings  
3. Variables that can be identified or constructed from the source  

---

# Category 1. Publicly Confirmed Prerequisites or Enabling Factors

## 1. *A Framework for Automated Driving System Testable Cases and Scenarios*

**Institution:** U.S. Department of Transportation / National Highway Traffic Safety Administration  
**Document link:** [NHTSA PDF](https://www.nhtsa.gov/sites/nhtsa.gov/files/documents/13882-automateddrivingsystems_092618_v1a_tag.pdf)  
**Evidence type:** Official federal technical framework

### 1. Summary and main findings

The document defines the **Operational Design Domain (ODD)** as the set of conditions under which an automated driving system is designed to operate.

The ODD includes:

- geographic area;
- roadway type;
- speed range;
- environmental and weather conditions;
- lighting conditions;
- traffic conditions;
- other operational constraints.

The document does not explain why a specific robotaxi company selected a specific city. It establishes the operating conditions that must be compatible with the ADS before deployment is technically feasible.

### 2. Variables identified from the source

| Variable | Meaning | Expected role in city entry | Possible measurement |
|---|---|---|---|
| Geographic operating-area compatibility | Whether the proposed service area is within the ADS-supported geographic domain | Confirmed technical prerequisite | Share of proposed service area covered by the authorized or validated geofence |
| Supported roadway-type share | Share of proposed roads belonging to roadway classes supported by the ADS | Confirmed technical prerequisite | Supported road miles divided by total proposed road miles |
| Supported speed-range share | Share of proposed roads within the ADS-supported speed range | Confirmed technical prerequisite | Compatible road miles divided by total proposed road miles |
| Weather-condition compatibility | Whether local operating conditions fall inside the supported weather domain | Confirmed technical prerequisite | Share of planned service hours within supported weather conditions |
| Lighting and time-of-day compatibility | Whether operation is supported during daytime, nighttime, or particular lighting conditions | Confirmed technical prerequisite | Share of desired operating hours within supported lighting conditions |
| Traffic-condition compatibility | Whether local traffic conditions fall within the supported operating domain | Confirmed technical prerequisite | Share of operating periods within supported traffic conditions |
| Temporary-road-condition compatibility | Whether the ADS can handle temporary lane changes, work zones, and altered road geometry | Confirmed technical prerequisite | Share of road network or operating periods unaffected by unsupported temporary configurations |

### Source conclusion

> ODD compatibility is a necessary technical prerequisite for robotaxi deployment. Geography, roadway type, speed, weather, lighting, traffic, and temporary road conditions should be treated as separate feasibility conditions rather than combined into one subjective score.

---

## 2. California DMV Autonomous Vehicle Programs

**Institution:** California Department of Motor Vehicles  
**Document link:** [California DMV — Autonomous Vehicles](https://www.dmv.ca.gov/portal/vehicle-industry-services/autonomous-vehicles/)  
**Evidence type:** Official state regulatory framework

### 1. Summary and main findings

The California DMV separates autonomous-vehicle activity into different authorization stages, including:

- testing with a safety driver;
- driverless testing;
- deployment.

This distinction shows that permission to test an AV does not automatically permit driverless deployment.

The DMV framework therefore provides direct evidence that regulatory authorization is a prerequisite for city entry.

### 2. Variables identified from the source

| Variable | Meaning | Expected role in city entry | Recommended variable form |
|---|---|---|---|
| Driverless testing legally permitted | Whether the operator can test without a human safety driver | Confirmed legal prerequisite | Binary indicator: 1/0 |
| Driverless deployment legally permitted | Whether the operator can deploy driverless vehicles beyond testing | Confirmed legal prerequisite | Binary indicator: 1/0 |
| Operator holds required permit | Whether the specific company has the permit required for the activity | Confirmed company-specific prerequisite | Binary indicator by company and jurisdiction |
| Authorized operating geography | Geographic limits stated in the permit | Confirmed legal-operational prerequisite | Service-area overlap ratio |
| Authorized operating conditions | Restrictions related to speed, roads, time, or other operating conditions | Confirmed legal-operational prerequisite | Number and type of permit restrictions |

### Source conclusion

> Driverless testing and driverless deployment must be treated as separate regulatory variables. A city cannot be considered fully feasible simply because autonomous testing is allowed.

---

## 3. CPUC Autonomous Vehicle Passenger Service Programs

**Institution:** California Public Utilities Commission  
**Document link:** [CPUC — Autonomous Vehicle Programs](https://www.cpuc.ca.gov/regulatory-services/licensing/transportation-licensing-and-analysis-branch/autonomous-vehicle-programs)  
**Evidence type:** Official passenger-service regulatory framework

### 1. Summary and main findings

The CPUC regulates autonomous passenger service separately from vehicle testing and deployment.

The CPUC framework distinguishes pilot programs and deployment programs and imposes requirements related to:

- passenger-service authorization;
- safety plans;
- insurance;
- operational reporting;
- quarterly reporting.

This means that a robotaxi operator may be technically able to deploy vehicles but still lack authorization to provide paid passenger service.

### 2. Variables identified from the source

| Variable | Meaning | Expected role in city entry | Recommended variable form |
|---|---|---|---|
| Paid passenger service legally permitted | Whether the operator may carry paying passengers | Confirmed commercial prerequisite | Binary indicator: 1/0 |
| Passenger-service authorization held | Whether the specific operator has CPUC authorization | Confirmed company-specific prerequisite | Binary indicator |
| Safety-plan requirement satisfied | Whether the required safety documentation has been submitted and accepted | Confirmed compliance prerequisite | Binary or categorical indicator |
| Insurance requirement satisfied | Whether the operator meets required insurance conditions | Confirmed compliance prerequisite | Binary indicator |
| Reporting requirement | Frequency and scope of required reporting | Confirmed compliance burden | Number of required reports or categories |
| Trip-data reporting availability | Whether deployment generates public operational data | Confirmed data-enabling factor | Binary indicator |

### Source conclusion

> Paid passenger-service authorization should be modeled separately from testing and deployment authorization. It is a direct commercial-entry prerequisite.

---

## 6. DOE Alternative Fuels Data Center

**Institution:** U.S. Department of Energy  
**Dataset links:**  
- [Alternative Fueling Station Locator](https://afdc.energy.gov/stations/)  
- [AFDC Data Downloads](https://afdc.energy.gov/data_download)  
**Evidence type:** Official infrastructure dataset

### 1. Summary and main findings

The AFDC provides nationwide data on public charging infrastructure, including:

- station locations;
- charger types;
- connector counts;
- charging levels;
- available station attributes.

The dataset can be used to measure general EV charging readiness.

However, it does not show whether a robotaxi company has access to private charging depots, cleaning facilities, maintenance facilities, or fleet parking.

### 2. Variables identified from the source

| Variable | Meaning | Expected role in city entry | Evidence status |
|---|---|---|---|
| Public charging-station count | Number of public charging stations in the city or proposed geofence | General infrastructure proxy | Dataset-derived proxy |
| DC fast-charger count | Number of fast-charging facilities | Charging-readiness proxy | Dataset-derived proxy |
| Connector count | Potential simultaneous charging capacity | Public-capacity proxy | Dataset-derived proxy |
| Charger power | Potential charging speed | Charging-duration proxy | Dataset-derived proxy |
| Distance from service area to chargers | Deadheading required to reach public charging | Operational-cost proxy | Dataset-derived proxy |

### Source conclusion

> AFDC data can measure general EV charging infrastructure, but it cannot be treated as direct evidence of proprietary robotaxi depot capacity.

---

# Category 2. Operational Risks Demonstrated by Actual Events

## 1. Reuters — Waymo Recall over Flooded-Road Risk

**Source:** Reuters  
**Article link:** [Waymo recall over flooded-road risk](https://www.reuters.com/legal/litigation/waymo-recall-nearly-3800-robotaxis-over-self-driving-software-issue-2026-05-12/)  
**Evidence type:** Reported real-world robotaxi operating event based on Waymo and NHTSA information

### 1. Summary and main findings

Waymo recalled approximately 3,800 robotaxis after a driverless vehicle entered a flooded lane during extreme weather.

The reported response included:

- stronger weather-related restrictions;
- reduced operating scope;
- restrictions on access to flash-flood-prone areas;
- software and map-related corrective actions.

This event provides direct evidence that flooding and severe weather can reduce robotaxi service availability.

It does not establish that Waymo uses a specific rainfall or FEMA threshold when selecting cities.

### 2. Variables identified from the source

| Variable | Observed operational effect | Expected role in city-entry analysis | Evidence status |
|---|---|---|---|
| Flooded-road exposure | Can make routes unsafe or unusable | Operational-risk factor | Demonstrated by actual event |
| Heavy-rain exposure | Can trigger operating restrictions | Operational availability factor | Demonstrated by actual event |
| Flash-flood exposure | Can cause route or area exclusion | Service-area reliability factor | Demonstrated by actual event |
| Weather-related service restriction | Reduces operating hours and effective fleet | Scenario-dependent capacity factor | Demonstrated by actual event |
| Hazard-related map or route update | Can temporarily change the geofence or route set | Dynamic feasibility factor | Demonstrated by actual event |

### Source conclusion

> Flooding, heavy rain, and flash-flood exposure are demonstrated operational risks. They should be modeled as factors that reduce service availability, not as publicly confirmed corporate city-selection thresholds.

---

## 2. USDOT Work Zone Data Exchange

**Institution:** U.S. Department of Transportation  
**Dataset link:** [Work Zone Data Exchange](https://www.transportation.gov/av/data/wzdx)  
**Evidence type:** Official temporary-road-condition dataset

### 1. Summary and main findings

The Work Zone Data Exchange standard provides data related to active work zones, such as:

- work-zone location;
- lane closure;
- temporary road changes;
- start and end times;
- road restrictions.

Construction zones change lane geometry, road markings, traffic control, and expected driving behavior.

The dataset does not prove that a company uses work-zone frequency as a formal city-selection criterion. It provides a way to measure exposure to temporary road complexity.

### 2. Variables identified from the source

| Variable | Meaning | Expected role in city entry | Evidence status |
|---|---|---|---|
| Active work-zone count | Number of active work zones in the proposed service area | Operational-risk proxy | Dataset-derived |
| Work-zone density | Work zones per road mile or square mile | Temporary-road-complexity proxy | Dataset-derived |
| Lane-closure hours | Total duration of lane closures | Route-capacity risk | Dataset-derived |
| Work-zone duration | Length of time a road is affected | Service-reliability risk | Dataset-derived |
| Share of major routes affected | Portion of key corridors affected by construction | Geofence-connectivity risk | Dataset-derived |

### Source conclusion

> Work-zone data can quantify exposure to temporary road configurations. It is best treated as an operational-risk proxy rather than a confirmed city-selection rule.

---

## 3. FHWA Highway Performance Monitoring System

**Institution:** Federal Highway Administration  
**Dataset link:** [FHWA HPMS](https://www.fhwa.dot.gov/policyinformation/hpms.cfm)  
**Evidence type:** Official road-network dataset

### 1. Summary and main findings

HPMS provides nationwide information on:

- functional road classification;
- road mileage;
- traffic volume;
- roadway characteristics;
- highway-system structure.

These data can be used to evaluate whether a proposed service area depends heavily on road types that the ADS may not support.

The dataset itself does not prove that robotaxi companies select cities based on a particular freeway-share threshold.

### 2. Variables identified from the source

| Variable | Meaning | Expected role in city entry | Evidence status |
|---|---|---|---|
| Freeway-road share | Share of road miles classified as freeway or interstate | Conditional operational factor | Dataset-derived proxy |
| Arterial-road share | Share of major arterial roads | ODD compatibility proxy | Dataset-derived proxy |
| Local-road share | Share of local roads | ODD compatibility proxy | Dataset-derived proxy |
| Traffic volume | AADT or related traffic measures | Operational-load proxy | Dataset-derived proxy |
| Road mileage by functional class | Network composition | Road-type compatibility measure | Dataset-derived proxy |

### Source conclusion

> Road-network composition can be measured through HPMS. Freeway dependence should be interpreted only in combination with the specific ADS's freeway capability.

---

## 4. NOAA Climate Data Online and Storm Events Database

**Institution:** National Oceanic and Atmospheric Administration  
**Dataset links:**  
- [NOAA Climate Data Online](https://www.ncei.noaa.gov/cdo-web/)  
- [NOAA Storm Events Database](https://www.ncei.noaa.gov/access/monitoring/storm-events/)  
**Evidence type:** Official weather and hazard datasets

### 1. Summary and main findings

NOAA provides historical weather and hazard data, including:

- precipitation;
- snowfall;
- temperature;
- visibility;
- severe storms;
- flash floods;
- other recorded weather events.

These data can be used to compare the exposure of candidate cities to weather conditions that may fall outside a robotaxi system's ODD.

The datasets do not independently establish the weather limits of any specific ADS.

### 2. Variables identified from the source

| Variable | Meaning | Expected role in city entry | Evidence status |
|---|---|---|---|
| Heavy-rain days or hours | Frequency of intense precipitation | Weather-risk proxy | Dataset-derived |
| Snow and ice days | Frequency of snow, ice, or freezing conditions | ODD exposure proxy | Dataset-derived |
| Low-visibility hours | Frequency of visibility below a threshold | ODD exposure proxy | Dataset-derived |
| Flash-flood frequency | Historical flash-flood events | Demonstrated flood-risk proxy | Dataset-derived |
| Severe-weather days | Frequency of major weather events | Service-interruption proxy | Dataset-derived |

### Source conclusion

> NOAA data can quantify weather exposure, but company-specific ODD thresholds are still required to determine whether a condition is actually unsupported.

---

## 5. FEMA National Flood Hazard Layer and National Risk Index

**Institution:** Federal Emergency Management Agency  
**Dataset links:**  
- [FEMA National Flood Hazard Layer](https://www.fema.gov/flood-maps/national-flood-hazard-layer)  
- [FEMA National Risk Index](https://hazards.fema.gov/nri/)  
**Evidence type:** Official hazard datasets

### 1. Summary and main findings

FEMA provides spatial data on flood hazard areas and broader hazard-risk indicators.

These datasets can be combined with road-network data to estimate how much of a proposed robotaxi service area is exposed to flooding.

The datasets do not establish that a company formally uses FEMA risk scores in its city-selection process.

### 2. Variables identified from the source

| Variable | Meaning | Expected role in city entry | Evidence status |
|---|---|---|---|
| Flood-exposed road share | Share of road miles overlapping FEMA flood zones | Demonstrated operational-risk proxy | Dataset-derived |
| Flood-exposed service-area share | Share of proposed geofence in flood hazard areas | Service-area reliability proxy | Dataset-derived |
| Hazard expected annual loss | FEMA estimate of long-run hazard exposure | General risk proxy | Dataset-derived |
| Number of critical corridors in flood zones | Count of key routes exposed to flooding | Network-resilience proxy | Dataset-derived |

### Source conclusion

> FEMA data can measure geographic exposure to flooding and other hazards. These measures are researcher-constructed proxies for documented operational risks.

---

# Category 3. Variables That Can Be Inferred or Constructed from Datasets

This category combines variables that can be operationalized across candidate cities using official datasets.

These variables are not publicly confirmed as internal corporate city-selection criteria.

## 1. Regulatory datasets

### 1. Potential sources:

- state DMV autonomous-vehicle permit records;
- state public-utility commission records;
- state transportation-agency AV laws and rules.

### 2. Summary and use

Regulatory datasets can be used to compare whether cities or states permit:

- driverless testing;
- driverless deployment;
- paid passenger service;
- commercial operation;
- specific operating geographies.

### 3. Variables that can be constructed

| Variable | Construction method | Recommended interpretation |
|---|---|---|
| Driverless testing eligibility | Binary indicator from state rules | Confirmed prerequisite |
| Driverless deployment eligibility | Binary indicator from state rules | Confirmed prerequisite |
| Paid passenger-service eligibility | Binary indicator from state rules | Confirmed prerequisite |
| Number of active AV permit holders | Count by jurisdiction | Market-readiness proxy |
| Regulatory reporting burden | Count or category of reporting requirements | Compliance-cost proxy |
| Regulatory approval duration | Time between application and authorization, where available | Entry-delay proxy |

---

## 2. Road-network datasets

### 1. Potential sources:

- FHWA HPMS;
- local DOT road GIS;
- EPA Smart Location Database;
- WZDx.

### 2. Summary and use

Road datasets can be used to measure whether a proposed service area is compatible with the ADS and how complex the operating environment may be.

### 3. Variables that can be constructed

| Variable | Construction method | Recommended interpretation |
|---|---|---|
| Supported roadway-type share | Supported road miles divided by total proposed road miles | Direct ODD compatibility measure |
| Supported speed-range share | Compatible road miles divided by total proposed road miles | Direct ODD compatibility measure |
| Freeway dependence | Freeway miles or freeway-dependent OD trips divided by total | Conditional proxy |
| Intersection density | Intersections per square mile | Road-complexity proxy |
| Work-zone exposure | Work zones or closure hours per road mile | Temporary-complexity proxy |
| Traffic volume | Average traffic flow on proposed service roads | Operational-load proxy |
| Travel-time reliability | Variation in travel time or Planning Time Index | Fleet-productivity proxy |

---

## 3. Weather and hazard datasets

### 1. Potential sources:

- NOAA Climate Data Online;
- NOAA Storm Events Database;
- FEMA National Flood Hazard Layer;
- FEMA National Risk Index.

### 2. Summary and use

Weather and hazard data can be used to measure exposure to operating conditions that have been documented as robotaxi risks or that may fall outside an ADS's ODD.

### 3. Variables that can be constructed

| Variable | Construction method | Recommended interpretation |
|---|---|---|
| Heavy-rain exposure | Annual days or hours above a defined rainfall threshold | Weather-risk proxy |
| Snow and ice exposure | Annual snow, ice, or freezing-condition days | ODD exposure proxy |
| Low-visibility exposure | Annual hours below a visibility threshold | ODD exposure proxy |
| Flash-flood frequency | Historical event count per year | Demonstrated-risk proxy |
| Flood-exposed road share | Road miles inside FEMA flood zones divided by total road miles | Demonstrated-risk proxy |
| Severe-weather exposure | Annual severe-weather events or hours | Service-interruption proxy |

---

## 4. Charging and depot-readiness datasets

### 1. Potential sources:

- DOE AFDC;
- local parcel and zoning data;
- commercial property or warehouse-cost data;
- local utility interconnection data.

### 2. Summary and use

These datasets can be used to approximate whether a candidate city has sufficient infrastructure to support robotaxi charging, parking, maintenance, and cleaning.

### 3. Variables that can be constructed

| Variable | Construction method | Recommended interpretation |
|---|---|---|
| Public fast-charger density | DC fast chargers per square mile or per 100,000 residents | General charging-readiness proxy |
| Connector capacity | Number of public charging connectors | Public-capacity proxy |
| Distance to charging infrastructure | Mean distance from proposed geofence to chargers | Charging deadheading proxy |
| Commercial land cost | Lease or property cost for potential depot areas | Depot-cost proxy |
| Suitable depot-parcel availability | Count or area of parcels meeting minimum requirements | Depot-feasibility proxy |
| Grid or utility readiness | Available interconnection or charging capacity, where public | Infrastructure-readiness proxy |

---

## 5. Prior AV activity and market-readiness data

### 1. Potential sources:

- company announcements;
- state permit records;
- local pilot-program records;
- company service maps.

### 2. Summary and use

Prior testing, pilot activity, and service announcements can be used to measure how far a city has progressed toward commercial deployment.

### 3. Variables that can be constructed

| Variable | Construction method | Recommended interpretation |
|---|---|---|
| Prior AV testing presence | Binary indicator | Enabling-factor proxy |
| Testing duration | Months or years since first local test | Validation-maturity proxy |
| Existing public-rider pilot | Binary indicator | Confirmed readiness factor |
| Announced future market | Binary indicator | Confirmed expansion status |
| Existing local partnership | Binary indicator | Confirmed enabling factor |
| Existing service-area size | Square miles or population covered | Operating-footprint measure |

---

# Final Variables for Research

## A. Publicly confirmed prerequisites or enabling factors

1. Driverless testing legally allowed  
2. Driverless deployment legally allowed  
3. Paid passenger service legally allowed  
4. Authorized geographic service area  
5. Supported roadway-type share  
6. Supported speed-range share  
7. Weather and lighting compatibility with the ODD  
8. Prior local testing or pilot activity  
9. Local operating or platform partnership  
10. Feasible initial geofence  
11. Feasible depot and charging plan  

## B. Operational risks demonstrated by actual events

1. Heavy-rain exposure  
2. Flooded-road exposure  
3. Flash-flood exposure  
4. Construction-zone exposure  
5. Temporary road-closure exposure  
6. Unsupported freeway dependence  
7. Weather-related service-interruption risk  

## C. Dataset-derived proxy variables

1. Flood-exposed road share  
2. Heavy-rain days or hours  
3. Snow and ice days  
4. Low-visibility hours  
5. Work-zone density  
6. Lane-closure hours  
7. Freeway-road share  
8. Intersection density  
9. Traffic volume  
10. Travel-time reliability  
11. Public fast-charger density  
12. Distance to charging infrastructure  
13. Commercial land or warehouse cost  
14. Number of active AV permit holders  
15. Historical AV testing duration  


