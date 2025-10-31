import heapq

def dijkstra(V, adj, S):
    # V: number of vertices
    # adj: adjacency list where adj[u] = [(v, weight), ...]
    # S: source vertex
    
    # Step 1: Initialize distances
    dist = [float('inf')] * V
    dist[S] = 0

    # Step 2: Min-heap (priority queue)
    pq = [(0, S)]  # (distance, vertex)
    
    while pq:
        current_dist, u = heapq.heappop(pq)
        
        # Skip if we already found a better path
        if current_dist > dist[u]:
            continue
        
        # Step 3: Check neighbors
        for v, weight in adj[u]:
            if dist[u] + weight < dist[v]:
                dist[v] = dist[u] + weight
                heapq.heappush(pq, (dist[v], v))
    
    return dist
