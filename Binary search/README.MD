## ✨ **Intro**

Binary Search is a conceptually simple yet powerful algorithm. At its core, it splits the search space into two halves, keeping the half likely to contain the target while discarding the other. This process reduces the search space exponentially, from linear Ω(n) to logarithmic Ω(log n). However, writing a bug-free binary search implementation is often challenging.

### Common Challenges

1. **Loop Exit Condition**: Should it be `left < right` or `left <= right`?
2. **Boundary Initialization**: How to set `left` and `right`?
3. **Boundary Updates**: Choosing between `left = mid`, `left = mid + 1`, `right = mid`, or `right = mid - 1`.

Binary search is not limited to simple problems like "find a specific value in a sorted array." It can tackle more complex scenarios with a systematic approach.

After extensive practice on platforms like LeetCode, a powerful binary search template has emerged, enabling efficient solutions for many "Hard" problems with slight modifications. This guide shares the template and practical tips to ensure you master its application and logic.

---

## ✨ **Most Generalized Binary Search**

### General Problem Statement
Minimize `k` such that `condition(k)` is `True`.

### Generalized Template in C++

```cpp
#include <vector>
#include <functional>

int binarySearch(const std::vector<int>& array, std::function<bool(int)> condition) {
    int left = 0, right = array.size() - 1; // Define boundaries based on the problem
    while (left < right) {
        int mid = left + (right - left) / 2; // Avoid potential overflow
        if (condition(mid)) {
            right = mid; // Narrow down the search space
        } else {
            left = mid + 1;
        }
    }
    return left; // Minimal `k` satisfying the condition
}
```

### Key Components of the Template

1. **Boundary Initialization**: Define `left` and `right` to include all potential values.
2. **Return Value**: After the loop, `left` is the minimal `k` satisfying the condition.
3. **Condition Function**: The heart of binary search; requires practice to design effectively.

### Advantages
- **Reusability**: Modify three parts for most problems:
  - Boundary initialization (`left`, `right`)
  - Return value (`left` or `left - 1`)
  - Condition function.
- **Reduced Bugs**: Simplifies handling of corner cases.

---

## ✨ **Insights and Summary**

### Why Use This Template?
- It abstracts the common pitfalls of binary search implementation.
- Offers a systematic approach to solve a wide range of problems beyond searching sorted arrays.

### Real-Life Applications
- **Find Target in Array**: Locate a specific value in a sorted array.
- **Threshold Problems**: Find the smallest/largest value meeting a condition.
- **Optimization Problems**: Binary search over a range of feasible solutions.

By mastering this template, binary search will become your go-to tool for efficient problem-solving, transforming frustration into confidence.


---

# 🌟 Basic Application

## 🚀 278. **First Bad Version** [Easy]

**Problem:**  
You are a product manager leading a team to develop a new product. Each version is based on the previous one, so if one version is bad, all versions after it are also bad. You are given an API `bool isBadVersion(version)` that returns whether a version is bad. The task is to find the first bad version.

### Example:

```markdown
Given n = 5, and version = 4 is the first bad version.

call isBadVersion(3) -> false  
call isBadVersion(5) -> true  
call isBadVersion(4) -> true  
```

Then, **4** is the first bad version.

### Solution (C++):

```cpp
class Solution {
public:
    int firstBadVersion(int n) {
        int left = 1, right = n;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (isBadVersion(mid)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
};
```

### Insights:
- The problem is solved using **binary search**.
- The key observation is that all versions after a bad version are also bad, so we can narrow down the search range effectively.
- **Time Complexity:** O(log n), where `n` is the number of versions.

---

## 🧑‍🔬 69. **Sqrt(x)** [Easy]

**Problem:**  
Implement `int sqrt(int x)`. Compute and return the square root of `x`, where `x` is a non-negative integer. The result should be truncated to an integer.

### Example:

```markdown
Input: 4  
Output: 2

Input: 8  
Output: 2
```

### Solution (C++):

```cpp
class Solution {
public:
    int mySqrt(int x) {
        int left = 0, right = x + 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (mid * mid > x) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left - 1;
    }
};
```

### Insights:
- This is a **binary search** problem where we need to find the largest integer `k` such that `k^2 <= x`.
- **Time Complexity:** O(log x), where `x` is the number for which we are calculating the square root.

---

## 🔍 35. **Search Insert Position** [Easy]

**Problem:**  
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be inserted in order. No duplicates are allowed.

### Example:

```markdown
Input: [1, 3, 5, 6], 5  
Output: 2

Input: [1, 3, 5, 6], 2  
Output: 1
```

### Solution (C++):

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left = 0, right = nums.size();
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] >= target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
};
```

### Insights:
- This problem is another **binary search** application to find the appropriate index where the target should be inserted.
- **Time Complexity:** O(log n), where `n` is the size of the array.

---

### 🔑 Summary:
- All three problems leverage **binary search** to efficiently find a solution.
- The first problem is about finding the first "bad version" in a sequence, while the other two deal with searching for an element or a position in a sorted array.
- Binary search allows us to reduce the time complexity to **O(log n)** in all these problems, making them much more efficient than a linear search approach.

---

Let me know if you need any further modifications or explanations!
