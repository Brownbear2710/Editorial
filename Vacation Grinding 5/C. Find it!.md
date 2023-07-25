# [C - Find it!](https://atcoder.jp/contests/abc311/tasks/abc311_c?lang=en)

## Solution
Perform DFS. Keep track of parent node while DFS is running.
Also keep track which node was the starting call for DFS when a new node is visited (instead of boolean array of visited, use integer)
Finding the answer:
While DFS is running, if the child node is already visited and the starting call for that node is the same as the current node, the loop is found.
To generate the sequence, use the parent-array (used to keep track of parents) to backtrack to the child node.
This will generate the sequence in reverse order, so print it in the proper order

<details>
<summary>Code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;
using ll = long long;

#define fast_IO ios_base::sync_with_stdio(0), cin.tie(NULL);
#define all(x) x.begin(), x.end()
#define MAXN 200005

vector <int> adj[MAXN];
int visited[MAXN];
int parent[MAXN];
int n;
vector <int> res;
 
void dfs(int node, int currentDFS_start)
{
    if(res.size() != 0) return; //ans already calculated
    for(auto child : adj[node])
    {
        if(visited[child] == visited[node]) // loop exist
        {
            res.push_back(node);
            while(node != child)
            {
                node = parent[node];
                res.push_back(node);
            }
            reverse(all(res));
            return;
        }
        if(visited[child] != 0)
            continue;
        visited[child] = currentDFS_start;
        parent[child] = node;
        dfs(child, currentDFS_start);
    }
}

int main()
{
    cin >> n;
    for(int i = 0 ; i < n ; i++)
    {
        int inp;
        cin >> inp;
        adj[i+1].push_back(inp);
    }
    for(int i = 1 ; i <= n ; i++)
    {
        if(res.size() != 0) break;
        if(visited[i] == 0)
        {
            visited[i] = i;
            dfs(i, i);
        }
    }
    cout << res.size() << endl;
    for(auto x : res) cout << x << " ";
    return 0;
}
```
</details>
