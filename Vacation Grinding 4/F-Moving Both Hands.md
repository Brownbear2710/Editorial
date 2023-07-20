# [F-Moving Both Hands](https://codeforces.com/problemset/problem/1725/M)

<details>
<summary>Hint1</summary>

```
This can be solved using dijkstra. But you can reverse the edges at most once.
```
</details>

<details>
<summary>Hint2</summary>

```
While runnig dijkstra algorithm we can minimize the backward distance using the forward distance and backward distance.
But forward distance can be minimized using forward distance only.
```
</details>

<details>
<summary>Solution</summary>

Suppose we are trying to find out the minimum time to get the hands from vertices $1$ and $k$ to the same vertex. If both hands end up on some vertex $v$, then the time required is $d(1,v)+d(k,v)$, with $d(x,y)$ being the minimum distance to go from vertex $x$ to $y$.

Suppose $d^′(x,y)$ is the minimum distance to go from vertex $x$ to $y$ in the reversed graph (i.e. all edges' directions are reversed). Then $d(1,v)+d(k,v) = d(1,v)+d^′(v,k)$.

The minimum time if both hands are initially on vertices $1$ and $k$ is the minimum value of $d(1,v)+d^′(v,k)$ for all vertices $v$. This is the same as the minimum distance to go from vertex $1$ to $k$ where in the middle of our path, we can reverse the graph at most once.

Therefore we can set up a graph like the following:

* Each vertex is a pair $(x,b)$, where $x$ is a vertex in the original graph and $b$ is a boolean determining whether we have already reversed the graph or not.

* For each edge $i$ in the original graph, there is an edge from $(U_i,0)$ to $(V_i,0)$ and an edge from $(V_i,1)$ to $(U_i,1)$, both with weight $W_i$.

* For each vertex $x$ in the original graph, there is a edge from $(x,0)$ to $(x,1)$ with weight $0$.

After this, we do the Dijkstra algorithm once on the new graph from vertex $(1,0)$. Then, the optimal time if both hands start from vertices $1$ and $k$ in the original graph is equal to $d((1,0),(k,1))$ in the new graph.

Time complexity: $O(N+M$ log $M)$
</details>

<details>
<summary>C++ Code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;
using ll = long long;

#define fast_IO ios_base::sync_with_stdio(0), cin.tie(NULL);
#define all(x) x.begin(), x.end()
#define MAXN 200005
 
#define PII pair<int,int>
 
ll dist[MAXN][2]; // [node][direction]
vector<pair<int,PII>> adj[MAXN]; // <adjacent node, <weight ,direction>>
 
void dij()
{
    priority_queue<pair<ll,int>,vector<pair<ll,int>>,greater<pair<ll,int>>> pq;
    pq.push({0,1});
    while(pq.size())
    {
        ll d = pq.top().first;
        int curr = pq.top().second;
        pq.pop();
        if(d != dist[curr][0] and d != dist[curr][1]) continue;
        for(auto p: adj[curr])
        {
            int child = p.first, way = p.second.second;
            ll weight = p.second.first;
            ll mn = 1e18;
            // If this is a forward edge, we update the forward distance
            // of the adjacent node using forward distance only
            if(way == 0 and dist[child][0] > dist[curr][0] + weight)
            {
                dist[child][0] = dist[curr][0] + weight;
                mn = min(mn, dist[child][0]);
            }
            // If this is a reverse edge, we update the backward
            // distance of the adjacent node using both the forward and
            // backward distance
            if(way == 1 and dist[child][1] > dist[curr][0] + weight)
            {
                dist[child][1] = dist[curr][0] + weight;
                mn = min(mn, dist[child][1]);
            }
            if(way == 1 and dist[child][1] > dist[curr][1] + weight)
            {
                dist[child][1] = dist[curr][1] + weight;
                mn = min(mn, dist[child][1]);
            }
            if(mn != 1e18) pq.push({mn,child});
        }
    }
}
 
int main()
{
    ios_base::sync_with_stdio(0);cin.tie(NULL);
    int n, m;
    cin >> n >> m;
    for(int i = 0; i <= n; i++)
    {
        dist[i][0] = dist[i][1] = 1e18;
    }
    dist[1][0] = dist[1][1] = 0;
    for(int i = 0; i < m; i++)
    {
        int u,v,w;
        cin >> u >> v >> w;
        adj[u].push_back({{v}, {w,0}}); // 0->forward edge
        adj[v].push_back({{u}, {w,1}}); // 1->reverse edge
    }
    dij();
    for(int i = 2; i <= n; i++)
    {
        ll ans = min(dist[i][0], dist[i][1]);
        if(ans == 1e18) ans = -1;
        cout << ans << " ";
    }
    return 0;
}
```
</details>
