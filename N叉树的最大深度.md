# [N叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-n-ary-tree/)

## 方法一：深度优先搜索（DFS）

### 思路与算法

首先令当前节点深度初始化为1，假设当前节点下有$N$个子节点，在for循环中$dfs$遍历这$N$个子节点的深度$depth$ <sub>$n$</sub> ，取其最大深度$max_child_depth+1$即为当前节点最大深度。每个节点按照同样原则计算。

所以递归计算出当前节点的所有子节点最大深度后，选取最大值+1这是当前节点的最大深度。

### 代码

```c++
class Solution {
public:
    int maxDepth(Node* root) {
        if(!root) return 0;
        int depth=1;
        for(Node* nod:root->children){
            depth=max(depth,maxDepth(nod)+1);
        }
        return depth;
    }
};
```

### 复杂度分析

**时间复杂度：**$O(N)$，$N$为节点个数。因为每个节点都会被递归访问一次，所以时间复杂度为$O(N)$。

**空间复杂度：**$O(depth)$，$depth$为多叉树深度。递归需要用到栈空间，而栈空间最大即为树深。

## 方法二：广度优先搜索（BFS）

### 思路与算法

这里我们可以按层去遍历所有节点，返回最大层数，即$BFS$遍历。我们这里用``pair<Node*,int>``中第二个值去维护层深度。

- 创建一个``queue<pair<Node*,int>>``用来顺序存放节点。
- 每次从队列头部取出节点，并将该节点的子节点插入队列尾部，同时深度+1。这样就能保证对节点的访问是按照层序进行的。
- 当队列为空时，当前遍历到的最后节点的深度就是多叉树的最大深度。

### 代码

```c++
class Solution {
public:
    int maxDepth(Node* root) {
        if(!root) return 0;
        queue<pair<Node*,int>> q;
        q.push(make_pair(root,1));
        int depth=0;
        while(!q.empty()){
            pair tmp=q.front();
            q.pop();
            depth=tmp.second;
            for(Node* nod:tmp.first->children){
                q.push(make_pair(nod,depth+1));
            }
        }
        return depth;
    }
};
```

### 复杂度分析

**时间复杂度：**$O(N)$，$N$为节点个数。因为每个节点都会被递归访问一次，所以时间复杂度为$O(N)$。

**空间复杂度：**$O(1)至O(N)$，用于队列中存放的是相邻两层的节点数，所以占用的最大队列空间与多叉树的最大层宽正相关。