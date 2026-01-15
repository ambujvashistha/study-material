## **Time Complexity Notations**

- **Big O (O)** → Represents the **upper bound** of the running time.
    
    It gives the **worst-case** scenario — the maximum time an algorithm can take.
    
- **Theta (Θ)** → Represents the **tight bound**, i.e., both **upper and lower bound**.
    
    It describes the **average-case** performance.
    
- **Omega (Ω)** → Represents the **lower bound** of the running time.
    
    It gives the **best-case** scenario — the minimum time an algorithm will take.
    

---

## **Examples with Common Time Complexities**

### **1. O(1) – Constant Time**

The time taken doesn’t depend on the input size. The algorithm always runs in the same amount of time.

```python
print("HI")   # Just prints "HI", constant time

```

---

### **2. O(log n) – Logarithmic Time**

Time grows logarithmically as input increases — often seen in algorithms that halve the input (like binary search).

```python
i = 1
while i < n:
    print(i)
    i *= 2   # Doubles each time → logarithmic growth

```
---

### **3. O(n) – Linear Time**

Time grows directly in proportion to the input size.

```python
  for i in range(n):   # Runs n times
    print(i)
```
Each element is processed once → **O(n)**.

---

### **4. O(n log n) – Linearithmic Time**

A combination of linear and logarithmic time — common in sorting algorithms like Merge Sort or Quick Sort.

```python
for i in range(n):          # Linear loop
    j = 1
    while j < n:            # Logarithmic loop
        print(i, j)
        j *= 2

```

Total → `n * log n` iterations → **O(n log n)**.

---

### **5. O(n²) – Quadratic Time**

Occurs when there are **nested loops** over the same input.

```python
for i in range(n):          # Outer loop
    for j in range(n):      # Inner loop
        print(i, j)

```

Each loop runs `n` times → **n × n = n²** → **O(n²)**.

---

###
### **6. O(2ⁿ) – Exponential Time**

The runtime doubles with each increase in input — often seen in recursive brute-force solutions.

```python
for i in range(n):
    for j in range(2 ** i):   # Exponential growth
        print(i, j)

```

Time grows exponentially → **O(2ⁿ)**.
