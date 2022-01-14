# [查找和最小的K对数字](https://leetcode-cn.com/problems/find-k-pairs-with-smallest-sums/)

## 方法：优先队列+N路归并

### 思路与算法

令``n1``为数组``nums1``的长度，令``n2``为数组``nums2``的长度。以此用数组``nums1``中的数与数组``nums2``中的每一个数相加，即为和的所有情况。

依照上述思路可以构造出``n1``路``n2``长度的递增数组，则上题转换为归并``n1``路数组的问题。

定义数组``p[n1]``记录每一路当前遍历索引，使用优先队列实时维护当前各路遍历值的最小值处于哪一路。

### 代码

```c++
class Solution {
public:
    vector<vector<int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {
        int n1=(int)nums1.size(),n2=(int)nums2.size();
        vector<int> p(n1,0);
        vector<vector<int>> res;
        priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> q;
        for(int i=0;i<n1;i++){
            q.push({nums2[p[i]]+nums1[i],i});
        }
        while(!q.empty()&&k-->0){
            pair<int,int> tmp=q.top();
            int idx=tmp.second;
            q.pop();
            res.push_back({nums1[idx],nums2[p[idx]]});
            p[idx]++;
            if(p[idx]<n2)
                q.push({nums2[p[idx]]+nums1[idx],idx});
        }
        return res;
    }
};
```

### 复杂度分析

- **时间复杂度**：$O(klog(n))$，优先队列维护最小值需要时间复杂度$O(logn)$，需要取出K个最小的和。

- **空间复杂度**：$O(n)$。
