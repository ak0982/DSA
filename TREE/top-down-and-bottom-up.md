# 🌟 **Top-Down vs Bottom-Up Approach in Tree Problems** 🌳

### **Understanding Recursion in Trees** 🔄
When solving tree problems, two common approaches to recursion are **Top-Down** and **Bottom-Up**. These techniques are powerful for traversing and solving tree-based problems.

---

## 🎯 **Top-Down Approach**:
> **Think from the root and pass information down!**

### **How It Works**: 🚀
- Start from the **root**.
- Pass information (like a target sum, max value, etc.) down to child nodes.
- Use this information to solve the problem as you traverse deeper.

### **Key Features**:
1. **Process nodes while traversing down**.
2. Pass parameters like path sums, max values, or state information.
3. Focuses on the flow **from root to leaves**.

### **Example Problem**:
**Check Root-to-Leaf Path Sum:**
- Does any root-to-leaf path have a sum equal to a target?
```cpp
bool hasPathSum(TreeNode* root, int targetSum) {
    if (!root) return false;
    if (!root->left && !root->right) return targetSum == root->val;
    return hasPathSum(root->left, targetSum - root->val) ||
           hasPathSum(root->right, targetSum - root->val);
}
```

### **Visual Representation**:
```
       5
      / \
     4   8
    /   / \
   11  13  4
  /  \
 7    2

Target Sum = 22
- Traverse top-down:
  5 -> 4 -> 11 -> 2
  Check sum at each leaf.
```

---

## 🎯 **Bottom-Up Approach**:
> **Think from the leaves and gather information upwards!**

### **How It Works**: 🚀
- Start from the **leaf nodes**.
- Solve smaller subproblems (e.g., subtree heights, subtree counts).
- Combine results as you return to the parent nodes.

### **Key Features**:
1. **Process nodes while returning up**.
2. Aggregate results (like subtree size, heights) from children.
3. Focuses on the flow **from leaves to root**.

### **Example Problem**:
**Find Tree Diameter:**
- Longest path between any two nodes in the tree.
```cpp
int treeDiameter = 0;

int diameterHelper(TreeNode* root) {
    if (!root) return 0;
    int leftHeight = diameterHelper(root->left);
    int rightHeight = diameterHelper(root->right);
    treeDiameter = max(treeDiameter, leftHeight + rightHeight);
    return 1 + max(leftHeight, rightHeight);
}

int diameterOfBinaryTree(TreeNode* root) {
    diameterHelper(root);
    return treeDiameter;
}
```

### **Visual Representation**:
```
       1
      / \
     2   3
    / \
   4   5

- Calculate subtree heights:
  At 4 and 5: Height = 1
  At 2: LeftHeight = 1, RightHeight = 1 -> Diameter = 2
  At 1: Combine heights for final diameter.
```

---

## ✨ **Comparison**:
| **Aspect**        | **Top-Down**                           | **Bottom-Up**                            |
|--------------------|----------------------------------------|------------------------------------------|
| **Flow Direction** | Root → Leaves                         | Leaves → Root                            |
| **Focus**          | Passing information to child nodes.    | Aggregating results from child nodes.    |
| **Examples**       | Path Sum, Max Depth                   | Tree Diameter, Subtree Node Count        |

---

## **Key Takeaways** 📌:
1. Choose **Top-Down** when information needs to flow **downwards** (e.g., path-specific calculations).
2. Choose **Bottom-Up** when aggregating results from **subtrees** (e.g., height, diameter).
3. Both approaches are recursive but differ in **direction and focus**.

---

🧠 **Visualization Tip**: Think of **Top-Down** as starting from the **top of a waterfall**, and **Bottom-Up** as building a **tower block-by-block from the base**.

