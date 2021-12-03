# [K 次取反后最大化的数组和](https://leetcode-cn.com/problems/maximize-sum-of-array-after-k-negations/)

## 方法：分类讨论

### 思路与算法

维护两个数组，一个数组内放正数的绝对值（含0），一个数组内放负数的绝对值并排序，负数的个数为``m``，如果``K<m``，则依次翻开前``k``个负数（绝对值排序后）。如果``k``比``m``大的部分是偶数，则全部能翻成正数，如果偶数，则选一个绝对值最小的为负数，其余皆为正数。

### 代码

```c++
class Solution {
public:
    int largestSumAfterKNegations(vector<int>& nums, int k) {
        vector<int> nums1;
        vector<int> nums2;
        int mi=abs(nums[0]);
        for(int &x:nums){
            if(x>=0) nums1.push_back(x);
            else nums2.push_back(-x);
            mi=min(mi,abs(x));
        }
        int sum1=accumulate(nums1.begin(),nums1.end(),0);
        int sum2=accumulate(nums2.begin(),nums2.end(),0);
        sort(nums2.rbegin(),nums2.rend());
        int res=0;
        if(k<nums2.size()){
            res=sum1-sum2;
            for(int i=0;i<k;i++)
                res+=2*nums2[i];
        }
        else{
            k-=nums2.size();
            if(k%2) res=sum1+sum2-2*mi;
            else res=sum1+sum2;
        }
        return res;
    }
};
```

### 复杂度分析

- **时间复杂度：**$O(NlogN)$，这是最坏情况，$N$为数组长度。
- **空间复杂度：**$O(N)$，$N$为数组长度。