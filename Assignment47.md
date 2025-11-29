# Assignment 47


## Problem Statement
Write a Program to implement Dijkstra’s algorithm to find shortest distance between two nodes of a user defined graph. Use Adjacency Matrix to represent a graph.

## Theory
•	Dijkstra’s Algorithm finds the shortest path from a single source node to all other nodes in a graph with non-negative edge weights. It is one of the most fundamental algorithms in graph theory and is extensively used in routing systems.
•	Why Adjacency Matrix?
•	An adjacency matrix enables direct access to edge weights in O(1) time. This is useful when:
•	The graph is dense
•	The number of nodes is relatively small
•	Fast edge-lookup is required
•	Each cell (i, j) stores either:
•	the weight of the edge from i → j
•	or 0/∞ if no edge exists
•	How Dijkstra Works
•	Maintain an array dist[] initialized to ∞
•	Set dist[source] = 0
•	Maintain a visited set
•	Repeat:
•	Pick vertex u with minimum dist[] not yet visited
•	Visit u
•	Relax all outgoing edges from u:
•	if dist[u] + weight(u,v) < dist[v]:
•	    update dist[v]
•	Continue until all vertices are visited
•	This ensures shortest paths are found in strictly increasing order of distance.

## Code
```cpp
#include <iostream>
#include <climits>
using namespace std;

const int V = 5;

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

void dijkstra(int graph[V][V], int src) {
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

        for (int v = 0; v < V; v++) {
            if (graph[u][v] && !visited[v] && dist[u] != INT_MAX
                && dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
            }
        }
    }

    cout << "Vertex   Distance from Source\n";
    for (int i = 0; i < V; i++)
        cout << i << "        " << dist[i] << "\n";
}

int main() {
    int graph[V][V] = {
        {0, 2, 0, 6, 0},
        {2, 0, 3, 8, 5},
        {0, 3, 0, 0, 7},
        {6, 8, 0, 0, 9},
        {0, 5, 7, 9, 0}
    };

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
•	GPS & Navigation apps – shortest driving route
•	Network routing (OSPF protocol) – fastest packet route between routers
•	Robotics path planning – determining shortest movement paths
•	Logistics & supply chain – optimizing delivery routes
•	Video games (AI pathfinding) – NPC movement on weighted maps

## Conclusion
Dijkstra’s Algorithm is one of the most widely used shortest-path algorithms. Using an adjacency matrix ensures predictable lookup and consistent performance for dense or medium-sized graphs. It is fundamental in navigation, routing, and optimization systems worldwide.