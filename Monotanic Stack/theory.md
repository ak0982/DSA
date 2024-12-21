# 🌟 **Important Conclusion** 🌟

### 🔹 **Nearest Smaller or Larger Element Tips**:

- **Nearest Smaller to Left** → 🟩 *Use an Increasing Stack*  
  📌 *Start putting the elements from the **right***  
- **Nearest Larger to Left** → 🟦 *Use a Decreasing Stack*  
  📌 *Start putting the elements from the **right***  
- **Nearest Smaller to Right** → 🟨 *Use an Increasing Stack*  
  📌 *Start putting the elements from the **left***  
- **Nearest Larger to Right** → 🟥 *Use a Decreasing Stack*  
  📌 *Start putting the elements from the **left***

---

### 📊 **Detailed Problem Breakdown**

| 🛠 **Problem**      | 🔄 **Stack Type**            | 🔢 **Operator in while loop** | 📝 **Assignment Position**  |
|---------------------|------------------------------|------------------------------|-----------------------------|
| **Next Greater**    | Decreasing (*equal allowed*) | `stackTop < current`         | Inside while loop           |
| **Previous Greater**| Decreasing (*strict*)        | `stackTop <= current`        | Outside while loop          |
| **Next Smaller**    | Increasing (*equal allowed*) | `stackTop > current`         | Inside while loop           |
| **Previous Smaller**| Increasing (*strict*)        | `stackTop >= current`        | Outside while loop          |

---

### 💡 **Insights**:

1. Using **increasing** or **decreasing stacks** helps optimize the search for nearest smaller or larger elements.
2. **Assignment position** depends on whether strict inequality is applied, ensuring accuracy during computation.

# 🌟 **What is a Monotonic Stack?**

A **monotonic stack** is a specialized stack where the elements are either **monotonically increasing** or **monotonically decreasing**. It combines the qualities of a typical stack while ensuring that its elements maintain a consistent order.

---

### 🔹 **Features of a Monotonic Stack:**

- 🛠 **Efficient for range queries** in array-based problems.
- 🎯 Identifies **minima/maxima** elements effectively.
- 🗑 Once an element is **popped**, it will never be utilized again.
- 📚 Typically solves **previous/next smaller/larger problems** by maintaining monotonicity while pushing and popping elements.

---

### 📖 **Understanding Monotonicity**:

In mathematics, a function is said to be **monotonic** if:
- As 𝑥 increases, 𝑦 increases (monotonically **increasing**).
- As 𝑥 increases, 𝑦 decreases (monotonically **decreasing**).

#### Examples:
- **Monotonically Increasing Function:** 𝑦 = 2𝑥 + 5  
- **Monotonically Decreasing Function:** 𝑦 = −(2𝑥)

Similarly, a stack is called a **monotonic stack** if all elements from the bottom to the top of the stack are either in **increasing** or **decreasing** order.

---

### 🔄 **Types of Monotonic Stacks**:

#### 1️⃣ **Monotonic Increasing Stack**
- **Definition:** Elements are in **increasing order** from the bottom to the top of the stack.  
  **Example:** `1, 3, 10, 15, 17`

#### **How to Achieve Monotonic Increasing Stack?**

To create a Monotonic Increasing Stack:
1. Start with an **empty stack**.
2. Iterate through elements in a sequence.
3. Remove elements from the stack as long as they are **smaller** than the current element.
4. Push the current element onto the stack.

This process ensures the stack maintains a **strictly increasing order** from bottom to top.

#### 2️⃣ **Monotonic Decreasing Stack**
- **Definition:** Elements are in **decreasing order** from the bottom to the top of the stack.

## Steps to Implement

### Understanding the Idea

#### Illustration:
- **Array**: `Arr[] = {1, 4, 5, 3, 12, 10}`
- Iteration Steps:
  - For `i = 0`: `stk = {1}`
  - For `i = 1`: `stk = {1, 4}`
  - For `i = 2`: `stk = {1, 4, 5}`
  - For `i = 3`: `stk = {1, 3}` *(pop 4 and 5 as 4 > 3 and 5 > 3)*
  - For `i = 4`: `stk = {1, 3, 12}`
  - For `i = 5`: `stk = {1, 3, 10}` *(pop 12 as 12 > 10)*

---

### C++ Code for Monotonic Increasing Stack

```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to build Monotonic increasing stack
void increasingStack(int arr[], int N) {
    // Initialise stack
    stack<int> stk;

    for (int i = 0; i < N; i++) {
        // Either stack is empty or all bigger nums are popped off
        while (stk.size() > 0 && stk.top() > arr[i]) {
            stk.pop();
        }
        stk.push(arr[i]);
    }

    int N2 = stk.size();
    int ans[N2] = {0};
    int j = N2 - 1;

    // Empty Stack
    while (!stk.empty()) {
        ans[j] = stk.top();
        stk.pop();
        j--;
    }

    // Display the results
    cout << "The Array: ";
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    cout << "The Stack: ";
    for (int i = 0; i < N2; i++) {
        cout << ans[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {1, 4, 5, 3, 12, 10};
    int N = sizeof(arr) / sizeof(arr[0]);
    increasingStack(arr, N);
    return 0;
}
```

#### Output:
```
The Array: 1 4 5 3 12 10
The Stack: 1 3 10
```

---

### Complexity Analysis:
- **Time Complexity**: \(O(N)\)
- **Auxiliary Space**: \(O(N)\)

---

### Monotonic Decreasing Stack
A stack is monotonically decreasing if its elements are in decreasing order from bottom to top.

