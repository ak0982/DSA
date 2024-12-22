## Breadth-First Search (BFS) Algorithm 🔎

### Basic Template: BFS Without Visited Set 

The following pseudocode demonstrates how to compute the shortest path between the root and a target node using BFS:

```cpp
/**
 * Return the length of the shortest path between root and target node.
 */
int BFS(Node root, Node target) {
    Queue<Node> queue;  // Store all nodes which are waiting to be processed
    int step = 0;       // Number of steps needed from root to current node

    // Initialize
    add root to queue;

    // BFS
    while (queue is not empty) {
        // Iterate the nodes which are already in the queue
        int size = queue.size();
        for (int i = 0; i < size; ++i) {
            Node cur = the first node in queue;
            return step if cur is target;
            for (Node next : the neighbors of cur) {
                add next to queue;
            }
            remove the first node from queue;
        }
        step = step + 1;
    }
    return -1;          // There is no path from root to target
}
```

### Key Insights 🫠

1. **Queue Mechanics**:
   - At any point, the nodes in the queue represent the nodes that are waiting to be processed.
   - Each iteration of the outer `while` loop corresponds to moving one step farther from the root node.

2. **Step Variable**:
   - The variable `step` keeps track of the distance between the root node and the current node being visited.

---

### BFS Template II: Ensuring No Revisited Nodes 🔐

When dealing with graphs containing cycles, it is essential to prevent revisiting nodes to avoid infinite loops. The following modification adds a `visited` set to the BFS algorithm:

```cpp
/**
 * Return the length of the shortest path between root and target node.
 */
int BFS(Node root, Node target) {
    Queue<Node> queue;  // Store all nodes which are waiting to be processed
    Set<Node> visited;  // Store all the nodes that we've visited
    int step = 0;       // Number of steps needed from root to current node

    // Initialize
    add root to queue;
    add root to visited;

    // BFS
    while (queue is not empty) {
        // Iterate the nodes which are already in the queue
        int size = queue.size();
        for (int i = 0; i < size; ++i) {
            Node cur = the first node in queue;
            return step if cur is target;
            for (Node next : the neighbors of cur) {
                if (next is not in visited) {
                    add next to queue;
                    add next to visited;
                }
            }
            remove the first node from queue;
        }
        step = step + 1;
    }
    return -1;          // There is no path from root to target
}
```

### When Can We Skip the Visited Set? 

In certain scenarios, the `visited` set may not be necessary:

1. **Tree Traversals**:
   - You can safely omit the `visited` set if you are certain the graph is a tree (i.e., no cycles).

2. **Revisiting Nodes**:
   - You intentionally allow the same node to be added to the queue multiple times, for example, in some weighted graph scenarios.

### Time Complexity ⏳
- **Without Visited Set**: O(V + E), where V is the number of vertices and E is the number of edges.
- **With Visited Set**: O(V + E), as each node is processed only once.

### Space Complexity 🔢
- Depends on the size of the queue and the `visited` set.
- In the worst case, O(V) space is required.
