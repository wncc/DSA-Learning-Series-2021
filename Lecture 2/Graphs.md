
## Graphs - what are they?

A graph is a non-linear data structure which consists of nodes and edges. Many real-life systems can be considered to be a collection of objects which are linked together to form a network. Some examples of such systems can be roadmaps of cities, electronic circuits, etc. Graphs can be used for representing such networks of entities.

## Graph Terminology

![Image](Images/Graphs%201c69060174364bd09f16c868e62470d5/Untitled.png)

As shown in the figure, every graph can be considered to be consisting of 2 sets, a set of nodes(or vertices) and a set of edges. 2 nodes are said to be connected if there is a path from one to the other. A graph is said to be connected if there is a path between any 2 nodes.

![Image](Images/Graphs%201c69060174364bd09f16c868e62470d5/Untitled%201.png)

### Directed/Undirected graph

Edges can be of two types - Unidirectional and bidirectional. Unidirectional edges have a direction assigned to them. Graphs having such edges are called directed graphs, whereas graphs having bidirectional edges are called undirected edges.

![Image](Images/Graphs%201c69060174364bd09f16c868e62470d5/Untitled%202.png)

### Weighted/Unweighted graph

Edges of a graph can have certain "weights" associated with them. They might be related to the path lengths, or resistances in case of electric circuits, etc. Graphs with edges having weights assigned to them are called weighted graphs.

![Image](Images/Graphs%201c69060174364bd09f16c868e62470d5/Untitled%203.png)

## Representation of Graphs:

### Adjacency List

In the adjacency list representation, each node x in the graph is assigned an adjacency list that consists of nodes to which there is an edge from x. Adjacency lists are the most popular way to represent graphs, and most algorithms can be efficiently implemented using them.

The adjacency list can be in the form of a linked list, a variable sized array or a vector of nodes to which the node being considered is connected to.

Here's an example how vectors can be used for adjacency lists to represent the following graph:

![Image](Images/Graphs%201c69060174364bd09f16c868e62470d5/Untitled%204.png)

```cpp
vector<int> adj[6];//For each index from 1,..,5 we have a vector to store neighbours
```

```cpp
adj[1].push_back(4);
adj[2].push_back(4);
adj[2].push_back(5);
adj[3].push_back(5);
adj[4].push_back(1);
adj[4].push_back(2);
adj[4].push_back(5);
adj[5].push_back(2);
adj[5].push_back(3);
adj[5].push_back(4);
```

For representing weighted graphs, each entry of an adjacency list can be stored as a pair of {node, edge weight}.

