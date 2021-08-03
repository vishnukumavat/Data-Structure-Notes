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

