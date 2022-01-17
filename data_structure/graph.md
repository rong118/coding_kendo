# Graph
## 1. 定义
- 多对多"逻辑关系数 据的结构——图存储结构。
- 一组定点： v （Vertex) / 一组边： E （edge)
- edge 本身可以有权重
- 不考虑重边和自回路

<img src="../assets/graph.png" width="300" />

<br/>

## 2. connected graph
对于任意两个节点， 有路径， 则称是连通图

<br/>

## 3. undirected vs directed
<img src="../assets/directed_vs_undirected.png" width="400" />

<br/>

## 4. cyclic vs acyclic
<img src="../assets/cyclic_vs_acyclic.png" width="400" />

<br/>

## 5. 图的表示:
- 邻接表 (adjacency list)

  <img src="../assets/adjacency_list.png" width="450" />

  ```c++
  // c++ Implementation
  unodered_map<char, vector<char>> graph;
  for(int i = 0; i < N; i++){
    graph[i] = {};
  }

  // edges
  graph['A'].push_back('B');
  graph['A'].push_back('C');
  graph['A'].push_back('D');

  graph['B'].push_back('C');

  graph['C'].push_back('A');
  graph['C'].push_back('B');

  graph['E'].push_back('B');
  ```

- 邻接矩阵 (adjacency matrix)
  
  <img src="../assets/adjacency_matrix.png" width="450" />

  ```c++
  // c++ Implementation
  vector<vector<int>> graph(N, vector<int>(N, 0));

  // A => 0
  // B => 1
  // C => 2
  // D => 3
  // E => 4

  // edges
  graph[0][1] = 1;
  graph[0][2] = 1;
  graph[0][3] = 1;

  graph[1][2] = 1;

  graph[2][0] = 1;
  graph[2][1] = 1;

  graph[4][1] = 1;
  ```
<br/>

## Topological sort 拓扑排序
在图论中，拓扑排序（Topological Sorting）是一个有向无环图（DAG, Directed Acyclic Graph）的所有顶点的线性序列。且该序列必须满足下面:
- 每个顶点出现且只出现一次。
- 若存在一条从顶点 A 到顶点 B 的路径，那么在序列中顶点 A 出现在顶点 B 的前面。
- 有向无环图（DAG）才有拓扑排序，非DAG图没有拓扑排序一说

<br/>

实现方式： 
- BFS Kahn算法, 基于贪心，每次从入度为0的点开始，正序为拓扑
- DFS 基于搜索，每次保证当前点出度为0后才遍历, 逆序为拓扑 (单纯拓扑不推荐DFS, 如果是二分图才用DFS)

<br/>

Kahn入度算法
1. 从图中选择一个入度为0的顶点， 输出该节点。
2. 从图中删除该节点和所有边。（相邻顶点入度-1）
3. 反复执行， 直至所有节点都输出， 或者图中如果有入度不为零的节点，则说明图中有环

```c++
// c++ Implementation
void kahn_bfs(vector<vector<int> >& edges, int N){
  // build graph and indegree
  unodered_map<int, vector<int>> g;
  vector<int> indegree(N, 0);

  for(vector<int> edge : edges){
    int end = edge[0];
    int start = edge[1];
    if(g.find(start) == g.end()){
      g[start] = {};
    }
    g[start].push_back(end);
    indegree[end]++;
  }

  // 入度为0的节点
  deque<int> q;
  for(int i = 0; i < N; i++){
    if(indegree[i] == 0){
      q.push_back(i);
    }
  }

  int count = 0;
  while(!q.empty()){
    int cur = q.front(); q.pop_front();
    
    // Print output
    cout<<cur<<endl;

    count++;
    for(int n : graph[cur]){
      if(--indegree[n] == 0) q.push_back(n)
    }
  }

  // Check if the graph has cycle
  if(count != N) {
    cout<<"Found Cycle!!"<<endl;
  }else{
    cout<<"No Cycle!!"<<endl;
  }

  return;
}
```
<br/>

DFS 法:
对于图中的任意一个节点，它在搜索的过程中有三种数字颜色状态，即：
- 「0 白色 未搜索」：我们还没有搜索到这个节点；

- 「1 灰色 搜索中」：我们搜索过这个节点，但还没有回溯到该节点，即该节点还没有入栈，还有相邻的节点没有搜索完成）；

- 「2 黑色 已完成」：我们搜索过并且回溯过这个节点，即该节点已经入栈，并且所有该节点的相邻节点都出现在栈的更底部的位置，满足拓扑排序的要求。

```c++
vector<int> visited;
bool valid = true;

void topological_dfs(int N, vector<vector<int> > edges){
    // 建图 和 建visited int[] 
    visited.resize(N, 0);
    unodered_map<int, vector<int>> g;

    for(vector<int> edge : edges){
      int end = edge[0];
      int start = edge[1];
      if(g.find(start) == g.end()){
        g[start] = {};
      }
      g[start].push_back(end);
    }

    // DFS
    if(visited[i] == 0) _dfs(i, g);

    if(valid == false){
      cout << "Found Cycle!!" <<endl;
    } else {
      cout << "No Cycle!!" <<endl;
    }

    return;
}

/*
遍历当前点为进行中灰色1
遍历neighbor:    遇到1则有环, 遇到0继续dfs
所有neighbor遍历结束，标记当前点为黑色2，已遍历结束
*/

void _dfs(int u, unodered_map<int, vector<int>>& g){
  visited[u] = 1;
  for(int n : g[u]){
    if(visited[n] == 0) _dfs(n);
    if(visited[n] == 1) valid = false;
  }
  visited[u] = 2;

  // print out (reverse order)
  cout<<u<<endl;
  return;
}

```

<br/>

## 无向图召唤
1. DFS + parent
2. Union Find


## Leetcode questions
1. Topological sort 拓扑排序 (有向图找环)
- [207 Course Schedule](../leetcode_questions/207_course_schedule.md)
- [210 Course Schedule II](../leetcode_questions/210_course_schedule_ii.md)
- [269 Alien Dictionary](../leetcode_questions/269_alien_dictionary.md)
- [2127 Maximum Employees to Be Invited to a Meeting](../leetcode_questions/2127_maximum_employees_to_be_invited_to_a_meeting.md)

2. (无向图找环)  => union find / dfs with parent
- [261 Graph Valid Tree](../leetcode_questions/261_graph_valid_tree.md)

3. Minimum Spanning Tree

4. Shortest Path (dijkstra)

5. Strong Connect Components