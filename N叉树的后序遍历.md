# [N叉树的后序遍历](https://leetcode-cn.com/problems/n-ary-tree-postorder-traversal/)

## 方法：DFS后序遍历

### 思路与算法

DFS后序遍历。

### 代码

```c++
class Solution {
public:
    vector<int> postorder(Node* root) {
        if(!root) return {};
        vector<int> res;
        for(auto& p:root->children){
            auto tmp=postorder(p);
            res.insert(res.end(),tmp.begin(),tmp.end());
        }
        res.push_back(root->val);
        return res;
    }
};
```

```python
class Solution:
    def postorder(self, root: 'Node') -> List[int]:
        def dfs(root: 'Node') -> List[int]:
            if root is None: return []
            res=[]
            for i, p in enumerate(root.children):
                res.extend(dfs(p))
            res.append(root.val)
            return res
        return dfs(root)
```

### 复杂度分析

- **时间复杂度**：$O(n)$，$N$为节点数。

- **空间复杂度**：$O(n)$，$N$为节点数。
