# Linked Lists

## Introduction

### Prerequisites

In this article we will be writing a good amount of code. Make sure you are refreshed and have a decent grasp over pointers, dynamic memory allocation and basic OOP concepts.

1. Read about pointers from [https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)
2. Dynamic Memory Allocation using `new` and `delete`. Read [https://www.geeksforgeeks.org/new-and-delete-operators-in-cpp-for-dynamic-memory/](https://www.geeksforgeeks.org/new-and-delete-operators-in-cpp-for-dynamic-memory/)
3. Classes in C++: [https://www.geeksforgeeks.org/c-classes-and-objects/](https://www.geeksforgeeks.org/c-classes-and-objects/)

Additionally, you can also read the excellent book "Let Us C++" by Yashavant Kanetkar to increase your understanding of C++.

### Data structures and linked lists

Programs often need to store, retrieve and manipulate data. An efficient program will ensure that these operations like adding, deleting and searching for data are as efficient as possible. Special "constructs" have been devised called data structures. A data structure is a data organization, management, and storage format that enables efficient access and modification.

We will study the data structure called linked list in this article. A linked list is a linear collection of data elements whose order is not given by their physical placement in memory. Instead, each element points to the next. It is a data structure consisting of a collection of nodes which together represent a sequence. Linked lists are of two types:

1. Singly linked list: each node points only to the next element
2. Doubly linked list: each node points to both, the next and the previous element.

![Image](Images\lists1.png)

A graphical representation of singly linked list

![Image](Images\lists2.png)

A graphical representation of doubly linked list

### Implementation of a singly linked list

> You will see the `nullptr` keyword a lot of times in the programs below. Here is what it means: in C++, when a pointer is created, it points to some random location in the memory. When we write `int *p = nullptr` we are creating a pointer and pointing it to "nothing." Null is Latin for nothing. This is very useful as we might be required to check if the pointer points to some meaningful location in the future.

Let's start with some C++ code. In the example below we set up the nodes of the linked list and then link them

```cpp
#include <iostream>
using namespace std;

// the basic unit of a singly linked list
struct node
{
    int val;
    node *next;
};

int main()
{
    node *n1 = new node();
    node *n2 = new node();
    node *n3 = new node();

    // set the values for the nodes
    n1->val = 42;
    n2->val = 271;
    n3->val = 314;

    // setup the linked list
    n1->next = n2;
    n2->next = n3;
    n3->next = nullptr;

    // transverse through the linked list
    node *n = n1;
    while (n != nullptr)
    {
        cout << n->val << " ";
        n = n->next;
    }

    // free the allocated memory
    delete n3;
    delete n2;
    delete n1;

    return 0;
}
```

Output: `42 271 314`

Notice how the links are formed, we set each node's `next` pointer to the node which comes after it. In this example `n1`, `n2` and `n3` together form what is called a singly linked list.

Also note how we transverse the linked list. We start from `n1` and move to the next node until the `next` is not `nullptr`.

## Operations on linked lists

### Inserting nodes at head

In the above example, we had to do the creation linking of the nodes ourselves in `main`. We can automate this process by writing a class `sllist` whose member function will encapsulate the above logic. In order to do this we will have to maintain a pointer to the head of the linked list. **The head of a linked list is the most recently added element.** In the above code, the head would point to `n3`.

![Image](Images\lists3.png)

The code below achieves the insertion of nodes at the head. Note that inserting a node at the head is $O(1)$ as all statements are constant time operations. The procedure is:

1. Create a new node `newnode` in memory and set its `val`
2. `newnode->next` will now point to `head`
3. `head` will point to `newnode`

Have a look at the code below, especially the `insert_value` member function.

```cpp
#include <iostream>
using namespace std;

struct node
{
    int val;
    node *next;
};

class sllist
{
private:
    node *head;
    int size;

public:
    // an empty linked list
    sllist()
    {
        head = nullptr;
        size = 0;
    }

    // free the memory allocated to all nodes
    ~sllist()
    {
        node *n = head;
        while (n != nullptr)
        {
            delete n;
            n = n->next;
        }
    }

    int length()
    {
        return size;
    }

    void print()
    {
        node *n = head;
        while (n != nullptr)
        {
            cout << n->val << " ";
            n = n->next;
        }
    }

    void insert_value(int k)
    {
        // allocate memory for a new node and set its val
        node *newnode = new node();
        newnode->val = k;

        // "link" the new node to the node which was created before it
        newnode->next = head;

        // the head points to the most recently created node
        head = newnode;

        size++;
    }
};

int main()
{
    sllist ll;
    ll.insert_value(1);
    ll.insert_value(2);
    ll.insert_value(3);

    ll.print();
    cout << endl << ll.length();

    return 0;
}
```

Output:

```cpp
3 2 1
3
```

### Searching for a node with a given value

This is simple: visit each node and check if it has the value we are looking for. Additionally, if the value is found, we return a pointer to the node containing this value. If the value is not found we return `nullptr`. We will use this pointer later.

Note than searching is $O(n)$.

Add the following function in the `sllist` class above

```cpp
class sllist
{
    // the code from above

    node *search_value(int k)
    {
        node *n = head;
        while ((n != nullptr) && (n->val != k))
            n = n->next;

        return n;
    }
};
```

We can test `search_value` in the following way

```cpp
int main()
{
    sllist ll;
    ll.insert_value(1);
    ll.insert_value(2);
    ll.insert_value(3);

    cout << "Searching for 1..." << endl;
    node *res = ll.search_value(1);
    if (res != nullptr)
        cout << "Found res->val = " << res->val << endl;
    else
        cout << "Not found!" << endl;

    cout << "Searching for 4..." << endl;
    res = ll.search_value(4);
    if (res != nullptr)
        cout << "Found res->val = " << res->val << endl;
    else
        cout << "Not found!" << endl;

    return 0;
}
```

Output:

```
Searching for 1...
Found res->val = 1
Searching for 4...
Not found!
```

### Deleting a given node

In order to delete a node, we must have a pointer pointing to it. We can obtain this pointer from the `search_value` function.

Deleting a node `p` involves these steps:

1. Find the node previous to `p` , call it `n`
2. Set `n->next` to `p->next`. Thus `n` now points to the node after `p`.
3. Free the memory allocated to `p`.

Deleting is $O(1)$. But deleting requires using `search_value`, so effectively deleting is $O(n)$. 

Add the following code to the `sllist` class

```cpp
class sllist
{
    // ...

    void delete_node(node *p)
    {
        node *n = head;

        // search for the node before p
        while (n->next != p)
            n = n->next;
        
        // node before p must point to node after p
        n->next = p->next;

        // free the memory allocated to the node at p
        delete p;
				size--;
    }
};
```

This function can be used as follows

```cpp
int main()
{
    sllist ll;
    ll.insert_value(1);
    ll.insert_value(2);
    ll.insert_value(3);
    ll.insert_value(4);

    ll.print();
    cout << endl;
    
    // search for the node with val == 3 and delete it
    node *res = ll.search_value(3);
    ll.delete_node(res);
    ll.print();

    return 0;
}
```

Output

```
4 3 2 1 
4 2 1
```

In the above implementation we assume that `delete_node` is given a valid pointer.

## Where next?

With this we cover the basic concepts of linked lists. But there is a lot to explore!

### More operations

The above implementation of singly linked list is quite rudimentary. One can add operations like insert after node, sorting, filtering etc.

Check [https://www.geeksforgeeks.org/data-structures/linked-list/](https://www.geeksforgeeks.org/data-structures/linked-list/) for the implementation of these operations.

### Doubly linked list

Efficiency and applicability of linked lists can be increased if each node stores pointers to both the next and the previous node.

### Applications

Linked lists can be used by themselves or as an implementation base for stacks, queues, etc. You will see these applications later in this course.

## Practice

Solve the following questions to cement the concepts covered above in your memory!

1. [https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)
2. [https://www.geeksforgeeks.org/flattening-a-linked-list/](https://www.geeksforgeeks.org/flattening-a-linked-list/)
3. [https://www.careercup.com/question?id=5717797377146880](https://www.careercup.com/question?id=5717797377146880)
4. [https://practice.geeksforgeeks.org/problem-page.php?pid=700196](https://practice.geeksforgeeks.org/problem-page.php?pid=700196)
5. [https://practice.geeksforgeeks.org/problem-page.php?pid=700013](https://practice.geeksforgeeks.org/problem-page.php?pid=700013)

For even more questions, please check [https://www.geeksforgeeks.org/top-20-linked-list-interview-question/](https://www.geeksforgeeks.org/top-20-linked-list-interview-question/)