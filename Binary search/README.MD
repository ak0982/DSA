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

Here’s a colorful and formatted version of your text for a GitHub README.md file:

```markdown
# 🌟 Advanced Application of Binary Search

## 🔎 Overview

The problems above may appear to be simple, especially because they provide an array to be searched. At first glance, binary search seems like the obvious solution. However, in many real-world scenarios, the search space and the search target are not as readily available. In fact, it might take us some time to recognize that binary search is the optimal approach. We might initially consider dynamic programming or DFS, only to end up stuck after spending too much time on those approaches. So, **when can we use binary search?**

### ⚡ Insight:

If we can discover a **monotonicity** property in the problem, such as:  
**If condition(k) is true, then condition(k + 1) is also true**,  
then we can consider using **binary search**.

---

## 🛳️ Problem 1011: **Capacity to Ship Packages Within D Days** [Medium]

A conveyor belt has packages that must be shipped within D days. The `i-th` package has a weight of `weights[i]`. Each day, we load the ship with packages from the conveyor belt (in the order given by `weights`). The ship cannot load more weight than its maximum capacity.  
Return the **least weight capacity** of the ship that allows all packages to be shipped within D days.

### Example:

```text
Input: weights = [1,2,3,4,5,6,7,8,9,10], D = 5
Output: 15
Explanation:
- 1st day: 1, 2, 3, 4, 5
- 2nd day: 6, 7
- 3rd day: 8
- 4th day: 9
- 5th day: 10
```

### Key Insight:
- **Binary search** is not the obvious solution at first, but once we observe that if we can ship within `D` days with capacity `m`, then we can also do it with any capacity larger than `m`, binary search becomes a feasible approach.

```cpp
int shipWithinDays(vector<int>& weights, int D) {
    auto feasible = [&](int capacity) {
        int days = 1, total = 0;
        for (int weight : weights) {
            total += weight;
            if (total > capacity) {
                total = weight;
                days++;
                if (days > D) return false;
            }
        }
        return true;
    };
    
    int left = *max_element(weights.begin(), weights.end());
    int right = accumulate(weights.begin(), weights.end(), 0);
    
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (feasible(mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return left;
}
```

---

## 💡 Problem 410: **Split Array Largest Sum** [Hard]

Given an array of non-negative integers and an integer `m`, split the array into `m` non-empty subarrays such that the largest sum among these subarrays is minimized.

### Example:

```text
Input: nums = [7,2,5,10,8], m = 2
Output: 18
```

### Key Insight:
- **Binary search** can be used similarly to problem 1011, where we seek the minimal value satisfying a condition.
  
```cpp
int splitArray(vector<int>& nums, int m) {
    auto feasible = [&](int threshold) {
        int count = 1, total = 0;
        for (int num : nums) {
            total += num;
            if (total > threshold) {
                total = num;
                count++;
                if (count > m) return false;
            }
        }
        return true;
    };
    
    int left = *max_element(nums.begin(), nums.end());
    int right = accumulate(nums.begin(), nums.end(), 0);
    
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (feasible(mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return left;
}
```

---

## 🍌 Problem 875: **Koko Eating Bananas** [Medium]

Koko loves to eat bananas. There are `N` piles of bananas, and Koko has `H` hours to eat them. Each hour, she can eat `K` bananas from any pile. Koko wants to finish all bananas before the guards return.

### Example:

```text
Input: piles = [3,6,7,11], H = 8
Output: 4
```

### Key Insight:
- The solution is similar to previous problems, where we design a **feasible function** that checks if Koko can finish within `H` hours at a given speed.

```cpp
int minEatingSpeed(vector<int>& piles, int H) {
    auto feasible = [&](int speed) {
        int total = 0;
        for (int pile : piles) {
            total += (pile + speed - 1) / speed;
        }
        return total <= H;
    };
    
    int left = 1, right = *max_element(piles.begin(), piles.end());
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (feasible(mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return left;
}
```

---

## 🌸 Problem 1482: **Minimum Number of Days to Make m Bouquets** [Medium]

Given a garden where flowers bloom on different days, we need to make `m` bouquets using `k` adjacent flowers. The goal is to find the minimum number of days required to make these bouquets.

### Example:

```text
Input: bloomDay = [1,10,3,10,2], m = 3, k = 1
Output: 3
```

### Key Insight:
- **Monotonicity** plays a key role here: if we can make `m` bouquets after waiting for `d` days, we can certainly make them by waiting more days. This allows us to apply binary search to find the minimum day `d`.

```cpp
int minDays(vector<int>& bloomDay, int m, int k) {
    auto feasible = [&](int days) {
        int bouquets = 0, flowers = 0;
        for (int bloom : bloomDay) {
            if (bloom > days) flowers = 0;
            else {
                flowers++;
                bouquets += flowers / k;
                flowers %= k;
            }
        }
        return bouquets >= m;
    };
    
    int left = 1, right = *max_element(bloomDay.begin(), bloomDay.end());
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (feasible(mid)) right = mid;
        else left = mid + 1;
    }
    return left;
}
```

---

## 🧮 Problem 668: **Kth Smallest Number in Multiplication Table** [Hard]

Given an `m * n` multiplication table, we need to find the `k-th` smallest number.

### Example:

```text
Input: m = 3, n = 3, k = 5
Output: 3
```

### Key Insight:
- The **multiplication table** has a monotonic property: as we move through each row, the values are increasing. Thus, binary search can be used to efficiently find the `k-th` smallest number.

```cpp
int findKthNumber(int m, int n, int k) {
    auto enough = [&](int num) {
        int count = 0;
        for (int i = 1; i <= m; ++i) {
            count += min(num / i, n);
        }
        return count >= k;
    };
    
    int left = 1, right = m * n;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (enough(mid)) right = mid;
        else left = mid + 1;
    }
    return left;
}
```

---

## 🧠 Summary

The key takeaway from all of these problems is the power of **binary search** when you can identify **monotonicity** in the problem. By designing a **feasible function** and setting appropriate boundaries, we can use binary search to find the minimal or maximal values satisfying the condition.
