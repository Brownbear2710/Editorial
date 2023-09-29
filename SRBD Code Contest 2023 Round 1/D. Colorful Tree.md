# Problem
[Colorful Tree](https://www.hackerrank.com/contests/srbd-code-contest-2023-round-1/challenges/colorful-tree-1)

# Solution

<details>
<summary>Idea</summary>

The problem can be simplified as: "We have to find the number of $1s$ in the path from node $x$ to $y$".
This problem can be solved using LCA. <br>
We keep count of the number of $1s$ from root to any node in an array $cnt[$ $]$. This can be done using dfs.<br>
Let's say, we are given $x$ and $y$. <br>
Using LCA, we can find the lowest common ancestor $p$.
So, the answer is $cnt[x] + cnt[y] - 2*cnt[p] + 1$. <br>
The extra $1$ is added, because, while eliminating the count of the $1s$ from root to $p$, we also eliminated the color of $p$. But $p$ is definitely on the path from $x$ to $y$.

</details>

<details>
<summary>Code</summary>

```cpp
/*
    So, which of the favours
    of your Lord would you deny?
*/

#include <bits/stdc++.h>

#ifdef ADIB_PC
#include "dbg.h"
#else
#define dbg(...)
#endif

using namespace std;
using ll = long long;

#define fast_IO ios_base::sync_with_stdio(0), cin.tie(NULL);
#define show(x) cout << #x << ": " << x << endl;
#define all(x) begin(x), end(x)
#define MAXN 500005

vector<int> adj[MAXN];

struct LCA {
    vector<int> height, euler, first, segtree;
    vector<bool> visited;
    int n;

    LCA(vector<int> adj[], int _n, int root = 0) {
        n = _n;
        height.resize(n);
        first.resize(n);
        euler.reserve(n * 2);
        visited.assign(n, false);
        dfs(adj, root);
        int m = euler.size();
        segtree.resize(m * 4);
        build(1, 0, m - 1);
    }

    void dfs(vector<int> adj[], int node, int h = 0) {
        visited[node] = true;
        height[node] = h;
        first[node] = euler.size();
        euler.push_back(node);
        for (auto to : adj[node]) {
            if (!visited[to]) {
                dfs(adj, to, h + 1);
                euler.push_back(node);
            }
        }
    }

    void build(int node, int b, int e) {
        if (b == e) {
            segtree[node] = euler[b];
        } else {
            int mid = (b + e) / 2;
            build(node << 1, b, mid);
            build(node << 1 | 1, mid + 1, e);
            int l = segtree[node << 1], r = segtree[node << 1 | 1];
            segtree[node] = (height[l] < height[r]) ? l : r;
        }
    }

    int query(int node, int b, int e, int L, int R) {
        if (b > R || e < L)
            return -1;
        if (b >= L && e <= R)
            return segtree[node];
        int mid = (b + e) >> 1;

        int left = query(node << 1, b, mid, L, R);
        int right = query(node << 1 | 1, mid + 1, e, L, R);
        if (left == -1) return right;
        if (right == -1) return left;
        return height[left] < height[right] ? left : right;
    }

    int lca(int u, int v) {
        int left = first[u], right = first[v];
        if (left > right)
            swap(left, right);
        return query(1, 0, euler.size() - 1, left, right);
    }
};


int cnt[MAXN];
string s;
void dfs(int curr, int par)
{
    cnt[curr] = cnt[par] + s[curr] - '0';
    for(auto child : adj[curr])
    {
        if(child == par) continue;
        dfs(child, curr);
    }
}

int main()
{
    fast_IO;
    int T = 1;
    cin >> T;
    while(T--)
    {
        int n, q;
        cin >> n >> q;
        for(int i = 2; i <= n; i++)
        {
            int p;
            cin >> p;
            adj[i].push_back(p);
            adj[p].push_back(i);
        }
        cin >> s;
        s = "#" + s;
        cnt[0] = 0;
        dfs(1,0);
        // Building lca
        LCA lca(adj,n+1,1);
        while(q--)
        {
            int x, y;
            cin >> x >> y;
            int p = lca.lca(x,y);
            int ans = cnt[x] + cnt[y] - 2*cnt[p] + 1;
            cout << ans << "\n";
        }
        for(int i = 0; i <= n; i++)
        {
            adj[i].clear();
            cnt[i] = 0;
        }
    }
    return 0;
}
```

</details>
