# Strategic Fleet Allocation Idea for Robotaxi Deployment

I wrote some thoughts about how to set a problem connecting with the E(c+ + c-) model you mentioned before. It's just an idea; I'm still unorganized with which variables is considerable and dealing with uncertainty.

Summary:
- File 01, current cities and potential cities for allocation of robotaxis
- File 02, variables related with demand of robotaxi
- File 03, city_entry_conditions(ex. regulations, weather risks) that could be variables for allocation of robotaxis

---
Potential idea of model:

> Use current robotaxi markets and demand-related city context to estimate future robotaxi demand, filter cities by deployment feasibility, and allocate limited additional fleet capacity to minimize expected over- and under-allocation costs.

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

## 2.2 Demand variables

This file identifies context variables that may explain future robotaxi demand, such as:

- current robotaxi, ride-hailing, or taxi demand;
- population and employment;
- income;
- land-use mix;
- walkability;
- transit service;
- POI, entertainment, restaurant, airport, and tourism activity.

These variables may form context $X_i$, 
and are used to estimate $P(D_i\mid X_i)$, where *D_i* is future demand

## 2.3 City-entry feasibility variables

This file identifies whether a city can realistically be considered for deployment.

Examples may include:

- driverless deployment authorization;
- paid passenger-service authorization;
- ODD compatibility;
- feasible service geofence;
- depot and charging feasibility;
- weather, flooding, freeway, and construction risks.

These variables form feasibility indicator $F_i$

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

※ I haven't thought about how to set the costs of entering city, over/under allocating a vehicle yet.
---

# 5. Core Allocation Logic

If too many vehicles are allocated: $(q_i-D_i)^+$

This creates over-allocation costs such as:

- cars that aren't being used;
- depreciation(car losing value over time);
- money spent to park, store and charge vehicles;
- opportunity cost(money you could have earned by using the cars in a better way).

If too few vehicles are allocated: $(D_i-q_i)^+$

This creates under-allocation costs such as:

- rejected rides(rides the system has to turn down because there aren't enough cars);
- money the company could have earned but couldn't;
- increase in passenger waiting time;
- lower service quality;
- cost of customers leaving and choosing another service.

The model balances these two costs.

---

# 6. Idea of Model

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

constraints:

$$
\sum_i q_i \leq Q
$$ 
-> sum of number of robotaxis allocated to city i should be less than total number of additional robotaxi fleet available

$$
q_i \leq \bar q_i y_i
$$ 
-> If you don’t enter(y_i=0) the city, you must allocate zero vehicles. If you do enter(y_i=1), you can allocate up to q_i vehicles.

$$
y_i \leq F_i
$$  
-> The decision to enter city i cannot be 1 unless the city is feasible

$$
q_i \in \mathbb{Z}_+,\quad y_i\in\{0,1\}
$$ 
-> q_i must be a non-negative integer, and y_i is a binary variable that can only be 0 or 1
