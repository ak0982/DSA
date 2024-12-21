# **IBH Method (Induction - Base Condition - Hypothesis)**

## **Summary**
The IBH method is a structured way to solve recursive problems. It ensures that each problem is broken into smaller sub-problems until a base condition is reached, and the solution is then built back step-by-step using recursion.

### **Core Steps of IBH**

1. **Base Condition:**
   - Identify the smallest valid input for which the solution is trivial.
   - Example: For printing numbers from 1 to `n`, the base condition is `n == 0`.

2. **Hypothesis:**
   - Assume the recursion works perfectly for the smaller input.
   - Example: To print numbers from 1 to `n`, assume the recursion prints from 1 to `n-1` correctly.

3. **Induction:**
   - Use the result of the smaller input to solve the current problem.
   - Example: Print `n` after the recursive call for `n-1`.

---

### **Examples**

#### **1. Printing Numbers from 1 to `n`**

**Problem Statement:** Print all numbers from 1 to `n` using recursion.

```java
class Main {
  public static void solve(int n) {
    if (n == 0) return;  // Base Condition
    solve(n - 1);        // Hypothesis
    System.out.println(n); // Induction
  }
}
```

#### **Visualization (Stack Representation):**

For `n = 3`:

| Call Stack         | Action              |
|--------------------|---------------------|
| `solve(3)`         | Print `3`          |
| `solve(2)`         | Print `2`          |
| `solve(1)`         | Print `1`          |
| **Base Condition** | Stop Recursion     |

---

#### **2. Printing Numbers from `n` to 1**

**Problem Statement:** Print all numbers from `n` to 1 using recursion.

```java
class Main {
  public static void solve(int n) {
    if (n == 0) return; // Base Condition
    System.out.println(n); // Induction
    solve(n - 1);         // Hypothesis
  }
}
```

---

#### **3. Calculating Height of a Binary Tree**

**Problem Statement:** Find the maximum depth of a binary tree.

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0; // Base Condition
        int left = maxDepth(root.left); // Hypothesis
        int right = maxDepth(root.right); // Hypothesis
        return Math.max(left, right) + 1; // Induction
    }
}
```

**Tree Example:**

```
        1
       / \
      2   3
     / \    \
    4   5    6
```

- **Base Condition:** `root == null`
- **Hypothesis:** Calculate depth of left and right subtrees.
- **Induction:** Take the maximum depth of the two subtrees and add 1.

#### **Stack Visualization for Tree Traversal:**

| Call Stack         | Left Subtree Depth | Right Subtree Depth | Result |
|--------------------|--------------------|----------------------|--------|
| `maxDepth(1)`      | `3`                | `2`                  | `4`    |
| `maxDepth(2)`      | `2`                | `1`                  | `3`    |
| `maxDepth(3)`      | `0`                | `1`                  | `2`    |
| **Base Condition** | `0`                | `0`                  | `0`    |

---

#### **4. Sorting an Array Using Recursion**

**Problem Statement:** Sort an array in ascending order using recursion.

**Example:** Input: `[5,1,0,2]`  Output: `[0,1,2,5]`

```java
import java.util.*;
class Main {
    public static ArrayList<Integer> sort(ArrayList<Integer> arr) {
        if (arr.size() == 1) return arr; // Base Condition
        int temp = arr.remove(arr.size() - 1); // Hypothesis
        sort(arr);
        insert(arr, temp); // Induction
        return arr;
    }

    public static void insert(ArrayList<Integer> arr, int temp) {
        if (arr.size() == 0 || temp >= arr.get(arr.size() - 1)) {
            arr.add(temp); // Base Condition
            return;
        }
        int val = arr.remove(arr.size() - 1); // Hypothesis
        insert(arr, temp);
        arr.add(val); // Induction
    }
}
```

#### **Stack Visualization for Sorting:**

Input: `[5, 1, 0, 2]`

1. Break the problem into smaller inputs until `arr.size() == 1`.
2. Insert elements back in sorted order.

| Call Stack         | Action              | Array State         |
|--------------------|---------------------|---------------------|
| `sort([5, 1, 0, 2])` | Remove `2`         | `[5, 1, 0]`         |
| `sort([5, 1, 0])`   | Remove `0`         | `[5, 1]`           |
| `sort([5, 1])`      | Remove `1`         | `[5]`              |
| **Base Condition** | Add back elements   | `[0, 1, 2, 5]`     |

---

### **Scenarios Where Smaller Input Isn’t Directly Used**

- **Traversal Problems:** Recursion is used only for breaking down or visiting parts of the problem.
- **Examples:**
  - Preorder/Traversal of Binary Trees.
  - Printing Patterns.

---

### **Key Takeaways for Revision**

1. **Always define the smallest valid input for Base Condition.**
2. **Use Hypothesis to break the problem into smaller sub-problems.**
3. **Induction builds the solution by combining results from smaller inputs.**
4. **Visualization of the call stack helps in understanding recursion.**

