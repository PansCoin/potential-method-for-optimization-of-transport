# README: Potential Method for Optimal Mass Distribution

## Overview

This script implements the Potential Method to solve a transportation problem involving excavation and embankment points. It distributes the available mass from excavation points to embankment points at minimal cost based on given distances.

### Key Features:

1. Calculates optimal mass distribution between excavation and embankment points.
2. Computes potentials (`ai` for excavation points and `bi` for embankment points) to determine complementary slackness.

---

## How to Use

### 1. Prerequisites

Ensure you have **Python 3.6+** installed, along with the **NumPy** library. You can install NumPy using pip:

```bash
pip install numpy
```

---

### 2. Script Description

- **Functions**:

  - `calculate_potentials(solution, distances)`: Calculates potentials based on the current solution matrix and distances.
  - `potential_method_with_potentials(ex_points, ex_volumes, emb_points, emb_volumes, distances)`: Solves the transportation problem and computes potentials.

- **Inputs**:

  - `excavation_points`: List of excavation point names.
  - `excavation_volumes`: List of volumes available at each excavation point.
  - `embankment_points`: List of embankment point names.
  - `embankment_volumes`: List of volumes needed at each embankment point.
  - `distances_matrix`: 2D list of distances between each excavation and embankment point.

- **Outputs**:

  - `solution`: Matrix representing the optimal mass distribution.
  - `ai`: Potentials for excavation points.
  - `bi`: Potentials for embankment points.

---

### 3. Steps to Run

1. Define your problem data by specifying:

   - Names and volumes of excavation and embankment points.
   - Distances matrix.

2. Call the `potential_method_with_potentials` function with your data as arguments.

3. Inspect the results: optimal mass distribution (`solution`) and the calculated potentials (`ai`, `bi`).

#### Example Input Data:

```python
excavation_points = ["A1", "A2", "A3", "A4", "A5", "A6"]
excavation_volumes = [39989, 9839, 12241, 2979, 1557, 1557]
embankment_points = ["B1", "B2", "B3"]
embankment_volumes = [8143, 9180, 50839]
distances_matrix = [
    [263.47, 260.37, 1280.0],
    [95.06, 143.96, 1295.92],
    [268.04, 203.28, 1405.67],
    [23.74, 105.63, 1350.54],
    [235.32, 240.51, 1271.38],
    [239.9, 219.65, 1319.17]
]
```

#### Example Run:

```python
optimal_routes, ai, bi = potential_method_with_potentials(
    excavation_points, excavation_volumes, embankment_points, embankment_volumes, distances_matrix
)

print("Optimal Mass Distribution Matrix:")
print(optimal_routes)

print("\nai (Potentials for Excavation Points):")
for i, a in enumerate(ai):
    print(f"{excavation_points[i]}: {a}")

print("\nbi (Potentials for Embankment Points):")
for j, b in enumerate(bi):
    print(f"{embankment_points[j]}: {b}")
```

---

### 4. Output

The script prints:

1. **Optimal Mass Distribution Matrix**: The allocation of volumes from excavation to embankment points.
2. **Potentials for Excavation Points (****`ai`****)**.
3. **Potentials for Embankment Points (****`bi`****)**.

---

## Customization

Modify the `excavation_points`, `excavation_volumes`, `embankment_points`, `embankment_volumes`, and `distances_matrix` as per your specific use case.

---

## Troubleshooting

1. **Sum Mismatch**: Ensure total excavation volume equals total embankment volume.
2. **Undefined Potentials**: The script ensures all potentials are defined; if not, recheck the `distances_matrix` and initial solution.

---

## License

This script is free to use and modify for educational and personal purposes.



