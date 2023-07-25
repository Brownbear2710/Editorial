# [F. Highways](https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1088)

This is a minimum spanning tree problem. Except some edges are already taken. This can be easily solved using [Kruskal's algorithm with DSU](https://cp-algorithms.com/graph/mst_kruskal_with_dsu.html).

At first, we will join the given edges using DSU.
After that we will check, if all nodes are connected. If so, we will simply print <i>"No new highways need"</i>
Otherwise, we will use kruskal's algorithm to select the optimal edges.

<details>
<summary>Code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;
using ll = long long;

#define fast_IO ios_base::sync_with_stdio(0), cin.tie(NULL);
#define all(x) x.begin(), x.end()
#define MAXN 755

struct edge {
    ll u, v, dist;
    bool operator<( edge const & e ) const { return dist < e.dist; }
};

//-----------------------------(DSU start)-----------------------------------//
vector<int> grp[MAXN];
int p[MAXN];
void init(int n)
{
    for(int i = 0; i <= n; i++)
    {
        p[i] = i;
        grp[i].clear();
        grp[i].push_back(i);
    }
}

int join(int a, int b)
{
    if(p[a] == p[b]) return 0;
    int pa = p[a], pb = p[b];
    if(grp[pa].size() < grp[pb].size())
        swap(pa,pb);
    for(auto e : grp[pb])
    {
        grp[pa].push_back(e);
        p[e] = pa;
    }
    grp[pb].clear();
    return 1;
}
//-----------------------------(DSU end)-----------------------------------//

ll distance(pair<ll, ll> p1, pair<ll, ll> p2)
{
    return (p1.first-p2.first)*(p1.first-p2.first) + (p1.second-p2.second)*(p1.second - p2.second);
}

void kruskal(vector<pair<ll,ll>> &points)
{
    int n = points.size();
    vector<edge> edges;

    // Calculate the distance between all pair of points
    for(int i = 0; i < n; i++)
        for(int j = i+1; j < n; j++)
            edges.push_back({i,j, distance(points[i],points[j])});

    // sort the edges based on distance
    sort(all(edges));
    for(int i = 0; i < edges.size(); i++)
        if(join(edges[i].u, edges[i].v)) // If this edge connects two cities, which are not already connected, this edge can be taken
            cout << edges[i].u+1 << " " << edges[i].v+1 << "\n";
}

int main()
{
    fast_IO;
    int T = 1;
    cin >> T;
    while(T--)
    {
        int n;
        cin >> n;
        init(n);
        vector<pair<ll,ll>> points(n);
        for(int i = 0; i < n; i++)
        {
            cin >> points[i].first >> points[i].second;
        }
        int m;
        cin >> m;
        int cnt = 0;
        for(int i = 0; i < m; i++)
        {
            int u, v;
            cin >> u >> v;
            u--, v--;
            cnt += join(u,v);
        }
        if(cnt == n-1)
            cout << "No new highways need\n";
        else
            kruskal(points);
        if(T)
            cout << "\n";
    }
    return 0;
}
```

</details>