# [UTF-8编码验证](https://leetcode-cn.com/problems/utf-8-validation/)

## 方法：递归

### 思路与算法

递归的判断后续字节是否满足UTF-8编码。

### 代码

```c++
class Solution {
public:
    bool validUtf8(vector<int>& data) {
        reverse(data.begin(),data.end());
        function<bool(vector<int>&)> check=[&](vector<int>& data){
            if(data.empty()) return true;
            int k=0;
            while(k<=4&&data.back()&(1<<(7-k))){
                k++;
            }
            if(k==1||k>4) return false;
            data.pop_back();
            if(k!=0) k--;
            for(int i=0;i<k;i++){
                if(data.empty()) return false;
                if((data.back()/64)!=2) return false;
                data.pop_back();
            }
            return check(data);
        };
        return check(data);
    }
};
```

```python
class Solution:
    def validUtf8(self, data: List[int]) -> bool:
        data=data[::-1]
        def check(data: List[int]) -> bool:
            if data==[]: return True
            k=0
            while k<=4 and data[-1]&(1<<(7-k)):
                k+=1
            if k==1 or k>4: return False
            data.pop()
            if k!=0: k-=1
            for i in range(k):
                if data==[]: return False
                if (data[-1]//64)!=2: return False
                data.pop()
            return check(data)
        return check(data)
```

### 复杂度分析

- **时间复杂度**：$O(n)$，$n$为字节长度。

- **空间复杂度**：$O(k)$，$k$为瞒住UTF编码的个数。
