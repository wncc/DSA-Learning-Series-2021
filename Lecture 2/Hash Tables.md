- [Hash Tables:](#hash-tables)
    - [Introduction:](#introduction)
    - [Hashing (Hash Function):](#hashing-hash-function)
    - [Collision Resolution:](#collision-resolution)
    - [Operations:](#operations)
    - [Time Complexity:](#time-complexity)
    - [Applications:](#applications)


# Hash Tables:

### Introduction:

![Image](Images/Hash%20Tables%20962a66b264284e23ae4473fcee5959b1/Untitled.png)

Hash Table is a data structure in which elements are stored in an associative manner, i.e. each element in a hash table is assigned a key to make searching for and inserting elements really fast irrespective of the size of the data. We generally use the value of the element to be added as the key itself. For example, each student in IIT Bombay is assigned a unique roll number(key) to store their information.

In a normal unsorted array, searching for an element takes O(n) time in a linear fashion but you can search for an element using its key ideally in O(1) time in a hash table(you'll soon learn that this is not always the case).  

### Hashing (Hash Function):

In a hash table, a new index is generated using the keys and the element corresponding to that key is stored at that index in an array or a list. It is not feasible to directly use keys as indexes of the array as the keys may be really large. This is done with the help of a hash function.

Let h(x) be a hash function then index=h(key). The value returned by the function may also be referred to as hash or hash value. 

![Image](Images/Hash%20Tables%20962a66b264284e23ae4473fcee5959b1/Untitled%201.png)

Sometimes, a hash function may return the same value for more than 1 key, this is called a hash collision. A good hash function is one which has minimum number of collisions and does a uniform distribution of keys across all indexes of the table, not leading to clustering.

The simplest hash function is (key%size) where % is the modulo operator for an integer key and size is size of the table. For a string as a key, a hash function may be sum of ascii values of all the characters in the string modulo size. It is preferable that the size be a prime number for modulo operations. 

A better hash function may be floor( (k*A mod 1)*s ) where k is key, s is size and A is a constant between 0 and 1. This function will avoid collision and clustering.      

### Collision Resolution:

Collision handling is divided into 2 major ways- separate chaining and open addressing.

1. **Separate Chaining** :

In this method, the hash table is an array of linked lists and and all the keys returning the same index are stored in a common linked list. The advantage of this is that the hash table will never fill up as we can just add more elements to a list. In order to search for an element, we transverse through the linked list at the index of its key. Thus, the complexity is no longer O(1) and increased to number of elements in the specific linked list. 

![Images](Images/Hash%20Tables%20962a66b264284e23ae4473fcee5959b1/Untitled%202.png)

                                      h(k3)=h(k4) so they are stored in the same linked list.

2. **Open Addressing:** 

This method does not store multiple elements in the same slot. A maximum of 1 element can be stored in each slot.

Let h(x) be the index computed using hash function and s be the size of the table. We can perform open addressing in multiple ways like: 

- Linear Probing: Here we linearly probe to the next slot in the array until we find an empty slot.      This means if slot h(x)%s is full, we check (h(x)+1)%s. If that is also full, we check (h(x)+2)%s and so on until we find an empty slot to store that element in.                                                             Consider a hash function h(x)=x%7 and we insert the series of keys 50,700,85,92,72,101 below :

![Images](Images/Hash%20Tables%20962a66b264284e23ae4473fcee5959b1/Untitled%203.png)

- Quadratic Probing: Instead of jumping 1 slot, we look for i^2th slot in the i th iteration.                  If h(x)%s is full, we try (h(x)+1*1)%s, then we try (h(x)+2*2)%s ... until we find an empty slot.
- Double Hashing: We use another hash function h2(x) and look for i*h2(x) th slot in i th iteration in case of collision. If h(x)%s is full, we look in the slot (h(x)+1*h2(x))%s, then we try (h(x)+2*h2(x))%s and so on until we find an empty slot.

The table may get full in open addressing when all the slots are filled and clustering may also be a problem. But there is no waste of empty space here like chaining(some slots may remain unfilled in chaining), so there is a better memory utilization.

### Operations:

The basic operations we can perform in a hash table are searching for an element, inserting and deleting elements. 

Here's an implementation of a hash table in C++:

```cpp
//implementation of a hash table using array
//you can also try to implement it using a linked list 

#include <iostream>
using namespace std;

//This hash table will follow linear probing and take only positive keys as elements

struct HashTable{
    private:
    int size; //size is the maximum number of elements you can insert in a hash table
    int * table; 
    int hash_func(int key); //returns index

    public:
    HashTable(int s);
    int search(int key); //returns index at which key is present or -1 if key is absent
    void insert_elem(int key);
    void delete_elem(int key);
};

int HashTable::hash_func(int key){
    int index=key%size; //this is the hash function
    return index;
}

HashTable::HashTable(int s){
    size=s;
    table= new int[size];
    for(int i=0;i<size;i++) {table[i]=-1;} // -1 means that slot is empty
}

int HashTable::search(int key){
    int index=hash_func(key);
    int initial_index=index;
    /*We will iterate through the table and check if the element at that 
			index is 'key' until we hit an empty slot.
	    This is because of linear probing, our key can be anywhere between the 
			current index and the index of the next empty slot. */
    while(table[index]!=-1){ 
        if(table[index]==key){
            return index;
        }
        else{index=(index+1)%size;}

        if(index==initial_index){break;} 
			//this means we have iterated through the entire table and didn't find the key
    }

    return -1; //key not found
}

void HashTable::insert_elem(int key){

    int index=hash_func(key);
    int initial_index=index;

    //searching for the next empty slot to insert key in to follow linear probing
    while(table[index]!=-1){
        index=(index+1)%size;

        if(index==initial_index){ 
				//we iterated through entire table and there were no empty slots
            cout<<"Table is full"<<endl;
            return;
        }
    }
    table[index]=key;
    cout<<"Added element "<<key<<" at index "<<index<<endl;
}

void HashTable::delete_elem(int key){
    int index=search(key); //we will delete the element if we find it on searching
    if(key==-1){
        cout<<"Cannot delete as element is absent."<<endl;
    }
    else{
        table[index]=0; 
        /*We have placed 0 as a dummy element to ensure the correctness of hash table.
        This ensures that there is not an empty gap between 2 elements which have the 
				same hash value but are stored at different indexes.
        Placing dummy elements is one of the disadvantages of open addressing. */
        cout<<"Deleted element "<<key<<endl;
    }
}

int main(){
    struct HashTable* myhash;
    myhash= new HashTable(10);
    myhash->insert_elem(13);
    myhash->insert_elem(2);
    myhash->insert_elem(22); 
    cout<<myhash->search(22)<<endl;
    myhash->delete_elem(22);
    cout<<myhash->search(22)<<endl; 
}
```

Output:

Added element 13 at index 3
Added element 2 at index 2
Added element 22 at index 4
4
Deleted element 22
-1

The element 22 was added at the index 4 in spite of having hash value as 2 to follow linear probing because index 2 and 3 were already occupied. 22 was also found at index 4 before deleting and not found after deleting(-1 implies not found).

### Time Complexity:

The ideal time complexity of all the operations are O(1). But in the case of hash collisions, the operations are slower and may even have a worst complexity of O(n).

### Applications:

- Associative arrays: Hash tables are used to implement associative arrays- arrays whose indices are strings or other complicated objects.
- Hash tables are used in indexing of data and as disk-based data structures.
- They are also used in cryptographic encoding and decoding of passwords.

Questions for practice:

1. [https://codeforces.com/problemset/problem/1520/D](https://codeforces.com/problemset/problem/1520/D) 
2. [https://www.hackerearth.com/practice/data-structures/hash-tables/basics-of-hash-tables/practice-problems/algorithm/lets-plot-this-47a575ed/](https://www.hackerearth.com/practice/data-structures/hash-tables/basics-of-hash-tables/practice-problems/algorithm/lets-plot-this-47a575ed/)
3. [https://codeforces.com/problemset/problem/1527/C](https://codeforces.com/problemset/problem/1527/C)
4. [https://www.codechef.com/problems/RECNDNOS](https://www.codechef.com/problems/RECNDNOS) 
5.
