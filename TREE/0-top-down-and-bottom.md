# Recursive Tree Problem Solving: Top-Down vs. Bottom-Up 🌳

Understanding tree problems becomes easy when approached with structured recursion. Here, we summarize the **Top-Down** and **Bottom-Up** approaches creatively with examples, diagrams, and general formats! ✨

---

## **Top-Down Approach** 🌟

### Concept 🛤️
The **Top-Down** approach solves the problem from the root and propagates information **down** to the child nodes. It focuses on breaking the problem into smaller subproblems during recursion.

### General Format 📜
```cpp
// Top-Down Approach: Solve from root to leaves
int solve(TreeNode* node, Params parentParams) {
    if (node == NULL) return baseCaseValue; // Handle base case, e.g., NULL node.

    // Compute current state or result using parentParams.
    Params currentParams = process(node, parentParams);

    // Recurse for child nodes.
    int leftResult = solve(node->left, currentParams);
    int rightResult = solve(node->right, currentParams);

    // Combine results (optional).
    return combineResults(leftResult, rightResult, node);
}
```

### Example 1: Maximum Root-to-Leaf Path Sum 🌞
```cpp
int maxPathSum(TreeNode* root, int currentSum) {
    if (root == NULL) return currentSum;

    currentSum += root->val;

    int leftSum = maxPathSum(root->left, currentSum);
    int rightSum = maxPathSum(root->right, currentSum);

    return max(leftSum, rightSum);
}
```
**Diagram** 🖼️:
```
        10
       /  \
      5    15
     / \     \
    2   7     20
```
- Start at `10`.
- Propagate sums down (`10 -> 15 -> 20` gives maximum `45`).

---

## **Bottom-Up Approach** 🌱

### Concept 🏔️
The **Bottom-Up** approach solves subproblems for child nodes first and combines their results to solve the parent problem. It works **up** from the leaf nodes to the root.

### General Format 📜
```cpp
// Bottom-Up Approach: Solve from leaves to root
int solve(TreeNode* node) {
    if (node == NULL) return baseCaseValue; // Handle base case, e.g., NULL node.

    // Recurse for child nodes.
    int leftResult = solve(node->left);
    int rightResult = solve(node->right);

    // Combine results from child nodes and process the current node.
    return process(node, leftResult, rightResult);
}
```

### Example 1: Tree Height 🌲
```cpp
int treeHeight(TreeNode* root) {
    if (root == NULL) return 0;

    int leftHeight = treeHeight(root->left);
    int rightHeight = treeHeight(root->right);

    return 1 + max(leftHeight, rightHeight);
}
```
**Diagram** 🖼️:
```
        10
       /  \
      5    15
     / \     \
    2   7     20
```
- Start at leaves (`2`, `7`, `20` -> height `1`).
- Combine results up to root (`max(2, 2) + 1 = 3`).

---

### **Key Differences** 📝
| Feature             | Top-Down 🌟                     | Bottom-Up 🌱                    |
|---------------------|--------------------------------|---------------------------------|
| **Flow**           | Root -> Leaves                | Leaves -> Root                 |
| **Focus**          | Pass parameters down          | Combine results up             |
| **Use Case**       | Path-related calculations     | Aggregation or subtree results |

---

### **When to Use?** 🤔
1. **Top-Down**:
   - Problems requiring propagation of information (e.g., path sums, distances).

2. **Bottom-Up**:
   - Problems needing child-to-parent aggregation (e.g., subtree calculations, depths).

---

### **Complete Examples** 📚
#### Example: Top-Down - Count Nodes with Greater Ancestors 🌟
```cpp
void countGreater(TreeNode* node, int maxVal, int &count) {
    if (node == NULL) return;

    if (node->val > maxVal) count++;

    maxVal = max(maxVal, node->val);

    countGreater(node->left, maxVal, count);
    countGreater(node->right, maxVal, count);
}
```

#### Example: Bottom-Up - Diameter of a Tree 🌱
```cpp
pair<int, int> diameter(TreeNode* root) {
    if (root == NULL) return {0, 0};

    pair<int, int> left = diameter(root->left);
    pair<int, int> right = diameter(root->right);

    int height = 1 + max(left.first, right.first);
    int dia = max({left.second, right.second, left.first + right.first});

    return {height, dia};
}
```

---

### Final Thoughts 💡
- **Top-Down**: Start at the root, solve on the way down.
- **Bottom-Up**: Start at the leaves, combine results on the way up.

Practice both approaches to master recursive problem solving! 🚀

