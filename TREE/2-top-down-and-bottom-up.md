# **Mastering Tree Problems: Top-Down vs Bottom-Up Approaches**

Tree problems can be solved using two key recursive strategies:

- **Top-Down Approach** 🌟
- **Bottom-Up Approach** 🌳

Both are powerful but differ in how they process the tree. Let’s break them down with **examples** and **code** to make these approaches unforgettable. 🚀

---

## **1. Top-Down Approach** 🌟
### **Key Idea:**
- Pass information from the **root to the leaves**.
- **Start from the root**, use parameters to pass information, and solve the subproblems along the way.

### **Example 1: Root-to-Leaf Path Sum**
> Check if there exists a root-to-leaf path with a given sum.

#### **Code**:
```cpp
bool hasPathSum(TreeNode* root, int targetSum) {
    if (!root) return false;
    if (!root->left && !root->right) {
        return targetSum == root->val;
    }
    return hasPathSum(root->left, targetSum - root->val) ||
           hasPathSum(root->right, targetSum - root->val);
}
```
#### **Diagram**:
```
Tree:
       5
      / \
     4   8
    /   / \
   11  13  4
  /  \
 7    2

Target Sum = 22
Recursive Flow:
- At 5, targetSum = 22 -> Pass 17 to 4, 17 to 8
- At 4, targetSum = 17 -> Pass 13 to 11
- At 11, targetSum = 13 -> Pass 2 to 7, 2 to 2
- Leaf 2 matches targetSum -> Return true
```
---

### **Example 2: Count Good Nodes in a Path**
> Count nodes greater than or equal to all their ancestors in a root-to-current path.

#### **Code**:
```cpp
void countGoodNodes(TreeNode* root, int maxVal, int& count) {
    if (!root) return;
    if (root->val >= maxVal) {
        count++;
        maxVal = root->val;
    }
    countGoodNodes(root->left, maxVal, count);
    countGoodNodes(root->right, maxVal, count);
}

int goodNodes(TreeNode* root) {
    int count = 0;
    countGoodNodes(root, INT_MIN, count);
    return count;
}
```
#### **Diagram**:
```
Tree:
       3
      / \
     1   4
    /   / \
   3   1   5

Recursive Flow:
- At 3, maxVal = INT_MIN -> Count = 1
- At 1, maxVal = 3 -> Count = 1
- At 3, maxVal = 3 -> Count = 2
- At 4, maxVal = 3 -> Count = 3
- At 5, maxVal = 4 -> Count = 4
```

---

## **2. Bottom-Up Approach** 🌳
### **Key Idea:**
- Process information from the **leaves to the root**.
- **Start from the leaves**, solve smaller subproblems, and aggregate results as we move up.

### **Example 1: Tree Diameter**
> Find the longest path between any two nodes in a tree.

#### **Code**:
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
#### **Diagram**:
```
Tree:
       1
      / \
     2   3
    / \
   4   5

Recursive Flow:
- At 4 and 5, height = 1
- At 2, leftHeight = 1, rightHeight = 1 -> diameter = 2
- At 3, height = 1
- At 1, leftHeight = 2, rightHeight = 1 -> diameter = 3
```
---

### **Example 2: Count Nodes in Subtree**
> Count the number of nodes in the subtree of each node.

#### **Code**:
```cpp
int countNodes(TreeNode* root) {
    if (!root) return 0;
    int leftSize = countNodes(root->left);
    int rightSize = countNodes(root->right);
    return 1 + leftSize + rightSize;
}
```
#### **Diagram**:
```
Tree:
       1
      / \
     2   3
    / \
   4   5

Recursive Flow:
- At 4 and 5, subtree size = 1
- At 2, leftSize = 1, rightSize = 1 -> Total size = 3
- At 3, subtree size = 1
- At 1, leftSize = 3, rightSize = 1 -> Total size = 5
```

---

## **Top-Down vs Bottom-Up Cheat Sheet**
| **Aspect**         | **Top-Down**                          | **Bottom-Up**                         |
|---------------------|---------------------------------------|---------------------------------------|
| **Direction**       | Root ➡ Leaves                      | Leaves ➡ Root                      |
| **Information Flow**| Pass information down                | Aggregate results up                 |
| **Focus**           | Parameters for each call             | Return values from each call         |
| **Use Cases**       | Path-based problems                  | Subtree-based problems               |
| **Example Problems**| Path Sum, Good Nodes in Path         | Tree Diameter, Subtree Node Count    |

---

### **Recap**:
- Use **Top-Down** for problems where you need to **pass constraints or states** down the tree.
- Use **Bottom-Up** for problems where you need to **aggregate results** from subtrees.

Happy Coding! 🚀🌳

