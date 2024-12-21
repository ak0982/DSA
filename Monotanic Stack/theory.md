Summery:

## 🌟 **Important Conclusions** 🌟

### **Nearest Elements and Stack Usage**

- **Nearest Smaller to Left**:
  - [34mUse an “Increasing Stack”[0m.
  - [32mStart putting the elements from the **right**.[0m

- **Nearest Larger to Left**:
  - [33mUse a “Decreasing Stack”[0m.
  - [35mStart putting the elements from the **right**.[0m

- **Nearest Smaller to Right**:
  - [34mUse an “Increasing Stack”[0m.
  - [32mStart putting the elements from the **left**.[0m

- **Nearest Larger to Right**:
  - [33mUse a “Decreasing Stack”[0m.
  - [35mStart putting the elements from the **left**.[0m

### **Stack Operation Summary Table**

| 🔍 **Problem**         | 🔎 **Stack Type**             | 🎮 **Operator in While Loop** | 🌒 **Assignment Position** |
|------------------|----------------------------|--------------------------|----------------------|
| [31m**Next Greater**[0m      | [33mDecreasing (Equal Allowed)[0m | [36m`stackTop < current`[0m | [32mInside While Loop[0m    |
| [31m**Previous Greater**[0m  | [33mDecreasing (Strict)[0m        | [36m`stackTop <= current`[0m | [32mOutside While Loop[0m   |
| [31m**Next Smaller**[0m      | [34mIncreasing (Equal Allowed)[0m | [36m`stackTop > current`[0m  | [32mInside While Loop[0m    |
| [31m**Previous Smaller**[0m  | [34mIncreasing (Strict)[0m        | [36m`stackTop >= current`[0m | [32mOutside While Loop[0m   |


What is a Monotonic Stack?
A monotonic stack is a stack whose elements are monotonically increasing or decreasing. It contains all qualities that a typical stack has and its elements are all monotonic decreasing or increasing.

Below are the features of a monotonic stack:

It is a range of queries in an array situation
The minima/maxima elements
When an element is popped from the monotonic stack, it will never be utilised again.
The monotonic stack problem is mainly the previous/next smaller/larger problem. It maintains monotonicity while popping elements when a new item is pushed into the stack.

Monotonic: It is a word for mathematics functions. A function y = f(x) is monotonically increasing or decreasing when it follows the below conditions: 
As x increases, y also increases always, then it’s a monotonically increasing function. 
As x increases, y decreases always, then it’s a monotonically decreasing function.
See the below examples:
y = 2x +5, it’s a monotonically increasing function.
y = -(2x), it’s a monotonically decreasing function.  
Similarly, A stack is called a monotonic stack if all the elements starting from the bottom of the stack are either in increasing or in decreasing order.
Types of Monotonic Stack:
There are 2 types of monotonic stacks:
Monotonic Increasing Stack
Monotonic Decreasing Stack
Monotonic Increasing Stack:
It is a stack in which the elements are in increasing order from the bottom to the top of the stack. 
Example: 1, 3, 10, 15, 17
How to achieve Monotonic Increasing Stack?
To create a Monotonic Increasing Stack, start with an empty stack, then, while iterating through elements in a sequence, keep removing elements from the stack as long as they are smaller than the current element, and push the current element onto the stack. This process ensures the stack maintains a strictly increasing order from bottom to top.
Steps to implement:
See the illustration below to understand the idea:
Consider an array Arr[] = {1, 4, 5, 3, 12, 10}
For i = 0: stk = {1}
For i = 1: stk = {1, 4}
For i = 2: stk = {1, 4, 5}
For i = 3: stk = {1, 3}  [pop 4 and 5 as 4 > 3 and 5 > 3]
For i = 4: stk = {1, 3, 12}
For i = 5: stk = {1, 3, 10} [pop 12 as 12 > 10] 
Below is the code for the above approach:
// C++ code to implement the approach

#include <bits/stdc++.h>
using namespace std;

// Function to build Monotonic
// increasing stack
void increasingStack(int arr[], int N)
{	// Initialise stack
	stack<int> stk;
	for (int i = 0; i < N; i++) {
		// Either stack is empty or
		// all bigger nums are popped off
		while (stk.size() > 0 && stk.top() > arr[i]) {
			stk.pop();
		}
		stk.push(arr[i]);
	}
	int N2 = stk.size();
	int ans[N2] = { 0 };
	int j = N2 - 1;
	// Empty Stack
	while (!stk.empty()) {
		ans[j] = stk.top();
		stk.pop();
		j--;
	}
	// Displaying the original array
	cout << "The Array: ";
	for (int i = 0; i < N; i++) {
		cout << arr[i] << " ";
	}
	cout << endl;
	// Displaying Monotonic increasing stack
	cout << "The Stack: ";
	for (int i = 0; i < N2; i++) {
		cout << ans[i] << " ";
	}
	cout << endl;
}
Output
The Array: 1 4 5 3 12 10 
The Stack: 1 3 10 


Time Complexity: O(N)
Auxiliary Space: O(N)
Monotonic Decreasing Stack:
A stack is monotonically decreasing if its elements are in decreasing order from the bottom to the top of the stack. 
Example: 17, 14, 10, 5, 1
How to achieve Monotonic Decreasing Stack?
To create a Monotonic Decreasing Stack, begin with an empty stack, then, while iterating through elements in a sequence, continuously remove elements from the stack as long as they are smaller than or equal to the current element, and finally, push the current element onto the stack. This process ensures the stack maintains a monotonic decreasing order from bottom to top.
Steps to implement:
As we need a monotonically decreasing stack, we should not have a bigger element on top of a smaller element.
So Iterate the elements of the list one by one:
Before pushing into the stack, POP all the elements till either of one condition fails:
Stack is not empty
Stack’s top is smaller than the element to be Inserted.
Then push the element into the stack.
See the below illustration for a better understanding:
Consider an array: arr[] = {15, 17, 12, 13, 14, 10}
For i = 0: stk = {15}
For i = 1: stk = {17} [pop 15 as 15 < 17]
For i = 2: stk = {17, 12}
For i = 3: stk = {17, 13}  [pop 12 as 12 < 13]
For i = 4: stk = {17, 14}  [pop 13 as 13 < 14]
For i = 5: stk = {17, 14, 10}
Below is the implementation of the above approach:
// C++ code to implement the approach

#include <bits/stdc++.h>
using namespace std;
// Function to find a Monotonic
// decreasing stack
void decreasingStack(int arr[], int N)
{
	// Initialising Stack
	stack<int> stk;
	for (int i = 0; i < N; i++) {
		// Either stack empty or
		// all smaller nums are popped off
		while (stk.size() > 0 && stk.top() < arr[i]) {
			stk.pop();
		}
		stk.push(arr[i]);
	}
	int N2 = stk.size();
	int ans[N2] = { 0 };
	int j = N2 - 1;
	// Empty stack
	while (!stk.empty()) {
		ans[j] = stk.top();
		stk.pop();
		j--;
	}
	// Displaying the original array
	cout << "The Array: ";
	for (int i = 0; i < N; i++) {
		cout << arr[i] << " ";
	}
	cout << endl;
	// Displaying Monotonic Decreasing Stack
	cout << "The Stack: ";
	for (int i = 0; i < N2; i++) {

		cout << ans[i] << " ";
	}
	cout << endl;
}
Output
The Array: 15 17 12 13 14 10 
The Stack: 17 14 10 

Time Complexity: O(N)
Auxiliary Space: O(N) 
Note that this implementation assumes that all elements in the input array are distinct. If there are duplicates, we need to modify the implementation to handle them correctly.
Applications of Monotonic Stack :
Monotonic stack is generally used to deal with a typical problem like Next Greater Element. NGE (Find the first value on the right that is greater than the element.
Also can be used for its varieties.
Next Smaller Element
Previous Greater Element
Previous Smaller Element
Also, we use it to get the greatest or smallest array or string by the given conditions (remaining size k/ no duplicate).
To understand the optimization power of monotonic stacks, let’s take this example problem: Minimum Cost Tree From Leaf Values. This problem can be solved in 3 different algorithm ways, out of which the monotonic stack is the most optimized approach.
Dynamic Programming Algorithmic Approach: O(N^3) Time O(N^2) Space
Greedy Algorithmic Approach: O(N^2) Time O(1) Space
Monotonic Stack Algorithmic Approach: O(N) Time O(N) Space
Follow the link to know How to Identify and Solve the Monotonic Stack Problems
Advantages of Monotonic Stack:
We can use the extra space of a monotonic stack to reduce the time complexity.
We can get the nearest smaller or greater element depending on the monotonic stack type, by just retrieving the stack’s top element, which is just an O(1) operation.
The monotonic stack helps us maintain maximum and minimum elements in the range and keeps the order of elements in the range. Therefore, we don’t need to compare elements one by one again to get minima and maxima in the range. Meanwhile, because it keeps the element’s order, we only need to update the stack based on the newest added element.
Disadvantages of Monotonic Stack:
It increases the space complexity of the algorithm by a factor of O(N), i.e. by a linear complexity.
It is often more complex to handle as now with the existing problem, we also need to handle the stack carefully. As once the elements are popped from the stack, we cannot get them back.

How to Identify and Solve Monotonic Stack Problems ?
We all know what is Stack and how it works so today we will learn about a special type of data structure called monotonic stack. Problems using monotonic stack are difficult to identify if you do not know its concept. So in this post, we are going to discuss some key points that will help us to identify these problems.
But Before that let’s discuss the monotonic stack and its features.
What is a Monotonic Stack?
A Monotonic Stack is a stack whose elements are monotonically increasing or decreasing. It contains all qualities that a typical stack has and its elements are all monotonically decreasing or increasing.Some features of a monotonic stack:
It is a range of queries in an array of situation
The minima/maxima elements
When an element is popped from the monotonic stack, it will never be utilized again.
Key Points to Identify Monotonic Stack Problems:
To identify problems where a monotonic stack may be useful, look for the following characteristics:
Nearest Greater or Smaller Element: Monotonic stacks are commonly used to find the nearest greater or smaller element to the left or right of each element in an array or sequence. If a problem requires you to find such elements efficiently, it’s a strong indicator that a monotonic stack might be useful.
Monotonic Property: The term “monotonic” refers to the fact that the stack maintains a specific ordering property. There are two types of monotonic stacks:
Increasing Monotonic Stack: This stack is used when you need to find the nearest smaller element to the right for each element. It keeps elements in non-decreasing order, meaning the top of the stack contains the smallest element seen so far.
Decreasing Monotonic Stack: This stack is used when you need to find the nearest greater element to the right for each element. It keeps elements in non-increasing order, meaning the top of the stack contains the largest element seen so far.
Problems Involving Element Removal: Monotonic stacks are often used in problems where you need to remove elements from the stack once their purpose is fulfilled. Elements are pushed onto the stack while certain conditions are met, and they are popped when no longer relevant.
Immediate Neighbors: The problems that require finding immediate neighbors, such as the nearest greater or smaller elements to the left or right, are good candidates for a monotonic stack.
Monotonicity Changes: Some problems involve changing monotonicity requirements during traversal, which can be handled using a combination of increasing and decreasing monotonic stacks.
Typical Use Cases: Monotonic stacks are often used in scenarios like finding the next greater element, next smaller element, calculating the maximum area under histograms, evaluating expressions with infix to postfix conversion, and solving problems related to stock span, building and trapping rainwater, etc.
Problems with Linear Time Constraints: If the problem statement mentions that you need to solve it in linear time, or it hints at optimizing the time complexity, a monotonic stack might be beneficial.
How to Solve Monotonic Stack Problems ?
There is a particular pattern which we can follow to solve these monotonic stack problems
Pseudo code to solve these problems
function solve(arr) {
 // initialize an empty stack
 stack = [];

 // iterate through all the elements in the array
 for (i = 1 to arr.length)) {
    // pop elements from stack if some particular condition satisfies
     while (stack is not empty && element represented by stack top "OPERATOR" arr[i]) {
    
         let stackTop = stack.pop();

     // do something with stackTop here e.g.
     // nextGreater[stackTop] = i
   }

   if (!stack.empty()) {
     // if stack has some elements left
     // do something with stack top here e.g.
     // previousGreater[i] = stack.at(-1)
   }
   // at the end, we push the current index into the stack
    stack.push(i);
 }

 // At all points in time, the stack maintains its monotonic property
}
Let's discuss some examples for better understanding of these patterns:
Problem Statement: Given an array, print the Next Greater Element (NGE) for every element. 
Problem Link: Click Here
Intuition:
In this problem we need to find out the next greater element of each element so we can use monotonic stack in this question. Why? Because we can store the elements in the stack in increasing order of index and value and if the current value of stack does not satisfy the current condition of having greater than current array element then this stack value never contributes to our answer so we can pop this value which maintains the monotonic behavior of the stack.
// A Stack based C++ program to find next
// greater element for all array elements.
#include <bits/stdc++.h>
using namespace std;

/* prints element and NGE pair for all
elements of arr[] of size n */
void printNGE(int arr[], int n)
{
	stack<int> s;
	/* push the first element to stack */
	s.push(arr[0]);
	// iterate for rest of the elements
	for (int i = 1; i < n; i++) {
		if (s.empty()) {
			s.push(arr[i]);
			continue;
		}
		/* if stack is not empty, then
		pop an element from the stack.
		If the popped element is smaller
		than next, then
		a) print the pair
		b) keep popping while elements are
		smaller and stack is not empty */
		while (s.empty() == false && s.top() < arr[i]) {
			cout << s.top() << " --> " << arr[i] << endl;
			s.pop();
		}
		/* push next to stack so that we can find
		next greater for it */
		s.push(arr[i]);
	}
	/* After iterating over the loop, the remaining
	elements in stack do not have the next greater
	element, so print -1 for them */
	while (s.empty() == false) {
		cout << s.top() << " --> " << -1 << endl;
		s.pop();
	}
}

/* Driver code */
int main()
{
	int arr[] = { 11, 13, 21, 3 };
	int n = sizeof(arr) / sizeof(arr[0]);
	printNGE(arr, n);
	return 0;
}


A monotonic stack is a stack whose elements are monotonically increasing or decreasing.
Sometimes we store the index of the elements in the stack and make sure the elements corresponding to those indexes in the stack forms a mono-sequence.
Increasing or decreasing?
If we need to pop smaller elements from the stack before pushing a new element, the stack is decreasing from bottom to top.
Otherwise, it's increasing from bottom to top.
For example,
Mono-decreasing Stack
Before: [5,4,2,1]
To push 3, we need to pop smaller (or equal) elements first
After: [5,4,3]
Notes
For a mono-decreasing stack:
we need to pop smaller elements before pushing.
it keeps tightening the result as lexicographically greater as possible. (Because we keep popping smaller elements out and keep greater elements).

Take 402. Remove K Digits (Medium) for example, since we are looking for lexicographically smallest subsequence, we should use a mono-increasing stack.
Both nextSmaller and prevSmaller
If we need to calculate both nextSmaller and prevSmaller arrays, we can do it using a mono-stack in one pass.
The following code is for 84. Largest Rectangle in Histogram (Hard)
// OJ: https://leetcode.com/problems/largest-rectangle-in-histogram/
// Author: github.com/lzl124631x
// Time: O(N)
// Space: O(N)
class Solution {
public:
    int largestRectangleArea(vector<int>& A) {
        A.push_back(0); // append a zero at the end so that we can pop all elements from the stack and calculate the corresponding areas
        int N = A.size(), ans = 0;
        stack<int> s; // strictly-increasing mono-stack
        for (int i = 0; i < N; ++i) {
            while (s.size() && A[i] <= A[s.top()]) { // Take `A[i]` as the right edge
                int height = A[s.top()]; // Take the popped element as the height
                s.pop();
                int left = s.size() ? s.top() : -1; // Take the element left on the stack as the left edge
                ans = max(ans, (i - left - 1) * height);
            }
            s.push(i);
        }
        return ans;
    }
};
Identification

If it is solved using an array and in brute force it takes o(n^2).
If J is dependent on i then in that case this question might be solved using stack.
By u

