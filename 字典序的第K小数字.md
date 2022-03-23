# [字典序的第K小数字](https://leetcode-cn.com/problems/k-th-smallest-in-lexicographical-order/)

## 方法：字典树思想

- 将数字看成字符串可以构建字典树，可以发现按字典序从小到达排序，就等效于前序遍历字典树。

- 定义方法``getSteps(int curr,long n)``用来计算节点``curr``的子树中节点值小于``n``的个数。

- 当当前节点的子树包含的小于``n``的节点个数大于``k``时，则将当前节点进入下一层节点。这样可以保证得到的节点字典序最小。

### 代码

```c++
class Solution{
public:
    int findKthNumber(int n,int k){
        auto getSteps=[](int curr,long n){
            int steps=0;
            long first=curr;
            long last=curr;
            while(first<=n){
                steps+=min(last,n)-first+1;
                first=first*10;
                last=last*10+9;
            }
            return steps;
        };
        int cur=1;
        k--;
        while(k>0){
            int steps=getSteps(cur,n);
            if(steps<=k){
                k-=steps;
                cur++;
            }
            else{
                k--;
                cur*=10;
            }
        }
        return cur;
    }
};
```

```python
class Solution:
    def findKthNumber(self, n: int, k: int) -> int:
        def getSteps(curr: int, n: int) -> int:
            steps,first,last=0,curr,curr
            while first<=n:
                steps+=min((last,n))-first+1
                first=first*10
                last=last*10+9
            return steps
        cur=1
        k-=1
        while k>0:
            steps=getSteps(cur,n)
            if steps<=k:
                k-=steps
                cur+=1
            else:
                k-=1
                cur*=10
        return cur
```

### 复杂度分析

- **时间复杂度**：$O(log^2n)$，每次计算子树节点的搜索深度最大为$O(log_{10}n)$，最多需要搜索$O(log_{10}n)$层。

- **空间复杂度**：$O(1)$。
