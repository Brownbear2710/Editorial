# [C - Morning Walk](https://vjudge.net/problem/UVA-10596/origin)
We have three things to consider here:

1. We cannot use same edge (road) twice.
2. Every edge must be visited.
3. We have to come back to the initial position

Now considering point 3, if we go to a particular node we also have get out of it. Now if we consider point 1, we need seperate edges to get in and get out of particular node. Thus we can say that every node must have even number of edges connected to it. If some node has odd number of edges connected to it, we cannot visit all the edges fulfilling these conditions.

After we have considered these, we have to check if all of these nodes are connected either directly or indirectly. To check this, we can simply start from any one node that has at least two edges connected to it and perform depth first search or breadh first search to visit the nodes. Once we go to a particular node we mark it as visited. After doing so, we check if all the nodes which have two or more edges connected to them are visited or not. If all are visited, that means they all are connected and we can visit these road fulfilling all the conditions. Otherwise they are not connected and we cannot do so.
<details>
<summary>C++ Code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;

set<int> adj[202];
bool visited[202];

void dfs(int curr)
{
    visited[curr] = true;

    for(auto child : adj[curr])
    {
        if(visited[child])
            continue;
        dfs(child);
    }
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(NULL);

    int n, r;
    while((cin >> n >> r))
    {
        set<int> to_visit;
        map<int, int> m;
        memset(visited, 0, sizeof(visited));
        for(int i = 0; i < r; i++)
        {
            int u, v;
            cin >> u >> v;
            m[u]++, m[v]++;
            to_visit.insert(u);
            to_visit.insert(v);
            adj[u].insert(v);
            adj[v].insert(u);
        }

        bool f = 1;
        if(to_visit.size() == 0)
            f = 0;

        for(auto it : m)
            if (it.second % 2)
                f = 0;

        if(to_visit.size())
            dfs(*(to_visit.begin()));

        for(auto it : to_visit)
            if(visited[it] == 0)
                f = 0;

        for(int i = 0; i < n; i++)
            adj[i].clear();

        if(f)
            cout << "Possible\n";
        else
            cout << "Not Possible\n";
    }
    return 0;
}
```
</details>
