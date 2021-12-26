# [Bigram分词](https://leetcode-cn.com/problems/occurrences-after-bigram/)

## 方法：遍历

### 思路与算法

第一步根据空格划分单词，第二步匹配``first``与``second``，如果匹配成功，当前单词便满足要求。

### 代码

```c++
class Solution{
public: 
    vector<string> findOcurrences(string text,string first,string second){
        vector<string> res;
        string pre1="",pre2="";
        text.push_back(' ');
        string tmp;
        for(char& ch:text){
            if(ch==' '){
                if(pre1==first&&pre2==second)
                    res.push_back(tmp);
                pre1=pre2;
                pre2=tmp;
                tmp.clear();
            }
            else
                tmp.push_back(ch);
        }
        return res;
    }       
};
```

### 复杂度分析

- **时间复杂度**：$O(N)$，$N$为字符串长度。

- **空间复杂度**：$O(1)$，只需要常数个变量存储中间值。
