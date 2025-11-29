# Assignment 45


## Problem Statement
Write a Program to accept a graph from a user and represent it with Adjacency List and perform BFS and DFS traversals on it.

## Theory
•	The Adjacency List is an efficient representation for storing sparse graphs. Each vertex maintains a linked list (or vector) of all its adjacent vertices. This structure requires memory proportional to the number of edges: O(V + E).
•	Traversals:
•	BFS (Breadth-First Search)
•	Uses queue
•	Visits nodes level-wise
•	Excellent for shortest path in unweighted graphs
•	Time complexity: O(V + E) using adjacency list
•	DFS (Depth-First Search)
•	Uses stack/recursion
•	Explores deep paths before backtracking
•	Useful for detecting cycles, components, topological sort
•	Time complexity: O(V + E)
•	Adjacency lists make both BFS and DFS more efficient compared to adjacency matrices, especially for large sparse graphs.

## Code
```cpp
#include <iostream>
#include <queue>
using namespace std;

struct Node {
    int v;
    Node* next;
};

Node* adj[20];   
int n;

Node* getNode(int v) {
    Node* temp = new Node();
    temp->v = v;
    temp->next = NULL;
    return temp;
}

void addEdge(int u, int v) {
    Node* p = getNode(v);
    p->next = adj[u];
    adj[u] = p;

    Node* q = getNode(u);
    q->next = adj[v];
    adj[v] = q;
}

void display() {
    cout << "\nAdjacency List:\n";
    for (int i = 0; i < n; i++) {
        cout << i << " -> ";
        Node* t = adj[i];
        while (t != NULL) {
            cout << t->v << " ";
            t = t->next;
        }
        cout << endl;
    }
}

void bfs(int start) {
    bool visited[20] = {false};
    queue<int> q;

    visited[start] = true;
    q.push(start);

    cout << "BFS: ";

    while (!q.empty()) {
        int u = q.front();
        q.pop();
        cout << u << " ";

        Node* t = adj[u];
        while (t != NULL) {
            int v = t->v;
            if (!visited[v]) {
                visited[v] = true;
                q.push(v);
            }
            t = t->next;
        }
    }
    cout << endl;
}

void dfsUtil(int u, bool visited[]) {
    visited[u] = true;
    cout << u << " ";

    Node* t = adj[u];
    while (t != NULL) {
        if (!visited[t->v])
            dfsUtil(t->v, visited);
        t = t->next;
    }
}

void dfs(int start) {
    bool visited[20] = {false};
    cout << "DFS: ";
    dfsUtil(start, visited);
    cout << endl;
}

int main() {
    int ch;

    for (int i = 0; i < 20; i++)
        adj[i] = NULL;

    while (true) {
        cout << "\n--- Graph BFS & DFS (Adjacency List) ---\n";
        cout << "1. Create Graph\n";
        cout << "2. Display Graph\n";
        cout << "3. BFS Traversal\n";
        cout << "4. DFS Traversal\n";
        cout << "5. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        if (ch == 1) {
            int edges, u, v;
            cout << "Enter number of vertices: ";
            cin >> n;

            for (int i = 0; i < n; i++)
                adj[i] = NULL;

            cout << "Enter number of edges: ";
            cin >> edges;

            cout << "Enter edges (u v):\n";
            for (int i = 0; i < edges; i++) {
                cin >> u >> v;
                addEdge(u, v);
            }
        }
        else if (ch == 2) display();
        else if (ch == 3) {
            int s;
            cout << "Enter start vertex: ";
            cin >> s;
            bfs(s);
        }
        else if (ch == 4) {
            int s;
            cout << "Enter start vertex: ";
            cin >> s;
            dfs(s);
        }
        else if (ch == 5) {
            cout << "Exiting...\n";
            break;
        }
        else {
            cout << "Invalid choice!\n";
        }
    }

    return 0;
}

```

## Output
--- Graph BFS & DFS (Adjacency List) ---
1. Create Graph
2. Display Graph
3. BFS Traversal
4. DFS Traversal
5. Exit
Enter choice: 1
Enter number of vertices: 4
Enter number of edges: 4
Enter edges (u v):
0 1
0 2
1 3
2 3

--- Graph BFS & DFS (Adjacency List) ---
1. Create Graph
2. Display Graph
3. BFS Traversal
4. DFS Traversal
5. Exit
Enter choice: 2

Adjacency List:
0 -> 2 1
1 -> 3 0
2 -> 3 0
3 -> 2 1

--- Graph BFS & DFS (Adjacency List) ---
1. Create Graph
2. Display Graph
3. BFS Traversal
4. DFS Traversal
5. Exit
Enter choice: 3
Enter start vertex: 0
BFS: 0 2 1 3

--- Graph BFS & DFS (Adjacency List) ---
1. Create Graph
2. Display Graph
3. BFS Traversal
4. DFS Traversal
5. Exit
Enter choice: 4
Enter start vertex: 0
DFS: 0 2 3 1

## Real-Life Applications
•	Finding connected components in social networks
•	Detecting cycles in dependency graphs
•	Maze solving (DFS)
•	Level-order exploration (BFS)
•	Task scheduling with topological sorting

## Conclusion
Representing a graph using adjacency lists is optimal for sparse graphs, and combining it with BFS and DFS provides powerful tools for traversal, connectivity analysis, and exploration.