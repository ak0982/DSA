Here is the beautified version of the provided content for a GitHub README.md file with added color and emojis, formatted to make it more visually appealing:

```markdown
# 🧑‍💻 **Template to Solve Substring Problems**

## 🚀 Code Template for Finding Substrings:

```cpp
int findSubstring(string s) {
    vector<int> map(128, 0); // 🗺️ ASCII size for character frequency map
    int counter = 0;         // 🔢 Counter to track validity
    int begin = 0, end = 0;  // ⏳ Two pointers: begin for shrinking, end for expanding
    int d = INT_MAX;         // 💎 Initialize the length for minimum substring

    // Step 1: Initialize the hash map
    // 📝 Example: Assume we want to find a substring with exactly `t` characters
    // Add your initialization logic here based on the problem
    for (char c : s) {
        map[c]++; // 🔠 Increase frequency of a character (depends on problem requirements)
    }

    // Step 2: Expand the window using the `end` pointer
    while (end < s.size()) {
        char endChar = s[end++]; // ➡️ Add character at `end` to the window

        if (map[endChar]-- > 0) { 
            counter++; // ✅ If the character is required (positive in map), decrease the counter
        }

        // Step 3: Shrink the window using the `begin` pointer
        while (counter == /* some condition */) { // 🎯 When the window is valid
            // Update the result `d` for the smallest substring
            if (end - begin < d) {
                d = end - begin; // ⏱️ Update minimum length
            }

            // 🪞 Remove character at `begin` from the window
            char beginChar = s[begin++];
            if (map[beginChar]++ == 0) {
                counter--; // 🔴 If removing makes the window invalid, increase the counter
            }
        }
    }

    return d == INT_MAX ? -1 : d; // Return the result
}
```

---

## 📊 **Substrings - Minimum & Maximum**:

### 🔑 **Minimum Substring**:
**Goal:** Find the smallest substring that satisfies the constraints.

**When to Update:** Inside the inner while loop, because as soon as the substring becomes valid, you want to check if it's the smallest valid substring.

**Why:**
- The inner loop shrinks the window.
- By the time the inner loop executes, the window is valid. If it becomes invalid during shrinking, you'll stop shrinking.

```cpp
while (counter == 0) { // Window is valid
    if (end - begin < d) d = end - begin; // ⬇️ Update minimum length
    if (map[s[begin++]]++ == 0) counter++; // Shrink the window
}
```

---

### 🏆 **Maximum Substring**:
**Goal:** Find the largest substring that satisfies the constraints.

**When to Update:** After the inner while loop, because shrinking the window is necessary to make it valid, and you need to ensure you're updating the maximum length only when the window is valid.

**Why:**
- During the inner loop, you are restoring validity by shrinking the window.
- The valid substring is found after the inner loop ends.

```cpp
while (end < s.size()) { // Expand the window
    if (map[s[end++]]++ > 0) counter++; // Expand the window

    while (counter > some_limit) { // Shrink to restore validity
        if (map[s[begin++]]-- == 1) counter--; // Shrink the window
    }

    d = max(d, end - begin); // 🔝 Update maximum length
}
```

---

## 🧩 **Key Difference**:

- **Minimum Substring:**
  - Update result **inside** the inner loop to capture the smallest valid substring while shrinking.
  
- **Maximum Substring:**
  - Update result **outside** the inner loop to ensure you capture the largest valid substring after restoring validity.

---

## 🧭 **Analogy**:
- **For minimum:** You check every step you take (inside the loop) to ensure you're taking the shortest route.
- **For maximum:** You wait until you've completed the route (outside the loop) to ensure you've covered the longest distance without breaking any rules.

---

## 📝 **Problem 1: Longest Substring with At Most Two Distinct Characters**

**Problem Statement:**  
Given a string `s`, find the length of the longest substring that contains at most two distinct characters.

```cpp
int lengthOfLongestSubstringTwoDistinct(string s) {
    vector<int> map(128, 0); // A frequency map for all possible characters (ASCII 0-127)
    int counter = 0; // Number of distinct characters in the current window
    int begin = 0, end = 0; // Two pointers defining the sliding window
    int d = 0; // The length of the longest substring

    while (end < s.size()) {
        // Expand the window by adding the current character
        if (map[s[end++]]++ == 0) counter++; // Increment counter if this is a new character

        // Shrink the window if we have more than 2 distinct characters
        while (counter > 2) {
            if (map[s[begin++]]-- == 1) counter--; // Reduce the frequency of the character and decrement counter if it becomes 0
        }

        // Update the maximum length
        d = max(d, end - begin);
    }

    return d;
}
```

---

## 🧩 **Problem 2: Longest Substring Without Repeating Characters**

**Problem Statement:**  
Given a string `s`, find the length of the longest substring that contains no repeating characters.

```cpp
int lengthOfLongestSubstring(string s) {
    vector<int> map(128, 0);   // Initialize a map to store character frequencies
    int counter = 0, begin = 0, end = 0, d = 0; 
    
    while (end < s.size()) {
        if (map[s[end++]]++ > 0) counter++;  // Character at 'end' is already in the substring, increment counter
        while (counter > 0) {
            if (map[s[begin++]]-- > 1) counter--;  // Shrink the window and adjust counter if a character repeats
        }
        d = max(d, end - begin);  // Update the length of the longest substring without repeating characters
    }
    return d;
}
```

---

## 💡 **Some Other Input:**

Thanks @zjh08177 for this great idea! 💡 Let me explain this algorithm:

1. **Use two pointers:** `start` and `end` to represent a window.
2. **Move `end`** to find a valid window.
3. When a valid window is found, move `start` to find a smaller window.

To check if a window is valid, we use a map to store `(char, count)` for chars in `t`. And use `counter` for the number of chars of `t` to be found in `s`. The key part is `m[s[end]]--;`. We decrease count for each char in `s`. If it does not exist in `t`, the count will be negative.

---

## 📝 **Optimized Code:**

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

**Performance:**
- The original code costs **76ms**. If we replace `unordered_map` with `vector<int> m(128, 0);`, it costs **12ms**.

---

🌟 **End of Documentation!** 🌟
```
