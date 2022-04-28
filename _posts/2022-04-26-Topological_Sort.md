---
layout: post
title:  Topological Sort
categories: [Graph]
---

## Topological Sort

A Directed Acyclic Graph (DAG) is a directed graph that contains no cycles.
Topological Sorting of DAG is a linear ordering of vertices such that for every directed edge from vertex ‘u’ to vertex ‘v’, vertex ‘u’ comes before ‘v’ in the ordering. Topological Sorting for a graph is not possible if the graph is not a DAG.
Given a DAG consisting of ‘V’ vertices and ‘E’ edges, you need to find out any topological sorting of this DAG. Return an array of size ‘V’ representing the topological sort of the vertices of the given DAG.


***NOTE***
>1. It is guaranteed that the given graph is DAG.
>2. There will be no multiple edges and self-loops in the given DAG.
>3. There can be multiple correct solutions, you can find any one of them.
>4. Don’t print anything, just return an array representing the topological sort of the vertices of the given DAG.

## Solution

```c++
vector<int> topologicalSort(vector<vector<int>> &edges, int v, int e)  {
    // Write your code here
	vector<int> visited(v, 0);
	vector<int> in_dgree(v, 0);
	vector<int> topo_sort;

	for(auto edge : edges) {
		in_degree[edge[1]]++;
	}

	queue<int> Q;
	for (int i = 0; i < v, i++) {
		if (in_degree[i] == 0) {
			Q.push(i);
			visited[i] = 1;
		}
	}
	while(!Q.empty()) {
		int vertex = Q.front();
		Q.pop();
		topo_sort.push_back(vetex);

	}
}
```
