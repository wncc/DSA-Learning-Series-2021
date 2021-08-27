# Trees

# Introduction to Trees:

We read about some linear data structures like an array, linked list, stack and queue in which all the elements are arranged in a sequential manner. A tree is used to represent data arranged in an hierarchical manner.

A tree data structure is defined as a collection of objects or entities known as nodes that are linked together to represent hierarchy.

A tree data structure is a non-linear data structure because it does not store in a sequential manner. 

### Terms related to trees:

A simple example of a tree would be a family tree. Many of the terms used to describe the components of a tree are in fact inspired from the representation of a family tree.

![Images](Images\trees1.png)

- Root

The root node is the topmost node in the tree hierarchy. A root node does not have any parent node.

- Parent node

If a node contains any sub-node, then that node is said to be the parent of that sub-node.

- Child node

If the node is a descendant of any node, then the node is known as a child node.

- Sibling nodes

The nodes that have the same parent are known as sibling nodes.

- Leaf node

The nodes of the tree, which do not have any child node, are called a leaf nodes. A leaf node is the bottom-most node of the tree. There can be any number of leaf nodes present in a general tree.

### Properties of nodes :

- Depth of node

The depth of node x can be defined as the length of the path from the root to the node x. In the diagram, the depth of node M is 3. By this convention, the depth of the root node is 0.

- Height of node

The height of node x can be defined as the longest path from the node x to a leaf node. In the diagram, the height of node A is 2. By this convention, the height of a leaf node is 0.

## Binary Trees:

A tree whose elements have at most 2 children is called a binary tree. Since each element in a binary tree can have only 2 children, we typically name them the left and right child.

![Image](trees2.jpg)

A binary tree node should store the following information:

1. The value stored in the node
2. Pointer to the left node
3. Pointer to the right node

It can be implemented in C++ in the following way:

```cpp
struct Node
{
	Node *left, *right;
	int value;
}
```

An example of the code for representing the following tree : 

![Image](trees3.png)

```cpp
#include <iostream>
using namespace std;

struct Node 
{
	int value;
	Node* left;
	Node* right;

	Node(int val)//Constructor initialiazes new node
	{
		value = val;
		left = NULL;
		right = NULL;
	}
};

int main()
{
	//Root
	Node* root = new Node(1); 

	//Level 1
	root->left = new Node(2);
	root->right = new Node(3);

	//Level 2
	root->left->left = new Node(5);
	root->left->right = new Node(6);

	return 0;
}
```

## Binary Search Trees:

Binary Search Tree is a form of binary tree in which nodes are arranged in a specific order :

1. The value of all the nodes on the left sub-tree is less than the value of the node.
2. The value of all the nodes on the right sub-tree is greater than the value of the node.

This rule will be applied recursively to all the left and right subtrees of the root node being considered.

Steps to create a BST using the following values in order : 10, 12, 5, 4, 20, 8, 7, 15, 13

![Image](trees4.png)

