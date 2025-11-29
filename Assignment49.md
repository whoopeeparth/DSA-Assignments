# Assignment 49


## Problem Statement
Write a Program to implement Kruskal’s algorithm to find the minimum spanning tree of a user defined graph. Use Adjacency List to represent a graph.

## Theory
•	Kruskal’s algorithm is another greedy algorithm for computing an MST. Unlike Prim’s, which grows from a starting vertex, Kruskal’s works by:
•	Sorting all edges in increasing order of weight
•	Picking the smallest edge
•	Adding it if it does not cause a cycle
•	Using Disjoint Set Union (DSU) / Union-Find to detect cycles efficiently
•	The adjacency list helps list out edges more naturally and efficiently.
•	Time complexity using Union-Find: O(E log E) ≈ O(E log V)
•	Kruskal’s is best for sparse graphs or graphs where edges are naturally sorted or easy to extract.

## Code
```cpp
#include <iostream>
using namespace std;

const int V = 5;

struct Node {
    int dest;
    int weight;
    Node* next;
};

struct Edge {
    int src, dest, weight;
};

int findParent(int parent[], int i) {
    while (parent[i] != i)
        i = parent[i];
    return i;
}

void unionSet(int parent[], int x, int y) {
    int xset = findParent(parent, x);
    int yset = findParent(parent, y);
    parent[xset] = yset;
}

void addEdge(Node* graph[], int src, int dest, int weight) {
    Node* newNode = new Node{dest, weight, graph[src]};
    graph[src] = newNode;

    newNode = new Node{src, weight, graph[dest]};
    graph[dest] = newNode;
}

void kruskalMST(Node* graph[]) {
    int edgesCount = 0;
    Edge edgeList[V*V];
    int parent[V];

    for (int i = 0; i < V; i++)
        parent[i] = i;

    for (int i = 0; i < V; i++) {
        Node* ptr = graph[i];
        while (ptr != nullptr) {
            if (i < ptr->dest) {  
                edgeList[edgesCount].src = i;
                edgeList[edgesCount].dest = ptr->dest;
                edgeList[edgesCount].weight = ptr->weight;
                edgesCount++;
            }
            ptr = ptr->next;
        }
    }

    for (int i = 0; i < edgesCount-1; i++) {
        for (int j = 0; j < edgesCount-i-1; j++) {
            if (edgeList[j].weight > edgeList[j+1].weight) {
                Edge temp = edgeList[j];
                edgeList[j] = edgeList[j+1];
                edgeList[j+1] = temp;
            }
        }
    }

    cout << "Edge   Weight\n";
    for (int i = 0; i < edgesCount; i++) {
        int u = edgeList[i].src;
        int v = edgeList[i].dest;
        int w = edgeList[i].weight;

        int set_u = findParent(parent, u);
        int set_v = findParent(parent, v);

        if (set_u != set_v) {
            cout << u << " - " << v << "    " << w << "\n";
            unionSet(parent, set_u, set_v);
        }
    }
}

int main() {
    Node* graph[V] = {nullptr};

    addEdge(graph, 0, 1, 2);
    addEdge(graph, 0, 3, 6);
    addEdge(graph, 1, 2, 3);
    addEdge(graph, 1, 3, 8);
    addEdge(graph, 1, 4, 5);
    addEdge(graph, 2, 4, 7);
    addEdge(graph, 3, 4, 9);

    kruskalMST(graph);

    return 0;
}

```

## Output
Edge   Weight
0 - 1    2
1 - 2    3
1 - 4    5
0 - 3    6

## Real-Life Applications
•	Network design with minimal redundancy
•	Image segmentation (graph-based clustering)
•	Road/transport cost minimization
•	Layout optimization in VLSI circuit design
•	Cable TV or broadband wire layout planning

## Conclusion
Kruskal’s algorithm is extremely flexible and works well even when edges are randomly structured. It provides a systematic way to construct MSTs and is widely used in network design and clustering algorithms.