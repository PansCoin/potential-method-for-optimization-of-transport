import numpy as np

def calculate_potentials(solution, distances):
    num_ex, num_emb = solution.shape
    ai = [None] * num_ex
    bi = [None] * num_emb
    
    ai[0] = 0
    
    changed = True
    while changed:
        changed = False
        
        for i in range(num_ex):
            for j in range(num_emb):
                if solution[i][j] > 0:
                    # If this route is used, enforce complementary slackness
                    if ai[i] is not None and bi[j] is None:
                        bi[j] = distances[i][j] - ai[i]
                        changed = True
                    elif ai[i] is None and bi[j] is not None:
                        ai[i] = distances[i][j] - bi[j]
                        changed = True
    
    for i in range(num_ex):
        if ai[i] is None:
            ai[i] = 0
    for j in range(num_emb):
        if bi[j] is None:
            bi[j] = 0
    
    return ai, bi

def potential_method_with_potentials(ex_points, ex_volumes, emb_points, emb_volumes, distances):
    num_ex = len(ex_points)
    num_emb = len(emb_points)

    solution = np.zeros((num_ex, num_emb))
    
    remaining_ex_volumes = ex_volumes.copy()
    remaining_emb_volumes = emb_volumes.copy()

    while sum(remaining_ex_volumes) > 0 and sum(remaining_emb_volumes) > 0:
        min_cost = float('inf')
        min_i, min_j = -1, -1

        for i in range(num_ex):
            for j in range(num_emb):
                if remaining_ex_volumes[i] > 0 and remaining_emb_volumes[j] > 0:
                    if distances[i][j] < min_cost:
                        min_cost = distances[i][j]
                        min_i, min_j = i, j

        transfer = min(remaining_ex_volumes[min_i], remaining_emb_volumes[min_j])
        solution[min_i][min_j] = transfer
        remaining_ex_volumes[min_i] -= transfer
        remaining_emb_volumes[min_j] -= transfer

    ai, bi = calculate_potentials(solution, distances)

    return solution, ai, bi

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

