# Assignment 48


## Problem Statement
Write a Program to implement Prim’s algorithm to find minimum
spanning tree of a user defined graph. Use Adjacency List to represent a graph.

## Theory
Prim’s algorithm is a greedy algorithm used to construct a Minimum Spanning Tree (MST) of a connected, weighted, undirected graph. An MST is a subset of edges that connects all vertices with minimum possible total weight, avoiding cycles.
Prim’s starts from any vertex and repeatedly adds the minimum-weight edge that connects the growing tree to an unvisited vertex. Priority queues (min-heaps) are commonly used to efficiently fetch the smallest edge.
Using an Adjacency List is space-efficient for sparse graphs. It stores only existing edges, reducing memory usage compared to a full adjacency matrix.

## Code
```cpp
#include <iostream>
#include <climits>
using namespace std;

const int V = 5;

struct Node {
    int dest;
    int weight;
    Node* next;
};

void addEdge(Node* graph[], int src, int dest, int weight) {
    Node* newNode = new Node{dest, weight, graph[src]};
    graph[src] = newNode;

    newNode = new Node{src, weight, graph[dest]}; // undirected
    graph[dest] = newNode;
}

int minKey(int key[], bool mstSet[]) {
    int minVal = INT_MAX, min_index = -1;
    for (int i = 0; i < V; i++) {
        if (!mstSet[i] && key[i] < minVal) {
            minVal = key[i];
            min_index = i;
        }
    }
    return min_index;
}

void printMST(int parent[], int key[]) {
    cout << "Edge   Weight\n";
    for (int i = 1; i < V; i++) {
        cout << parent[i] << " - " << i << "    " << key[i] << "\n";
    }
}

void primMST(Node* graph[]) {
    int parent[V];
    int key[V];
    bool mstSet[V];

    for (int i = 0; i < V; i++) {
        key[i] = INT_MAX;
        mstSet[i] = false;
    }

    key[0] = 0;
    parent[0] = -1;

    for (int count = 0; count < V - 1; count++) {

        int u = minKey(key, mstSet);
        mstSet[u] = true;

        Node* ptr = graph[u];
        while (ptr != nullptr) {
            int v = ptr->dest;
            int w = ptr->weight;

            if (!mstSet[v] && w < key[v]) {
                key[v] = w;
                parent[v] = u;
            }
            ptr = ptr->next;
        }
    }

    printMST(parent, key);
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

    primMST(graph);

    return 0;
}

```

## Output
Edge   Weight
0 - 1    2
1 - 2    3
0 - 3    6
1 - 4    5

## Real-Life Applications
•	Designing least-cost network wiring (telecom, electricity, internet)
•	Road/railway construction with minimum material cost
•	Cluster analysis in data mining
•	Approximation algorithms in NP-hard problems
•	Sensor network layout optimization

## Conclusion
Prim’s algorithm efficiently builds a minimum spanning tree using a greedy strategy. When combined with adjacency lists and priority queues, it becomes fast, memory-efficient, and practical for large sparse networks.