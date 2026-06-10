# Strategic Fleet Allocation Idea for Robotaxi Deployment

This file summarizes the core modeling idea behind the robotaxi allocation project.

The goal is not to model real-time dispatching, routing, or charging. The goal is to define a **city-level strategic allocation problem**:

> Given limited additional robotaxi fleet capacity, which feasible cities should receive vehicles, and how many vehicles should be allocated to each city?

---

# 1. Overall Research Flow

The project can be organized as:

$$
\text{Current robotaxi markets}
\rightarrow
\text{Candidate cities}
\rightarrow
X_i
\rightarrow
P(D_i\mid X_i)
\rightarrow
F_i
\rightarrow
q_i^*
$$

where:

- \(X_i\): city-level demand context for city \(i\);
- \(D_i\): uncertain future robotaxi demand or required fleet capacity;
- \(F_i\): feasibility indicator for city \(i\);
- \(q_i\): number of robotaxis allocated to city \(i\).

---

# 2. What the Previous Files Provide

## 2.1 Robotaxi companies and markets

This file defines the initial candidate cities using:

- current operating markets;
- announced future markets;
- company-specific expansion patterns.

## 2.2 Demand variables

This file identifies context variables that may explain future robotaxi demand, such as:

- current robotaxi, ride-hailing, or taxi demand;
- population and employment;
- income;
- land-use mix;
- walkability;
- transit service;
- POI, entertainment, restaurant, airport, and tourism activity.

These variables form:

$$
X_i
$$

and are used to estimate:

$$
P(D_i\mid X_i)
$$

## 2.3 City-entry feasibility variables

This file identifies whether a city can realistically be considered for deployment.

Examples include:

- driverless deployment authorization;
- paid passenger-service authorization;
- ODD compatibility;
- feasible service geofence;
- depot and charging feasibility;
- weather, flooding, freeway, and construction risks.

These variables form:

$$
F_i
$$

---

# 3. Decision Variables

## City-entry decision

$$
y_i =
\begin{cases}
1, & \text{if the company enters city } i \\
0, & \text{otherwise}
\end{cases}
$$

## Fleet allocation decision

$$
q_i = \text{number of robotaxis allocated to city } i
$$

---

# 4. Key Parameters

| Symbol | Meaning |
|---|---|
| \(Q\) | Total additional robotaxi fleet available |
| \(D_i\) | Uncertain future demand or required fleet in city \(i\) |
| \(F_i\) | Whether city \(i\) is feasible |
| \(\bar q_i\) | Maximum feasible fleet in city \(i\) |
| \(f_i\) | Fixed cost of entering city \(i\) |
| \(c_i^+\) | Cost of over-allocating one vehicle |
| \(c_i^-\) | Cost of under-allocating one vehicle |

---

# 5. Core Allocation Logic

If too many vehicles are allocated:

$$
(q_i-D_i)^+
$$

This creates over-allocation costs such as:

- idle vehicles;
- depreciation;
- depot and charging costs;
- opportunity cost.

If too few vehicles are allocated:

$$
(D_i-q_i)^+
$$

This creates under-allocation costs such as:

- rejected rides;
- lost revenue;
- passenger waiting;
- lower service quality;
- customer churn.

The model balances these two costs.

---

# 6. Simple Strategic Allocation Model

$$
\min_{y,q}
\sum_i f_i y_i
+
\mathbb{E}
\left[
\sum_i
c_i^+(q_i-D_i)^+
+
c_i^-(D_i-q_i)^+
\mid X
\right]
$$

subject to:

$$
\sum_i q_i \leq Q
$$

$$
q_i \leq \bar q_i y_i
$$

$$
y_i \leq F_i
$$

$$
q_i \in \mathbb{Z}_+,\quad y_i\in\{0,1\}
$$

---

# 7. Interpretation

This model does not simply allocate vehicles to the cities with the highest predicted demand.

It also considers:

- uncertainty in future demand;
- asymmetric costs of over- and under-allocation;
- limited total fleet size;
- whether the city is legally and operationally feasible;
- the maximum number of vehicles that each city can support.

---

# 8. Why This Is Contextual Optimization

A prediction-only approach estimates demand:

$$
\hat D_i = f(X_i)
$$

and may allocate:

$$
q_i = \hat D_i
$$

But this ignores the actual decision cost.

A contextual optimization approach chooses the decision directly:

$$
q_i^* =
\arg\min_{q_i}
\mathbb{E}
\left[
c_i^+(q_i-D_i)^+
+
c_i^-(D_i-q_i)^+
\mid X_i
\right]
$$

This is the main modeling idea:

> Use city context to predict future demand uncertainty, then allocate limited fleet capacity to minimize expected over-allocation and under-allocation costs.

---

# 9. What This Model Does Not Cover Yet

This is a strategic city-level model. It does not yet model:

- vehicle-level dispatching;
- real-time rebalancing;
- passenger matching;
- charging schedules;
- state of charge;
- road-link routing.

Those can be added later as operational extensions.

---

# Final Summary

The project can be summarized as:

> Use current robotaxi markets and demand-related city context to estimate future robotaxi demand, filter cities by deployment feasibility, and allocate limited additional fleet capacity to minimize expected over- and under-allocation costs.
