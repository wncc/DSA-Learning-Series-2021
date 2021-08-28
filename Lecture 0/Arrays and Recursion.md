# Arrays and Recursion

- [Arrays and Recursion](#arrays-and-recursion)
	- [Arrays:](#arrays)
		- [Initializing arrays](#initializing-arrays)
		- [Indexing](#indexing)
		- [Arrays and Pointers](#arrays-and-pointers)
		- [Function calls involving arrays](#function-calls-involving-arrays)
		- [2-D arrays:](#2-d-arrays)
		- [Vectors](#vectors)
	- [Recursion:](#recursion)
		- [Example - Searching](#example---searching)

## Arrays:

An array can be thought of as a collection of variables at contiguous memory locations. This makes it easy to store and work with a number of items of the same time together.

### Initializing arrays

The syntax used for declaring arrays in C and C++ is:

`data_type array_name[array_size];`

For example:

```cpp
int primes[5] = {2, 3, 5, 7, 11};
double values[15];
double arr[] = {1.2, 3.3, 6.5, 4.1}; //The array size is inferred from the assignment
```

### Indexing

C++ and many other programming language use 0-based indexing for arrays. The first element of the array is given index 0, the second is given 1 and so on. The elements of the array can be accessed by the "[]" operator. All the operations that can be done with a variable can also be done with elements of the array of the same type.

```cpp
int store[1000]; 
cin >> store[0] >> store[1]; //Gets the first and second element of the array as input
store[5] = 100;  //Assigns 100 to the 6th element of the array
int sum = store[0] + store[1];
```

***Typeset the question below in a box in the margin***

What if you try to access an index out of bounds of the array?

In C/C++, this would lead to something called an "Undefined Behavior". The program may generate wrong values, fail to terminate, or terminate with an error message. The behavior literally is "undefined!"

### Arrays and Pointers

In C and C++, the name of the array by itself is defined to have the value equal to the starting address from where the array is stored. However, the value associated with the name of the array, (eg. arr) can not be changed, it always means the address of arr[0]. The array name by itself yields a memory location, so it can be treated as a pointer :

```cpp
int arr[6] = {1,2,3,4,5,6};
arr[2] = 21; //Changes 3rd element of array to 21
*(arr+2) = 42; //Again changes the third element of array to 21
```

What do you think will be the output of the following program :

```cpp
int arr[5] = {1,2,3,4,5};
int *p = arr;
int *q = &arr[0];
p[0] = 68;
q[1] = 70;
cout << arr[0] << " " << arr[1];
```

***Typeset the question below in a box in the margin***

You can read more about arrays and pointers here : [http://people.scs.carleton.ca/~mjhinek/W13/COMP2401/notes/Arrays_and_Pointers.pdf](http://people.scs.carleton.ca/~mjhinek/W13/COMP2401/notes/Arrays_and_Pointers.pdf)

### Function calls involving arrays

Generally, to pass an array to a function we have to pass 2 arguments, the name of the array and the length of the array as the name of the array only gives the starting address of the array. The array name can be passed to the function as a pointer  as follows :

```cpp
int sum1(int* arr, int n) 
{
	int sum = 0;
	for(int i=0;i<n;i++)
	{
		sum+=arr[i];
	}
	return sum;
}
int sum2(int arr[], int n) //This is equivalent to the previous function.
{
	int sum = 0;
	for(int i=0;i<n;i++)
	{
		sum+=arr[i];
	}
	return sum;
}

int main()
{
	int values[5] = {2,3,1,4,7};
	int s1 = sum1(values,5);
	int s2 = sum1(values,5);
}
```

One important thing to note is that although the array name is passed by value, the elements of the array are in fact passed by reference to the function, because the array name actually points to the memory location of the starting of the array. Hence, elements stored in an array can be affected by operations taking place in a function :

```cpp
#include <iostream>
using namespace std;

void change(int* arr)
{
		arr[2] = 37;
}

int main()
{
		int values[5] = {1, 2, 3, 4, 5};
		change(values);
		cout << values[2]; // Prints 37
}
```

### 2-D arrays:

Often we need 2-D or even higher dimensional arrays to represent matrices or for data structures that will be introduced later. 2-D arrays can be declared in a similar way :

```cpp
int arr[m][n]; //This causes space for m*n variables of type int to be allotted
```

2-D arrays can be thought of as an array of 1-D arrays for practical purposes. They can even be initialized in the following way:

```cpp
int arr[3][2] = {{2,3}, {4,5}, {1,8}};
```

2-D arrays can be passed to a function. However, in the called function, at least the second dimension of the array must be given as a compile time constant :

```cpp
void func(int arr[][20], int n)
{
		//body
}
```

### Vectors

The template class vector in C++ can be thought of as dynamic arrays which can resize itself automatically when elements are inserted or deleted. To use vectors, you have to include the header file <vector>.  (`#include <vector>`)

Many different constructors are available for initializing vectors:

```cpp
vector<int> v1; //Creates empty vector v1
vector<double> v2(100); //Creates vector of 100 elements, each of type double
vector<int> v3(10,1); //Vector of 10 ints, each initialized to 1
```

The elements of a vector can be accessed in the same way as arrays(v[index]). Some useful vector functions:

```cpp
vector<int> v1(5, 1);
v1.push_back(8); // Inserts the 6th element(8) to the end of the vector
int sz = v1.size(); // Returns the current size of the vector
v1.pop_back(); // Removes the last element of the vector
v1.clear(); // Removes all elements of the vector
```

You can learn more about vectors and functions associated here : [https://www.cplusplus.com/reference/vector/vector/](https://www.cplusplus.com/reference/vector/vector/)

## Recursion:

Recursion means defining a problem as a simpler version of itself. Recursion generally finds use when a problem can be split of reduced into a simplified version of itself. Recursive functions include a call to itself, gradually simplifying the problem towards the base cases whose solutions are known, on reaching which the function finally terminates. Therefore, a recursive function has these 3 main parts :

- A base case - The simplest case for a problem, whose solution is already known. (Eg: The sum of elements of an empty array is 0). The base case is where the function finally terminates and without it the function will either be stuck in an infinite loop or give an error for not returning any value (non-void function).
- Reduction of the problem - The problem is simplified into subproblems, gradually working to get to the base case
- A call to itself

### Example - Searching

Let's see how recursion can be used to find the index of an element in an array.

1. **Linear Search**: Each element of the array is compared sequentially to the element we need to find, and the function returns the index as soon as we find the required element or -1 if we reach the end of the array and the element is not found :

```cpp
int search(int* arr, int elem, int index, int n)
{
		if(n==0) // Base case, the element is not present in an empty array
		{
				return -1;
		}

		if(arr[0]==elem)
		{
				return index;
		}

		return search(arr+1,elem,index+1,n-1); // Recursive call to itself
}
```

Here, in every recursive call, the subarray arr[1,...,n-1] of length 1 less than the current array is passed into the function. Thus the problem is reduced into a smaller problem and it ultimately reaches the base case if the element is not present in the array.

2. **Binary Search**: If the elements of an array are already sorted, we can search for an element faster as we know the relative ordering of the elements. 

Say the array is sorted in non-decreasing order. In binary search, we first compare the required element with the middle element. If the middle element is bigger, then the required element can be present only in the subarray to the left of the middle, as only those elements are smaller than the mid and vice versa if the middle element is smaller.  

If the middle element is equal to the required element, then we have already found it! 

 

```cpp
// low - first index of the subarray being considered
// high - last index of the subarray being considered
int bsearch(int arr[], int x, int low, int high)
{
		if (high < low) //Base case
		{
				return -1;
		}
    int mid = low + (high - low) / 2;
    if (arr[mid] == x)
        return mid;
    else if (arr[mid] > x)
        return bsearch(arr, x, low, mid - 1); //Recursive call with subarray to the left
    else
        return bsearch(arr, x, mid + 1, high); //Recursive call with subarray to the right
}
```

Reaching the base case implies that there is no subarray of length 1 that contains the required element, hence the element is not present in the array.

Try these out!

1. A palindrome is a sequence which is the same forwards or backwards. Write a program that checks if a given sequence of length n is a palindrome or not. Try to solve this using a recursive function as well.
2. Recursive functions can be generally implemented using loops as well. Try to implement the linear and binary search algorithms mentioned earlier using for-loops. Keep the base-case in mind or the program might get stuck in an infinite loop!
3. Euclid's algorithm states that : **For 2 positive integers m and n, if m%n=0, then gcd(m,n) = n; else gcd(m,n) = gcd(n,m%n)**. Thus you have the base case and the recursive relation respectively. Using this information, write a program that calculates the gcd of 2 positive numbers.