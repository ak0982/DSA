Here's the text you requested, beautified with colors and emojis for a GitHub README.md file:

```markdown
# 🧩 **Minimum Window Substring** 🧩

### 🔥 **Template to solve the problem** 🔥

```cpp
int findSubstring(string s) {
    vector<int> map(128, 0); // 📊 ASCII size for character frequency map
    int counter = 0;         // ⏱ Counter to track validity
    int begin = 0, end = 0;  // 🔄 Two pointers: begin for shrinking, end for expanding
    int d = INT_MAX;         // 📏 Initialize the length for minimum substring

    // Step 1: Initialize the hash map
    for (char c : s) {
        map[c]++; // 🗂 Increase frequency of a character (depends on problem requirements)
    }

    // Step 2: Expand the window using the `end` pointer
    while (end < s.size()) {
        char endChar = s[end++]; // ➡ Add character at `end` to the window

        if (map[endChar]-- > 0) { 
            counter++; // ✅ If the character is required (positive in map), decrease the counter
        }

        // Step 3: Shrink the window using the `begin` pointer
        while (counter == /* some condition */) { // 🔁 When the window is valid
            // Update the result `d` for the smallest substring
            if (end - begin < d) {
                d = end - begin; // 📏 Update the minimum length
            }

            // Remove character at `begin` from the window
            char beginChar = s[begin++];
            if (map[beginChar]++ == 0) {
                counter--; // ➖ If removing makes the window invalid, increase the counter
            }
        }
    }

    return d == INT_MAX ? -1 : d; // ✅ Return the result
}
```

### 🧠 **Explanation:**

#### **Minimum Substring**
- **Goal:** Find the smallest substring that satisfies the constraints.
- **When to Update:** Inside the inner while loop, because as soon as the substring becomes valid, you want to check if it's the smallest valid substring.
- **Why:** The inner loop shrinks the window, and by the time it executes, the window is valid. If it becomes invalid during shrinking, you'll stop shrinking.

#### **Maximum Substring**
- **Goal:** Find the largest substring that satisfies the constraints.
- **When to Update:** After the inner while loop, because shrinking the window is necessary to make it valid, and you need to ensure you're updating the maximum length only when the window is valid.
- **Why:** During the inner loop, you are restoring validity by shrinking the window. The valid substring is found after the inner loop ends.

---

### 🔄 **Key Differences:**

#### **Minimum Substring:**
- **Update result inside** the inner loop to capture the smallest valid substring while shrinking.

#### **Maximum Substring:**
- **Update result outside** the inner loop to ensure you capture the largest valid substring after restoring validity.

---

### 🌍 **Analogy:**
- **For minimum:** Think of checking every step you take on a path to ensure you're taking the shortest route. 🏃‍♂️💨
- **For maximum:** Wait until you've completed the route to ensure you've covered the longest distance without breaking any rules. 🛤️

---

### 📝 **Code Examples:**

#### **Problem 1: Longest Substring with At Most Two Distinct Characters** 💻

```cpp
int lengthOfLongestSubstringTwoDistinct(string s) {
    vector<int> map(128, 0); // 📊 A frequency map for all possible characters (ASCII 0-127)
    int counter = 0; // 🧮 Number of distinct characters in the current window
    int begin = 0, end = 0; // 🔄 Two pointers defining the sliding window
    int d = 0; // 📏 The length of the longest substring

    while (end < s.size()) {
        if (map[s[end++]]++ == 0) counter++; // 🔄 Increment counter if this is a new character

        while (counter > 2) { // ⬇ Shrink the window if we have more than 2 distinct characters
            if (map[s[begin++]]-- == 1) counter--; // 🧮 Reduce the frequency of the character
        }

        d = max(d, end - begin); // 📏 Update the maximum length
    }

    return d;
}
```

#### **Problem 2: Longest Substring Without Repeating Characters** 💡

```cpp
int lengthOfLongestSubstring(string s) {
    vector<int> map(128, 0); // 🗂 Initialize a map to store character frequencies
    int counter = 0, begin = 0, end = 0, d = 0; 
    
    while (end < s.size()) {
        if (map[s[end++]]++ > 0) counter++;  // 💥 Character at 'end' is already in the substring
        while (counter > 0) {
            if (map[s[begin++]]-- > 1) counter--;  // Shrink the window and adjust counter
        }
        d = max(d, end - begin);  // 📏 Update the length of the longest substring
    }
    return d;
}
```

---

### 💭 **Understanding the Algorithm:**
1. **Two pointers:** start and end to represent a window. 🔄
2. Move **end** to find a valid window. ⬇
3. When a valid window is found, move **start** to find a smaller window. 🔽

**Map Usage:** We use a map to store character counts and a counter to track the number of required characters. If a character doesn't exist in the target string, the count will be negative.

#### **Optimized Code:**
```cpp
string minWindow(string s, string t) {
    unordered_map<char, int> m;
    for (auto c : t) m[c]++;
    size_t start = 0, end = 0, counter = t.size(), minStart = 0, minLen = INT_MAX;
    size_t size = s.size();
    
    while (end < size) {
        if (m[s[end]] > 0) counter--;
        m[s[end]]--;
        end++;
        
        while (counter == 0) {
            if (end - start < minLen) {
                minStart = start;
                minLen = end - start;
            }
            m[s[start]]++;
            if (m[s[start]] > 0) counter++;
            start++;
        }
    }
    if (minLen != INT_MAX) return s.substr(minStart, minLen);
    return "";
}
```

---

### ⏱ **Performance Comparison:**
- The optimized version of the code executes in **12ms** instead of **76ms**. 🚀

---

This is a **beautifully styled** explanation and code for the **Minimum Window Substring** problem! 🎨 Let me know if you need further adjustments! 😃
