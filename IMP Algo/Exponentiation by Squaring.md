### Summary of the Exponentiation by Squaring Algorithm

The **Exponentiation by Squaring** algorithm efficiently calculates powers of a number using bit manipulation. It reduces the time complexity from \( O(n) \) to \( O(\log n) \), where \( n \) is the exponent.

### Steps:

1. **Initialization**:
   - Start with `result = 1`.
   - The base is the number you want to raise to the power.
   - The exponent is the power to which the base is raised.

2. **Main Loop**:
   - While the exponent is greater than 0:
     - If the exponent is odd, multiply the result by the base.
     - Square the base (`base *= base`).
     - Right shift the exponent by 1 (`exponent >>= 1`), which effectively divides the exponent by 2.

3. **Exit Condition**:
   - The loop terminates when the exponent becomes 0. The final value of `result` is the answer.

### Example Code in C++:

```cpp
int power(int base, int exponent) {
    int result = 1;  // Initialize result as 1
    
    while (exponent > 0) {
        // If exponent is odd, multiply the result by the base
        if (exponent & 1) {
            result *= base;
        }
        
        // Square the base
        base *= base;
        
        // Right shift exponent (divide by 2)
        exponent >>= 1;
    }
    
    return result;
}

int main() {
    int base = 5;
    int exponent = 5;
    
    int result = power(base, exponent);
    std::cout << "5^5 = " << result << std::endl;  // Output: 3125
    
    return 0;
}
```

### Key Points:
- **Exponentiation by Squaring** reduces the number of multiplications required to compute \( a^b \) from \( O(n) \) to \( O(\log n) \).
- The algorithm works by repeatedly squaring the base and halving the exponent.
- Bit shifting (`>>`) is used to divide the exponent by 2 efficiently.

### Time Complexity:
- **Time Complexity**: \( O(\log n) \), where \( n \) is the exponent.

---

## Exponentiation by Squaring Algorithm 🔢

The **Exponentiation by Squaring** algorithm is a highly efficient way to calculate powers of a number. By utilizing bit manipulation, it reduces the time complexity from **O(n)** to **O(log n)**, where **n** is the exponent.

### Steps 📝

1. **Initialization**:
   - Start with `result = 1` as the identity element for multiplication.
   - Set the base to the number that you want to raise to the power.
   - Set the exponent to the desired power.

2. **Main Loop 🔄**:
   - While the exponent is greater than 0:
     - If the exponent is **odd** (`exponent & 1`), multiply the result by the base.
     - Square the base (`base *= base`).
     - Right shift the exponent by 1 (`exponent >>= 1`), effectively dividing the exponent by 2.

3. **Exit Condition**:
   - The loop ends when the exponent becomes 0, and the `result` will hold the computed value of the power.

### Example Code in C++ 🖥️

```cpp
int power(int base, int exponent) {
    int result = 1;  // Initialize result as 1
    
    while (exponent > 0) {
        // If exponent is odd, multiply the result by the base
        if (exponent & 1) {
            result *= base;
        }
        
        // Square the base
        base *= base;
        
        // Right shift exponent (divide by 2)
        exponent >>= 1;
    }
    
    return result;
}

int main() {
    int base = 5;
    int exponent = 5;
    
    int result = power(base, exponent);
    std::cout << "5^5 = " << result << std::endl;  // Output: 3125
    
    return 0;
}


### Key Points 🧠:
- **Exponentiation by Squaring** significantly reduces the number of multiplications needed to compute \( a^b \).
- The algorithm squares the base and halves the exponent in each iteration, resulting in logarithmic time complexity.
- **Bitwise operations** like shifting (`>>`) and checking odd/even (`& 1`) make the algorithm both efficient and elegant.

### Time Complexity ⏱️:
- **Time Complexity**: **O(log n)**, where **n** is the exponent.
```

