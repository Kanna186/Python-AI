def water_jug_problem(jug1_capacity, jug2_capacity, target):
    initial_state = (0, 0)
    stack = [(initial_state, [])]
    visited = set()
    actions = [
        ("Fill Jug 1", lambda j1, j2: (jug1_capacity, j2)),
        ("Fill Jug 2", lambda j1, j2: (j1, jug2_capacity)),
        ("Empty Jug 1", lambda j1, j2: (0, j2)),
        ("Empty Jug 2", lambda j1, j2: (j1, 0)),
        ("Pour Jug 1 -> Jug 2", lambda j1, j2: (max(0, j1 - (jug2_capacity - j2)), min(jug2_capacity, j1 + j2))),
        ("Pour Jug 2 -> Jug 1", lambda j1, j2: (min(jug1_capacity, j1 + j2), max(0, j2 - (jug1_capacity - j1)))),
    ]
    while stack:
        (j1, j2), path = stack.pop()
        if (j1, j2) in visited:
            continue
        visited.add((j1, j2))
        if j1 == target or j2 == target:
            return path + [f"Reached target: {target}"]
        for action_name, action in actions:
            next_state = action(j1, j2)
            if next_state not in visited:
                stack.append((next_state, path + [action_name]))
    return None
jug1_capacity = int(input("Enter the capacity of Jug 1: "))
jug2_capacity = int(input("Enter the capacity of Jug 2: "))
target = int(input("Enter the target amount of water: "))
result = water_jug_problem(jug1_capacity, jug2_capacity, target)
if result:
    print("Sequence of actions to reach the target:", result)
else:
    print("No solution found.")