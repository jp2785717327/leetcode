# [Z字形变换](https://leetcode-cn.com/problems/zigzag-conversion/)

## 方法：数学

### 思路与算法

按行依次直接计算出当前字符在原字符串中的下标索引，然后加入答案。

### 代码

```c++
class Solution {
public:
    string convert(string s, int numRows) {
        int n=s.length();
        if(numRows==1) return s;
        string res;
        for(int i=0;i<numRows;i++){
            for(int j=i;j<n;j+=(2*numRows-2)){
                res.push_back(s[j]);
                int next=j+2*(numRows-1-i);
                if(i!=0&&i!=numRows-1&&next<n)
                    res.push_back(s[next]);
            }
        }
        return res;
    }
};
```

```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows==1: return s
        res=[]
        for i in range(0,numRows):
            for j in range(i,len(s),2*numRows-2):
                res.append(s[j])
                next=j+2*(numRows-1-i)
                if i!=0 and i!=numRows-1 and next<len(s):
                    res.append(s[next])
        return ''.join(res)
```

### 复杂度分析

- **时间复杂度**：$O(n)$，$n$为字符串长度。

- **空间复杂度**：$O(1)$，返回值不计入空间复杂度。
