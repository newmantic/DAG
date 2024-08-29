# DAG


A topological sort of a directed acyclic graph (DAG) is a linear ordering of its vertices such that for every directed edge u→v from vertex u to vertex v, vertex u comes before vertex v in the ordering.
Topological sorting is only possible for directed acyclic graphs (DAGs). If the graph contains cycles, a topological sort is not possible.

Multiple Orders: A DAG may have multiple valid topological sorts.

Given a DAG represented as G=(V,E) where:
V is the set of vertices. 
E is the set of directed edges.
A valid topological sort is a sequence T of vertices such that:
If there is an edge (u,v) ∈ E, then u appears before v in T.


Depth-First Search (DFS) Based Approach:
Perform a DFS traversal of the graph.
Maintain a stack to store the order of vertices.
When a vertex is finished (i.e., all its adjacent vertices have been processed), push it onto the stack.
At the end, the stack will contain the topological ordering.

Pseudocode:
function topological_sort_dfs(G):
    visited = set()
    stack = []

    for each vertex v in G:
        if v not in visited:
            dfs(v, visited, stack)

    return reverse(stack)

function dfs(v, visited, stack):
    visited.add(v)
    for each neighbor n of v:
        if n not in visited:
            dfs(n, visited, stack)
    stack.append(v)


Kahn's Algorithm:

Compute the in-degree (number of incoming edges) for each vertex.
Initialize a queue with all vertices having an in-degree of 0 (no dependencies).

While the queue is not empty:
Dequeue a vertex u and add it to the topological order.
For each neighbor v of u, decrease the in-degree of v by 1.
If the in-degree of v becomes 0, enqueue v.
If the number of vertices in the topological order is equal to the number of vertices in the graph, a valid topological sort exists.

Pseudocode:
function topological_sort_kahn(G):
    in_degree = compute_in_degree(G)
    queue = []

    for each vertex v in G:
        if in_degree[v] == 0:
            queue.append(v)

    top_order = []

    while queue is not empty:
        u = queue.pop(0)
        top_order.append(u)

        for each neighbor n of u:
            in_degree[n] -= 1
            if in_degree[n] == 0:
                queue.append(n)

    if len(top_order) != len(G):
        return "Graph has a cycle"
    return top_order
    
