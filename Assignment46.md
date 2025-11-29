# Assignment 46


## Problem Statement
Write a Program to implement Kruskal’s algorithm to find the minimum spanning tree of a user defined graph. Use Adjacency Matrix to represent a graph.

## Theory
A Minimum Spanning Tree (MST) of a connected, undirected, weighted graph is a subset of edges that connects all vertices together with minimum possible total edge weight and no cycles.
Kruskal’s Algorithm is a classic greedy algorithm used to compute the MST. Unlike Prim’s algorithm that grows a tree from a starting vertex, Kruskal’s builds the MST by repeatedly selecting the edge with the smallest weight from the entire graph.
Why Adjacency Matrix?
An adjacency matrix is a 2D array where:
•	matrix[i][j] = 0 or ∞ → no edge
•	matrix[i][j] = weight → edge exists
Although adjacency lists are usually preferred for sparse graphs, adjacency matrices provide constant-time access to check whether an edge exists. This makes scanning all edges simple and structured.
Steps of Kruskal’s Algorithm
1.	Generate a list of all edges from the adjacency matrix.
2.	Sort edges in increasing order of weight.
3.	Initialize a disjoint-set (Union-Find structure).
4.	For each smallest edge:
o	If it does not form a cycle, include it in MST.
o	Union the two vertices in the DSU.
5.	Continue until MST has V−1 edges.

## Code
```cpp
#include <iostream>
using namespace std;

const int V = 5;

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

void kruskalMST(int graph[V][V]) {
    int edgesCount = 0;
    Edge edgeList[V*V];
    int parent[V];

    for (int i = 0; i < V; i++)
        parent[i] = i;

    for (int i = 0; i < V; i++) {
        for (int j = i+1; j < V; j++) {
            if (graph[i][j] != 0) {
                edgeList[edgesCount].src = i;
                edgeList[edgesCount].dest = j;
                edgeList[edgesCount].weight = graph[i][j];
                edgesCount++;
            }
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
    int graph[V][V] = {
        {0, 2, 0, 6, 0},
        {2, 0, 3, 8, 5},
        {0, 3, 0, 0, 7},
        {6, 8, 0, 0, 9},
        {0, 5, 7, 9, 0}
    };

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
•	Telecommunication networks – laying minimum-cost fiber cable across cities
•	Roadway design – selecting roads to connect towns with minimum construction cost
•	Electrical grid layout – designing minimum wiring infrastructure
•	Cluster analysis in Machine Learning – identifying natural clusters using MST-based segmentation
•	Computer chip / VLSI design – minimizing wire-length on circuit boards

## Conclusion
Kruskal’s algorithm is a powerful greedy approach for constructing an MST. Representing the graph using an adjacency matrix makes edge extraction systematic, though slightly expensive for dense graphs. The algorithm’s clarity and cycle-prevention using DSU make it widely used in network optimization and clustering.