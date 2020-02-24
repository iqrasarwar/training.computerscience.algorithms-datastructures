# Algorithms and Data Structures

- My notes from UC San Diego MicroMasters Program, [Algorithms and Data Structures](https://www.edx.org/micromasters/ucsandiegox-algorithms-and-data-structures) and all the readings that I made in parallel (see [references](#references) below)
- My anki flashcards:
    - [Anki flashcards package](https://github.com/hamidgasmi/AlgorithmsDataStructures/blob/master/algorithms-datastructures_ankiflashcard.apkg): 34 cards
    - [Install Anki](https://apps.ankiweb.net/)

## Table of Contents
- [Prerequisites](#prerequisites)
- [Algorithm Design and Techniques](#algorithm-design-and-techniques)
- [Data Structures Fundamentals](#data-structures-fundamentals)
- [Graph Algorithms](#graph-algorithms)
- [NP-Complete Problem](#np-complete-problem)
- [String Processing and Pattern Matching Algorithms](#string-processing-and-pattern-matching-algorithms)
- [Dynamic Programming: Applications In Machine Learning and Genomics](#dynamic-programming-applications-in-machine-learning-and-genomics)
- [Graph Algorithms in Genome Sequencing ](#graph-algorithms-in-genome-sequencing)
- [References](#references)

## Prerequisites

<details>
<summary>Proof by Induction</summary>

- It allows to prove a statement about an arbitrary number n by:
    - 1st proving it's true when n is 1 and then 
    - assuming it's true for n = k and showing it's true for n = k + 1
- [For more details](http://comet.lehman.cuny.edu/sormani/teaching/induction.html)

</details>

<details>
<summary>Proofs by contradiction</summary>

- It allow to prove a proposition is valid (true) by showing that assuming the proposition to be false leads to a contradiction
- [For more details](https://en.wikipedia.org/wiki/Proof_by_contradiction)

</details>

<details>
<summary>Logarithms</summary>

- See [this](https://www.khanalscademy.org/math/algebra2/x2ec2f6f830c9fb89:logs/x2ec2f6f830c9fb89:log-intro/a/intro-to-logarithms)

</details>

<details>
<summary>Iterated logarithm</summary>

- It's symbolized: **log∗(n)**: 
- It's the number of times the logarithm function needs to be applied to n before the result is ≤ 1
-      Log*(n) = 0 if n ≤ 1 = 1 + Log* (Log (n)) if n > 1
-      n                           Log*(n)
       n = 1                        0
       n = 2                        1
       n ∈ {3, 4}                   2
       n ∈ {5,..., 16}              3
       n ∈ {17, ..., 65536}         4
       n ∈ {65537,..., 2^65536}     5

</details>

<details>
<summary>Recursion</summary>

- To [Get Started](https://www.khanacademy.org/computing/computer-science/algorithms/recursive-algorithms/a/recursion)
- Stack optimization and Tail Recursion

</details>

<details>
<summary>T(n)</summary>

- It's the number of lines of code executed by an algorithm

</details>    


## Algorithm Design and Techniques

<details>
<summary>Test Cases</summary>

- **Boundary** values
- **Biased**/**Degenerate** tests cases
    - They're particular in some sense
    - See example for each data structure below
- **Randomly** generated cases and **large** dataset:
    - It's to check random values to catch up cases we didn't think about
    - It's also to check how long it takes to process a large dataset
    - Implement our program as a function **solve(dataset)**
    - Implement an additional procedure **generate()** that produces a random/large dataset 
    - E.g., if an input to a problem is a sequence of integers of length 1 ≤ n ≤ 10^5, then: 
        - Generate a sequence of length 10^5, 
        - Pass it to our solve() function, and 
        - Ensure our algorithm outputs the result quickly: we could measure the duration time
- **Stress** testing:
    - Implement a slow but simple and correct algorithm
    - Check that both programs produce the same result (this is not applicable to problems where the output is not unique) 
    - Generate random test cases as well as biased tests cases
- When dealing with **numbers**:
    - Think about number size: Int. Long, ... ?
    - If there is any division: division by 0; Precision?
    - Integers Biased cases: a **Prime/Composite** number; an **Even/Odd** number
- When dealing with **String**:
    - Biased/Degenerate tests: 
        - Empty string
        - A strings that contains a sequence of a single letter (“aaaaaaa”) or 2 letters ("abbaabaa") as opposed to those composed of all possible Latin letters
    - Encoding (ASCII, UTF-8, UTF-16)?
    - Special characters
    - such as those with only small numbers or a small range of large numbers, 
- When dealing with **arrays/lists**:
    - Biased/Degenerate tests: 
        - It's empty
        - It contains only small numbers or a small range of large numbers
    - It contains **few** elements: 1, 2
    - It contains **many** elements: 10^6
    - It contains same elements: min value only (0 for integers), max value only (2^32 for integers), any specific value
- When dealing with **Trees**:
    - Biased/Degenerate tests: a tree which consists of a linked list, binary trees, stars
- When dealing with **Graphs**:
    - Biased/Degenerate tests: a graph which consists of a linked list, a tree, a disconnected graph, a complete graph, a bipartite graph

</details>

<details>
<summary>Big O vs. Big-Ω vs. Big-Θ</summary>

- **Big-Ω** (Omega):
    - It's a lower bound of a function
    - A function f(n) = Ω(g(n)), if there're positive constants C and k, such that 0 ≤ C g(n) ≤ f(n) for all n ≥ k
    - E.g., f(n) = n^2 + n = Ω(n) because n ≤ f(n) for n ≥ 1
    - ![Example](https://xlinux.nist.gov/dads/Images/omegaGraph.gif)
    - It's NOT used in the industry
- **Big-O**:
    - It's an upper bound of a function
    - A function f(n) = O(g(n)), if there're positive constants C and k, such that 0 ≤ f(n) ≤ C g(n) for all n ≥ k
    - E.g., f(n) = n^2 = O(n^3) because f(n) ≤ n^3 for k ≥ 1
    - ![Example](https://upload.wikimedia.org/wikipedia/commons/8/89/Big-O-notation.png)
    - It's used in the Industry with a different definition (see below, Big-Theta)
- **Big-Θ** (Theta):
    - A function f grows at same rate as a function g
    - If f = Ω(g) and f = O(g)
    - E.g., f(n) = n^2 + n = Θ(n^2) because n^2 ≤ f(n) ≤ n^2 for k ≥ 1
    - It's used in the industry as Big-O
- **Small-o**:
    - A function f is o(g) if f(n)/g(n) → 0 as n → ∞
    - f grows slower than g
    - It's NOT used in the industry
- [For more details](https://www.khanacademy.org/computing/computer-science/algorithms/asymptotic-notation/a/asymptotic-notation)

</details>

<details>
<summary>Time Complexity</summary>

- It describes the rate of increase of an algorithm
- It describes how an algorithm scales when input grows
- Big-O notation is used
- It's also called **Asymptotic runtime**:
    - It's only asymptotic
    - It tells us about what happens when we put really big inputs into the algorithm
    - It doesn't tell us anything about how long it takes
    - Its hidden constants:
        - They're usually moderately small, and therefore, we have something useful
        - They're could be big
    - Sometimes an algorithm A with worse Big-O runtime than algorithm B:
        - Algorithm A is worse asymptotically on very large inputs than algorithm B does
        - But algorithm A is better for all practical sizes and very large inputs couldn't be stored 
- E.g., O(1), O(n), O(n^2) , O(Log n), O(n log n), O(2^n)
- [Data structure and theirs related algorithms time complexity](https://www.bigocheatsheet.com/)

</details>

<details>
<summary>Space Complexity</summary>

- It describes the amount of memory - or space - required for an algorithm
- It useful to compare the performance of algorithms
    - Input size from which an algorithm will experience unsufficient memory (RAM) and start using Disk lookups
- Big O notation and concept are used 

</details>

<details>
<summary>Big-O Rules</summary>

- **Drop the constants**: we'll use O(n) instead of O(2 n)
- **Drop the Non-Dominant Terms**: we'll use O(n^2) instead of O(n^2 + n) or O(n) instead of O(n + log n) 
- Multi-Part Algorithms - Add: **O(A+B)**
    - When an algorithm is in the form 
    - Do A, 
    - When you're done, Do B
- Multi-Part Algorithms - Multiply: **O(A*B)**
    - When an algorithm is in the form: 
    - Do B for each time you do A
- **Amortized Time**
    - When the worst case happens once a while 
    - But once it happens, it won't happen again for so long that the cost is "amortized" 
    - E.g., insert in a dynamic resizing array (an array list): 
        - It's implemented with an array 
        - When the array hits its capacity, it will create a new array with double the capacity and copy all the elements over to the new array
        - Insert time complexity in expected case (the array isn't full): O(1)
        - Insert time complexity in worst case (the array is full): O(n)
        - Insert time complexity for n inserts: O(n) (for n expected cases) + O(w * n) (w worst cases): O((w+1)n) = O(n)
        - The amortization time for each insertion (the time complexity for n inserts divided by n): O(1)
- **Log n** runtimes: O(log n)
    - It when the number of elements in a problem space is halved each time (or divided by n) 
    - E.g. **Dichotomic search**: search in a sorted array
- The base of Log(n) isn't import
    - E.g. O(Log2 n) = O(Log3 n) = O(Log n) 
- **Recursive Runtimes**, a recursive algorithm usually is defined by:
    - Its **depth**: n and the **number of times each recursive call branches** (itself). 
    - **Time complexity: O(branchesNbr^n)** 
    - **Space complexity: O(n)**
    - E.g., Fibonacci Recursive time complexity: O(2^n)
    - E.g., Fibonacci Space complexity: O(n): because only O(N) nodes exist at any given time 
- The **base of an Exponent**:
    - Log(8^n) is completely different than Log(2^n)
 
</details>

<details>
<summary>Algorithm Design</summary>

- **Reading problem statement**: 
    - The problem statement specifies the input-output format, the constraints for the input data as well as time and memory limits 
    - Our goal is to implement a fast program that solves the problem and works within the time and memory limits
    - Question inputs:
        - **String**: Encoding (ASCII, UTF-8, UTF-16)?, Special characters?
        - **Number**: Size (Int. Long, ...)? Precision, Rounding?
- **Build your intuition**:
    - *In progress*
- **Designing an algorithm**: 
    - When the problem statement is clear, start designing an algorithm and 
    - Don’t forget to **prove that it works correctly**
    - Don't forget to **estimate its expected running time**:
        - E.g.
        -       Time Complexity:     O(n^2)                  O(n log n)
                    Machine ops:      10^9                   10^9
                              n:      10^5                   10^5
                 Estimated Time:      > 10s (10^10/10^9)     < 1 ms (10^5*log(10^5)/10^9)
- **Implementing an algorithm**: 
    - After you developed an algorithm, start implementing it in a programming language
- **Testing and debugging your program** 
    - Testing is the art of revealing bugs
    - 1st start with **simple test cases**: 
        - Small dataset
        - Make sure our program produces correct results
    - 2nd check **degenerate** cases: see test cases section above
    - 3rd check **boundary** values: see test cases section above
    - 4th check **randomly** generated cases
    - 5th check **large** dataset: see test cases section above
    - 6th finish with **stress** testing: see test cases section above

</details>

<details>
<summary>General Approaches</summary>

- **Tournament** approach:
    - To find the kth largest number in an array, compare each paire of 2 elements together
    - compare(elem 0, elem 1), compare(elem 2, elem 3)...
    - O(n + log(n) − 2)
- **Euclidean** Algorithm

</details>

<details>
<summary>Greedy Algorithms</summary>

- **Greedy Strategy**:
    - **1. Make a greedy choice**
    - **2. Prove that it is a safe choice**
    - **3. Reduce to a subproblem**
    - **4. Solve the subproblem (Iterate)**
    - E.g. Problem, Queue of Patients:
        - n patients have come to the doctor’s office at same time
        - Ti is the time needed for treatment of the i-th patient
        - They can be treated in any order 
        - Output: Arrange the patients in such a queue that the total waiting time is minimized
    - E.g. Solution:
        - Make a greedy choice: choose the patient (Pi) with the smallest treatment time (with the minimum Ti)
        - Prove that it's a safe choice
        - Reduce to a smaller problem: remove Pi from the queue
        - Iterate: Treat all the remaining patients in such order as to minimize their total waiting time as if there wasn't 1st patient
- **Subproblem** 
    - It's a similar problem of smaller size
    - Minimum total waiting time for n patients = (n − 1) · T min + minimum total waiting time for n − 1 patients without T min
    - Min total waiting time for n = 4 partients: (15, 10, 25, 20) = (4 - 1) * 10 + Min total waiting time for (15, 25, 20)
- **Safe Choice**:
    - It's a greedy choice which there's an optimal solution consistent with this 1st choice
    - It requires to **prove** that a greedy choice is safe
    - E.g. Queue of Patients: 
        - If we prove that there's an optimal solution that starts with treating a patient with the minimum treatment time
        - Therefore such a choice is a safe choice
        - However, if we choose a patient with the maximum treatment time, there's not an optimal solution that starts with it
        - Therefore such a choice isn't a safe choice
- E.g. Fractional Knapsack (or Backpack) Problem:
    - N items with total weight and total value (Wi, Vi)
    - A Backpack with a capacity W
    - Goal: Maximize value ($) while limiting total weight (kg)
    - It's possible to take fraction of items
    - Item 1: (6, $30), Item 2 (3, $14), Item 3 (4, $16), Item 4 (2, $9)
        - Knapsack capacity: 10
        - Value per Unit: Item 1: $5; Item2: $4.66; Item3: $4; Item4: $4.5
        - Solution: 6 * $5 + 3 * $4.666 + 1 * $4.5 (fraction of item4) = $48.5

</details>

<details>
<summary>Divide and Conquer</summary>

- **Divide**: Break into non-overlapping subproblems of the same type
- **Conquer**:
    - Solve subproblems: each one indepently of the others
    - Combine results
- Implementation: it's often implemented with a **recursive** algorithm
- Calculate its Time Complexity:
    - Define a corresponding **recurrence relation**, **T**
        - It's an equation recursively defining a sequence of values
        - For Linear Search *T(n) = T(n - 1) + c*; *T(0) = c*
        - *c* is the runtime for a constant amount of work: checking high vs. low indexes; if A[low] == key); preparing the parameters for the recursive call
        - *T(0)* is the runtime for the **base case** of the recursion (empty array): checking high vs. low indexes, returning not found
        - For Binary Search *T(n) = T(n/2) + c*; *T(0) = c*
    - Determine **worst-case runtime**, T(n) from the recurrence relation
        - Look at the **recursion tree**
        - For Linear Search T(n) = T(n - 1) + c = T(n - 2) + 2 * c = n * c = T(n) = Θ(n)
        - For Binary Search T(n) = T(n/2) + c = T(n/2^2) + 2 * c = T(n/2^3) + 3 * c = Θ(log2 n) = Θ(log n)
- Optionally, create iterative solution
    - It allows to save space
- For more details:
    - [Binary Search](https://www.khanacademy.org/computing/computer-science/algorithms/binary-search/a/binary-search)
    - **Merge Sort**
        - [Course Material](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/1_algorithm_design_and_techniques/week4_divide_and_conquer/03_divide_and_conquer_4_sorting.pdf)
        - [Merge Sort on khanacademy](https://www.khanacademy.org/computing/computer-science/algorithms#merge-sort)
    - **Quick Sort**
        - It's more efficient in practice than Merge Sort
        - Average Time Complexity: O(n log n)
        - Time Complexity in the worst case: O(n^2)
        - [Course Material](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/1_algorithm_design_and_techniques/week4_divide_and_conquer/03_divide_and_conquer_5_quicksort.pdf)
        - [Quick Sort on khanacademy](https://www.khanacademy.org/computing/computer-science/algorithms#quick-sort)
        - [Deterministic and Randomized Quicksort](http://faculty.cs.tamu.edu/klappi/csce411-f12/csce411-set13.pdf)
        - [3 way partition Quick Sort](https://www.geeksforgeeks.org/3-way-quicksort-dutch-national-flag/)
        - [Quick Sort Recursive Tail Elimination](https://www.geeksforgeeks.org/quicksort-tail-call-optimization-reducing-worst-case-space-log-n/)
        - [Quick Sort wth deterministic pivot selection heuristic]:
            - The pivot could be the median of the 1st, middle, and last element
            - If the recursion depth exceeds a certain threshold ***c log n***, the algorithm switches to heap sort
            - It's a simple but heuristic approach:: it's not guaranteed to be optimal
            - The time complexity is: O(n log n) in the worst case
    - [Counting Sort](https://www.geeksforgeeks.org/counting-sort/)

</details>

<details>
<summary>Dynamic Programming</summary>

- It's a general algorithmic design technique: Approach can be used to solve many kinds of problems
- It's Frequently used for optimization problems: finding best way to do something
- It's typically used when brute-force solution is to enumerate all possibilities:
    - May not know which subproblems to solve, so we solve many or all!
    - Reduce number of possibilities by:
        - Finding optimal solutions to subproblems
        - Avoiding non-optimal subproblems (when possible)
        - Frequently gives a polynomial algorithm for brute force exponential one
- It's like Divide and Conquer:
    - General design technique
    - Uses solutions to subproblems to solve larger problems
    - Difference: Dynamic Programming subproblems typically overlap
- It's an alternative for Recursive algorithms:
    - Recursive algorithms may be not efficient: they could do a compute several times
    - E.g. Money change problem MinCoin(40 cents) in Tanzania:
    - MinCoin(40s) = 1 + Min( MinCoin(40c - 1c), MinCoin(40c - 5c), MinCoin(40c - 10c), MinCoin(40c - 20c), MinCoin(40c - 25c))
    - MinCoin(20c) is computed at least 4 times: MinCoin(40c - 1c), MinCoin(40c - 5c), MinCoin(40c - 10c), MinCoin(40c - 20c)
- It's an alternative for Greedy Algorithms: 
    - When there is not a safe choice
    - E.g.1, Money change problem MinCoin(40 cents) in US:
        - US coins <= 40c: 1c, 5c, 10c, 25c
        - A Greedy choice: take the max coin such that coin <= 40c
        - Result: 3 coins: 40c = 1 * 25c + 1 * 10c + 1 * 5c
        - Here this choice is safe
    - E.g.2, Money change problem MinCoin(40 cents) in Tanzania:
        - Tanzanian coins <= 40c: 1c, 5c, 10c, 20c, 25c
        - A greedy choice: take the max coin such that the coin <= 40c
        - Result: 3 coins: 40c = 1 * 25c + 1 * 10c + 1 * 5c
        - Here this choice isn't safe: 40c = 2 * 20c
- Steps:
    - Express a solution mathematically
        - **Cut and Paste Trick Dynamic Programming**:
        - Cut and paste proof: optimal solution to problem must use optimal solution to subproblem: otherwise we could remove suboptimal solution to subproblem and replace it with a better solution, which is a contradiction
        - [For more details](https://stackoverflow.com/questions/9553162/what-is-the-cut-and-paste-proof-technique)
    - Express a solution recursively
    - Either develop a **bottom up algorithm**:
        - Find a bottom up algorithm to find the optimal value
        - Find a bottom up algorithm to construct the solution
    - Or develop a **memoized recursive algorithm**
- **Alignment game** (String Comparison):
    - Remove all symbols from 2 strings in such a way that the number of points is maximized:
    - Remove the 1st symbol from **both** strings: 1 point if the symbols match; 0 if they don't
    - Remove the 1st symbol from **one** of the strings: 0 point
    - E.g.,:    
        -       A T G T T A T A  => A T - G T T A T A
                A T C G T C C    => A T C G T - C - C
                                   +1+1  +1+1         = +4
    - **Sequence Alignment**:
        - It's a 2-row matrix
        - 1st row: symbols of the 1st string (in order) interspersed by "-"
        - 2nd row: symbols of the 2nd string (in order) interspersed by "-"
        - E.g.:  
        -        A T - G T T A T C
                 A T C G T - C - C
                     ^-Del ^--Insert.
        - **Alignment score**: 
            - Premium (**+1**) for every **match** 
            - Penalty (**-μ**) for every **mismatch**
            - Penatly (**-σ**) for every **indel** (insertion/deletion)
            - E.g.:
            -  A T - G T T A T A
               A T C G T - C - C
              +1+1-1+1+1-1-0-1+0 = +1
        - **Optimal alignment**:
            - Input: 2 strings, mismatch penatly μ, and indel penalty σ
            - Output: An alignment of the strings maximizing the score
    - **Common Subsequence**: **Matches** in an alignment of 2 strings form their **common subsequence**
        - E.g. 
        -      A T - G T T A T C
               A T C G T - C - C
               AT    G T 
              (ATGT) is a common subsequence
- **Longest common subsequence**:
    - Input: 2 strings
    - Output: A longest common subsequence of these strings
    - It corresponds to **highest alignment score** with **μ = σ = 0** (maximizing the score of an alignment)
- **Edit distance**
    - Input: 2 strings
    - Output: the **minimum number of operations** (insertions, deletions, and substitutions of symbols) **to transform one string into another**
    - It corresponds to the **minimum number of mismatches and indels** in an alignment of 2 strings (among all possible alignments)
    - E.g.: 
    -       E D I - T I N G -
            - D I S T A N C E
            ^-Del ^-Ins.----^
    - **Minimizing edit distance = Maximizing Alignment score**
    - Let ***D(i,j)*** be the edit distance of an *i*-prefix *A*[1... *i*] and a *j*-prefix *B*[1.... *j*]
    - ***D(i,j) = MIN(D(i,j-1) + 1, D(i-1,j) + 1, D(i-1,j-1) + 1) if A[i] <> B[j]*** OR
    - ***D(i,j) = MIN(D(i,j-1) + 1, D(i-1,j) + 1, D(i-1,j-1)) if A[i] = B[j]***
- **Reconstructing an **Optimal Alignment**:
    - It could be done by backtracking pointers that are stored in the edit distance computation matrix
- E.g., Discrete Knapsack problem
    - N items with total weight Wi (Kg) and total value Vi ($)
    - A Backpack with a capacity W
    - Each item is either taken or not
    - Goal: Maximize value ($) while limiting total weight (kg)
    - Discrete Knapsack with unlimited repetitions quantities:
        - Input: Weights (W1,..., Wn) and values (V1,..., Vn) of n items; total weight W (Vi’s, Wi’s, and W are non-negative integers)
        - Output: The maximum value of items whose weight doesn't exceed W 
        - Each item can be used any number of times
        - Item 1 (6, $30), Item 2 (3, $14), Item 3 (4, $16), Item 4 (2, $9)
        - Knapsack capacity: 10
        - Solution: 6 ($30) + 2 ($9) + 2 ($9) = $48
        - Greedy Algorithm doesn't work: 6 ($30) + 
    - Discrete Knapsack without one of each repetitions item:
        - Input: Weights (W1,..., Wn) and values (V1,..., Vn) of n items; total weight W (Vi’s, Wi’s, and W are non-negative integers)
        - Output: The maximum value of items whose weight doesn't exceed W 
        - Each item can be used at most once
        - Item 1 (6, $30), Item 2 (3, $14), Item 3 (4, $16), Item 4 (2, $9)
        - Knapsack capacity: 10
        - Solution: 6 ($30) + 4 ($16) = $46
    - Greedy Algorithm fails:
        - Item1 (6, $30), Item2 (3, $14), Item3 (4, $16), Item4 (2, $9)
        - Value per Unit: Item 1: $5; Item2: $4.66; Item3: $4; Item4: $4.5
        - 6 ($30) + 3 ($14) = 9 items ($44)
        - taking an element of maximum value per unit of weight is not safe!
- For more details:
    - [Course material](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/1_algorithm_design_and_techniques/week5_and_6_dynamic_programming/04_dynamic_programming_2_editdistance.pdf)
    - [Advanced dynamic programming lecture notes]() by Jeff Erickson
    - [How Do We Compare Biological Sequences?](https://www.youtube.com/playlist?list=PLQ-85lQlPqFNmbPEsMoxb5dM5qtRaVShn) by Phillip Compeau and Pavel Pevzner
- For more details:
    - [Money change problem: Greedy vs. Recursive vs. Dynamic Programming](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/1_algorithm_design_and_techniques/week5_and_6_dynamic_programming/04_dynamic_programming_1_changeproblem.pdf)
    - [Dynamic Programming](https://www.geeksforgeeks.org/dynamic-programming/) in geeksforgeeks
    - [Dynamic Programming](https://www.radford.edu/~nokie/classes/360/dynprog.html)

</details>

---

## Data Structures Fundamentals

<details>
<summary>Arrays</summary>

- It's a contiguous area of memory
- It's consisting of equal-size elements indexed by contiguous integers
- **1-D Array**: accessing **array[i]** consists of accessing the memory address: **array_addr + elem_size × (i − first_index)**
- **2-D Array**:
    - It could be laid out in **Row-Major order**:
        - Its 2nd index (column) changes most rapidly
        - Its elements are laid out as follow: (1,1), (1,2), (1,3), ..., (2,1), (2,2),...
        - Accessing **[i][j]** consists of accessing the memory address: **array_addr + elem_size × [row_lenth * (i  − 1st_row_index) + (j − 1st_column_index)]**
    - It could be laid out in **Column-Major order**:
        - Its 1st index (row) changes most rapidly
        - Its elements are laid out as follow: (1,1), (2,1), (2,1), ..., (1,2), (2,2),...
        - Accessing **[i][j]** consists of accessing the memory address: **array_addr + elem_size × [column_lenth * (j  − 1st_column_index) + (i − 1st_row_index)]**
- Time for common operations:
    -                     Read    Remove   Add
            Beginning:    O(1)     O(n)    O(n) 
                  End:    O(1)     O(1)    O(1)
               Middle:    O(1)     O(n)    O(n)
- Programming Languages:
    - Python: there is no static array data structure
- For more details:
    - [Arrays and Lists Course](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/1_basic_data_structures/01_1_arrays_and_lists.pdf)

</details>

<details>
<summary>Linked Lists</summary>

- Singly-Linked List
    -                APIs                Time (wout tail)   Time (w tail)         Description 
                PushFront(Key):               O(1)                                 Aadd to front
                Key TopFront():               O(1)                                 Return front item
                    PopFront():               O(1)                                 Remove front item
                 PushBack(Key):               O(n)              O(1)               Add to back
                 Key TopBack():               O(n)              O(1)               Return back item
                     PopBack():               O(n)                                 Remove back item
             Boolean Find(Key):               O(n)                                 Is key in list?
                    Erase(Key):               O(n)                                 Remove key from list
               Boolean Empty():               O(1)                                 Empty list?
          AddBefore(Node, Key):               O(n)                                 Adds key before node
           AddAfter(Node, Key):               O(n)                                 Adds key after node 
- **Doubly-Linked List**:
    - Its node consists of a key, a pointer to the next node and a pointer to the previous node
    -                APIs                    Time (wout tail)   Time (w tail)
                PushFront(Key):               O(1)                                 
                Key TopFront():               O(1)                                 
                    PopFront():               O(1)                                 
                 PushBack(Key):               O(n)              O(1)               
                 Key TopBack():               O(n)              O(1)               
                     PopBack():               O(n)              O(1)                 
             Boolean Find(Key):               O(n)                                 
                    Erase(Key):               O(n)                                 
               Boolean Empty():               O(1)                                 
          AddBefore(Node, Key):               O(n)
           AddAfter(Node, Key):               O(n)
- Programming Languages:
    - Python:
- For more details:
    - [Arrays and Lists Course](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/1_basic_data_structures/01_1_arrays_and_lists.pdf)

</details>

<details>
<summary>Stacks</summary>

- For more details:
    - [Stacks and Queues Course](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/1_basic_data_structures/01_2_stacks_and_queues.pdf)
- Programming Languages:
    - Python:

</details>

<details>
<summary>Queues</summary>

- For more details:
    - [Stacks and Queues Course](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/1_basic_data_structures/01_2_stacks_and_queues.pdf)
- Programming Languages:
    - Python:

</details>

<details>
<summary>Trees</summary>

- It is empty, or a node with a key, and a list of child trees
- Terminology:
    - A **Root**: top node in the tree
    - A **child** has a line down directly from a **parent**
    - An **Ancestor** is a parent, or a parent of parent, etc.
    - **Descendant** is a child, or a child of child, etc.
    - A **Sibling** is sharing the same parent
    - A **Leaf** is a node without children
    - An **Interior node** is a node that isn't a leaf
    - An **Edge** is a link between two nodes
    - A **Level**: 
        - 1 + number of edges between a tree root and a node
        - E.g., The root node is level 1
    - A **Height**: 
        - It's the maximum depth of subtree node and its farthest leaf
        - It could be calculated by counting the number of nodes or edges
    - A **Forest** is a collection of trees
- Walking a Tree:
    - **Depth-First** (**DFS**): To traverse one sub-tree before exploring a sibling sub-tree
    - **Breadth-First** (**BFS**): To traverse all nodes at one level before progressing to the next level
- A **Binary Tree**: 
    - It's a tree where each node has 0, 1, or 2 children
    - DFS types: 
        - **In Order Traversal** of a node: InOrderTraversal of its Left child; Visit node; InOrderTraversal of its Right child
        - **Pre Order Traversal** of a node: Visit node; PreOrderTraversal of its Left child; PreOrderTraversal of its Right child
        - **Post Order Traversal** of a node: PostOrderTraversal of its Left child; PostOrderTraversal of its Right child; Visit node
    - A **Complete Binary Tree**: 
        - It's a binary tree in which all its levels are filled except possibly the last one which is filled from left to right
        - Its height is **Low**: it's at most **O(log n)** (n is nbr of nodes)
        - It could be **stored effeciently** as an **array**
    - A **Full Binary Tree**:
        - It's also called **Proper Binary Tree** or **2-tree**
        - It's a tree in which every node other than the leaves has 2 children
        - Its height is Low: it's equal to O(log n)
        - It could be stored effeciently as an array
- For more details:
    - [Course](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/1_basic_data_structures/01_3_trees.pdf)

</details>

<details>
<summary>Dynamic Arrays</summary>

- It's also known as **Resizable array**
- It's a solution for limitations of **static** arrays and **dynamically-allocated** arrays (see below):
    - It can be resized at runtime
    - It stores (implementation):
        - Arr: dynamically-allocated array
        - Capacity: size of the dynamically-allocated array
        - Size: number of elements currently in the array
    - When an element is added to the end of the array and array's size and capacity are equal:
        - It allocates a new array
        - New Capacity = Previous Capacity x 2
        - Copy all elements from old array to new array
        - Insert new element
        - New Size = Old Size + 1
        - Free old array space
- Time Complexity and Operations:
    -                       Time Complexity
                  Get(i):       O(1) 
             Set(i, val):       O(1)
           PushBack(val):       O(1) or O(n): O(n) when size = capacity; O(1) otherwise (amortized analysis)
               Remove(i):       O(1)
                  Size():       O(1)
- Programming Languages:
    - Python: list (the only kind of array)
    - C++: vector
    - Java: ArrayList
- Static array:
    - it's static!
    - It requires to know its size at compile time
    - Problem: we might not know max size when declaring an array
- Dynamically-allocated arrays:
    - int *my_array = new int[ size ]
    - It requires to know its size at runtime
    - Problem: we might not know max size when allocating an array
- More details:
    - [UC San Diego Course](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/2_dynamic_arrays_and_amortized_complexity/02_1_dynamic_arrays_and_amortized_analysis.pdf)

</details>

<details>
<summary>Amortized Analysis</summary>

- Methods to calculate amortized cost:
    - The **Aggregate method**: 
        - It calculates amortized cost based on amortized cost definition
        - E.g. Dynamic Array:
    - The **Banker's Method**:
    - The **Physicist's Method**:
- More details:
    - [Amortized Analysis](https://youtu.be/U5XKyIVy2Vc) 
    - [UC San Diego](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/2_dynamic_arrays_and_amortized_complexity/02_1_dynamic_arrays_and_amortized_analysis.pdf)

</details>

<details>
<summary>Priority Queues: Max/Min Heap</summary>

- **Max Heap**:
    - It's a binary tree where the value of each node is at least the values of its children
    - For each edge of the tree, the value of the parent is at least the value of the child
- **Min Heap**:
    - It's a binary tree where the value of each node is at most the values of its children
- Implementation, Time Complexity and Operations:
    - An efficient implementation is a **Complete Binary Tree** in an **Array**
    -            Operations        0-based index      1-based index array
                  Parent(i):          ⌊ i / 2 ⌋         ⌊ i / 2 ⌋
               Leftchild(i):          2 * i + 1         2 * i
              Rightchild(i):          2 * i + 2         2 * i + 1
    -                               Time Complexity     Comment
                   GetMax():             O(1)            or GetMin()
               ExtractMax():           O(log n)        n is the nodes # (or ExtractMin)
                  Insert(i):           O(log n)
                  SiftUp(i):           O(log n)
                SiftDown(i):           O(log n)
          ChangePriority(i):           O(log n)
                  Remove(i):           O(log n)
- Programming Languages:
    - Python:
        - Lib/heapq.py
        - [Description](https://docs.python.org/2/library/heapq.html)
        - [Git](https://github.com/python/cpython/blob/2.7/Lib/heapq.py)
    - C++:
    - Java:
- For more details:
    - UC San Diego Course:[Overview & Naive Implementations](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/3_priority_queues_and_disjoint_sets/03_1_priority_queues_intro.pdf)
    - UC San Diego Course:[Binary Heaps](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/3_priority_queues_and_disjoint_sets/03_2_priority_queues_heaps.pdf)

</details>

<details>
<summary>Priority Queues: Heap Sort</summary>

- Not-In place algorithm to sort an Array (A) with a Heap Sort:
    -       Create an empty priority queue MaxHeap
            for i from 1 to n:
                MaxHeap.Insert(A[i])
            for i from n downto 1:
                A[i] = MaxHeap.ExtractMax()
    - Time Complexity:  O(n log n)
    - **Space Complexity: O(n)** (It's not an in place algorithm)
    - It's a natural generalization of selection sort:
        - Instead of simply scanning the rest of the array to find the maximum value,
        - It uses a smart data structure
- In place algorithm to sort an array (A) with a Heap Sort:
    - Step 1: Turn the array A[] into a heap by permuting its elements
        - We repair the heap property going from bottom to top
        - Initially, the heap property is satisfied in all the leaves (i.e., subtrees of depth 0)
        - We then start repairing the heap property in all subtrees of depth 1
        - When we reach the root, the heap property is satisfied in the whole tree
    -       BuildHeap(A[1 ... n])
                for i from ⌊n/2⌋ downto 1:
                    SiftDown(i)
        - Space Complexity: O(1) (In place algorithm)
        - Time Complexity:
                Height          Nodes #    T(SiftDown)       T(BuildHeap)
                log_2(n)          1         log_2(n)          1 * log_2(n) 
                log_2(n) - 1      2         log_2(n) - 1      2 * [ log_2(n) - 1]
                  ...            ...         ...                 ...
                   2            ≤ n/4        2                n/4 * 2
                   1            ≤ n/2        1                n/2 * 1
                T(BuildHeap) = n/2 * 1 + n/4 * 2 + ... + 1 * log_2(n) 
                             = n/2 * 1 + n/4 * 2 + ... + n / 2^log_2(n) * log_2(n)
                             = n [1/2 + 2/4 + 2/8 + ... log_2(n)/2^log_2(n)] < n * 2
                             = **O(n)**
    - Step 2: Sort the Heap
    -       HeapSort(A[1 . . . n])
                BuildHeap(A)
                repeat (n − 1) times:
                    swap A[1] and A[size]
                    size = size − 1
                    SiftDown(1)
        - Space Complexity: O(1) (In place algorithm)
        - Time Complexity: O(n long n)
- Use cases:
    - It's used for external sort when we need to sort huge files that don’t fit into memory of our computer 
        - In opposite of QuickSort which is usually used in practice because typically it is faster
    - **IntraSort** algorithm:
        - It's a sorting algorithm
        - It 1st runs QuickSort algorithm (Avergae Running time: O(n log n); Worst Running time: O(n^2))
        - If it turns out to be slow (the recursion depths exceed c log n, for some constant c),
        - Then it stops the current call to QuickSort algorithm and switches to HeapSort algorithm (Guaranteed Running time: O(n log n))
        - It's a QuickSort algorithm with worst running time: O(n log n)
    - **Partial Sorting**:
        - Input: An array A[1 . . . n], an integer k: 1 ≤ k ≤ n
        - Output: The last k elements of a sorted version of A
        -       PartialSort(A[1 . . . n], k)
                BuildHeap(A)
                for i from 1 to k:
                    print(A.ExtractMax())
        - BuildHeap Running Time: O(n)
        - Printing: the last k elements of a sorted version of A: O(k * log n)
        - Running time: O(n + k log n)
        - if k = O(n / log n) => **Running time = O(n)**
        - E.g. Printing the last 102 elements of a sorted version of an array of 1024 elements:
            - It takes a linear time
            - if n = 1024 = 2^10 then k = 2^10 / log 2^10 = 1024 / 10 = 102
- For more details:
    - UC San Diego Course:[Overview & Naive Implementations](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/3_priority_queues_and_disjoint_sets/03_1_priority_queues_intro.pdf)
    - UC San Diego Course:[Binary Heaps](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/3_priority_queues_and_disjoint_sets/03_2_priority_queues_heaps.pdf)

</details>

<details>
<summary>Priority Queues: d-ary Heap</summary>

- In a **d-ary heap** nodes on all levels have exactly **d children** except for possibly the last one
- Its height is about: ***Log_d n***
    - An efficient implementation is a **Complete D-ary Tree** in an **Array**
    -            Operations:    0-based index     1-based index array
                  Parent(i):     ⌊ i / d ⌋         ⌊ i / d ⌋
               1st child(i):     d * i + 1         d * i
               2nd child(i):     d * i + 2         d * i + 1
                    ...             ...               ...
              d-th child(i):     d * i + d         d * i + d - 1
    -                           Time Complexity   Comment
                   GetMax():     O(1)              or GetMin()
               ExtractMax():     O(d * Log_d n)    See running time of SiftDown
                  Insert(i):     O(Log_d n)
                  SiftUp(i):     O(Log_d n)        On each level, there is only 1 comparison: child vs. parent
                SiftDown(i):     O(d * Log_d n)    On each level, there are d comparisons among d children
          ChangePriority(i):     O(d * Log_d n)
                  Remove(i):     O(d * Log_d n)

</details>

<details>
<summary>Disjoint Sets</summary>

- It's also called **Union-Find data structure**
- It's a data structure that keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets
- A 1st efficient implementation is **Union by Rank Heuristic**: 
    - It consists of a **Tree** in **2 Arrays**
    - Each set is a rooted tree
    - The ID of a set is the root of the tree
    - Array 1: **Parent**[1 ... n], Parent[i] is the parent of i, or i if it is the root
    - Array 2: **Rank**[1 ... n], Rank[i] = height of subtree which root is i, rank of the tree's root = 0
    - MakeSet(i):
        - It creates a singleton set {i}
        - It consists of a tree with a single node: parent[i] = i
    - Find(i):
        - It returns the ID of the set that is containing i
        - It consists of the root of the tree where i belongs
    - Union(i, j):
        - It merges 2 sets containing i and j
        - It consists of merging 2 trees
        - For effenciency purposes, it must keep the resulting tree as shallow as possible
        - It hang the shorter tree under the root of the longer one (we'll use **rank** array here)
        - The resulted tree height = the longer tree height if the 2 trees height are different
        - The resulted tree height = the height of one of the trees + 1 if the 2 trees height are equal:
        -                       Time Complexity
                MakeSet(x):      O(1)
                   Find(x):      O(tree height) = O(log n) 
               Union(x, y):      O(tree height) = O(log n) 
- A 2nd more efficient implementation is **Path Compression Heuristic**:
    - We keep the same data structure as the Union by rank heuristic implementation
    - When finding the root of a tree for a particular node i, reattach each node from the traversed path to the root
    - From an initially empty disjoint set, we make a sequence of m operations including n calls to MakeSet:
        - The total running time is O(m log∗(n))
        - The **Amortized time** of a single operation is: **O(log∗(n))**
        -                       Time Complexity
                MakeSet(x):      O(1)
                   Find(x):      O(log*(n)) = O(1) if n ≤ 2^65536
               Union(x, y):      O(log*(n)) = O(1) if n ≤ 2^65536
        - For more details about log*(n), see [Prerequisites](#prerequisites)
- Programming Languages:
    - Python:
    - C++:
    - Java:
- Use Cases:
    - Keep track of the connected compoents of an undirected graph
        - To determine whether 2 vertices belong to the same component
        - To determine whether adding an edge between 2 vertices would result in a cycle
    - **Kruskal's algorithm**:
        - It's used to find the minimum spanning tree of a graph
        - [For more details](#graph-algorithms)
    - In a maze (a grid with walls): Is a given cell B reachable from another given cell A?
        - Build disjoint sets where each non-wall cell represent a singleton set
            for each cell c in maze:
                if c isn't a wall MakeSet(c)
        - Modify disjoint sets above so that if a path between A and B exists, then A and B are in the same set
            for each cell c in maze:
                for each neighbor n of c:
                    Union(c, n)
        - Check is a path between A and B exists:
            IsReachable(A, B)
                return Find(A) = Find(B)
    - Building a Network:
- Related Problems:
    - [Find whether individual x is a friend of individual y](https://github.com/hamidgasmi/algorithms-datastructures/issues/33)
    - [Dish Owner](https://github.com/hamidgasmi/algorithms-datastructures/issues/35)
    - [Galactik Football](https://github.com/hamidgasmi/algorithms-datastructures/issues/36)
    - [Merging tables](https://github.com/hamidgasmi/algorithms-datastructures/issues/32)
    - [Jam Board](https://github.com/hamidgasmi/algorithms-datastructures/issues/37)
    - [The Last Droid](https://github.com/hamidgasmi/algorithms-datastructures/issues/40)
    - [Substrings and Repetitions](https://github.com/hamidgasmi/algorithms-datastructures/issues/38)
    - [Tiptoe through the tulips](https://github.com/hamidgasmi/algorithms-datastructures/issues/39)
    - [Ada Farm](https://github.com/hamidgasmi/algorithms-datastructures/issues/34)
- For more details:
    - UC San Diego Course:[Overview & Naive Implementations](https://github.com/hamidgasmi/algorithms-datastructures/tree/master/2-data-sructures-fundamentals/3_priority_queues_and_disjoint_sets)
    - UC San Diego Course:[Efficient Implementations](https://github.com/hamidgasmi/algorithms-datastructures/blob/master/2-data-sructures-fundamentals/3_priority_queues_and_disjoint_sets/03_4_disjoint_sets_efficient.pdf)
    - [Tutorial](https://www.topcoder.com/community/competitive-programming/tutorials/disjoint-set-data-structures/)

</details>

<details>
<summary>Hashing</summary>
</details>

<details>
<summary>Binary Search Trees</summary>
</details>

---

## Graph Algorithms

---

## NP-Complete Problem

---

## String Processing and Pattern Matching Algorithms

---

## Dynamic Programming: Applications In Machine Learning and Genomics 

---

## Graph Algorithms in Genome Sequencing

---

## References

<details>
<summary>Whitepapers & Books</summary>

- [The Algorithm Design Manual](http://mimoza.marmara.edu.tr/~msakalli/cse706_12/SkienaTheAlgorithmDesignManual.pdf) by Steven S. Skiena

- [Algorithm](http://algorithmics.lsi.upc.edu/docs/Dasgupta-Papadimitriou-Vazirani.pdf) by S. Dasgupta,C. H.Papadimitriou,andU. V. Vazirani

</details>

<details>
<summary>Talks & Courses</summary>

- [UC San Diego MicroMasters Program](https://www.edx.org/micromasters/ucsandiegox-algorithms-and-data-structures)
- Princeton University Coursera Courses:
    - [Algorithms, Part I](https://www.coursera.org/learn/algorithms-part1/home/welcome)
    - [Algorithms, Part II](https://www.coursera.org/learn/algorithms-part2/home/welcome)
- [Grokking the Coding Interview: Patterns for Coding Questions](https://www.educative.io/courses/grokking-the-coding-interview)

</details>

<details>
<summary>Articles</summary>

- [14 Patterns to Ace Any Coding Interview Question](https://hackernoon.com/14-patterns-to-ace-any-coding-interview-question-c5bb3357f6ed)
- [Solving Coding Problems With PEDAC](https://medium.com/launch-school/solving-coding-problems-with-pedac-29141331f93f)
- [Interview Questions (and answers)](http://readyforsoftwareinterview.blogspot.com/)
- [How To Approach Any Algorithm Interview Without Panicking](https://www.freecodecamp.org/news/how-to-approach-any-algorithm-interview-without-panicking-b6d7ae5c050/)
- [Top 10 Algorithms for Coding Interview](https://www.programcreek.com/2012/11/top-10-algorithms-for-coding-interview/)

</details>

---
