# Leetcode 948 令牌放置
***
### 题目描述
你的初始能量位`P`，初始分数为`0`，只有一包令牌。  

令牌的值为`token[i]`，每个令牌最多只能使用一次，可能的两种使用方法如下：  

* 如果你至少有`token[i]`点能量，可以将令牌置为正面朝上，失去`token[i]`点能量，并得到`1`分。   
* 如果我们至少有`1`分，可以将令牌置为反面朝上，获得`token[i]`点能量，并失去一分。  

在使用任意数量的令牌后，返回我们可以得到的最大分数。


**示例1:**   
	
	输入：tokens = [100], P = 50
	输出：0
	

**示例2:**   
	
	输入：tokens = [100,200], P = 150
	输出：1
	
	
**示例3:**   
	
	输入：tokens = [100,200,300,400], P = 200
	输出：2
	
    	
**提示：**  

* `tokens.length <= 1000`
* `0 <= tokens[i] < 10000`
* `0 <= P < 1000`
	

### 考点

* 双指针+贪心

### 思路    
指针一直指向当前最小能量对应的令牌，循环中一直用自己已有的能量一直翻转所需能量最小的令牌换取分数，直到不能换为止，然后用一个分数去翻转能得到最大能量的令牌。一直循环，直到分数为0或者所有令牌都已翻转为止。


### 代码  
执行用时: **276ms**, 内存消耗: **12.9MB** 

```
class Solution:
    def bagOfTokensScore(self, tokens: List[int], P: int) -> int:
        tokens.sort()
        l, r = 0, len(tokens) - 1
        res = 0
        while l <= r:
            if P < tokens[l]:
                if res == 0 or l == r:
                    break
                else:
                    res -= 1
                    P += tokens[r]
                    r -= 1
            else:
                res += 1
                P -= tokens[l]
                l += 1
        
        return res        
```









	