A nice visualization of Binary Search Trees : [https://www.cs.usfca.edu/~galles/visualization/BST.html](https://www.cs.usfca.edu/~galles/visualization/BST.html) 

### Basic operations:

The binary search tree data structure should support 2 basic operations:

1. Insert : To insert a new node in the BST. This is used for creating the binary search tree.
2. Find : To search for a given element in our tree and return true or false accordingly if the element is present or not. This is the major use of the BST(hence the name).

### Insertion

As you have seen in the illustration, to insert any element in the BST, we start at the root. If the element is smaller than the root value, then we go to the left subtree or else to the right subtree. We continue this procedure recursively until we reach a NULL node. That is where the node with the given value will be inserted.

```cpp
void insert(Node* &curr_root, int val) 
//The current node we are at is passed by reference
{
	if(curr_root == NULL) //Insert a new node at this location
	{
		curr_root = new Node(val);
		curr_root->left = curr_root->right = NULL;
	}
	else
	{
		if(val == curr_root->value) //Node with that value already exists
		{
			return;
		}
		if(val < curr_root->value)
		{
			insert(curr_root->left, val);
		}
		else
		{
			insert(curr_root->right, val);
		}
	}
}
```

### Searching

The procedure for searching for a node is very similar to the insertion algorithm. In fact, while inserting a new node, we actually searched for the position at which a node with the given value should have been present, and that is where we created the new node. This time we have to search for the node and return true if we found it or false if our search ultimately reaches a NULL node. The program can be implemented by tweaking the insert function a bit:

```cpp
bool find(Node* &curr_root, int val)
{
	if(curr_root == NULL)
	{
		return false;
	}
	if(curr_root->value == val)
	{
		return true;
	}
	else
	{
		if(val < curr_root->value)
		{
			return find(curr_root->left, val);
		}
		else
		{
			return find(curr_root->right, val);
		}
	}
}
```

Here is the complete code for creating the BST given in the illustration and searching for a few elements :

```cpp
#include <iostream>
using namespace std;

struct Node //Same as binary tree
{
	int value;
	Node* left;
	Node* right;

	Node(int val)//Constructor initialiazes new node
	{
		value = val;
		left = NULL;
		right = NULL;
	}
};

void insert(Node* &curr_root, int val) 
{
	//Body of the insert function mentioned earlier
}

bool find(Node* &curr_root, int val)
{
	//Body of the find function mentioned earlier
}

int main()
{
	Node* BST = NULL;
	int values[] = {10, 12, 5, 4, 20, 8, 7, 15, 13};
	for(int i=0;i<9;i++)
	{
		insert(BST, values[i]);
	}
	int elements[] = {2,20,79,10};
	for(int i=0;i<4;i++)
	{
		if(find(BST, elements[i])) { cout << "FOUND\n"; }
		else { cout << "NOT FOUND\n"; }
	}
	return 0;
}
```

Output:

```cpp
NOT FOUND
FOUND
NOT FOUND
FOUND
```

What will be the time complexity of search operation?

 In the worst case for a Binary Search tree which might look like this :

![Image](trees5.png)

The search operation might have to go through all elements, resulting in a worst case time complexity of O(N). However in a balanced binary tree, the height of the left and right subtree of any node differs by not more than 1. Therefore, searching in a balanced binary tree is analogous to the Binary Search algorithm discussed earlier, where we compared the given value with the middle element of the subarray being considered. Similarly, searching for an element in a balanced binary search tree is O(logN).

An example of balanced binary tree :

![Image](trees6.png)

Self-balancing binary search trees are used for storing (key, value) pairs constituting a *map* from the C++ standard library.

### Traversal of Binary Trees:

Unlike linear data structures (Array, Linked List, Queues, Stacks) which have only one logical way to traverse them, trees can be traversed in different ways. Following are the generally used ways for traversing trees.

1. Inorder : (Left → Root → Right)

    In this traversal method, the left subtree is visited first, then the root and later the right sub-tree.

2. Preorder : (Root → Left → Right)

    In this traversal method, the root node is visited first, then the left subtree and finally the right subtree.

3. Postorder : (Left → Right → Root)

    In this traversal method, the left subtree is visited first, then the right subtree and finally the root node.

All the three common traversal methods can be implemented using similar recursive functions.

Inorder, Preorder and Postorder traversals of the given binary tree : 

![Image](trees3.png)

```cpp
#include <iostream>
using namespace std;

struct Node 
{
	int value;
	Node* left;
	Node* right;

	Node(int val)//Constructor initialiazes new node
	{
		value = val;
		left = NULL;
		right = NULL;
	}
};

void inorder(Node* curr_node) //Left -> Root -> Right
{
	if(curr_node == NULL) { return; }
	//Left :
	inorder(curr_node->left);
	//Current Root :
	cout << curr_node->value << " ";
	//Right :
	inorder(curr_node->right);
}

void preorder(Node* curr_node) //Root -> Left -> Right
{
	if(curr_node == NULL) { return; }
	//Current Root :
	cout << curr_node->value << " ";
	//Left :
	preorder(curr_node->left);
	//Right :
	preorder(curr_node->right);
}

void postorder(Node* curr_node) //Left -> Right -> Root
{
	if(curr_node == NULL) { return; }
	//Left :
	postorder(curr_node->left);
	//Right :
	postorder(curr_node->right);
	//Current Root :
	cout << curr_node->value << " ";
}

int main()
{
	//Root
	Node* root = new Node(1); 
	//Level 1
	root->left = new Node(2);
	root->right = new Node(3);
	//Level 2
	root->left->left = new Node(5);
	root->left->right = new Node(6);
	cout << "Inorder Traversal : ";
	inorder(root); cout << endl;
	cout << "Preorder Traversal : ";
	preorder(root); cout << endl;
	cout << "Postorder Traversal : ";
	postorder(root); cout << endl;
	return 0;
}
```

Output :

```cpp
Inorder Traversal : 5 2 6 1 3 
Preorder Traversal : 1 2 5 6 3 
Postorder Traversal : 5 6 2 3 1
```

How would the respective traversals of a Binary Search Tree be? Which of the 3 traversal method would output the values in a sorted order? Try implementing the functions for the Binary Search Tree we had constructed earlier.

Try these out :

1. Given a binary tree, write a program that checks whether it is a Binary Search Tree or not.
2. Find the total number of leaf nodes in a given Binary Tree. 
3. Find the kth largest element in a Binary Search Tree. Some useful links for this problem:
    - [https://www.geeksforgeeks.org/kth-largest-element-in-bst-when-modification-to-bst-is-not-allowed/](https://www.geeksforgeeks.org/kth-largest-element-in-bst-when-modification-to-bst-is-not-allowed/)
    - [https://www.geeksforgeeks.org/kth-largest-element-bst-using-constant-extra-space/](https://www.geeksforgeeks.org/kth-largest-element-bst-using-constant-extra-space/)

For further exploring BST, you can practice questions from here :

1. A few nice questions sorted by difficulty : [https://www.hackerearth.com/practice/data-structures/trees/binary-search-tree/practice-problems/](https://www.hackerearth.com/practice/data-structures/trees/binary-search-tree/practice-problems/)
2. [https://leetcode.com/tag/binary-search-tree/](https://leetcode.com/tag/binary-search-tree/)
3. To explore what else can be done with Binary Trees, try to attempt the problems given here :

    [https://medium.com/techie-delight/binary-search-tree-bst-practice-problems-and-interview-questions-ea13a6731098](https://medium.com/techie-delight/binary-search-tree-bst-practice-problems-and-interview-questions-ea13a6731098)