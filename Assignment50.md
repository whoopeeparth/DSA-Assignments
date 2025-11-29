# Assignment 50


## Problem Statement
Write a Program to implement Dijkstra’s algorithm to find shortest distance between two nodes of a user defined graph. Use Adjacency List to represent a graph.

## Theory
•	Dijkstra’s algorithm computes the shortest path from a single source node to all other nodes in a graph with non-negative edge weights. It uses a priority queue (min-heap) to repeatedly pick the node with the smallest tentative distance.
•	Steps:
•	Set initial distances: source = 0, others = ∞
•	Pick the vertex with minimum tentative distance
•	Update distances to neighbors
•	Repeat until all nodes are processed
•	Adjacency lists make neighbor lookup efficient, especially when the graph is sparse.
•	Time complexity: O(E log V) with min-priority queue.
•	Dijkstra’s is one of the most widely used real-world algorithms because shortest path problems appear in countless applications.

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

    newNode = new Node{src, weight, graph[dest]};
    graph[dest] = newNode;
}

int minDistance(int dist[], bool visited[]) {
    int min = INT_MAX, min_index = -1;
    for (int v = 0; v < V; v++) {
        if (!visited[v] && dist[v] < min) {
            min = dist[v];
            min_index = v;
        }
    }
    return min_index;
}

void dijkstra(Node* graph[], int src) {
    int dist[V];
    bool visited[V];

    for (int i = 0; i < V; i++) {
        dist[i] = INT_MAX;
        visited[i] = false;
    }

    dist[src] = 0; 

    for (int count = 0; count < V - 1; count++) {
        int u = minDistance(dist, visited); 
        visited[u] = true;

        Node* ptr = graph[u];
        while (ptr != nullptr) {
            int v = ptr->dest;
            int w = ptr->weight;
            if (!visited[v] && dist[u] != INT_MAX && dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
            }
            ptr = ptr->next;
        }
    }

    cout << "Vertex   Distance from Source\n";
    for (int i = 0; i < V; i++)
        cout << i << "        " << dist[i] << "\n";
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

    int source = 0;
    dijkstra(graph, source);

    return 0;
}

```

## Output
Vertex   Distance from Source
0        0
1        2
2        5
3        6
4        7

## Real-Life Applications
•	GPS navigation (Google Maps, Uber routing)
•	Network routing protocols (OSPF)
•	Airline/railway route planning
•	Logistics & supply chain optimization
•	Video game pathfinding (NPC movement)

## Conclusion
Dijkstra’s algorithm is essential for shortest-path computation in positively weighted graphs. When implemented with adjacency lists and heaps, it becomes extremely efficient and scalable for large real-world systems.