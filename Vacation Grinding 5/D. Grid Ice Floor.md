# [D - Grid Ice Floor](https://atcoder.jp/contests/abc311/tasks/abc311_d?lang=en)

## Solution
Brute force, traversal problem. <br>
Just simulate all possible movement. <br>
Start from (2,2). Then go to the leftmost, rightmost, topmost, bottom-most possible position and mark all the nodes visited. <br>
Make sure to mark the node which you just started from (in the first iteration it will be 2-2) as DONE <br>
Now if the final nodes from the 4 direction are not marked as DONE, redo the 4 directional movement from those nodes. <br>
Note: You might need to traverse a visited node multiple times. So we are only marking them visited to count the answer (How many total nodes visited) and not for traversal.

<details>
<summary>Code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;
using ll = long long;

#define fast_IO ios_base::sync_with_stdio(0), cin.tie(NULL);
#define all(x) x.begin(), x.end()

vector <vector<char>> board(205, vector<char>(205, 0));
int dx[] = {0,0,1,-1};
int dy[] = {1,-1,0,0};
int n, m, ans;
 
void traverse(int x, int y)
{
    if(board[x][y] == 'X') return;
    if(board[x][y] == '.') ans++;
    board[x][y] = 'X';
    int ix = x, iy = y;
    for(int i = 0; i < 4; i++) // trying all 4 directions
    {
        while(board[x+dx[i]][y+dy[i]] != '#')
        {
            x += dx[i];
            y += dy[i];
            if(board[x][y] == '.')
            {
                ans++;
                board[x][y] = 'V';
            }
        }
        traverse(x, y);
        x = ix, y = iy;
    }
}

int main()
{
        cin >> n >> m;
 
    for(int i = 0 ; i < n ; i++)
    {
        for(int j = 0 ; j < m ; j++)
            cin >> board[i][j];
    }
    ans = 0;
    traverse(1, 1);
    cout << ans << endl;
    return 0;
}
```
</details>
