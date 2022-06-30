---
layout: post
title:  DFS template Matrix, Tree, Graph problems
categories: [DFS, Graph, BinaryTree, Matrix]
---

Below are some similar ***Leetcode*** questions which can be solved via ***DFS*** algorithm.
DFS algorithm can be applied to a Matrix representation, Binary Trees and Graphs.

Below is the pseudo code for DFS in Graphs.
### iterative DFS
```
DFS-iterative (G, s):                                   //Where G is graph and s is source vertex
    let S be stack
    S.push( s )            //Inserting s in stack
    mark s as visited.
    while ( S is not empty):
        //Pop a vertex from stack to visit next
        v  =  S.top( )
       S.pop( )
       //Push all the neighbours of v in stack that are not visited   
      for all neighbours w of v in Graph G:
          if w is not visited :
                   S.push( w )             
                  mark w as visited
```
### recursive DFS
```
  DFS-recursive(G, s):
      mark s as visited
      for all neighbours w of s in Graph G:
          if w is not visited:
              DFS-recursive(G, w)


```
Some typical DFS problems


## [133. Clone Graph](https://leetcode.com/problems/clone-graph/)
Given a reference of a node in a connected undirected graph.
Return a deep copy (clone) of the graph.

### Solution

```c++
class Solution {
    void DFS(Node* source, Node* copy, unordered_map<int, Node*>& visited) {
        vector<Node *> nc;

        for (Node *n : source->neighbors) {
            if (visited.find(n->val) == visited.end()) {
                 Node *nn = new Node(n->val);
                 visited.insert(make_pair(n->val, nn));
                 nc.push_back(nn);
                 DFS(n, nn, visited);
             } else {
                 nc.push_back(visited.at(n->val));
            }     
             copy->neighbors = nc;
        }
    }
public:
    Node* cloneGraph(Node* node) {
        if (!node) {
            return NULL;
        }
        Node *ansnode =  new Node(node->val);
        if(node->neighbors.empty()) {
            return ansnode;
        }
        unordered_map<int, Node*> visited;

        visited.insert(make_pair(node->val, ansnode));
        DFS(node, ansnode, visited);
        return ansnode;

    }
};
```

## [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)
Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.
An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

### Solution

We take a cell with value 1 and do DFS on it and mark those visited. The number of such iteration in the loop will be the number of islands

```c++
class Solution {

public:
    int numIslands(vector<vector<char>>& grid) {
        if(grid.empty()) {
            return 0;
        }
        int row = grid.size();
        int col = grid[0].size();
        int ans = 0;
        vector<vector<int>> dirs{ {0, 1}, {1, 0}, {0, -1}, {-1, 0} };

        for(int i=0; i<row; i++){
            for(int j=0; j<col; j++) {
                if(grid[i][j] == '0') {
                    continue;
                }
                ans++;
                queue<pair<int, int>> neighbors;
                neighbors.push(make_pair(i,j));
                while (!neighbors.empty()) {
                    auto neighbor = neighbors.front();
                    neighbors.pop();
                    int r = neighbor.first;
                    int c = neighbor.second;
                    for (auto dir: dirs) {
                        int nr = r + dir[0];
                        int nc = c + dir[1];
                        if (nr < 0 || nc < 0 || nr >= row || nc >= col) {
                            continue;
                        }
                        if (grid[nr][nc] == '1') {
                            neighbors.push({nr, nc});
                            grid[nr][nc] = '0';
                        }
                    }
                }
            }
        }
        return ans;
    }
};
```

## [207. Course Schedule](https://leetcode.com/problems/course-schedule/)
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1.
You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.
For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.

Return true if you can finish all courses. Otherwise, return false.
###  Solution


```c++
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        int count = 0;
        vector<int> inDegree(numCourses, 0);
        vector<vector<int>> adj_list(numCourses);

        for (auto edge: prerequisites) {
            inDegree[edge[1]]++;
            adj_list[edge[0]].push_back(edge[1]);
        }

        queue<int> q;

        for(int i =0; i < numCourses; i++) {
            if (inDegree[i] == 0) {
                q.push(i);
            }
        }

        while(!q.empty()) {
            int u = q.front();
            q.pop();

            for (int node: adj_list[u]) {
                if (--inDegree[node] == 0) {
                    q.push(node);
                }
            }  
            count++;
        }

        if(count == numCourses) {
            return true;
        } else {
            return false;
        }  
    }
};
```

## [797. All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/)
Given a directed acyclic graph (DAG) of n nodes labeled from 0 to n - 1, find all possible paths from node 0 to node n - 1 and return them in any order.

The graph is given as follows: graph[i] is a list of all nodes you can visit from node i (i.e., there is a directed edge from node i to node graph[i][j]).

### Solution


```c++
class Solution {
  class Solution {
  public:
      void DFS(vector<vector<int>> &res, vector<int> &out, vector<vector<int>> &G, int V) {
          if(V == G.size()-1) {
              res.push_back(out);
          } else {
             for(auto node: G[V]) {
                  out.push_back(node);
                  DFS(res, out, G, node);
                  out.pop_back();
              }
          }
      }

      vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {      
          vector<vector<int>> res;
          vector<int> out;
          if (graph.size() <= 1) {
              return {{0}};
          }
          out.push_back(0);
          DFS(res, out, graph, 0);
          return res;
      }
  };
```
