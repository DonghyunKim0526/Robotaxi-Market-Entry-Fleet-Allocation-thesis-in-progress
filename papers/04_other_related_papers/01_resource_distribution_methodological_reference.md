# Methodological Reference: Resource Distribution Under Spatiotemporal Uncertainty of Disease Spread

## Paper

**Title:** *Resource Distribution Under Spatiotemporal Uncertainty of Disease Spread: Stochastic versus Robust Approaches*  
**Authors:** Beste Basciftci, Xian Yu, and Siqian Shen  
**Paper type:** Methodological reference for stochastic and distributionally robust allocation under uncertain demand  
**Relevance to robotaxi research:** **Indirect but highly transferable**

---

# 1. Research Problem

The paper studies how to locate distribution centers and allocate disease-control resources under uncertain regional and temporal demand.

The model jointly considers:

- facility opening;
- installed capacity;
- shipment decisions;
- inventory;
- unmet demand;
- operating cost;
- demand uncertainty;
- equity and service coverage.

The paper compares:

- a deterministic approach;
- a stochastic programming approach;
- a distributionally robust optimization approach.

---

# 2. Core Decision Structure

The model follows a two-stage structure.

## First-stage decisions

These decisions are made before uncertain demand is realized:

\[
x_i
=
\text{whether facility }i\text{ is opened}
\]

\[
h_{i,t}
=
\text{installed capacity at facility }i\text{ in period }t
\]

## Second-stage decisions

These decisions respond to each demand scenario:

\[
s_{i,j,t}^{\omega}
=
\text{shipment from facility }i\text{ to demand site }j
\]

\[
I_{j,t}^{\omega}
=
\text{inventory at demand site }j
\]

\[
u_{j,t}^{\omega}
=
\text{unmet demand or backlog at demand site }j
\]

---

# 3. Objective Function

The stochastic model minimizes facility operating cost, capacity-installation cost, expected shipping cost, expected inventory cost, and expected unmet-demand penalty.

\[
\min
\sum_i c_i^o x_i
+
\sum_{i,t} c_i^h h_{i,t}
+
\mathbb E_{\omega}
\left[
\sum_{i,j,t} c_{i,j,t}^s s_{i,j,t}^{\omega}
+
\sum_{j,t} c_{j,t}^I I_{j,t}^{\omega}
+
\sum_{j,t} c_{j,t}^u u_{j,t}^{\omega}
\right]
\]

---

# 4. Main Constraints

## Facility-capacity activation

\[
h_{i,t}\le M_i x_i
\]

Capacity can be installed only at an open facility.

## Total temporal capacity

\[
\sum_i h_{i,t}\le B_t
\]

The system has a limited total resource capacity in each period.

## Shipment capacity

\[
\sum_j s_{i,j,t}^{\omega}\le h_{i,t}
\]

Total shipment from a facility cannot exceed its installed capacity.

## Flow balance

\[
\sum_i s_{i,j,t}^{\omega}
+
I_{j,t-1}^{\omega}
+
u_{j,t}^{\omega}
=
d_{j,t}^{\omega}
+
I_{j,t}^{\omega}
+
u_{j,t-1}^{\omega}
\]

Demand is balanced by incoming resources, inventory, and unmet demand.

---

# 5. Stochastic Programming and DRO

## Stochastic programming

The stochastic program assumes that demand scenarios and their probabilities are sufficiently known or estimated. It minimizes expected total cost over sampled demand scenarios.

## Distributionally robust optimization

The DRO model assumes that the exact probability distribution is uncertain. It minimizes cost under the worst-case probability distribution inside an ambiguity set.

The paper uses a moment-based ambiguity set defined through bounds on:

- the mean of uncertain demand;
- the second moment of uncertain demand.

---

# 6. Main Findings

- The stochastic and DRO approaches generally outperform the deterministic approach in demand coverage and out-of-sample robustness.
- The stochastic approach often achieves the lowest overall expected cost.
- The DRO approach tends to install more capacity and reduce worst-case unmet demand, but at a higher total cost.
- When resources become extremely scarce, the differences among methods shrink because all approaches have limited flexibility.
- The proposed solutions are demand-driven: they increase allocation where demand is high and avoid unnecessary production, shipping, and inventory when demand is low.

---

# 7. Transfer to Robotaxi Allocation

| Resource-distribution model | Robotaxi equivalent | Role in robotaxi model |
|---|---|---|
| Distribution center | Robotaxi city or depot | Strategic service location |
| Facility opening | City entry or depot opening | First-stage binary decision |
| Facility capacity | Fleet size or depot capacity | First-stage capacity decision |
| Demand site | City or service zone | Location requiring vehicles |
| Uncertain demand | Uncertain ride demand | Scenario-dependent requests |
| Shipment | Vehicle relocation or rebalancing | Inter-zone or inter-city movement |
| Inventory | Idle available robotaxis | Vehicles available for future periods |
| Unmet demand or backlog | Rejected or delayed ride requests | Shortage variable |
| Facility operating cost | City or depot fixed cost | Entry cost |
| Capacity cost | Vehicle acquisition and operating cost | Fleet cost |
| Shipping cost | Rebalancing cost | Empty-movement cost |
| Inventory cost | Idle-fleet cost | Over-allocation cost |
| Unmet-demand penalty | Lost trip, waiting, and service failure cost | Under-allocation cost |

---

# 8. Robotaxi Two-Stage Interpretation

## First-stage decisions

\[
y_i
=
\text{whether to enter city }i
\]

\[
q_i
=
\text{initial fleet allocated to city }i
\]

## Second-stage decisions

\[
r_{i,j,t}^{\omega}
=
\text{vehicles rebalanced from }i\text{ to }j
\]

\[
u_{i,t}^{\omega}
=
\text{unserved ride requests}
\]

\[
I_{i,t}^{\omega}
=
\text{idle available vehicles}
\]

---

# 9. Simplified Robotaxi Objective

\[
\min
\sum_i f_i y_i
+
\sum_i c_i^{fleet}q_i
+
\mathbb E_{\omega}
\left[
\sum_{i,j,t}c_{i,j}^{reb}r_{i,j,t}^{\omega}
+
\sum_{i,t}c_i^{idle}I_{i,t}^{\omega}
+
\sum_{i,t}c_i^{unmet}u_{i,t}^{\omega}
\right]
\]

subject to:

\[
q_i\le M_i y_i
\]

\[
\sum_i q_i\le Q
\]

and vehicle-flow and demand-balance constraints.

---

# 10. Why This Paper Matters for the Robotaxi Project

The paper provides methodological justification for the proposed research direction:

> Predict uncertain future demand and allocate limited capacity to minimize over-allocation and under-allocation costs.

Its most transferable ideas are:

1. **First-stage strategic decisions:** choose service locations and initial fleet capacities before future demand is known.
2. **Second-stage operational recourse:** rebalance vehicles and absorb unmet demand after demand is realized.
3. **Expected-cost optimization:** use stochastic programming when the demand distribution is reasonably estimated.
4. **Worst-case protection:** use DRO when the future demand distribution is ambiguous.
5. **Demand-driven allocation:** allocate more vehicles to high-demand areas while avoiding excessive idle capacity.

---

# Paper Conclusion

> This paper provides a transferable two-stage stochastic and distributionally robust framework for robotaxi deployment. City entry and fleet capacity can be chosen before future demand is observed, while vehicle rebalancing, idle capacity, and unmet demand can be adjusted after uncertainty is realized.
