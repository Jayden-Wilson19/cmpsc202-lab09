# Lab 09: Exploring D&C Algorithms

**Instructions:** Work in small groups to complete the following exercises. Try sketching out your work on the whiteboards or scratch paper. Everyone should submit their own answers to the exercises, but you are encouraged to discuss your reasoning with your group members.

Name(s): Jayden Wilson

---

## Exercise 1: Recurrence Extraction

Consider the following divide-and-conquer algorithm, which takes an array $A$ of $n$ numbers as input and returns a single number. 

```text
Procedure Mystery(A, n)
    if n <= 1:
        return A[1]                              // Base case
        
    k = floor(n / 3)                             // Find the one-third point
    
    left = Mystery(A[1..k], k)                   // Recur on the left third
    right = Mystery(A[k+1..n], n - k)            // Recur on the rest
    
    total = 0 
    for i = 1 to n:
        total = total + (A[i] * left * right)    // Combine results
        
    return total
```

### Part A: The Recurrence Relation
Let $T(n)$ be the running time of `Mystery` on an input of size $n$. Write down a recurrence relation for the worst-case running time $T(n)$. You may assume $n$ is a power of 3 for simplicity. *(Note: You do not need to solve the recurrence relation yet, just formulate it).*

T(n) = T([n/3]) + T(n - [n/3]) + cn with a case of T(1) = Θ(1)

In the algorithm, you first need to break down the two recursive calls (left and right). After doing so, you'll find the input sizes (left input size: k = [n/3] right input size: n - k = n - [n/3]). You are now able to add them together as the recurrence relation.

To find the worst-case running time, you need to identify what value the algorithm's total initializes to. In this algorithm, the total is 0, which lets us know that the constant time is O(1). Further looking at our algorithm we can see it runs a loop from i = 1 to n, therfore the loop take O(n).

### Part B: Visualizing Algorithm Behavior
Without solving the recurrence, look closely at the recursive calls and the combine step. If you were to draw the recursion tree for this algorithm, what would it look like? Is the tree balanced or skewed? 

                 n
            n/3     2n/3
         n/9  2n/9 2n/9 4n/9

After writing out the recurrence tree, the tree appears to be skewed. The right branch is shown to have larger subproblems than compared to the left.
---

## Exercise 2: Unrolling the Recursion Tree

Suppose you have developed a new divide-and-conquer algorithm. You analyze your pseudocode and determine that its worst-case running time $T(n)$ satisfies the following recurrence relation:

$$T(n) \leq 3T\left(\frac{n}{2}\right) + cn^2 \quad \text{for } n > 1$$
$$T(1) \leq c$$

where $c$ is a positive constant. 

### Part C: Recursion Tree Analysis

Analyze the running time of the algorithm by unrolling the recursion tree. Specifically, answer the following questions:

1. **Root Work:** Find the amount of work done at the root level (level $0$) of the recursion tree.
2. **First Levels:** Find the amount of work done at level $1$ and level $2$ of the recursion tree.
3. **Tree Height:** Find the height of the recursion tree (at what level does the input size reach $1$?).

**Bonus!** Find a general formula for the total work done at level $i$ of the recursion tree.


1. In the algorithm, the non-recursion work shows the size of n as cn^2. Telling us that the amount of work done at root level 0 is cn^2. (W0 = cn^2).

2. Each call in the tree creates smaller subproblems half the size of its parent. At level 1 the number of nodes is 3. Its input size per node is n/2. And shown in this algorthm, it showing the work for each node is c(n/2)^2. 

After mulitplying all known information (W1 = 3 x c(n/2)^2) you'll end with W1 = 3cn^2/4.

At level 2 in the recursion tree, it's shown that each of the 3 nodes creates another 3 nodes (3^2 = 9). Its input for each of those nodes (n/2^2 = n/4), and the work for each node (c(n/4)^2).

Again mulitplying all the known information (W2 = 9 x c(n/4)^2) will leave you with W2 = 9cn^2/16

3. At each level, the input size is divded by 2, so at level i in the recurrence algorithm, the input size is: n/2^i. Since we need to find when the input size reaches 1, set 1 equal to n/2^1. Next, multiply both sides by 2^1 (n = 2^1). Then take the logarithm base of 2 (i = log2(n)), which will leave you with a height of log2(n).
---

## Exercise 3: Reflection

1. During lecture last week, we looked at two different divide-and-conquer algorithms. What were these algorithms and what problems did they solve?





2. How do the algorithms you analyzed in this lab compare to the ones we discussed in lecture? Specifically, each algorithm differs from the two we discussed in lecture in one important way. For each of the algorithms above, what is that difference?