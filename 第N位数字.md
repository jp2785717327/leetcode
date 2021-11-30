# [第N位数字](https://leetcode-cn.com/problems/nth-digit/)

## 方法：数学计算

### 思路与算法

我们观察数字规律不难发现1-9有个9个一位数，10-99有90个二位数，100-999有900个三位数......，根据上述规律可以先判断第N个数处于哪个数字段，然后在进一步判断该数在那个数字段的第几个数的第几位即可。

### 代码

```c
class Solution {
public:
    int findNthDigit(int n) {
        int i=1;
        long long sum=9;
        long long sums=sum*i;
        while(n>sums){
            n-=sums;
            sum*=10;
            sums=sum*++i;
        }
        int k=(n-1)/i;
        int rest=(n-1)%i;
        int num=sum/9;
        int val=num+k;
        int c=i-rest;
        int res;
        while(c-->0){
            res=val%10;
            val/=10;
        }
        return res;
    }
};
```

### 复杂度分析

- **时间复杂度：**$O(lgn)$，$n$为输入。
- **空间复杂度：**$O(1)$。

