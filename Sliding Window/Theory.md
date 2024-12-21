## 🌟 **The Sliding Window Technique** 🌟  

The **Sliding Window Technique** is a powerful problem-solving method, often used for optimizing array or sequence traversal.

### ✨ **Applications of Sliding Window**  

1. 🎯 **Running Average**:  
   Efficiently calculate the average of a fixed-size window as new elements stream in.  

2. 🔗 **Formulating Adjacent Pairs**:  
   Easily access and operate on neighboring elements in ordered data structures.  

3. 🎯 **Target Value Identification**:  
   Find specific values or subarrays by dynamically adjusting window size.  

4. 🔎 **Optimal Sequences**:  
   Identify the **longest, shortest**, or most optimal sequence satisfying a condition with minimal iteration.

---

### 💡 **Core Concept**  
The technique transforms nested loops into a **single loop**, reducing **time complexity** from `O(n²)` to `O(n)` by maintaining a subarray of fixed size, updated dynamically.  

---

### 🛠️ **Techniques Used**  

- 🧩 **Hashing**: Quickly look up elements in the window.  
- 🪡 **Two Pointers**: Track window's start and end efficiently.  
- ⚡ **Optimization**: Combine hashing and pointers for performance boosts.  

---

### 🔍 **Fixed Window Example**  
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, k;
    cin >> n >> k;

    vector<int> v(n, 0);
    for (int i = 0; i < n; i++)
        cin >> v[i];

    int i = 0, j = 0, sum = 0;

    while (j < n) {
        if (j - i + 1 < k) {
            sum += v[j++];
        } else {
            sum += v[j];
            cout << sum << endl;
            sum -= v[i++];
            j++;
        }
    }
}
```

---

### 🔄 **Variable Window Example**  

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int i = 0, j = 0, ans = 0;
        map<char, int> m;

        while (j < s.size()) {
            m[s[j]]++;
            int windowSize = j - i + 1;

            if (m.size() == windowSize) {
                ans = max(ans, windowSize);
                j++;
            } else {
                while (m.size() < windowSize) {
                    m[s[i]]--;
                    if (m[s[i]] == 0) m.erase(s[i]);
                    i++;
                }
                j++;
            }
        }
        return ans;
    }
};
```

---

### 📌 **Common Questions**  

- 🔵 Fixed Window:  
  - Substrings with distinct characters  
  - Maximum average subarray  
  - Find all anagrams in a string  

- 🔴 Variable Window:  
  - Longest substring without repeating characters  
  - Sliding Window Maximum  
  - Minimum Window Substring  

---

### 🚀 **Master Two Pointer Problems**  

1. **Run from both ends**:  
   - 2 Sum Problem  
   - Trapping Water  
   - Reverse Array  

2. **Slow & Fast Pointers**:  
   - Linked List Operations  
   - Cycle Detection  

---

