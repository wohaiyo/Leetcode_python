# Leetcode 面试题 62 圆圈中最后剩下的数字

***
### 题目描述

0,1,,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字。求出这个圆圈里剩下的最后一个数字。

例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。


**示例1：**

	输入: n = 5, m = 3
	输出: 3

**示例2：**

	输入: n = 10, m = 17
	输出: 2


**说明：**

* `1 <= n <= 10^5`
* `1 <= m <= 10^6`



**考点**

数组

**思路**

记f(n)为游戏结束后最后一个数字的index，那么关键在于找到f(n,start=0)和f(n-1,start=0)的关系。显然，第一次扔出去的元素是(m-1)%n，记作k，那么根据游戏规则f(n,start=0)=f(n-1,start = k+1)。接下来我们可以看到f(n-1,start = k+1) = (f(n-1,start=0)+k+1)%n。有了这个中间桥梁，可知f(n,start=0) = (f(n-1,start=0)+k+1)%n = (f(n-1,start=0)+m)%n。然后从f(1)=0推广过去即可。

迭代公式为：f(n) = (f(n-1)+m)%n

### 代码
执行用时: **48ms**, 内存消耗: **13.4MB**

```
class Solution:
    def lastRemaining(self, n: int, m: int) -> int:
        res = 0
        for i in range(2, n+1):
            res = (res + m) % i
        return res
```



