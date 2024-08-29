# LEETCODE-Graphs-947
To perform a dry run of the `removeStones` method from the `Solution` class, let's walk through the logic step-by-step with an example input. The method is designed to compute the maximum number of stones that can be removed such that no row or column is completely empty.

### Explanation of the Code

1. **Graph Representation**: 
   - The `graph` is an adjacency list where each stone is represented as a node, and an edge exists between two nodes if they share the same row or column.

2. **Building the Graph**:
   - Iterate over every pair of stones. If two stones share the same row or column, create a bidirectional edge between them.

3. **Counting Connected Components**:
   - The `dfs` function is used to traverse all nodes connected to a given node. Each connected component represents a group of stones that can be removed, keeping one stone.

4. **Result Calculation**:
   - The number of moves possible is the total number of stones minus the number of connected components (islands).

### Dry Run Example

Let's dry run the code with an example input:

```java
int[][] stones = {{0, 0}, {0, 1}, {1, 0}, {1, 2}, {2, 1}, {2, 2}};
```

#### Step-by-Step Execution:

1. **Initialization**:
   - `numOfIslands = 0`
   - `graph` is initialized with 6 empty lists (one for each stone).
   - `seen` is an empty set.

2. **Building the Graph**:
   - Compare each pair of stones:
     - `stones[0]` and `stones[1]` share row `0`, so add edge: `graph[0].add(1)`, `graph[1].add(0)`.
     - `stones[0]` and `stones[2]` share column `0`, so add edge: `graph[0].add(2)`, `graph[2].add(0)`.
     - `stones[1]` and `stones[3]` share row `1`, so add edge: `graph[1].add(3)`, `graph[3].add(1)`.
     - `stones[2]` and `stones[4]` share column `1`, so add edge: `graph[2].add(4)`, `graph[4].add(2)`.
     - `stones[3]` and `stones[5]` share column `2`, so add edge: `graph[3].add(5)`, `graph[5].add(3)`.
     - `stones[4]` and `stones[5]` share row `2`, so add edge: `graph[4].add(5)`, `graph[5].add(4)`.
   - The graph now looks like:
     ```
     graph = [[1, 2], [0, 3], [0, 4], [1, 5], [2, 5], [3, 4]]
     ```

3. **DFS to Count Connected Components**:
   - Iterate through each stone:
     - For stone `0`, since it's not in `seen`, perform DFS:
       - Add `0` to `seen`, traverse its neighbors (`1` and `2`):
         - Add `1` to `seen`, traverse its neighbor (`3`):
           - Add `3` to `seen`, traverse its neighbor (`5`):
             - Add `5` to `seen`, traverse its neighbor (`4`):
               - Add `4` to `seen`, traversal ends as all are visited.
     - `numOfIslands` is incremented to `1`.

4. **Calculating the Result**:
   - `stones.length` is `6`.
   - `numOfIslands` is `1`.
   - Maximum stones that can be removed: `6 - 1 = 5`.

### Final Output

The output for the given input is `5`, meaning you can remove 5 stones while ensuring at least one stone remains in every connected row or column component.
