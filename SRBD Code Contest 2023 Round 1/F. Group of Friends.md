# Problem
[Group of Friends](https://www.hackerrank.com/contests/srbd-code-contest-2023-round-1/challenges/group-of-friends)

# Solution

<details>
<summary>Idea</summary>

It is clear that, if there are two numbers $x$ and $y$, where $x$ is a multiple of $y$, then $x$ and $y$ are in the same group.
So, for all $A_i$ we find the number that divides $A_i$ (other than $1$) and join them together using $DSU$. After that, the answer is the number of groups formed which contain at least one element from the array $A$.

Complexity: $O(N \sqrt {max(A_i)})$

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
#define MAXN 100005


int p[MAXN];
int sz[MAXN];
void init(int n)
{
    for(int i = 0; i <= n; i++)
    {
        p[i] = i;
        sz[i] = 1;
    }
}

int parent(int n)
{
    if(n == p[n]) return n;
    return p[n] = parent(p[n]);
}

void join(int a, int b)
{
    int pa = parent(a), pb = parent(b);
    if(sz[pa] < sz[pb])
    {
        swap(pa, pb);
        swap(a,b);
    }
    sz[pa] += sz[pb];
    sz[pb] = 0;
    p[pb] = pa;
}


int main()
{
    fast_IO;
    int n;
    cin >> n;
    init(MAXN-2);
    vector<int> a(n);
    for(int i = 0; i < n; i++)
    {
        cin >> a[i];
        for(int j = 2; j*j <= a[i]; j++)
        {
            if(a[i] % j == 0)
            {
                join(a[i],j);
                join(a[i],a[i]/j);
            }
        }
    }
    set<int> x;
    for(auto ai: a)
    {
        x.insert(parent(ai));
    }
    cout << x.size() << "\n";
    return 0;
}

```

</details>
