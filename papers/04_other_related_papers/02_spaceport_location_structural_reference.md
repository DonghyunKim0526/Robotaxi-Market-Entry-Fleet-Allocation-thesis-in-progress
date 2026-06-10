# Structural Reference: Spaceport Facility Location Planning

## Paper

**Title:** *Spaceport Facility Location Planning within the US National Airspace System*  
**Authors:** Haochen Wu, Kevin R. Sun, Jackson A. Miller, Oliver Jia-Richards, and Max Z. Li  
**Paper type:** Capacitated facility-location planning under operational constraints  
**Relevance to robotaxi research:** **Indirect structural reference**

---

# 1. Research Problem

The paper develops a facility-location planning model for future U.S. spaceports.

The model determines:

- which candidate counties should be selected;
- which mission types should be assigned to each selected facility;
- whether all projected demand can be served;
- how operational, transportation, launch, and rerouting costs can be minimized.

The model first filters candidate locations according to operational feasibility and then optimizes facility selection and demand allocation.

---

# 2. Feasibility Filtering

Candidate counties must first satisfy trajectory and safety conditions, including:

- feasible launch azimuths;
- population exposure under hazard zones;
- geographic suitability;
- operational safety requirements.

Only counties with at least one feasible launch direction are included in the final facility-location model.

\[
\text{Operational feasibility filtering}
\rightarrow
\text{Facility selection and capacity allocation}
\]

---

# 3. Demand and Capacity

The paper forecasts future launch demand and divides total demand into mission types.

\[
k_j
=
\text{demand for mission type }j
\]

\[
y_{i,j}
=
\text{number of missions of type }j\text{ assigned to location }i
\]

Each facility has a maximum capacity:

\[
\sum_j y_{i,j}\le P
\]

Demand for each mission type must be satisfied:

\[
\sum_i y_{i,j}\ge k_j
\]

---

# 4. Facility-Selection Variables

\[
x_i
=
\begin{cases}
1,&\text{if a spaceport is selected at candidate location }i\\
0,&\text{otherwise}
\end{cases}
\]

Facility selection and mission assignment are linked so that missions cannot be assigned unless the facility is selected.

---

# 5. Cost Components

The objective minimizes:

- transportation cost;
- facility operation cost;
- mission launch cost;
- aircraft rerouting cost.

\[
\min
\sum_i
(C_i^T+C_i^O)x_i
+
\sum_{i,j}
(C_{i,j}^L+C_{i,j}^R)y_{i,j}
\]

where:

- \(C_i^T\): transportation cost;
- \(C_i^O\): operating cost;
- \(C_{i,j}^L\): launch cost;
- \(C_{i,j}^R\): aircraft rerouting cost.

---

# 6. Spatial-Dispersion Constraint

Selected facilities must satisfy a minimum separation distance:

\[
d_{i,i'}\ge D
\]

This supports resilience by reducing the possibility that one disruptive event affects multiple facilities.

---

# 7. Main Findings

- Feasible locations depend strongly on operational constraints.
- Optimal locations change when the weighting of operating, transportation, launch, and rerouting costs changes.
- Hazard-zone size changes the feasible candidate set.
- Different mission types prefer different regions because location-specific operating costs differ.
- The model jointly chooses locations and assigns demand rather than ranking sites with a simple score.

---

# 8. Transfer to Robotaxi Research

| Spaceport model | Robotaxi model |
|---|---|
| Candidate county | Candidate city or service zone |
| Feasible trajectory | Feasible ODD and road network |
| Population-safety filtering | Regulatory, weather, and technical feasibility filtering |
| Spaceport selection | City or depot entry |
| Mission demand | Ride demand |
| Spaceport capacity | Fleet or depot capacity |
| Mission allocation | Vehicle allocation |
| Operation and transportation cost | Fleet, depot, and rebalancing cost |
| Safety constraint | Regulatory and ODD constraint |
| Minimum separation | Geographic diversification or resilience constraint |

---

# 9. Robotaxi Interpretation

## Step 1: Eliminate infeasible locations

A candidate city or zone can be removed when:

- paid driverless service is not legally permitted;
- the roadway network is outside the supported ODD;
- the weather or hazard exposure is incompatible with operations;
- no feasible charging or depot infrastructure can be established.

## Step 2: Optimize among feasible locations

\[
y_i
=
\text{whether to enter city }i
\]

\[
q_i
=
\text{fleet allocated to city }i
\]

The objective can include:

- entry and depot cost;
- vehicle acquisition and operating cost;
- rebalancing cost;
- idle-capacity cost;
- unmet-demand cost.

---

# 10. Simplified Robotaxi Location-Allocation Structure

\[
\min
\sum_i f_i y_i
+
\sum_i c_i^{fleet}q_i
+
\mathbb E
\left[
\sum_i c_i^{under}(R_i-q_i)^+
+
c_i^{over}(q_i-R_i)^+
\right]
\]

subject to:

\[
y_i\le F_i
\]

\[
q_i\le M_i y_i
\]

\[
\sum_i q_i\le Q
\]

where:

- \(F_i\): feasibility indicator for city \(i\);
- \(y_i\): city-entry decision;
- \(q_i\): allocated fleet;
- \(M_i\): maximum deployable fleet;
- \(Q\): total available fleet;
- \(R_i\): uncertain vehicle requirement.

---

# 11. Why This Paper Matters for the Robotaxi Project

The paper supports a clean separation between:

1. **Which locations are technically feasible?**
2. **How should capacity be allocated among feasible locations?**

This is preferable to combining all city attributes into one subjective score.

> First filter out locations that violate operational constraints, and then optimize location selection and capacity allocation among the feasible alternatives.

---

# Paper Conclusion

> The spaceport study is not direct evidence about robotaxi variables, but it provides a useful structural template. Robotaxi research can first remove legally or technically infeasible cities and then jointly optimize city entry and fleet allocation among the remaining candidates.
