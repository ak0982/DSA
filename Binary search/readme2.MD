# 🌟 <span style="color:gold">Ultimate Binary Search Guide</span> 🌟

## 📖 <span style="color:skyblue">Introduction</span>
<span style="color:lime">Binary Search</span> is a powerful algorithm that divides the search space into two halves, discarding the half that does not contain the target. This reduces the search time complexity from **<span style="color:purple">O(n)</span>** to **<span style="color:purple">O(log n)</span>**. However, implementing it correctly can be challenging due to:

- Deciding the correct loop condition (`<span style="color:orange">left < right</span>` vs. `<span style="color:orange">left <= right</span>`).
- Proper initialization of boundary variables (`<span style="color:orange">left</span>` and `<span style="color:orange">right</span>`).
- Choosing appropriate updates (`<span style="color:orange">left = mid</span>`, `<span style="color:orange">left = mid + 1</span>`, etc.).

<span style="color:lime">Binary Search</span> extends beyond simple "find an element in a sorted array" scenarios to more complex problems. Let's explore its power through a generalized template and practical examples.

---

## 🚀 <span style="color:skyblue">Generalized Binary Search Template</span>

### Problem Statement:
Minimize **<span style="color:orange">k</span>** such that **<span style="color:orange">condition(k)</span>** is true.

```cpp
int binarySearch(vector<int>& array) {
    auto condition = [&](int value) -> bool {
        // Define your condition here
    };

    int left = 0, right = array.size(); // Adjust based on the problem
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (condition(mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return left; // Minimum `k` satisfying the condition
}
```

### Key Steps:
1. **<span style="color:lime">Initialize boundaries</span>** to include all possible values.
2. **<span style="color:lime">Determine the return value</span>** (usually `<span style="color:orange">left</span>` after the loop).
3. **<span style="color:lime">Design the condition function</span>** based on problem constraints.

**<span style="color:gold">Insight:</span>** This template handles most binary search problems by focusing on initialization, return value, and condition function design.

---

## 🛠️ <span style="color:skyblue">Basic Applications</span>

### Example 1: <span style="color:gold">First Bad Version</span> (Easy)
**<span style="color:lime">Problem:</span>** Find the first bad version among `<span style="color:orange">n</span>` versions using an API `<span style="color:orange">isBadVersion</span>`.

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
**<span style="color:gold">Summary:</span>** Using the API, we search for the smallest version where `<span style="color:orange">isBadVersion(k)</span>` is true. The template adapts perfectly.

---

### Example 2: <span style="color:gold">Square Root</span> (Easy)
**<span style="color:lime">Problem:</span>** Compute the integer square root of a non-negative integer `<span style="color:orange">x</span>`.

```cpp
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
```
**<span style="color:gold">Summary:</span>** This implementation finds the largest integer `<span style="color:orange">k</span>` such that `<span style="color:orange">k^2 <= x</span>`, leveraging binary search over `[<span style="color:orange">0, x+1</span>]`.

---

### Example 3: <span style="color:gold">Search Insert Position</span> (Easy)
**<span style="color:lime">Problem:</span>** Return the index of `<span style="color:orange">target</span>` in a sorted array or where it would be inserted.

```cpp
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
```
**<span style="color:gold">Summary:</span>** Finds the position to insert `<span style="color:orange">target</span>` by searching for the smallest index `<span style="color:orange">k</span>` where `<span style="color:orange">nums[k] >= target</span>`.

---

## ⚙️ <span style="color:skyblue">Advanced Applications</span>

### Example 1: <span style="color:gold">Capacity to Ship Packages Within D Days</span> (Medium)
**<span style="color:lime">Problem:</span>** Minimize the ship's capacity to deliver packages within `<span style="color:orange">D</span>` days.

```cpp
int shipWithinDays(vector<int>& weights, int D) {
    auto feasible = [&](int capacity) -> bool {
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
**<span style="color:gold">Summary:</span>** This solution determines the minimal ship capacity by iterating over possible capacities using binary search.

---

### Example 2: <span style="color:gold">Koko Eating Bananas</span> (Medium)
**<span style="color:lime">Problem:</span>** Determine the minimum eating speed for Koko to finish bananas in `<span style="color:orange">H</span>` hours.

```cpp
int minEatingSpeed(vector<int>& piles, int H) {
    auto feasible = [&](int speed) -> bool {
        int hours = 0;
        for (int pile : piles) {
            hours += (pile + speed - 1) / speed;
        }
        return hours <= H;
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
**<span style="color:gold">Summary:</span>** Finds the minimal eating speed `<span style="color:orange">k</span>` such that all bananas are consumed within `<span style="color:orange">H</span>` hours using binary search.

---

## 💡 <span style="color:skyblue">Insights & Summary</span>
1. **<span style="color:lime">Monotonicity:</span>** Binary search works best with problems exhibiting monotonic behavior.
2. **<span style="color:lime">Template Power:</span>** A reusable template simplifies implementation across varied problems.
3. **<span style="color:lime">Boundary Initialization:</span>** Proper initialization avoids edge case errors.
4. **<span style="color:lime">Practice:</span>** Regular practice is key to mastering condition function design and application.

Master these principles, and binary search becomes a versatile tool in your problem-solving arsenal.

---

## 📚 <span style="color:skyblue">References</span>
- [<span style="color:lime">LeetCode Discuss</span>](https://leetcode.com/discuss/)
- [<span style="color:lime">Binary Search Handbook</span>](https://leetcode.com/problems/)