Representation of adjacency lists using linked list : [https://www.techiedelight.com/implement-graph-data-structure-c/](https://www.techiedelight.com/implement-graph-data-structure-c/) 

### Adjacency Matrix:

An adjacency matrix is a 2-D array that indicates which edges the graph contains. In an unweighted graph, adj[a][b] = 1 implies that there is an edge between a and b, while adj[a][b] = 0 implies no edge between them. In a weighted graph, adj[a][b] = L can represent an edge of length L between a and b.

![Images](Images/Graphs%201c69060174364bd09f16c868e62470d5/Untitled%205.png)

### Edge List :

An edge list contains all the edges of a graph. This is a convenient way to represent a graph if the algorithm processes all edges of a graph and it is not required to find edges that start at a given node. Edges can be represented explicitly as structs, or as pairs storing the nodes they are connected to.

As structs:

```cpp
struct Node{
	int value;
}
struct Edge{
	int weight;
	Node *from, *to;
}
Edge edgelist[E]; //E -> Total edges in the graph
```

As pairs:

```cpp
vector<pair<int,int>> edgelist;

//To add an edge from 1->2
edgelist.push_back(make_pair(1,2));
```

Representation of graphs in different programming languages : [https://www.geeksforgeeks.org/graph-and-its-representations/](https://www.geeksforgeeks.org/graph-and-its-representations/) 

## Graph Traversal:

Graph traversal algorithms visit all the nodes that can be reached from a given starting node. There are 2 main traversal methods :

### Depth First Search(DFS)

DFS begins at a starting node, and proceeds to all other nodes that are reachable from the starting node using the edges of the graph. Depth-first search always follows a single path in the graph as long as it finds new nodes. After this, it returns to previous nodes and begins to explore other parts of the graph. The algorithm keeps track of visited nodes, so that it processes each node only once.

DFS algorithm can be implemented using stack or by using a recursive function.

A nice visualization of the algorithm implementation using stack : [http://www.btechsmartclass.com/data_structures/graph-traversal-dfs.html](http://www.btechsmartclass.com/data_structures/graph-traversal-dfs.html) 

Implementation with recursive DFS function :

```cpp
vector<int> adj[N]; //Adjacency list representation
bool visited[N] = {}; //Keeps track of nodes we are visiting

void dfs(int a)
{
	if(visited[a]) return;
	visited[a] = true;
	//Process node a, in this case we are printing it
	cout << a << " ";
	for(int i=0;i<adj[a].size();i++)
	{
		dfs(adj[a][i]);
	}
}
```

The function can be called with the starting node for example : `dfs(2)`  Depth First Search from node 2 on the graph we earlier represented using adjacency list gives output : `2 4 1 5 3`

The time complexity of depth-first search is O(n+ m) where n is the number
of nodes and m is the number of edges, because the algorithm processes each
node and edge once.

Read more about depth first search and its applications :

1. [https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)
2. [https://www.geeksforgeeks.org/applications-of-depth-first-search/](https://www.geeksforgeeks.org/applications-of-depth-first-search/)

### Breadth First Search (BFS)

Breadth-first search (BFS) visits the nodes in increasing order of their distance from the starting node. Thus, we can calculate the distance from the starting node to all other nodes using breadth-first search. Here distance implies the number of edges to be traversed to go from one node to the next.
Breadth-first search goes through the nodes one level after another. First the search explores the nodes whose distance from the starting node is 1, then the nodes whose distance is 2, and so on. This process continues until all nodes have been visited.

Breadth First Search can be implemented using a queue. When the search reaches a node, all the nodes which are connected to this node by an edge and which haven't been visited are added into the queue. The search then proceeds to the next element of the queue, till all the nodes have been visited. In the following implementation we will be using the template class `queue` provided in the C++ STL, however you can use the queue we have seen in the earlier lecture as well. The following data structures will be required :

```cpp
queue<int> q;
bool visited[N] = {};
int distance[N];
```

Now, BFS can be implemented as follows :

```cpp
//Supposing node 1 is the starting node
visited[1] = true;
distance[1] = 0;
q.push(1);
while (!q.empty()) 
{
	int a = q.front(); 
	q.pop();
	// process node a, here we print it
	cout << a << " ";
	for (int i=0;i<adj[a].size();i++) 
	{
		if (visited[adj[a][i]]) continue;
		visited[adj[a][i]] = true;
		distance[adj[a][i]] = distance[a]+1;
		q.push(adj[a][i]);
	}
}
```

Breadth First Search from node 2 on the graph we earlier represented using adjacency list gives output : `2 4 5 1 3`

Read more about breadth first search and its applications :

1. [https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)
2. [https://www.geeksforgeeks.org/applications-of-breadth-first-traversal/](https://www.geeksforgeeks.org/applications-of-breadth-first-traversal/) 

A nice side by side visualization of DFS and BFS : [https://cs.stanford.edu/people/abisee/tutorial/bfsdfs.html](https://cs.stanford.edu/people/abisee/tutorial/bfsdfs.html) 

Some problems which require DFS or BFS :

1. [https://practice.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1](https://practice.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1) 
2. [https://practice.geeksforgeeks.org/problems/bfs-traversal-of-graph/1](https://practice.geeksforgeeks.org/problems/bfs-traversal-of-graph/1) 
3. [https://codeforces.com/problemset/problem/115/A](https://codeforces.com/problemset/problem/115/A) 
4. [https://codeforces.com/problemset/problem/893/C](https://codeforces.com/problemset/problem/893/C) 
5. [https://codeforces.com/problemset/problem/1337/C](https://codeforces.com/problemset/problem/1337/C) 
6. [https://www.codechef.com/LTIME95B/problems/SPTREE](https://www.codechef.com/LTIME95B/problems/SPTREE)
7. [https://codeforces.com/contest/1520/problem/G](https://codeforces.com/contest/1520/problem/G)

## Shortest Paths:

### Bellman-Ford

The Bellman-Ford algorithm finds the shortest paths from a given starting node to all the nodes of the graph. The algorithm can process all kinds of graphs, provided that the graph does not contain a cycle with negative length.

The algorithm works the following way:

1. Create a distance array(like in BFS) and initialize all distances to infinity except the starting index which is initialized to 0.
2. Now, for N-1 iterations(N → Number of nodes), go through each edge of the graph and if considering that edge reduces the distance of the destination, then change the distance value. After 1 iteration, the algorithm has calculated all shortest distances with at most 1 edge in the path. After 2 iterations, the shortest distance with 2 edges and so on.
3. In a graph, if there are more than N-1 edges, then there is surely a cycle present(try proving or disproving this). Therefore, if after N-1 iterations, if we do an Nth iteration and that reduces the distance to any node, it means that the shortest path to that node consists of a cycle. And a cycle can reduce the path length only if it is a negative weight cycle. Hence, in this way you can detect negative weight cycles in the graph using the Bellman-Ford Algorithm.

Since the algorithm goes through all the edges of the graph, the edge list representation of the graph is the most convenient for this method. Implementation of the algorithm for the following graph:

![Image](Images/Graphs%201c69060174364bd09f16c868e62470d5/Untitled%206.png)

```cpp
#include <iostream>
#include <vector>
using namespace std;

const int N = 6;
int INF = int(1e8);

struct Edge
{
	int src,dest,weight;
	Edge(int from,int to,int w)
	{
		src = from;
		dest = to;
		weight = w;
	}
};

int main()
{
	vector<Edge> edgelist; //Bidirectional edges can be thought of as 2 unidirectional edges
	edgelist.push_back(Edge(1,2,7));
	edgelist.push_back(Edge(2,1,7));
	edgelist.push_back(Edge(1,3,9));
	/*....Adding Edges...
	......*/

	int distance[N+1];
	for (int i = 1; i <= N; i++) distance[i] = INF;
	distance[1] = 0;
	for (int i = 1; i <= N-1; i++) 
	{
		for(int j=0;j<edgelist.size();j++) 
		{
			int a, b, w;
			a = edgelist[j].src;
			b = edgelist[j].dest;
			w = edgelist[j].weight;
			distance[b] = min(distance[b], distance[a]+w);
		}
	}
	cout << "Minimum Distance to :\n";
	for(int i=1;i<=6;i++)
	{
		cout << i << " " << distance[i] << "\n";
	}
}
```

Output:

```cpp
Minimum Distance to :
1 0
2 7
3 9
4 20
5 20
6 11
```

The time complexity of the algorithm is O(n*m) as evident from the nested for loops. Here, n is the number of nodes and m is the number of edges.

### Dijkstra's Algorithm

Dijkstra's can be thought of as a modification of the Breadth First Search Algorithm. Instead of visiting nodes in a level wise manner, we act greedily on the distance from root. At any point of time, we select a node with the minimum distance from the starting node and traverse one edge from this node and evaluate the distances. This kind of greedy work allows us to reach the destination node in the shortest possible time. However, this algorithm doesn't work for negative weight edges in the graph.

The algorithm consists of the following steps :

1. Just like BFS, you need a distance array that is initialized the same was as Bellman-Ford. Also you need a min-heap to store the nodes in order of the distance from the starting node. For min-heap, we can use the min-heap we saw in the previous lecture, or C++ standard library classes like priority queue and set.
2. At each step, Dijkstra’s algorithm selects a node that has not been processed yet and whose distance is as small as possible. This is the node at the top of the min-heap. The first such node is node 1 with distance 0.
3. When a node is selected, the algorithm goes through all edges that start at the node and reduces the distances using them. If the distance gets reduces, the node is added into the min-heap and the algorithm continues, till all nodes are visited.

A remarkable property in Dijkstra’s algorithm is that whenever a node is selected, its distance is final.(Why?)

One way to have min-heap in C++ is to use priority queue(which is a max-heap) and consider everything as negative! Such an implementation results in a very short code :P

![Images](Images/Graphs%201c69060174364bd09f16c868e62470d5/Untitled%206.png)

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

const int N = 6;
int INF = int(1e8);

int main()
{
	vector<pair<int,int>> adj[N+1];
	int distance[N+1];
	bool visited[N+1] = {};
	priority_queue<pair<int,int>> q;

	//Setting up the graph
	adj[1].push_back(make_pair(2,7));
	adj[1].push_back(make_pair(3,9));
	adj[1].push_back(make_pair(6,14));
	adj[2].push_back(make_pair(3,10));
	/*...add all edges..
	.....*/
	
	//Dijkstra's Algorithm
	for (int i = 1; i <= N; i++) distance[i] = INF;
	distance[1] = 0;
	q.push({0,1});
	while (!q.empty()) 
	{
		int a = q.top().second; 
		q.pop();
		if (visited[a]) continue;
		visited[a] = true;
		for(int i=0;i<adj[a].size();i++) 
		{
			pair<int,int> p = adj[a][i];
			int b = p.first, w = p.second;
			if (distance[a]+w < distance[b])
			{
				distance[b] = distance[a]+w;
				q.push({-distance[b],b});
			}
		}
	}

	cout << "Minimum Distance to :\n";
	for(int i=1;i<=6;i++)
	{
		cout << i << " " << distance[i] << "\n";
	}
}
```

Output:

```cpp
Minimum Distance to :
1 0
2 7
3 9
4 20
5 20
6 11
```

The time complexity of the above implementation is O(n+ mlogm), because
the algorithm goes through all nodes of the graph and adds for each edge at most
one distance to the priority queue.

Of course you can implement Dijkstra's with the min-heap we have seen before. Such an implementation is given here : [https://www.geeksforgeeks.org/dijkstras-algorithm-for-adjacency-list-representation-greedy-algo-8/](https://www.geeksforgeeks.org/dijkstras-algorithm-for-adjacency-list-representation-greedy-algo-8/) 

### Floyd-Warshall

This algorithm finds the shortest path between all the nodes in a single run. The algorithm maintains a two-dimensional array that contains distances between the nodes. First, distances are calculated only using direct edges between the nodes, and after this, the algorithm reduces distances by using intermediate nodes in the paths.

This algorithm is the easiest to implement, however its time complexity is O($n^3$). The 2-D distance array is initialized as follows :

```cpp
for (int i = 1; i <= n; i++) 
{
		for (int j = 1; j <= n; j++) 
		{
				if (i == j) distance[i][j] = 0;
				else if (adj[i][j]) distance[i][j] = adj[i][j];
				else distance[i][j] = INF;
		}
}
```

The algorithm consists of consecutive rounds. On each round, the algorithm selects a new node that can act as an intermediate node in paths from now on, and distances are reduced using this node. `distance[i][j]` finally stores the minimum length of the path from node i to node j.

```cpp
for (int k = 1; k <= n; k++)
{
		for (int i = 1; i <= n; i++) 
		{
				for (int j = 1; j <= n; j++) 
				{
					distance[i][j] = min(distance[i][j],
					distance[i][k]+distance[k][j]);
				}
		}
}
```

Try these out!

1. [https://cses.fi/problemset/task/1671](https://cses.fi/problemset/task/1671)
2. [https://www.hackerearth.com/problem/algorithm/dijkstras/](https://www.hackerearth.com/problem/algorithm/dijkstras/) 
3. [https://codeforces.com/problemset/problem/20/C](https://codeforces.com/problemset/problem/20/C) 
4. [https://cses.fi/problemset/task/1672](https://cses.fi/problemset/task/1672)
