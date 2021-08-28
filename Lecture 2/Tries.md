# Tries

- [Tries](#tries)
- [Intro to Trie](#intro-to-trie)
    - [What is a trie ?](#what-is-a-trie-)
    - [Advantages of a Trie :](#advantages-of-a-trie-)
    - [Disadvantages of a Trie :](#disadvantages-of-a-trie-)
    - [Implementing a Trie :](#implementing-a-trie-)
    - [Application Problems of Trie :](#application-problems-of-trie-)
- [Operations on a Trie :](#operations-on-a-trie-)
    - [Insertion](#insertion)
    - [Search](#search)

# Intro to Trie

### What is a trie ?

A trie is a special kind of tree used to store strings. The maximum number of children of a node is equal to the size of the alphabet. 

**Costs of a Trie (worst case):**

Here, k is the length pf the word and n is the total number of words

- Space : O(n*k)
- Insertion : O(k)
- LookUp/ Search : O(k)

### Advantages of a Trie :

1. With Trie, we can insert and find strings in **O(L)** time where L represents a single word's length. This is obviously faster than BST (O(N*L), *where N is the total number of words*). This is also faster than Hashing because of the ways it is implemented. We do not need to compute any hash function. No collision handling is required (like we do in **[open addressing](https://www.geeksforgeeks.org/hashing-set-3-open-addressing/)** and **[separate chaining](https://www.geeksforgeeks.org/hashing-set-2-separate-chaining/)**)
2. Another advantage of Trie is, we can **[easily print all words in alphabetical order](https://www.geeksforgeeks.org/sorting-array-strings-words-using-trie/)** which is not easily possible with hashing.
3. We can efficiently do

### Disadvantages of a Trie :

The main disadvantage of tries is that they need a lot of memory for storing the strings. For each node, we have too many node pointers(equal to the number of characters of the alphabet)

### Implementing a Trie :

A Trie is a special data structure used to store strings that can be visualized like a graph. It consists of nodes and edges. Each node consists of at max 26 children and edges connect each parent node to its children. We need to mark the last node of every key as end of word node. A Trie node field isEndOfWord is used to distinguish the node as end of word node.

![Image](Images/Tries%20ebbde95dec6641ddaa072f0be93b9ea3/Untitled.png)

Fig showing a sample trie. Source: [https://www.interviewcake.com/concept/java/trie](https://www.interviewcake.com/concept/java/trie)

```cpp
//C++ implementation of a Trie
#include <bits/stdc++.h>
using namespace std;
  
const int ALPHABET_SIZE = 26;
  
// trie node
struct TrieNode
{
    struct TrieNode *children[ALPHABET_SIZE];
  
    // isEndOfWord is true if the node represents
    // end of a word
    bool isEndOfWord;
};

// Returns new trie node (initialized to NULLs)
struct TrieNode *getNode(void)
{
    struct TrieNode *pNode =  new TrieNode;
  
    pNode->isEndOfWord = false;
  
    for (int i = 0; i < ALPHABET_SIZE; i++)
        pNode->children[i] = NULL;
  
    return pNode;
}

int main()
{
    // Input keys (use only 'a' through 'z'
    // and lower case)
    string keys[] = {"the", "a", "there",
                    "answer", "any", "by",
                     "bye", "their" };
    int n = sizeof(keys)/sizeof(keys[0]);
  
    struct TrieNode *root = getNode();
  
    // Construct trie
    for (int i = 0; i < n; i++)
        insert(root, keys[i]);

		return 0;
}
```

### Application Problems of Trie :

- [**To count number of distinct substrings**](https://www.hackerrank.com/challenges/ctci-contacts/problem)
- **[Prefix-based problems](http://codeforces.com/contest/455/problem/B)**
- **[Prefix search (or auto-complete) with Trie](https://www.geeksforgeeks.org/auto-complete-feature-using-trie/)**.

# Operations on a Trie :

### Insertion

Every character of the input key is inserted as an individual Trie node. Note that the children is an array of pointers (or references) to next level trie nodes. The key character acts as an index into the array children. If the input key is new or an extension of the existing key, we need to construct non-existing nodes of the key, and mark end of the word for the last node. If the input key is a prefix of the existing key in Trie, we simply mark the last node of the key as the end of a word. The key length determines Trie depth.

```cpp
//Inserting a word in a Trie
// If not present, inserts key into trie
// If the key is prefix of trie node, just
// marks leaf node
void insert(struct TrieNode *root, string key)
{
    struct TrieNode *pCrawl = root;
  
    for (int i = 0; i < key.length(); i++)
    {
        int index = key[i] - 'a';
        if (!pCrawl->children[index])
            pCrawl->children[index] = getNode();
  
        pCrawl = pCrawl->children[index];
    }
  
    // mark last node as leaf
    pCrawl->isEndOfWord = true;
}
```

### Search

Searching for a key is similar to insert operation, however, we only compare the characters and move down. The search can terminate due to the end of a string or lack of key in the trie. In the former case, if the isEndofWord field of the last node is true, then the key exists in the trie. In the second case, the search terminates without examining all the characters of the key, since the key is not present in the trie.

```cpp
//Searching for a key in te Trie
// Returns true if key presents in trie, else
// false
bool search(struct TrieNode *root, string key)
{
    struct TrieNode *pCrawl = root;
  
    for (int i = 0; i < key.length(); i++)
    {
        int index = key[i] - 'a';
        if (!pCrawl->children[index])
            return false;
  
        pCrawl = pCrawl->children[index];
    }
  
    return (pCrawl != NULL && pCrawl->isEndOfWord);
}
```


