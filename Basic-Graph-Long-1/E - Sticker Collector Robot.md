# [E - Sticker Collector Robot](https://vjudge.net/problem/UVA-11831)
If you look at how the directions change, the robot ends up facing North(0 deg), South(180 deg), East(90 deg) or West(270 deg) because we add 90 deg to the current direction when the instruction is 'D' and subtract 90 deg when the instruction os 'E'. We use this idea of four distinct angles to set the starting direction:

<details>
  <summary>Code to set directions</summary>
    
 ```cpp 
if(g[i][j]  == 'N')
{
    deg = 0;
    kx = i;
    ky = j;
}
if(g[i][j]  == 'S')
{
    deg = 180;
    kx = i;
    ky = j;
}
if(g[i][j]  == 'L')
{
    deg = 90;
    kx = i;
    ky = j;
}
if(g[i][j]  == 'O')
{
    deg = 270;
    kx = i;
    ky = j;
}
```
</details>
  
<br>
Using only four angles to represent the direction simplifies things i.e.less angle ranges to look out for :) . Hence, every time we subtract or add 90 we do the following operation:

```cpp
deg %= 360;
```

<br>  
Also note that any time the angle is negative i.e. an 'E' instruction(subtract 90 deg) when the robot is facing North(0 deg), we can add 360 to it get a positive value which would equal the same direction change - we'll end up at the same positon. Look at the graph for further clarification:

<details>
  <summary>Graph</summary>
  
![image](https://user-images.githubusercontent.com/52543544/172056758-d78c7a84-6552-4411-8b1d-295b06a8abcb.png)
</details>
   
<br>   
Thus, for every 'D' or 'E' instruction we adjust the robot's position using this:
<details>
  <summary>Code to change directions</summary>
    
```cpp
void change_dir(char c)
{
    if(c == 'D')
    {
        deg += 90;
    }
    else if(c == 'E')
    {
        deg -= 90;
        if(deg<0){
            deg+=360;
        }
    }
    deg %= 360;
}
```
</details>

<br>
For every 'F' instruction we move:<br>
- one row up when the current orientation is 0 deg,  <br>
- one column right when the orientation is 90 deg,<br>
- one row down when the current orientation is 180 deg,  <br>
- one column left when the orientation is is 270 deg.<br>
<br>
<br>

We should check that the 'F' instructions don't make the robot move out of the grid thus we add conditions that the robot only moves if the positions are limited to (0<= current_row <= r) && (0<= current_column <= c). We should also make sure that the robot doesn't move if the 'F' instruction tells it to move into a cell marked with '#' . If the robot moves into a cell that has a sticker we add it to the number collected and mark the position with a '.' so that if the cell is revisited, it doesn't count the sticker again.

<details>
<summary>C++ Code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;
#define ll long long
int t, n, m;
int deg = 0;
vector<vector<char>> g(110, vector<char>(110));

void change_dir(char c)
{
    if(c == 'D')
    {
        deg += 90;
    }
    else if(c == 'E')
    {
        deg -= 90;
        if(deg<0){
            deg+=360;
        }
    }
    deg %= 360;
}

bool isValid(int x, int y)
{
    if(x < 0 || y < 0 || x >= n || y >= m)
    {
        return false;
    }

    if(g[x][y] == '#')
    {
        return false;
    }

    return true;
}

void make_move(int &x, int &y)
{
    if(deg == 0)
    {
        if(isValid(x - 1, y))
        {
            --x;
        }

    }
    if(deg == 90)
    {
        if(isValid(x, y + 1))
        {
            ++y;
        }

    }
    if(deg == 180)
    {
        if(isValid(x + 1, y))
        {
            ++x;
        }

    }
    if(deg == 270)
    {
        if(isValid(x, y - 1))
        {
            --y;
        }

    }

}

int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);

    
    int kx, ky, px, py,s;
    while(cin>>n>>m>>s)
    {

        if(n==m && m==s && m==0){
            break;
        }
        int stickers =0;
        

        int buff;
        bool lost = 0;
        for (int i = 0; i < n ; ++i)
        {
            for (int j = 0; j < m ; ++j)
            {
                cin >> g[i][j];
                if(g[i][j]  == 'N')
                {
                    deg = 0;
                    kx = i;
                    ky = j;
                }
                if(g[i][j]  == 'S')
                {
                    deg = 180;
                    kx = i;
                    ky = j;
                }
                if(g[i][j]  == 'L')
                {
                    deg = 90;
                    kx = i;
                    ky = j;
                }
                if(g[i][j]  == 'O')
                {
                    deg = 270;
                    kx = i;
                    ky = j;
                }

            }

        }

        string c;

        cin>>c;
        for(auto i:c){
            if(i=='D' || i=='E'){
                change_dir(i);
            }

            else if(i=='F'){
                make_move(kx, ky);

                if(g[kx][ky] == '*'){

                    // cout << deg << " " << kx << " " << ky << "\n";
                    g[kx][ky] = '.';
                    stickers++;
                }   
            }
        }

        cout << stickers ;

        cout << "\n";


    }
}
```
</details>

