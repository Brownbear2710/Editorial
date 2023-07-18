# [H - Tree Recovery](https://vjudge.net/problem/UVA-536)

We simply traverse the left subtree then the right subtree and output the root node elements. Code is commented for further clarification. <br>
<br>
Idea and code(kind-of :3) from [here](https://www.cnblogs.com/mofushaohua/p/7789353.html)
<details>
<summary>C++ Code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;
#define ll long long


string pre, in, post;



void construct(int l1, int r1, int l2, int r2)
{

    if(l1 > r1)
    {
        return ; //no more elements left to check
    }


    int root_in_inorder = l2; //we consider the root in inorder is at the index passed as l2

    for(;; root_in_inorder++)
    {
        // we then see if index we considered is actually the position of the root else we update
        if(pre[l1] == in[root_in_inorder])
        {
            break;
        }
    }


    //number of elements to the left of the root in the the inorder
    int number_of_elements_in_left_subtree = root_in_inorder - l2;

    //recurse the left subtree
    construct(l1 + 1, l1 + number_of_elements_in_left_subtree, l2, root_in_inorder - 1);
    //recurse the right subtree
    construct(l1 + 1 + number_of_elements_in_left_subtree, r1, root_in_inorder + 1, r2);
    //print root
    cout << in[root_in_inorder];
}
int main()
{



    while(cin >> pre >> in)
    {

        construct(0, pre.size() - 1, 0, in.size() - 1);;

        cout << "\n";


    }
}
```
</details>
