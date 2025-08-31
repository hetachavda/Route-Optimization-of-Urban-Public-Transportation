
# 🚌 Route Optimization of Urban Public Transportation  

A **data-driven operations analytics project** that applies **mathematical modeling, optimization, and Python (Google OR-Tools)** to improve bus scheduling and routing efficiency in urban transit systems.  

This project was developed as part of **Operations Analytics (DAMO 610-1)** at the **University of Niagara Falls, Canada**.  

---

## 📌 Project Overview  
Public transport plays a critical role in urban life. However, challenges such as **demand fluctuations, traffic congestion, operational costs, and environmental impact** make bus scheduling a complex optimization problem.  

This project addresses these challenges by:  
- Designing a **mathematical optimization model**  
- Implementing it in **Python using Google OR-Tools**  
- Extending it with **real-world constraints** (traffic, emissions, demand variation)  
- Providing **visualizations and insights** for decision-making  

---

## 🎯 Objectives  
- Minimize **passenger waiting time**  
- Optimize **bus allocation & fleet utilization**  
- Reduce **operational costs** (fuel, labor, maintenance)  
- Integrate **real-time traffic & congestion factors**  
- Ensure **sustainable operations** by controlling emissions  
- Improve **service reliability and social equity**  

---

## 📂 Methodology  

### 1. Mathematical Model  
- **Decision Variables:** Bus assignment (X_ij), arrival times (Y_ij)  
- **Objective Function:** Minimize costs, delays, transfers, and emissions  
- **Constraints:**  
  - Demand satisfaction  
  - Fleet size limitations  
  - Travel time & congestion factors  
  - Emission caps  

### 2. Python Implementation  
- **Library:** Google OR-Tools  
- **Approach:** Linear & Mixed Integer Programming (MIP)  
- **Extensions:**  
  - Dynamic traffic adjustments  
  - Emission & fuel efficiency tracking  
  - Passenger demand fluctuations  

---

## ⚙️ Example Python Snippet  

```python
from ortools.linear_solver import pywraplp

def optimize_bus_scheduling():
    solver = pywraplp.Solver.CreateSolver('SCIP')
    num_stops = 5
    cost_matrix = [[0, 10, 15, 30, 25],
                   [10, 0, 20, 35, 40],
                   [15, 20, 0, 25, 30],
                   [30, 35, 25, 0, 15],
                   [25, 40, 30, 15, 0]]

    num_buses = 3
    X = {}

    for i in range(num_stops):
        for j in range(num_stops):
            if i != j:
                X[i, j] = solver.BoolVar(f'X[{i},{j}]')

    solver.Minimize(solver.Sum(cost_matrix[i][j] * X[i, j]
                               for i in range(num_stops) for j in range(num_stops) if i != j))

    for i in range(num_stops):
        solver.Add(sum(X[i, j] for j in range(num_stops) if i != j) == 1)

    status = solver.Solve()
    if status == pywraplp.Solver.OPTIMAL:
        print("Optimal solution found:")
        for i in range(num_stops):
            for j in range(num_stops):
                if i != j and X[i, j].solution_value() > 0.5:
                    print(f'Bus route: {i} -> {j}')
    else:
        print("No solution found.")
````
---

## 📊 Visualizations

* **Route Visualization** → NetworkX + Matplotlib
* **Heatmap of Travel Costs** → Seaborn
* **Passenger Demand by Time** → Bar charts

---

## ✅ Results & Key Insights

* 🚍 Optimized allocation reduced **idle time** and **overuse**
* ⏱ Passenger waiting time **decreased significantly**
* 💰 Lower **operational costs** through efficient scheduling
* 🌱 Environmental impact reduced by **emission control constraints**
* 🚦 Real-time **traffic-aware routing** improved punctuality
* 📈 Service reliability increased → higher potential ridership

---

## ⚠️ Limitations & Future Enhancements

* Current model tested on **synthetic data** → needs integration with **real GPS & IoT feeds**
* Passenger demand forecasting can be improved with **AI/ML models**
* Future scope: Real-time **dashboard for city planners** to optimize dynamically

---

## 👨‍💻 Contributors

* **Setu Chaudhari** (NF1009018) – Code & Report
* **Heta Chavda** (NF1014555) – Presentation
* **Enejo David Colonel** – Report & Presentation

📚 Course: **Operations Analytics (DAMO 610-1)**
👨‍🏫 Professor: **Cosimo Girolamo**

---

## 📂 Tech Stack

* **Python** (Google OR-Tools, NumPy, NetworkX, Seaborn, Matplotlib)
* **Optimization Algorithms (MIP, Linear Programming)**
* **Visualization Tools** for insights

---

## 📌 Conclusion

This project highlights how **operations analytics and optimization** can transform urban public transportation by:

* Reducing costs
* Enhancing passenger satisfaction
* Supporting sustainable urban development

By combining **mathematical modeling, Python optimization, and visualization**, the project provides a framework for smarter and greener **public transit systems**.

---
