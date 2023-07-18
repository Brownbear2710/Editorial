# [J - Party](https://vjudge.net/problem/CodeForces-177C2/origin)
First of all, we have to make sets of friends who know each other directly or indirectly. To do this we can use the concept of Disjoint Set Union.<br>
At first we take an array P, where P[<i>i</i>] donotes the parent of element <i>i</i>. To join two elements <i>u</i> and <i>v</i>, we at first find the parent of <i>u</i> and <i>v</i>, P[<i>u</i>] and P[<i>v</i>] respectively. Now we take another array which stores the size of set that the parent is a part of. Let's say P[<i>u</i>] is a part of greater set. So, we set the parent of P[<i>v</i>] to P[<i>u</i>] i.e P[P[<i>v</i>]] = P[<i>u</i>] and update the size of P[<i>u</i>].<br>
<details>
<summary><u>How to find parent or the root</u></summary>
<p>Initially, we set the parent of every element to themselves, namely, P[i] = i. So, whenever we find such a node for which P[<i>node</i>] holds the value <i>node</i>, we can be sure that it is the root node. Otherwise we find the parent of P[<i>node</i>] and so on.</p>

```cpp
int find_parent(int node)
{
    if(p[node] == node)
        return node;

    return p[node] = find_parent(p[node]);
}
```
</details>
Whenever two friends know each other, we can join them by the above process. After we have joined all of them, we have to see if two friends, who hate each other, belong to same set or not. To check this, we simply find the root node of both of them. If they have same root node, they belong to the same set. If they belong to the same set, we cannot invite that set of friends even if they are the largest group. So, we exclude that set from consideration. After excluding the unwanted sets. We iterate through the size of the remaining sets and find the largest size. This is the answer.
<br><br>
<details>
<summary>C++ Code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;

#define MAXN 2003

int p[MAXN], sz[MAXN];

int find_parent(int node)
{
    if(p[node] == node)
        return node;
    return p[node] = find_parent(p[node]);
}

void join(int u, int v)
{
    int pu = find_parent(u);
    int pv = find_parent(v);
    
    if (pu == pv)
        return;
    else if (sz[pu] > sz[pv])
    {
        p[pv] = pu;
        sz[pu] += sz[pv];
    }
    else
    {
        p[pu] = pv;
        sz[pv] += sz[pu];
    }
    return;
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(NULL);

    int n, k, m;
    set<int> root;

    for (int i = 0; i < MAXN; i++)
    {
        p[i] = i;
        sz[i] = 1;
    }

    cin >> n >> k;

    for (int i = 0; i < k; i++)
    {
        int u, v;
        cin >> u >> v;
        join(u, v);
    }

    for (int i = 1; i < n + 1; i++)
    {
        root.insert(find_parent(i));
    }
    
    cin >> m;
    for (int i = 0; i < m; i++)
    {
        int u, v;
        cin >> u >> v;
        if(find_parent(u) == find_parent(v))
        {
            root.erase(find_parent(u));
        }
    }

    int mx = 0;
    for (auto node : root)
        mx = max(mx, sz[node]);
    cout << mx;

    return 0;
}
```
</details>