#### Example:
- **Array**: `arr[] = {15, 17, 12, 13, 14, 10}`
- Iteration Steps:
  - For `i = 0`: `stk = {15}`
  - For `i = 1`: `stk = {17}` *(pop 15 as 15 < 17)*
  - For `i = 2`: `stk = {17, 12}`
  - For `i = 3`: `stk = {17, 13}` *(pop 12 as 12 < 13)*
  - For `i = 4`: `stk = {17, 14}` *(pop 13 as 13 < 14)*
  - For `i = 5`: `stk = {17, 14, 10}`

---

### C++ Code for Monotonic Decreasing Stack

```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to build Monotonic decreasing stack
void decreasingStack(int arr[], int N) {
    // Initialise stack
    stack<int> stk;

    for (int i = 0; i < N; i++) {
        // Either stack empty or all smaller nums are popped off
        while (stk.size() > 0 && stk.top() < arr[i]) {
            stk.pop();
        }
        stk.push(arr[i]);
    }

    int N2 = stk.size();
    int ans[N2] = {0};
    int j = N2 - 1;

    // Empty Stack
    while (!stk.empty()) {
        ans[j] = stk.top();
        stk.pop();
        j--;
    }

    // Display the results
    cout << "The Array: ";
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    cout << "The Stack: ";
    for (int i = 0; i < N2; i++) {
        cout << ans[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {15, 17, 12, 13, 14, 10};
    int N = sizeof(arr) / sizeof(arr[0]);
    decreasingStack(arr, N);
    return 0;
}
```

#### Output:
```
The Array: 15 17 12 13 14 10
The Stack: 17 14 10
```

---

## Applications of Monotonic Stack:
1. **Next Greater Element (NGE)**
2. **Next Smaller Element**
3. **Previous Greater Element**
4. **Previous Smaller Element**
5. **Maximum Area Under Histogram**
6. **Stock Span Problem**

---

## Key Points to Identify Monotonic Stack Problems:
- Look for **Nearest Greater/Smaller Element** queries.
- Problems requiring **Linear Time Constraints**.
- Scenarios involving **Immediate Neighbors** or **Range Queries**.
- Use cases like **Trapping Rainwater**, **Histogram Problems**, etc.

---

## Advantages:
- Efficient in maintaining **range maxima/minima**.
- Provides linear time solutions for many problems.

## Disadvantages:
- Increases space complexity by \(O(N)\).
- Requires careful handling during implementation.



# Monotonic Stack

A **Monotonic Stack** is a data structure where elements are stored in a strictly increasing or decreasing order. This ensures efficient management of elements based on specific conditions, especially for problems requiring range maxima/minima queries.

---

## **Understanding Monotonic Stack**

### Key Features:
- A stack can be **monotonically increasing** or **monotonically decreasing**.
- **Monotonically Increasing Stack**:
  - Push elements in increasing order.
  - Pop smaller elements before pushing a larger one.
- **Monotonically Decreasing Stack**:
  - Push elements in decreasing order.
  - Pop larger elements before pushing a smaller one.

---

## **C++ Code Implementation**

### Monotonic Increasing Stack:
```cpp
#include <bits/stdc++.h>
using namespace std;

void increasingStack(int arr[], int N) {
    stack<int> stk;

    for (int i = 0; i < N; i++) {
        while (!stk.empty() && stk.top() > arr[i]) {
            stk.pop();
        }
        stk.push(arr[i]);
    }

    vector<int> result;
    while (!stk.empty()) {
        result.push_back(stk.top());
        stk.pop();
    }
    reverse(result.begin(), result.end());

    cout << "Monotonic Increasing Stack: ";
    for (int num : result) {
        cout << num << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {1, 4, 5, 3, 12, 10};
    int N = sizeof(arr) / sizeof(arr[0]);
    increasingStack(arr, N);
    return 0;
}
```

#### **Output**:
```
Monotonic Increasing Stack: 1 3 10
```

### Monotonic Decreasing Stack:
```cpp
#include <bits/stdc++.h>
using namespace std;

void decreasingStack(int arr[], int N) {
    stack<int> stk;

    for (int i = 0; i < N; i++) {
        while (!stk.empty() && stk.top() < arr[i]) {
            stk.pop();
        }
        stk.push(arr[i]);
    }

    vector<int> result;
    while (!stk.empty()) {
        result.push_back(stk.top());
        stk.pop();
    }
    reverse(result.begin(), result.end());

    cout << "Monotonic Decreasing Stack: ";
    for (int num : result) {
        cout << num << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {15, 17, 12, 13, 14, 10};
    int N = sizeof(arr) / sizeof(arr[0]);
    decreasingStack(arr, N);
    return 0;
}
```

#### **Output**:
```
Monotonic Decreasing Stack: 17 14 10
```

---

## **Applications of Monotonic Stack**

- **Next Greater Element (NGE)**
- **Next Smaller Element**
- **Previous Greater Element**
- **Previous Smaller Element**
- **Maximum Area Under Histogram**
- **Stock Span Problem**

---

## **Advantages & Disadvantages**

### Advantages:
- Maintains range maxima/minima efficiently.
- Reduces time complexity to \(O(N)\).

### Disadvantages:
- Increases space complexity to \(O(N)\).
- Requires careful handling to avoid logical errors.

---

## **Key Identification Points**

- Problems involving **Nearest Greater/Smaller Elements**.
- Scenarios demanding **Linear Time Solutions**.
- Use cases such as **Trapping Rainwater**, **Histogram Problems**, etc.

