import heapq
def best_first_search(graph, start, goal):
    visited = set()
    priority_queue = []
    heapq.heappush(priority_queue, (0, start))   
    while priority_queue:
        cost, node = heapq.heappop(priority_queue)
        if node in visited:
            continue
        print(f"Visiting node: {node}")
        visited.add(node)
        if node == goal:
            print("Goal reached!")
            return
        for neighbor, weight in graph[node]:
            if neighbor not in visited:
                heapq.heappush(priority_queue, (weight, neighbor))
def main():
    graph = {}
    num_edges = int(input("Enter the number of edges: "))
    for _ in range(num_edges):
        u, v, w = input("Enter edge (u v w): ").split()
        w = int(w)
        if u not in graph:
            graph[u] = []
        if v not in graph:
            graph[v] = []
        graph[u].append((v, w))
        graph[v].append((u, w))
    start = input("Enter the start node: ")
    goal = input("Enter the goal node: ")
    best_first_search(graph, start, goal)
if __name__ == "__main__":
    main()