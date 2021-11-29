# [第K个最小素数分数](https://leetcode-cn.com/problems/k-th-smallest-prime-fraction/)

## 方法：优先队列

### 思路与算法

固定分母，分子越小，分数值越小。根据分母的值不同，可以得到多路严格递增的序列。然后可以参考合并K个升序链表的方法，使用优先队列来维护不同递增序列中的当前最小情况。优先队列经过K次弹出后返回的便是第K小的素数分数。

### 代码

```c++
class Solution {
public:
    vector<int> kthSmallestPrimeFraction(vector<int>& arr, int k) {
		int n=arr.size();
        function<bool(const pair<int,int>& x, const pair<int,int>& y)> cmp=[&](const pair<int,int>& x, const pair<int,int>& y){
            return arr[x.first]*arr[y.second]>arr[y.first]*arr[x.second];
        };
        priority_queue<pair<int,int>,vector<pair<int,int>>,decltype(cmp)> q(cmp);
        for(int i=1;i<n;i++){
            q.push(make_pair(0,i));
        }
        pair<int,int> ret;
        for(int i=0;i<k;i++){
            ret=q.top();
            q.pop();
            if(ret.first+1<ret.second){
                q.push(make_pair(ret.first+1,ret.second));
            }
        }
        return {arr[ret.first],arr[ret.second]};
    }
};
```

### 复杂度分析

- 时间复杂度：$O(klogn)$，$n$是数组arr的长度，$k$是选取的第$k$个最小的素数分数。
- 空间复杂度：$O(n)$，$n$是数组arr的长度。

