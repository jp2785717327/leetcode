# [两数之和4-输入BST](https://leetcode-cn.com/problems/two-sum-iv-input-is-a-bst/)

## 方法：先序遍历+哈希集合

### 思路与算法

遍历每个节点的值并使用哈希集合记录已经遍历过的数，以当前节点值为基准根据哈希集合查看所需的另一个数是否已经遍历。

### 代码

```c++
class Solution {
public:
    bool findTarget(TreeNode* root, int k) {
        unordered_set<int> se;
        function<bool(TreeNode*)> dfs=[&](TreeNode* node){
            if(!node) return false;
            if(se.count(k-node->val))
                return true;
            se.insert(node->val);
            return dfs(node->left)||dfs(node->right);
        };
        return dfs(root);
    }
};
```

```python
class Solution:
    def findTarget(self, root: Optional[TreeNode], k: int) -> bool:
        s=set()
        def dfs(node: Optional[TreeNode]) -> bool:
            if node is None: return False
            if (k-node.val) in s: return True
            s.add(node.val)
            return dfs(node.left) or dfs(node.right)
        return dfs(root)
```

### 复杂度分析

- **时间复杂度**：$O(n)$，$n$为节点数。

- **空间复杂度**：$O(n)$，$n$为节点数。
