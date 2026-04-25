# Graphs (Week 10)

## Task 1

```
        A
       / \
      B   C
     / \   \
    D   E---F
         \ /
          G
```
```
Adjacency List

A: B, C
B: A, D, E
C: A, F
D: B
E: B, F, G
F: C, E, G
G: E, F
```

## Task 2
```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class Graph {
private:
    int V;
    vector<vector<int>> adj;

public:
    Graph(int vertices) {
        V = vertices;
        adj.resize(V);
    }

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // undirected graph
    }

    void BFS(int start) {
        vector<bool> visited(V, false);
        queue<int> q;

        visited[start] = true;
        q.push(start);

        cout << "BFS: ";
        while (!q.empty()) {
            int node = q.front();
            q.pop();
            cout << char(node + 'A') << " ";

            for (int neighbor : adj[node]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    q.push(neighbor);
                }
            }
        }
        cout << endl;
    }

    void DFSUtil(int node, vector<bool>& visited) {
        visited[node] = true;
        cout << char(node + 'A') << " ";

        for (int neighbor : adj[node]) {
            if (!visited[neighbor]) {
                DFSUtil(neighbor, visited);
            }
        }
    }

    void DFS(int start) {
        vector<bool> visited(V, false);
        cout << "DFS: ";
        DFSUtil(start, visited);
        cout << endl;
    }
};

int main() {
    Graph g(7);

    // A=0, B=1, C=2, D=3, E=4, F=5, G=6
    g.addEdge(0, 1); // A-B
    g.addEdge(0, 2); // A-C
    g.addEdge(1, 3); // B-D
    g.addEdge(1, 4); // B-E
    g.addEdge(2, 5); // C-F
    g.addEdge(4, 5); // E-F
    g.addEdge(4, 6); // E-G
    g.addEdge(5, 6); // F-G

    g.BFS(0); // start at A
    g.DFS(0); // start at A

    return 0;
}
```

## Task 3
Breadth-First Search (BFS) and Depth-First Search (DFS) both have a time complexity of O(V + E), where V is the number of vertices and E is the number of edges. This is because each vertex is visited once and each edge is explored once. The space complexity differs slightly between the two algorithms. BFS uses a queue and may require storing multiple nodes at the same level, giving it a space complexity of O(V). DFS uses a stack (or recursion), which in the worst case can also take up to O(V) space. Overall, both algorithms are efficient for graph traversal, but BFS is better for finding shortest paths in unweighted graphs, while DFS is better for exploring all possible paths or detecting cycles.