For **more patterns and examples**, dive into:  
🌐 [Two Pointer Techniques](#)  
🌐 [Bit Manipulation Techniques](#)


# 🌟 The Sliding Window Technique 🌟

The **Sliding Window Technique** is a problem-solving technique that is used to:

1. **🧮 Running Average**: Use a sliding window to efficiently calculate the average of a fixed-size window as new elements arrive in a stream of data.  
2. **🔗 Formulating Adjacent Pairs**: Sliding windows are useful when you need to process adjacent pairs of elements in an ordered data structure, allowing you to easily access and operate on neighboring elements.  
3. **🎯 Target Value Identification**: When you want to find a specific target value or combination of values in an array, a sliding window can help by adjusting the window size and efficiently searching for the desired value or subarrays that meet specific criteria.  
4. **📏 Longest/Shortest/Most Optimal Sequence**: Sliding windows are handy when you need to find the longest, shortest, or most optimal sequence that satisfies a given condition in a collection. By sliding a window through the collection and tracking relevant information within it, you can identify the desired sequence more efficiently than scanning the entire collection.  

The main idea behind the sliding window technique is to convert two nested loops into a single loop.  
This is done by maintaining a sliding window, which is a subarray of the original array that is of a fixed size. The algorithm then iterates over the original array, updating the sliding window as it goes. This allows the algorithm to keep track of a contiguous sequence of elements in the original array, without having to iterate over the entire array multiple times.

Both fixed and variable window sliding window problems can use the techniques of **hashing**, **two pointers**, and **sliding window optimization**.  
- **🔑 Hashing**: A common technique for tracking the elements in a sliding window. This is because a hash table can quickly and efficiently look up the presence of an element in the window.  
- **🔀 Two Pointers**: Another common technique for tracking the elements in a sliding window. This is because two pointers can easily track the start and end of the window.  
- **⚡ Sliding Window Optimization**: A technique that combines hashing and two pointers to improve the performance of the sliding window algorithm.

The choice of technique for solving a sliding window problem depends on the specific problem and the constraints of the problem. For example, if the sliding window is small, then hashing may be a good choice. However, if the sliding window is large, then two pointers may be a better choice.  

## 🖼️ Identifying Fixed and Variable Size Windows

### 🛠️ Fixed Window:
In a fixed window problem, we have a predefined window size that remains constant throughout the problem-solving process.

**Template for Fixed Window**:
```cpp
fixed_window() {
    int low = 0, high = 0, windowsize = k;
    while (i < sizeofarray) {
        if (high - low + 1 < windowsize) {
            high++; // Expand the window
        } else {
            // Process the window and adjust
        }
    }
}
```

**Example**:  
Given an array `arr[]` and an integer `K`, calculate the sum of all subarrays of size `K`.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, k;
    cin >> n >> k;

    vector<int> v(n, 0);
    for (int i = 0; i < n; i++)
        cin >> v[i];

    int i = 0, j = 0;
    int sum = 0;

    while (j < n) {
        if (j - i + 1 < k) {
            sum += v[j];
            j++;
        } else {
            sum += v[j];
            cout << sum << endl;
            sum -= v[i];
            i++, j++;
        }
    }
}
```

### 🪄 Variable Window:
In a variable window problem, the window size can change dynamically based on certain conditions.

**Template for Variable Window**:
```cpp
variable_window() {
    int start = 0, end = 0;
    while (end < n) {
        // Process the window
        if (end - start + 1 < k) {
            end++; // Expand the window
        } else if (end - start + 1 == k) {
            // Process the window
            end++;
        } else {
            while (end - start + 1 > k) {
                start++; // Reduce the window
            }
            end++;
        }
    }
}
```

**Example**:  
Longest substring without repeating characters:
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int i = 0, j = 0, ans = 0;
        map<char, int> m;

        while (j < s.size()) {
            m[s[j]]++;
            int windowSize = j - i + 1;

            if (m.size() == windowSize) {
                ans = max(ans, windowSize);
                j++;
            } else {
                while (m.size() < windowSize) {
                    m[s[i]]--;
                    if (m[s[i]] == 0) m.erase(s[i]);
                    i++;
                    windowSize = j - i + 1;
                }
                ans = max(ans, windowSize);
                j++;
            }
        }
        return ans;
    }
};
```

## 🤔 Questions on Fixed Window Size

- Substrings-of-size-three-with-distinct-characters
- Maximum-number-of-vowels-in-a-substring-of-given-length
- Find-all-anagrams-in-a-string
- Maximum Average Subarray I

## 🔄 Questions on Variable Window Size

- Longest Substring Without Repeating Characters
- Sliding Window Maximum
- Minimum Window Substring
- Minimum Size Subarray Sum

## ⚙️ Two Pointer Patterns
If you want to master Two pointer techniques, focus on these patterns:
1. **Running from both ends**  
2. **Slow & Fast Pointers**  
3. **Running from beginning of 2 arrays / Merging 2 arrays**  
4. **Split & Merge of an array / Divide & Conquer**  

[Read more about Two Pointer Problems](https://example.com)
``` 

This markdown includes colorful text, emojis, and is ready for use in a GitHub README.md file as requested.
