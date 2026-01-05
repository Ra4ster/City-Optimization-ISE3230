# Urban Facility Placement Optimization

[![Python](https://img.shields.io/badge/python-3.11-blue.svg)](https://www.python.org/)
[![Gurobi](https://img.shields.io/badge/Gurobi-13.0.0-green.svg)](https://www.gurobi.com/)
[![License](https://img.shields.io/badge/license-Academic-lightgrey.svg)](https://www.gurobi.com/academic-license/)

---

## Overview

This project addresses the **urban facility placement problem** using **Mixed-Integer Programming (MIP)**. The goal is to optimally place multiple types of facilities on a 2D grid so that:

1. Every grid location is within a maximum **Manhattan distance** `T` from at least one facility of each type.
2. Facility placements do not overlap and respect maximum allowed counts per type.
3. Total facilities used are minimized once the minimum feasible `T` is found.

The model is implemented in **Python** using **Gurobi** for optimization and **Matplotlib** for visualization. The framework also includes **sensitivity analysis** to study how variations in `T` affect feasibility and required resources.

---

## Supported Facility Types

- School  
- Hospital  
- Police Station  
- Fire Station  
- Convenience Store  
- Park  
- Bank  
- Gym  
- Library  
- Post Office  

Each type can have a configurable maximum number of facilities.

---

## How It Works

1. **Binary Search on T**  
   Finds the smallest `T` such that all locations are covered by all facility types.

2. **Sensitivity Analysis**  
   Evaluates `T* ± 1` and `T* ± 2` to observe how the number of facilities changes with distance constraints.

3. **Facility Minimization**  
   Given `T_min`, the total number of facilities is minimized while maintaining coverage.

4. **Visualization**  
   Facility locations and sensitivity results are plotted for intuitive analysis.

---

## Results

**Optimal Maximum Manhattan Distance (T\_min):** 3  
**Total Facilities Required:** 70  

**Cutting Planes Used:**
- Gomory: 17  
- MIR: 6  
- Flow Cover: 35  
- Zero Half: 13  

**Solver Statistics:**
- Explored Nodes: 32,902  
- Simplex Iterations: 10,613,473  
- Runtime: 128.86 s (376.54 work units)  
- Threads: 10  

**Solution Range:** 70–81 facilities  

---

### Selected Facility Placements

- **School:** (1,7), (2,3), (4,9), (5,3), (8,6), (10,1), (10,10)  
- **Convenience:** (1,4), (3,9), (5,1), (6,5), (8,10), (9,2), (10,5)  
- **Hospital:** (1,1), (2,8), (4,5), (6,3), (7,10), (9,3), (9,7)  
- **Park:** (1,5), (3,10), (4,1), (5,8), (8,4), (9,9), (10,3)  
- **Fire:** (2,2), (2,6), (2,10), (5,6), (7,2), (8,9), (10,4)  
- **Police:** (1,3), (2,9), (4,3), (5,7), (8,1), (9,5), (9,10)  
- **Library:** (1,2), (1,9), (4,6), (6,9), (7,1), (8,3), (10,8)  
- **Gym:** (1,10), (2,1), (2,5), (6,8), (7,3), (9,8), (10,2)  
- **Bank:** (1,6), (3,2), (4,10), (6,6), (8,5), (9,1), (10,9)  
- **Post Office:** (1,8), (3,1), (3,4), (5,5), (6,10), (8,2), (10,7)  

---

### Sensitivity Analysis

| T  | Status      | Minimum Facilities |
|----|------------|-----------------|
| 2  | Infeasible | -               |
| 3  | Feasible   | 70              |
| 4  | Feasible   | 45              |
| 5  | Feasible   | 40              |

**Observation:** Increasing `T` reduces the number of facilities required but increases the maximum distance any location is from a facility.

---

### Visualization

**Facility Placement Visualized:**

![Facility Grid](https://i.ibb.co/SX8gPrSr/download.png)

**Sensitivity Plot:**  
Feasible vs. Infeasible points showing the trade-off between `T` and total facilities.

![Sensitivity Plot](https://i.ibb.co/zTjmQ93m/download-1.png)

---

## Installation

```bash
pip install gurobipy matplotlib
```
> Requires an academic or commercial license for Gurobi.

## Usage

```python
from facility_placement import addPoint

# Add a custom point
addPoint(2, 3, 'blue')
```

Run the main script to compute T_min, optimal facility placements, and generate plots:

```bash
python facility_placement.py
```

---

## Contributors

This project was developed by:

- **[Jack Rose](https://github.com/ra4ster)** – Algorithm design, optimization modeling, and Jupyter setup.
- **[Samuel Gadkar](https://github.com/sgadkar)** – Data visualization, sensitivity analysis, and file uploads.
- **Noah Mudrick** – Final report, slideshow, video, and project formulation.

---

## License

Academic Use Only – [Gurobi Academic License](https://www.gurobi.com/academia/academic-program-and-licenses/)
