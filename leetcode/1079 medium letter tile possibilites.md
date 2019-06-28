# letter tile possibilities
[leetcode出处](https://leetcode.com/problems/letter-tile-possibilities/)

```c++

#include <iostream>
#include <string.h>
#include <string>
#include <map>
using namespace std;

class Solution{
    public:
        int numTilePossibilities(string tiles){
            int len = tiles.size();
            int cnt[26];
            memset(cnt,0,sizeof(cnt));

            for (char i : tiles)
            {
                cnt[i-'A']++;
               // cout<<cnt[i-'A']<<endl;
            }
            return dfs(cnt);
            
        }
        int dfs(int cnt[]){
            int sum = 0;
            for (int i = 0; i < 26; i++)
            {
                if(cnt[i]==0) continue;
                sum++;
                cnt[i]--;
                sum+=dfs(cnt);
                cnt[i]++;
                /* code */
            }
            return sum;
        }
        Solution(){

        }
};



int main(){
    Solution *so = new Solution();
    cout<<so->numTilePossibilities("AAB");
    getchar();
    return 0;
}
```


以下思路来源 https://leetcode.com/problems/letter-tile-possibilities/discuss/308284/Concise-java-solution


input: AAB
count: A -> 2, B -> 1

For sequence of length 1:

We can pick either A, or B.
So we have "A", "B".

For sequence of length 2:

We build it based on "sequence of length 1"
For "A": 
count: A -> 1, B -> 1
We can still pick either A, or B
So we have "AA", "AB"
For "B": 
count: A -> 2, B -> 0
We can only pick A
So we have "BA"

For sequence of length 3: blablabla

Implementation

We don't need to keep track of the sequence. We only need count
If we implement the above idea by each level (Count all sequence of length 1, then count all sequence of length 2, etc), we have to remember previous sequence.
So we use recursion instead. Just remember to add the count back (arr[i]++).