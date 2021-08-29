# Lecture 3

# Algorithms

- [Lecture 3](#lecture-3)
- [Algorithms](#algorithms)
	- [Characteristics of an Algorithm](#characteristics-of-an-algorithm)
	- [How to Write an Algorithm?](#how-to-write-an-algorithm)
		- [Example](#example)
	- [Algorithm Analysis](#algorithm-analysis)
	- [Algorithm Complexity](#algorithm-complexity)
	- [Space Complexity](#space-complexity)
	- [Time Complexity](#time-complexity)
	- [Greedy Algorithm](#greedy-algorithm)
		- [Example - Counting Coins](#example---counting-coins)
	- [Divide and Conquer](#divide-and-conquer)
		- [Divide/Break](#dividebreak)
		- [Conquer/Solve](#conquersolve)
		- [Merge/Combine](#mergecombine)
		- [Examples](#examples)
	- [Dynamic Programming](#dynamic-programming)
	- [Comparison](#comparison)
		- [Example](#example-1)
	- [Sorting](#sorting)
	- [Bubble Sort](#bubble-sort)
		- [**Applications**](#applications)
		- [**Algorithm**](#algorithm)
		- [**Implementation**](#implementation)
		- [Specifications](#specifications)
	- [Insertion Sort](#insertion-sort)
		- [Applications](#applications-1)
		- [Algorithm](#algorithm-1)
		- [Implementation](#implementation-1)
		- [Specifications](#specifications-1)
	- [Heap Sort](#heap-sort)
		- [Applications](#applications-2)
		- [Algorithm](#algorithm-2)
		- [Implementation](#implementation-2)
		- [Specifications](#specifications-2)
	- [Merge Sort](#merge-sort)
		- [Applications](#applications-3)
		- [Algorithm](#algorithm-3)
		- [Implementation](#implementation-3)
		- [Specifications](#specifications-3)
	- [Summary](#summary)
		- [Some good references](#some-good-references)
	- [Searching](#searching)
	- [Linear Search](#linear-search)
		- [Implementation](#implementation-4)
	- [Binary Search](#binary-search)
		- [Implementation](#implementation-5)
- [Questions](#questions)

An algorithm is a step-by-step procedure, which defines a set of instructions to be executed in a certain order to get the desired output. Algorithms are generally created independent of underlying languages, i.e. an algorithm can be implemented in more than one programming language.

From the data structure point of view, following are some important categories of algorithms −

- **Search** − Algorithm to search an item in a data structure.
- **Sort** − Algorithm to sort items in a certain order.
- **Insert** − Algorithm to insert item in a data structure.
- **Update** − Algorithm to update an existing item in a data structure.
- **Delete** − Algorithm to delete an existing item from a data structure.

    ![Image](Images/Lecture%203%201e70e09c443846958159b1baa301b2c2/i-heard-you-like-algorithms-soiused-an-algorithm-to-pick-23469909.jpg)

## Characteristics of an Algorithm

*Not all procedures can be called an algorithm.* An algorithm should have the following characteristics −

- **Unambiguous** − Algorithm should be clear and unambiguous. Each of its steps (or phases), and their inputs/outputs should be clear and must lead to only one meaning.
- **Input** − An algorithm should have 0 or more well-defined inputs.
- **Output** − An algorithm should have 1 or more well-defined outputs, and should match the desired output.
- **Finiteness** − Algorithms must terminate after a finite number of steps.
- **Feasibility** − Should be feasible with the available resources.
- **Independent** − An algorithm should have step-by-step directions, which should be independent of any programming code.

## How to Write an Algorithm?

There are no well-defined standards for writing algorithms. Rather, it is problem and resource-dependent. Algorithms are never written to support a particular programming code.

We write algorithms in a step-by-step manner, but it is not always the case. Algorithm writing is a process and is executed after the problem domain is well-defined. That is, we should know the problem domain, for which we are designing a solution.

### Example

Let's try to learn algorithm-writing by using an example.

**Problem** − Design an algorithm to add two numbers and display the result.

```
Step 1 − START
Step 2 − declare three integersa,b &cStep 3 − define values ofa &bStep 4 − add values ofa &bStep 5 − store output ofstep 4 tocStep 6 − printcStep 7 − STOP

```

Algorithms tell the programmers how to code the program. Alternatively, the algorithm can be written as −

```
Step 1 − START ADD
Step 2 − get values ofa &bStep 3 − c ← a + b
Step 4 − display c
Step 5 − STOP

```

In design and analysis of algorithms, usually the second method is used to describe an algorithm. It makes it easy for the analyst to analyze the algorithm ignoring all unwanted definitions. He can observe what operations are being used and how the process is flowing.

Writing **step numbers**, is optional.

We design an algorithm to get a solution of a given problem. A problem can be solved in more than one ways.

![https://www.tutorialspoint.com/data_structures_algorithms/images/problem_solutions.jpg](https://www.tutorialspoint.com/data_structures_algorithms/images/problem_solutions.jpg)

Hence, many solution algorithms can be derived for a given problem. The next step is to analyze those proposed solution algorithms and implement the best suitable solution.

## Algorithm Analysis

The efficiency of an algorithm can be analyzed at two different stages, before implementation and after implementation. 

They are the following −

- **A Priori Analysis** − This is a theoretical analysis of an algorithm. The efficiency of an algorithm is measured by assuming that all other factors, for example, processor speed, are constant and have no effect on the implementation.
- **A Posterior Analysis** − This is an empirical analysis of an algorithm. The selected algorithm is implemented using programming language. This is then executed on target computer machine. In this analysis, actual statistics like running time and space required, are collected.

Algorithm analysis deals with the execution or running time of various operations involved. The **running time** of an operation can be defined as the number of computer instructions executed per operation.

## Algorithm Complexity

Suppose **X** is an algorithm and **n** is the size of input data, the time and space used by the algorithm X are the two main factors, which decide the efficiency of X.

- **Time Factor** − Time is measured by counting the number of key operations such as comparisons in the sorting algorithm.
- **Space Factor** − Space is measured by counting the maximum memory space required by the algorithm.

The complexity of an algorithm **f(n)** gives the running time and/or the storage space required by the algorithm in terms of **n** as the size of input data.

## Space Complexity

Space complexity of an algorithm represents the amount of memory space required by the algorithm in its life cycle. The space required by an algorithm is equal to the sum of the following two components −

- A fixed part that is a space required to store certain data and variables, that are independent of the size of the problem. For example, simple variables and constants used, program size, etc.
- A variable part is a space required by variables, whose size depends on the size of the problem. For example, dynamic memory allocation, recursion stack space, etc.

Space complexity S(P) of any algorithm P is S(P) = C + SP(I), where C is the fixed part and S(I) is the variable part of the algorithm, which depends on instance characteristic I. Following is a simple example that tries to explain the concept −

```
Algorithm: SUM(A, B)
Step 1 -  START
Step 2 -  C ← A + B + 10
Step 3 -  Stop

```

Here we have three variables A, B, and C and one constant. Hence S(P) = 1 + 3. Now, space depends on data types of given variables and constant types and it will be multiplied accordingly.

## Time Complexity

![Image](Images/Lecture%203%201e70e09c443846958159b1baa301b2c2/0_XHbfteIJTLQHOHzO.jfif)

The time complexity of an algorithm represents the amount of time required by the algorithm to run to completion. Time requirements can be defined as a numerical function T(n), where T(n) can be measured as the number of steps, provided each step consumes constant time.

For example, the addition of two n-bit integers takes **n** steps. Consequently, the total computational time is T(n) = c ∗ n, where c is the time taken for the addition of two bits. Here, we observe that T(n) grows linearly as the input size increases.

## Greedy Algorithm

Greedy is an algorithmic paradigm that builds up a solution piece by piece, always choosing the next piece that offers the most obvious and immediate benefit. Greedy algorithms are used for optimization problems.

At every step, we can make a choice that looks best at the moment, and we get the optimal solution of the complete problem. 

If a Greedy Algorithm can solve a problem, then it generally becomes the best method to solve that problem as the Greedy algorithms are in general more efficient than other techniques like Dynamic Programming. 

But Greedy algorithms cannot always be applied. For example, the **[Fractional Knapsack](https://www.geeksforgeeks.org/fractional-knapsack-problem/)** problem can be solved using Greedy, but **[0-1 Knapsack](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)** cannot be solved using Greedy. Following are some standard algorithms that are Greedy algorithms. 

**1) [Kruskal’s Minimum Spanning Tree (MST)](https://www.geeksforgeeks.org/greedy-algorithms-set-2-kruskals-minimum-spanning-tree-mst/):** In Kruskal’s algorithm, we create a MST by picking edges one by one. The Greedy Choice is to pick the smallest weight edge that doesn’t cause a cycle in the MST constructed so far.

**2) [Prim’s Minimum Spanning Tree](https://www.geeksforgeeks.org/prims-algorithm-using-priority_queue-stl/):** In Prim’s algorithm also, we create a MST by picking edges one by one. We maintain two sets: a set of the vertices already included in MST and the set of the vertices not yet included. The Greedy Choice is to pick the smallest weight edge that connects the two sets. 

**3) [Dijkstra’s Shortest Path](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/):** Dijkstra’s algorithm is very similar to Prim’s algorithm. The shortest-path tree is built up, edge by edge. We maintain two sets: a set of the vertices already included in the tree and the set of the vertices not yet included. The Greedy Choice is to pick the edge that connects the two sets and is on the smallest weight path from source to the set that contains not yet included vertices. 

[Images](Images/Lecture%203%201e70e09c443846958159b1baa301b2c2/download.jfif)

**4) [Huffman Coding](https://www.geeksforgeeks.org/greedy-algorithms-set-3-huffman-coding/):** Huffman Coding is a loss-less compression technique. It assigns variable-length bit codes to different characters. The Greedy Choice is to assign the least bit length code to the most frequent character.

The greedy algorithms are sometimes also used to get an approximation for Hard optimization problems. For example, **[Traveling Salesman Problem](https://www.geeksforgeeks.org/travelling-salesman-problem-set-1/)** is an NP-Hard problem. A Greedy choice for this problem is to pick the nearest unvisited city from the current city at every step. These solutions don’t always produce the best optimal solution but can be used to get an approximately optimal solution.

Let us consider the **[Activity Selection problem](http://en.wikipedia.org/wiki/Activity_selection_problem)** as our first example of Greedy algorithms. Following is the problem statement. You are given n activities with their start and finish times. Select the maximum number of activities that can be performed by a single person, assuming that a person can only work on a single activity at a time. 

Example:

```cpp
Example 1 : Consider the following 3 activities sorted by
by finish time.
     start[]  =  {10, 12, 20};
     finish[] =  {20, 25, 30};
A person can perform at mosttwo activities. The
maximum set of activities that can be executed
is {0, 2} [ These are indexes in start[] and
finish[] ]

Example 2 : Consider the following 6 activities
sorted by by finish time.
     start[]  =  {1, 3, 0, 5, 8, 5};
     finish[] =  {2, 4, 6, 7, 9, 9};
A person can perform at mostfour activities. The
maximum set of activities that can be executed
is {0, 1, 3, 4} [ These are indexes in start[] and
finish[] ]
```

The greedy choice is to always pick the next activity whose finish time is least among the remaining activities and the start time is more than or equal to the finish time of the previously selected activity. We can sort the activities according to their finishing time so that we always consider the next activity as minimum finishing time activity.

### Example - Counting Coins

This problem is to count to a desired value by choosing the least possible coins and the greedy approach forces the algorithm to pick the largest possible coin. If we are provided coins of ₹ 1, 2, 5 and 10 and we are asked to count ₹ 18 then the greedy procedure will be −

- **1** − Select one ₹ 10 coin, the remaining count is 8
- **2** − Then select one ₹ 5 coin, the remaining count is 3
- **3** − Then select one ₹ 2 coin, the remaining count is 1
- **4** − And finally, the selection of one ₹ 1 coins solves the problem

Though, it seems to be working fine, for this count we need to pick only 4 coins. But if we slightly change the problem then the same approach may not be able to produce the same optimum result.

For the currency system, where we have coins of 1, 7, 10 value, counting coins for value 18 will be absolutely optimum but for count like 15, it may use more coins than necessary. For example, the greedy approach will use 10 + 1 + 1 + 1 + 1 + 1, total 6 coins. Whereas the same problem could be solved by using only 3 coins (7 + 7 + 1)

Hence, we may conclude that the greedy approach picks an immediate optimized solution and may fail where global optimization is a major concern.

Most networking algorithms use the greedy approach.

There are lots of similar problems that uses the greedy approach to find an optimum solution.

## Divide and Conquer

n divide and conquer approach, the problem in hand, is divided into smaller sub-problems and then each problem is solved independently. When we keep on dividing the subproblems into even smaller sub-problems, we may eventually reach a stage where no more division is possible. Those "atomic" smallest possible sub-problem (fractions) are solved. The solution of all sub-problems is finally merged in order to obtain the solution of an original problem.

![https://www.tutorialspoint.com/data_structures_algorithms/images/divide_and_conquer.jpg](https://www.tutorialspoint.com/data_structures_algorithms/images/divide_and_conquer.jpg)

Broadly, we can understand **divide-and-conquer** approach in a three-step process.

### Divide/Break

This step involves breaking the problem into smaller sub-problems. Sub-problems should represent a part of the original problem. This step generally takes a recursive approach to divide the problem until no sub-problem is further divisible. At this stage, sub-problems become atomic in nature but still represent some part of the actual problem.

### Conquer/Solve

This step receives a lot of smaller sub-problems to be solved. Generally, at this level, the problems are considered 'solved' on their own.

### Merge/Combine

When the smaller sub-problems are solved, this stage recursively combines them until they formulate a solution of the original problem. This algorithmic approach works recursively and conquer & merge steps works so close that they appear as one.

### Examples

The following computer algorithms are based on **divide-and-conquer** programming approach −

- Merge Sort
- Quick Sort
- Binary Search
- Strassen's Matrix Multiplication
- Closest pair (points)

There are various ways available to solve any computer problem, but the mentioned are a good example of divide and conquer approach.

## Dynamic Programming

Dynamic programming approach is similar to divide and conquer in breaking down the problem into smaller and yet smaller possible sub-problems. But unlike, divide and conquer, these sub-problems are not solved independently. Rather, results of these smaller sub-problems are remembered and used for similar or overlapping sub-problems.

Dynamic programming is used where we have problems, which can be divided into similar sub-problems, so that their results can be re-used. Mostly, these algorithms are used for optimization. Before solving the in-hand sub-problem, dynamic algorithm will try to examine the results of the previously solved sub-problems. The solutions of sub-problems are combined in order to achieve the best solution.

So we can say that −

- The problem should be able to be divided into smaller overlapping sub-problem.
- An optimum solution can be achieved by using an optimum solution of smaller sub-problems.
- Dynamic algorithms use Memoization.

## Comparison

In contrast to greedy algorithms, where local optimization is addressed, dynamic algorithms are motivated for an overall optimization of the problem.

In contrast to divide and conquer algorithms, where solutions are combined to achieve an overall solution, dynamic algorithms use the output of a smaller sub-problem and then try to optimize a bigger sub-problem. Dynamic algorithms use Memoization to remember the output of already solved sub-problems.

### Example

The following computer problems can be solved using dynamic programming approach −

- Fibonacci number series
- Knapsack problem
- Tower of Hanoi
- All pair shortest path by Floyd-Warshall
- Shortest path by Dijkstra
- Project scheduling

Dynamic programming can be used in both top-down and bottom-up manner. And of course, most of the times, referring to the previous solution output is cheaper than recomputing in terms of CPU cycles.

---

## Sorting

Sorting refer to arranging data in a particular format. The importance of sorting lies in the fact that data searching can be optimized to a very high level, if data is stored in a sorted manner. The most common example we experience every day is sorting clothes or other items on an e-commerce website either by lowest-price to highest, or list by popularity, or some other order.

We'll be looking at four sorting algorithms : Bubble Sort, Insertion Sort, Heap Sort and Merge Sort.

## Bubble Sort

![Images](Images/Lecture%203%201e70e09c443846958159b1baa301b2c2/0_PgiLG7NytqKAh8WT_.png)

### **Applications**

Due to its simplicity, bubble sort is often used to introduce the concept of a sorting algorithm.

In computer graphics it is popular for its capability to detect a very small error (like swap of just two elements) in almost-sorted arrays and fix it with just linear complexity (2n). For example, it is used in a polygon filling algorithm, where bounding lines are sorted by their x coordinate at a specific scan line (a line parallel to x axis) and with incrementing y their order changes (two elements are swapped) only at intersections of two lines

### **Algorithm**

We compare adjacent elements and see if their order is wrong (i.e 

```jsx
a[i] > a[j] for 1 <= i < j <= size of array; 
```

if array is to be in ascending order, and vice-versa). If yes, then swap them. We continue this process up to we do not reach the point where we have had no swaps in the array.

### **Implementation**

```cpp
//  implementation of Bubble sort
#include <stdio.h>

void swap(int *xp, int *yp)
{
	int temp = *xp;
	*xp = *yp;
	*yp = temp;
}

// An optimized version of Bubble Sort
void bubbleSort(int arr[], int n)
{
int i, j;
bool swapped;
for (i = 0; i < n-1; i++)
{
	swapped = false;
	for (j = 0; j < n-i-1; j++)
	{
		if (arr[j] > arr[j+1])
		{
		swap(&arr[j], &arr[j+1]);
		swapped = true;
		}
	}

	// IF no two elements were swapped by inner loop, then break
	if (swapped == false)
		break;
}
}
```

### Specifications

**Worst and Average Case Time Complexity:**
O(n*n). Worst case occurs when array is reverse sorted.

**Best Case Time Complexity:**
O(n). Best case occurs when array is already sorted.

**Auxiliary Space:**
O(1)

**Boundary Cases:**
Bubble sort takes minimum time (Order of n) when elements are already sorted.

## Insertion Sort

### Applications

Insertion sort is used when number of elements is small. It can also be useful when input array is almost sorted, only few elements are misplaced in complete big array.

### Algorithm

We iterate from second to the last element of the array and keep every time we move through one element we ensure that the sub-list before it is sorted at all times.

Let's see this through an example. Consider the following array: 25, 17, 31, 13, 2 

Since the array has 5 elements we'll have 4 iterations. 

After 1st iteration, array will be : 17, 25, 31, 13, 2  //since  17 < 25

After 2nd iteration, array will be : 17, 25, 31, 13, 2  //since 31 > 17 and 31 > 25

After 3rd iteration, array will be : 13, 17, 25, 31, 2 //since 13 < 31 and 13 < 25 and 13 < 17

After 4th iteration, array will be: 2, 13, 17, 25, 31 //since 2 < 31 and 2 < 25 and 2 < 17 and 2 < 13

### Implementation

```cpp
// C++ program for insertion sort
#include <bits/stdc++.h>
using namespace std;

/* Function to sort an array using insertion sort*/
void insertionSort(int arr[], int n)
{
	int i, key, j;
	for (i = 1; i < n; i++)
	{
		key = arr[i];
		j = i - 1;

		/* Move elements of arr[0..i-1], that are
		greater than key, to one position ahead
		of their current position */
		while (j >= 0 && arr[j] > key)
		{
			arr[j + 1] = arr[j];
			j = j - 1;
		}
		arr[j + 1] = key;
	}
}
```

### Specifications

**Time Complexity:**
O(n^2)

**Auxiliary Space:**
O(1)

**Boundary Cases:**
Insertion sort takes maximum time to sort if elements are sorted in reverse order. And it takes minimum time (Order of n) when elements are already sorted.

A very interesting video on **[Bubble Sort v/s Insertion Sort and some Analysis](https://www.youtube.com/watch?v=TZRWRjq2CAg&ab_channel=udiprod)**

## Heap Sort

### Applications

Heap sort algorithm has limited uses because Quick Sort and Merge Sort are better in practice. Nevertheless, the Heap data structure itself is enormously used. See [Applications of Heap Data Structure.](https://www.geeksforgeeks.org/applications-of-heap-data-structure/)

### Algorithm

A **heap** is a tree data structure that satisfies the following properties:

1. **Shape property**: Heap is always a complete binary tree which means that all the levels of a tree are fully filled. There should not be a node which has only one child. Every node except leaves should have two children then only a heap is called as a complete binary tree.
2. **Heap property**: All nodes are either greater than or equal to or less than or equal to each of its children. This means if the parent node is greater than the child node it is called as a max heap. Whereas if the parent node is lesser than the child node it is called as a min heap.

**Working of Heap Sort:**

Suppose an array consists of N distinct elements in memory, then the heap sort algorithm works as follows:

1. To begin with, a heap is built by moving the elements to its proper position within the array. This means that as the elements are traversed from the array the root, its left child, its right child are filled in respectively forming a binary tree.
2. In the second phase, the root element is eliminated from the heap by moving it to the end of the array.
3. The balance elements may not be a heap. So again steps 1 and 2 are repeated for the balance elements. The procedure is continued until all the elements are eliminated.

Refer to the following 2-min video to see this logic in a run-through example: [https://www.youtube.com/watch?v=MtQL_ll5KhQ&ab_channel=GeeksforGeeks](https://www.youtube.com/watch?v=MtQL_ll5KhQ&ab_channel=GeeksforGeeks)

### Implementation

```cpp
// C++ program for implementation of Heap Sort
#include <iostream>

using namespace std;

// To heapify a subtree rooted with node i which is
// an index in arr[]. n is size of heap
void heapify(int arr[], int n, int i)
{
	int largest = i; // Initialize largest as root
	int l = 2 * i + 1; // left = 2*i + 1
	int r = 2 * i + 2; // right = 2*i + 2

	// If left child is larger than root
	if (l < n && arr[l] > arr[largest])
		largest = l;

	// If right child is larger than largest so far
	if (r < n && arr[r] > arr[largest])
		largest = r;

	// If largest is not root
	if (largest != i) {
		swap(arr[i], arr[largest]);

		// Recursively heapify the affected sub-tree
		heapify(arr, n, largest);
	}
}

// main function to do heap sort
void heapSort(int arr[], int n)
{
	// Build heap (rearrange array)
	for (int i = n / 2 - 1; i >= 0; i--)
		heapify(arr, n, i);

	// One by one extract an element from heap
	for (int i = n - 1; i > 0; i--) {
		// Move current root to end
		swap(arr[0], arr[i]);

		// call max heapify on the reduced heap
		heapify(arr, i, 0);
	}
}
```

### Specifications

**Time Complexity:**
 Time complexity of heapify is O(Logn). Time complexity of createAndBuildHeap() is O(n) and the overall time complexity of Heap Sort is O(nLogn).

## Merge Sort

### Applications

1. **[Inversion Count Problem](https://www.geeksforgeeks.org/counting-inversions/)**
2. Used in **[External Sorting](http://en.wikipedia.org/wiki/External_sorting)**

### Algorithm

Merge sort is one of the most efficient sorting algorithms. It works on the principle of Divide and Conquer. Merge sort repeatedly breaks down a list into several sublists until each sublist consists of a single element and merging those sublists in a manner that results into a sorted list.

For example, Consider an array: 25, 17, 31, 13, 2

Step 1: divide the array into halves until single element arrays are achieved:

25, 17, 31   13, 2

25, 17   31   13  2

25   17  31  13  2

Step 2: start merging by checking that the order is maintained

17, 25  13, 31  2

13, 17, 25, 31  2

2, 13, 17, 25, 31  //final sorted array

### Implementation

```cpp
// example of merge sort in C++
// merge function take two intervals
// one from start to mid
// second from mid+1, to end
// and merge them in sorted order

void merge(int *Arr, int start, int mid, int end) {
	// create a temp array
	int temp[end - start + 1];

	// crawlers for both intervals and for temp
	int i = start, j = mid+1, k = 0;

	// traverse both arrays and in each iteration add smaller of both elements in temp 
	while(i <= mid && j <= end) {
		if(Arr[i] <= Arr[j]) {
			temp[k] = Arr[i];
			k += 1; i += 1;
		}
		else {
			temp[k] = Arr[j];
			k += 1; j += 1;
		}
	}

	// add elements left in the first interval 
	while(i <= mid) {
		temp[k] = Arr[i];
		k += 1; i += 1;
	}

	// add elements left in the second interval 
	while(j <= end) {
		temp[k] = Arr[j];
		k += 1; j += 1;
	}

	// copy temp to original interval
	for(i = start; i <= end; i += 1) {
		Arr[i] = temp[i - start]
	}
}

// Arr is an array of integer type
// start and end are the starting and ending index of current interval of Arr

void mergeSort(int *Arr, int start, int end) {

	if(start < end) {
		int mid = (start + end) / 2;
		mergeSort(Arr, start, mid);
		mergeSort(Arr, mid+1, end);
		merge(Arr, start, mid, end);
	}
}
```

### Specifications

**Time Complexity:** 
Sorting arrays on different machines. Merge Sort is a recursive algorithm and time complexity can be expressed as following recurrence relation. 
T(n) = 2T(n/2) + θ(n)

The above recurrence can be solved either using the Recurrence Tree method or the Master method. It falls in case II of Master Method and the solution of the recurrence is θ(nLogn). Time complexity of Merge Sort is  θ(nLogn) in all 3 cases (worst, average and best) as merge sort always divides the array into two halves and takes linear time to merge two halves.

**Auxiliary Space:** 
O(n)

## Summary

![Images](Images/Lecture%203%201e70e09c443846958159b1baa301b2c2/Untitled.png)

Source : InterviewBit

### Some good references

To have a good visualization of all the sorting algorithms over different type of data, refer to this link [https://www.toptal.com/developers/sorting-algorithms](https://www.toptal.com/developers/sorting-algorithms) for animations

See working of sorting algorithms using go-through examples via a short 2-3 min video, refer here: [https://www.youtube.com/playlist?list=PL9xmBV_5YoZOZSbGAXAPIq1BeUf4j20pl](https://www.youtube.com/playlist?list=PL9xmBV_5YoZOZSbGAXAPIq1BeUf4j20pl)

## Searching

The searching algorithms are used to search or find one or more than one element from a dataset. These type of algorithms are used to find elements from a specific data structures.

Searching may be sequential or not. If the data in the dataset are random, then we need to use sequential searching. Otherwise we can use other different techniques to reduce the complexity.

We'll see two searching algorithms: Linear Search and Binary Search

## Linear Search

This is the most basic way of searching. We navigate one-by-one through all the elements to find the element of our choice.

Thus, **Time Complexity** is **O(n)**  and **Space Complexity**  is **O(1)**
Worst case when the element is at the last cell and best case if present at the first cell

### Implementation

```cpp
//C++ implementation of Linear Search
int linSearch(int array[], int size, int key) {
   for(int i = 0; i<size; i++) {
      if(array[i] == key) //search key in each places of the array
         return i; //location where key is found for the first time
   }
   return -1; //when the key is not in the list
}
```

This is barely used because of being extremely slow. Let's see a better implementation in Binary Search.

## Binary Search

In this, we use the benefit of sorting an array. We first sort the array and then compare the element with the middle element, this brings up three cases:

1.  Middle element > Required element :  we search for the number in the left part of the array
2. Middle element < Required element :  we search for the number in the right part of the array
3. Middle element = Required element : return because element is found

    ![Image](Images/Lecture%203%201e70e09c443846958159b1baa301b2c2/g7r4mnsok78z.jpg)

We keep on iterating this process of breaking into halves and comparing with the middle element, until we find the element or we have reached the leftmost/rightmost point n the array and still haven't found the Required element (element not present case)

**Complexity of Search** 

- **Time Complexity:** O(1) for the best case. O(log2 n) for average or worst case.
- **Space Complexity:** O(1)

### Implementation

```cpp
//C++ implementation of Binary Search
int binarySearch(int array[], int start, int end, int key) {
   if(start <= end) {
      int mid = (start + (end - start) /2); //mid location of the list
      if(array[mid] == key)
         return mid;
      if(array[mid] > key)
         return binarySearch(array, start, mid-1, key);
         return binarySearch(array, mid+1, end, key);
   }
   return -1;
}
```

A slower walk through of the above algorithms can be seen here : **[https://www.studytonight.com/data-structures/search-algorithms](https://www.studytonight.com/data-structures/search-algorithms)**

# Questions

<!-- [All Questions](https://www.notion.so/e634b265cfb24feb9d41f7fd800d3528) -->

|                |                                                                                                                                                            |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|Searching and Sorting|[Find a fixed point(Value equal to index) in a given array](https://practice.geeksforgeeks.org/problems/value-equal-to-index-value1330/1)                                                                                                                                                                 |
|                     |[Search in a rotated sorted array](https://leetcode.com/problems/search-in-rotated-sorted-array/)                                                                                                                                                                                |
|                     |[Square root of an integer](https://practice.geeksforgeeks.org/problems/count-squares3649/1)                                                                                                                                                                              |
|                     |[Maximum and minimum of an array using minimum number of comparisions](https://practice.geeksforgeeks.org/problems/middle-of-three2926/1)                                                                                                                                                                            |
|                     |[Optimum location of a point to minimize total distance](https://www.geeksforgeeks.org/optimum-location-point-minimize-total-distance/#:~:text=We%20need%20to%20find%20a,set%20of%20points%20is%20minimum.&text=In%20above%20figure%20optimum%20location,is%20minimum%20obtainable%20total%20distance.)|
|                     |[Find the repeating and the missing](https://practice.geeksforgeeks.org/problems/find-missing-and-repeating2512/1)                                                                                                                                                                 |
|                     |[Find the majority element](https://practice.geeksforgeeks.org/problems/majority-element/0)                                                                                                                                                                               |
|                     |[Searching in an array where adjacent differ by atmost k](https://www.geeksforgeeks.org/searching-array-adjacent-differ-k/)                                                                                                                                                                             |
|                     |[Find a pair with given difference](https://practice.geeksforgeeks.org/problems/find-pair-given-difference/0)                                                                                                                                                                     |
|                     |[Find 4 elements that sum to a given value](https://practice.geeksforgeeks.org/problems/find-all-four-sum-numbers/0)                                                                                                                                                                      |
|                     |[Maximum sum such that no 2 elements are adjacent](https://practice.geeksforgeeks.org/problems/stickler-theif/0)                                                                                                                                                                                 |
|                     |[Count triplet with sum smaller than given value](https://practice.geeksforgeeks.org/problems/count-triplets-with-sum-smaller-than-x5549/1)                                                                                                                                                     |
|Binary Search Tree   |[Deletion of a node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/)                                                                                                                                                                                          |
|                     |[Find min and max value in BST](https://practice.geeksforgeeks.org/problems/minimum-element-in-bst/1)                                                                                                                                                                         |
|                     |[Find inorder successor and predecessor in BST](https://practice.geeksforgeeks.org/problems/predecessor-and-successor/1)                                                                                                                                                                      |
|Greedy               |[Job sequencing problem](https://practice.geeksforgeeks.org/problems/job-sequencing-problem/0)                                                                                                                                                                         |
|                     |[Huffman encoding](https://practice.geeksforgeeks.org/problems/huffman-encoding/0)                                                                                                                                                                               |
|                     |[Water Connection Problem](https://practice.geeksforgeeks.org/problems/water-connection-problem/0)                                                                                                                                                                       |
|                     |[Fractional Knapsack Problem](https://practice.geeksforgeeks.org/problems/fractional-knapsack/0)                                                                                                                                                                            |
|Dynamic Programming  |[Optimal Strategy for a game](https://practice.geeksforgeeks.org/problems/optimal-strategy-for-a-game/0)                                                                                                                                                                    |
|                     |[Optimal Binary Search Tree](https://www.geeksforgeeks.org/optimal-binary-search-tree-dp-24/)                                                                                                                                                                              |
|                     |[Palindrome Partition Problem](https://practice.geeksforgeeks.org/problems/palindromic-patitioning4845/1)                                                                                                                                                                    |
|                     |[Word Wrap Problem](https://practice.geeksforgeeks.org/problems/word-wrap/0)                                                                                                                                                                                      |
|                     |[Mobile Numeric Keypad Problem](https://practice.geeksforgeeks.org/problems/mobile-numeric-keypad5456/1)                                                                                                                                                                      |
