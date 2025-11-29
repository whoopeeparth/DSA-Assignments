# Assignment 41


## Problem Statement
Write a Program to accept a graph from a user and represent it with Adjacency Matrix and perform BFS and DFS traversals on it.

## Theory
A graph is a collection of vertices (nodes) connected by edges (links). To store a graph in memory, one common representation is the Adjacency Matrix, which is a 2D array where each cell (i, j) indicates whether an edge exists between vertex i and vertex j.
•	For unweighted graphs: 0 = no edge, 1 = edge exists.
•	For weighted graphs: cell stores the weight of the edge.
The adjacency matrix provides O(1) time to check if an edge exists, making it suitable for dense graphs or when quick connectivity tests are needed.
Once the graph is represented, two major traversal algorithms are applied:
Breadth-First Search (BFS)
•	Uses a queue
•	Explores the graph level by level
•	Ideal for finding shortest paths in unweighted graphs
•	Time complexity: O(V²) for adjacency matrix implementation
Depth-First Search (DFS)
•	Uses recursion or a stack
•	Explores deeply before backtracking
•	Useful for cycle detection, connected components, and topological sorting
•	Time complexity: O(V²) for adjacency matrix
These traversal methods are foundational algorithms in graph theory and are used to explore, analyze, and process connectivity and structure within networks.

## Code
```cpp
#include <iostream>
#include <queue>
using namespace std;

int graph[20][20];
int visited[20];
int n;

void inputGraph()
{
    cout<<"Enter number of vertices: ";
    cin>>n;
    cout<<"Enter adjacency matrix: \n";
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            cin>>graph[i][j];
        }
    }
    cout<<"Graph sorted successfully.\n";
}

void displayMatrix()
{
    cout<<"\nAdjacency Matrix: \n";
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            cout<<graph[i][j]<<" ";
        }
        cout<<endl;
    }
}

void DFS(int v)
{
    cout<<v<<" ";
    visited[v] = 1;

    for(int i = 0; i < n; i++)
    {
        if(graph[v][i] == 1 && !visited[i])
        {
            DFS(i);
        }
    }
}

void BFS(int start)
{
    queue<int> q;
    for(int i = 0; i < n; i++)
    {
        visited[i] = 0;
    }

    visited[start] = 1;
    q.push(start);

    cout<<"BFS Traversal: ";
    while(!q.empty())
    {
        int v = q.front();
        q.pop();
        cout<<v<<" ";

        for(int i = 0; i < n; i++)
        {
            if(graph[v][i] == 1 && !visited[i])
            {
                visited[i] = 1;
                q.push(i);
            }
        }
    }
    cout<<endl;
}

int main()
{
    int choice, start;

    while(true)
    {
        cout<<"\n-----Graph Operations-----\n";
        cout<<"1. Input Graph\n";
        cout<<"2. Display Adjacency Matrix\n";
        cout<<"3. DFS Traversal\n";
        cout<<"4. BFS Traversal\n";
        cout<<"5. Exit\n";
        cout<<"Enter your choice: ";
        cin>>choice;

        switch(choice)
        {
            case 1:
                inputGraph();
                break;

            case 2:
                displayMatrix();
                break;

            case 3:
                cout<<"Enter starting vertex for DFS: ";
                cin>>start;
                for(int i = 0; i < n; i++)
                {
                    visited[i] = 0;
                }
                cout<<"DFS Traversal: ";
                DFS(start);
                cout<<endl;
                break;

            case 4:
                cout<<"Enter starting vertex for BFS: ";
                cin>>start;
                BFS(start);
                break;

            case 5:
                cout<<"Exiting...";
                return 0;

            default: 
                cout<<"Invalid choice!\n";
        }
    }
    return 0;

}

```

## Output
-----Graph Operations-----
1. Input Graph
2. Display Adjacency Matrix
3. DFS Traversal
4. BFS Traversal
5. Exit
Enter your choice: 1
Enter number of vertices: 4
Enter adjacency matrix:
0 1 1 0
1 0 0 1
1 0 0 1
0 1 1 0
Graph sorted successfully.

-----Graph Operations-----
1. Input Graph
2. Display Adjacency Matrix
3. DFS Traversal
4. BFS Traversal
5. Exit
Enter your choice: 2

Adjacency Matrix:
0 1 1 0
1 0 0 1
1 0 0 1
0 1 1 0

-----Graph Operations-----
1. Input Graph
2. Display Adjacency Matrix
3. DFS Traversal
4. BFS Traversal
5. Exit
Enter your choice: 3
Enter starting vertex for DFS: 3
DFS Traversal: 3 1 0 2

-----Graph Operations-----
1. Input Graph
2. Display Adjacency Matrix
3. DFS Traversal
4. BFS Traversal
5. Exit
Enter your choice: 4
Enter starting vertex for BFS: 3
BFS Traversal: 3 1 2 0

## Real-Life Applications
•	Social network friend-of-friend exploration
•	Web crawling (searching links systematically)
•	GPS shortest unweighted route detection
•	Network broadcast simulation
•	AI state-space search (games, puzzles)

## Conclusion
Representing graphs using an adjacency matrix and applying BFS & DFS offers a clear and systematic way to explore a graph. Both algorithms are fundamental, forming the base for advanced operations like pathfinding, cycle detection, and network analysis.