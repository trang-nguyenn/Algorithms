This is probaly the most interesting data structure among all the basics for coding interview.    
The looping and indexing techniques over this data structure have full of `twist` and `turn`.     

The fundamental is still the `graph_out` (a node to a set of nexts), `graph_in`, (a node to a set of previous).    
`number_out`, `number_in` can be a slight dimensionality reduction for the length of the `graph_out` and `graph_in`.     

Sometimes we see `queue` and `stack` to loop over this graph, and we stop the looping when we are out of elements in the `queue` or `stack`. We are still looking for the next elements from the neighbors in `graph_out` and `graph_in`. But if we want to work out graph problems, there is `something extra` ... What is this `something extra`?

## Queue (or you might think about its duality BFS) and the detecting loop problem

Something extra here is the update rule of the `number_out`. We need to do an extra step of deleting the "visited" connection over our looping. 

```python
        queue = [i for i in num_out if num_out[i]==0]
        while queue:
            node = queue.pop(0)
            for prev in incoming[node]:
                num_out[prev] -= 1
                if num_out[prev] == 0: queue.append(prev)
```

Think deeper on this technique? What is bfs here? What are the layers of the bfs? What nodes have the same "bfs depth"?   
The "depth" here is the number of "directed outflows". We need a trick to reveal this data.

## Stack (or you might think about its duality DFS) for Topological Sorting

When we do sorting, we need a "value", such as 2<3, but what can be the "value" here in graph?     
There is always extra flavors in the graph structure, something similar but not quite.    
We are talking about the order of flows. Prev must come before node, and node must come before its nexts.


## Critical Connections (stack or queue? search deep or search nearby first?) 
