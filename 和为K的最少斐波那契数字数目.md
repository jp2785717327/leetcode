# [和为K的最少斐波那契数字数目](https://leetcode-cn.com/problems/find-the-minimum-number-of-fibonacci-numbers-whose-sum-is-k/)

## 方法：贪心

### 思路与算法

- 首先根据输入构建有限长度的斐波那契数列。每次都选取不大于K的最大的斐波那契数，用K减去该数，重复上述操作直到K等于0。

- 证明思路：只需要证明存在一种操作次数最少的选取斐波那契数方案，该方案选取了不超过K的最大斐波那契数字。

### 代码

```c++
class Solution {
public:
    int findMinFibonacciNumbers(int k) {
        vector<int> f={1};  // 存放斐波那契数
        int sum=1;
        while(sum<=k){
            int a=f.back();
            f.emplace_back(sum);
            sum+=a;
        }
        int res=0;
        for(int i=(int)f.size()-1;i>=0&&k>0;i--){
            if(k>=f[i]){
                res++;
                k-=f[i];
            }
        }
        return res;
    }
};
```

### 复杂度分析

- **时间复杂度**：$O(logn)$，$n$为输入的数。

- **空间复杂度**：$O(logn)$。
