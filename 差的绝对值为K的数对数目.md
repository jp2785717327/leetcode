# [差的绝对值为K的数对数目](https://leetcode-cn.com/problems/count-number-of-pairs-with-absolute-difference-k/)

## 方法：哈希表

### 思路与算法

遍历下标``j``，同时使用哈希表记录已经遍历过的数，查询哈希表得到能够与当前遍历到的数形成数对的数目，并累计到答案中。

### 代码

```c++
class Solution {
public:
    int countKDifference(vector<int>& nums, int k) {
        unordered_map<int,int> mp;
        int res=0;
        for(int& x:nums){
            res+=mp[x-k]+mp[x+k];
            mp[x]++;
        }
        return res;
    }
};
```

```python
class Solution:
    def countKDifference(self, nums: List[int], k: int) -> int:
        res = 0
        cnt = Counter()
        for x in nums:
           res += cnt[x+k]+cnt[x-k] 
           cnt[x] += 1
        return res
```

### 复杂度分析

- **时间复杂度**：$O(n)$，$n$为数组的长度。

- **空间复杂度**：$O(k)$，$k$为数组中数的种类数。 
