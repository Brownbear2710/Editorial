# [B - Knight in a War Grid](https://vjudge.net/problem/UVA-11906)

Let's say we are in cell[ i ][ j ]. The possible moves from this position are:

(i + n, j + m) 

(i + n, j - m)

(i - n, j + m)

(i - n, j - m)

(i + m, j + n)

(i + m, j - n)

(i - m, j + n)

(i - m, j - n)

So, we can iterate through all these cells and count the number of visitable cells i.e. how many of these are inside the field and not filled with water. Then we can check if the count is even or odd. While doing so, if the cell is not already visited, we will go to that cell and do the same. This can be done recursively.

But we haven't considered two cases yet. If n equals m or one of them is 0. In this case, number of visitable cell will just be half of the actual count.

<details>
<summary>C++ Code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;

int n, m, r, c;
bool can_visit[102][102], visited[102][102];
int cnt[102][102];

bool visitable(int x, int y)
{
    if (x < 0 || x >= r || y < 0 || y >= c)
        return false;
    return can_visit[x][y];
}
void go(int x, int y, int *dx, int *dy)
{
    int visits = 0;
    visited[x][y] = 1;
    for (int i = 0; i < 8; i++)
    {
        int nx = dx[i] + x, ny = dy[i] + y;
        if (visitable(nx, ny))
        {
            visits++;
            if (!visited[nx][ny])
                go(nx, ny, dx, dy);
        }
    }
    if (m == n || !m || !n)
        visits /= 2;
    cnt[x][y] = visits;
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(NULL);

    int T;
    cin >> T;

    for (int t = 0; t < T; t++)
    {
        int w;
        cin >> r >> c >> m >> n >> w;
        for (int i = 0; i < r; i++)
            for (int j = 0; j < c; j++)
                can_visit[i][j] = 1, visited[i][j] = 0;

        memset(cnt, -1, sizeof(cnt));

        int dx[] = {n, n, m, m, -n, -n, -m, -m};
        int dy[] = {m, -m, n, -n, m, -m, n, -n};

        while (w--)
        {
            int x, y;
            cin >> x >> y;
            can_visit[x][y] = 0;
        }

        go(0, 0, dx, dy);

        int evenOddCount[2] = {0};
        for (int i = 0; i < r; i++)
        {
            for (int j = 0; j < c; j++)
            {
                if (cnt[i][j] != -1)
                {
                    evenOddCount[cnt[i][j] % 2]++;
                }
            }
        }
        cout << "Case " << t + 1 << ": " << evenOddCount[0] << " " << evenOddCount[1] << "\n";
    }
    return 0;
}
```
</details>

