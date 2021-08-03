# Graph

A Graph is a collection of Vertices(V) and Edges(E).

Vertices also called as nodes. V is a finite set of nodes and it is a nonempty set.

Edge refers to the link between two vertices or nodes. So, E is a set of pairs of vertices.

In general,

`G = (V,E)`.

where,

`G - Graph`

`V - a set of nodes. Nonempty set.`

`E - a set of pairs of nodes. It can be an empty set.`

The graph can be of Two types:

1. Directed Graph

   In the Directed Graph, each edge(E) will be associated with directions.
   So, directed Graph have the ordered pair of edges. Edge can only be traversed from the specified direction.

   `Eg. (0, 1) and (1, 0) are two different edges`
    
   ![Directed Graph Image](https://www.log2base2.com/images/ds/digraph.png)


2. Undirected Graph

   In Undirected Graph have unordered pair of edges.
   Edge can be traversed from any direction.
   
   `Eg. (0, 1) and (1, 0) represent the same edge`

   ![Undirected Graph Image](https://www.log2base2.com/images/ds/undirected-graph.png)


&nbsp;

# Graph Representation
The graph can be represented in 3 ways, and they are as follows, with the above graphs as an example.

1. **Edge List**

   For Directed Graph
   ```python
   graph = [
       [0, 1],[0, 3], [0, 2],
       [1, 3], [1, 4],
       [2, 3],
       [3, 4]
   ]
   ```

   For Undirected Graph
   ```python
   graph = [
       [0, 1], [1, 0],
       [0, 4], [4, 0],
       [4, 3], [3, 4],
       [1, 4], [4, 1],
       [1, 2], [2, 1],
       [3, 2], [2, 3],
    ]
   ```

2. **Adjacency Matrix**

   For Directed Graph
   ```python
   graph = [
       [0, 1, 1, 1, 0],
       [0, 0, 0, 1, 1],
       [0, 0, 0, 1, 0],
       [0, 0, 0, 0, 1],
       [0, 0, 0, 0, 0],
   ]
   ```

   For Undirected Graph
   ```python
   graph = [
       [0, 1, 1, 1, 0],
       [1, 0, 0, 1, 1],
       [1, 0, 0, 1, 0],
       [1, 1, 1, 0, 1],
       [0, 1, 0, 1, 0],
    ]
   ```
3.  **Adjacency List**

      For Directed Graph
    ```python
    graph = {
        0 : [1, 2, 3],
        1 : [3, 4],
        2 : [3],
        3 : [4],
        4 : [],
    }
    ```

    For Undirected Graph
    ```python
    graph = {
        0 : [1, 2, 3],
        1 : [0, 3, 4],
        2 : [0, 3],
        3 : [0, 1, 2, 4],
        4 : [1, 3],
    }
    ```

> We mostly use Adjacency List to represt a graph in a memory since this method is more memory efficient. 

> Edge lists are rarely used (even not) to represent graph and solve problem with it.

&nbsp;
### How to convert graph from **Edge List** to **Adjacency List** ?

&nbsp;

```python
# Python code snippet

def convert_graph_to_adjacency_list(edge_list):
    hash_map = {}
    for edge in edge_list:
        start_node = edge[0]
        end_node = edge[1]
        if not hash_map.get(start_node):
            hash_map[start_node] = []
        hash_map[start_node].append(end_node)

        # start for undirected graph  - only if graph is undirected
        if not hash_map.get(end_node):
            hash_map[end_node] = []
        hash_map[end_node].append(start_node)
        #end for undirected graph
    return hash_map

edge_list = [[0, 1], [0, 3], [0, 2], [1, 3], [1, 4], [2, 3], [3, 4]]
graph = convert_graph_to_adjacency_list(edge_list)
print(graph)
# output : {0: [1, 3, 2], 1: [0, 3, 4], 3: [0, 1, 2, 4], 2: [0, 3], 4: [1, 3]}
```

&nbsp;
# Graph Traversal

1. BFS (Breadth First Search)

   ```python
   def bfs_traversal_helper(graph, vertex, visited_map):
    traversed_nodes = [vertex]
    queue = [vertex]
    visited_map[vertex] = True
    while queue:
        active_node = queue.pop(0)
        if graph.get(active_node): # handling for directed graph, if node doesn't have any outgoing edge or outdegree is 0. 
            for connected_node in graph[active_node]:
                if not visited_map.get(connected_node):
                    visited_map[connected_node] = True
                    queue.append(connected_node)
                    traversed_nodes.append(connected_node)
    return traversed_nodes, visited_map
    
    def bfs_traversal(graph):
        # graph : type -> Adjacency List
        result = list()
        visited_map = dict()
        for vertex in graph.keys():
            if not visited_map.get(vertex):
                traversed_nodes ,visited_map = bfs_traversal_helper(graph, vertex, visited_map)
                result.append(traversed_nodes)
        return result



    edge_list = [[1, 2], [1, 3], [2, 4], [3, 4], [2, 7], [7, 8], [8, 6], [5, 6], [5, 10], [3, 5],[9, 3]]
    
    graph = convert_graph_to_adjacency_list(edge_list)
    result = bfs_traversal(graph)

    print(graph)
    print(result)
   ```

   Output
   ```python
   # For Undirected Graph (if above edge list is directed)
   graph = {1: [2, 3], 2: [1, 4, 7], 3: [1, 4, 5, 9], 4: [2, 3], 7: [2, 8], 8: [7, 6], 6: [8, 5], 5: [6, 10, 3], 10: [5], 9: [3]}
   result = [[1, 2, 3, 4, 7, 5, 9, 8, 6, 10]]

   # For Undirected Graph (if above edge list is directed)
   graph = {1: [2, 3], 2: [4, 7], 3: [4, 5], 7: [8], 8: [6], 5: [6, 10], 9: [3]}
   result = [[1, 2, 3, 4, 7, 5, 8, 6, 10], [9]]
   ```
