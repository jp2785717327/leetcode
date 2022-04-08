# [N叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)

## 方法：BFS

### 思路与算法

- BFS遍历，逐层存放节点于队列中。

### 代码

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(Node* root) {
        if(!root) return {};
        vector<vector<int>> res;
        queue<Node*> q;
        q.push(root);
        while(!q.empty()){
            vector<int> ans;
            int len=q.size();
            for(int i=0;i<len;i++){
                for(Node* p:q.front()->children){
                    if(p) q.push(p);
                }
                ans.push_back(q.front()->val);
                q.pop();
            }
            res.push_back(ans);
        }
        return res;
    }
};
```

```python
class Solution:
    def levelOrder(self, root: 'Node') -> List[List[int]]:
        if not root: return []
        res=list()
        q=deque([root])
        while q:
            cnt=len(q)
            ans=list()
            for _ in range(cnt):
                cur=q.popleft()
                ans.append(cur.val)
                for p in cur.children:
                    q.append(p)
            res.append(ans)
        return res
```

### 复杂度分析

- **时间复杂度**：$O(n)$，$n$为节点的数量。

- **空间复杂度**：$O(w)$，$w$为树的最大宽度。
