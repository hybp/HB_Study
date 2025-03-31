Basically: Queue + visited set
BFS DFS 차이는 - 큐에서 꺼내는 순서
### BFS (FIFO, 먼저 들어간거 꺼내기)
*Shortest distance*
```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    
    while queue:
        node = queue.popleft()  # Dequeue from the front
        if node not in visited:
            print(node, end=" ")  # Process the node
            visited.add(node)
            queue.extend(graph[node])  # Enqueue all neighbors
```

### BFS with Travel Record (최단 "루트" 리턴 해야 하는 경우)
```python
from collections import deque

def bfs_shortest_path(graph, start, end):
    visited = set()
    
    # 큐에 Path record를 같이 실어준다
    queue = deque([(start, [start])])  # (current_node, path_to_node)
    
    while queue:
        node, path = queue.popleft()
        
        if node == end:
            return path
        
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append((neighbor, path + [neighbor]))
    
    return []  # No path found
```

### DFS (LIFO, 마지막거 꺼내기)
*어차피 전체 순환 해야 할 때*
```python
def dfs_iterative(graph, start):
    visited = set()
    stack = [start]

    while stack:
        node = stack.pop()  # LIFO: Last-In, First-Out
        if node not in visited:
            print(node, end=" ")  # Process the node
            visited.add(node)
            stack.extend(reversed(graph[node]))  # Push neighbors to stack

```

### Dijkstra (BFS + Weight + graph to store distance record)
```python
import heapq

def dijkstra(graph, start):
    pq = [(0, start)]  # (distance, node)
    distances = {node: float('inf') for node in graph}
    distances[start] = 0

    while pq:
        curr_dist, node = heapq.heappop(pq)  # Get the node with the smallest distance

        if curr_dist > distances[node]:  
            continue  # Ignore outdated distances

        for neighbor, weight in graph[node]:  
            distance = curr_dist + weight
            if distance < distances[neighbor]:  # Found a shorter path
                distances[neighbor] = distance
                heapq.heappush(pq, (distance, neighbor))

    return distances
```

