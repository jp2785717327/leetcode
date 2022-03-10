# [N叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/)

## 方法：递归

### 思路与算法

递归调用

### 代码

```c++
class Solution {
public:
    vector<int> preorder(Node* root) {
        if(!root) return {};
        vector<int> res;
        res.push_back(root->val);
        for(Node* p:root->children){
            auto ans=preorder(p);
            res.insert(res.end(),ans.begin(),ans.end());
        }
        return  res;
    }
};
```

```python
class Solution:
    def preorder(self, root: 'Node') -> List[int]:
        res=[]
        def dfs(node:'Node') -> None:
            if root is None: return
            res.append(node.val)
            for  i,p in enumerate(node.children):
                dfs(p)
        dfs(root)
        return res
```

### 复杂度分析

- **时间复杂度**：$O(m)$，$m$为节点数量。

- **空间复杂度**：$O(m)$，$m$为节点数量。
