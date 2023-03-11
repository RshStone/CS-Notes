# 剑指Offer

按照刷题指南二刷剑指Offer

[「剑指 Offer」 - 学习计划 - 力扣（LeetCode）全球极客挚爱的技术成长平台 (leetcode-cn.com)](https://leetcode-cn.com/study-plan/lcof/?progress=d71igym)

## Day1栈与队列（简单）

### [剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

针对不同语言的 <u>Stack</u>的实现形式，Java语言 Stack类的使用问题

一个主栈，一个辅助栈

### [剑指 Offer 30. 包含min函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

一个主栈，一个辅助栈（设计含有pop出min的功能）

## Day2 链表（简单）

### [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

充分说明了递归的本质就是栈，栈的时候可以用递归去表示。

我的思路是遍历两遍，没有思考进一步优化的方法。

### [剑指 Offer 24. 反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

遍历写出来了，递归版本不熟练没写出来。练

### [剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

方法问题， HashMap原表映射新表

## Day3 字符串（简单）

### [剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

涉及到字符串的可变性问题。 

java中常考面试题， StringBuilder 和 StringBuffer的区别。

[`StringBuffer`](http://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html) is synchronized, [`StringBuilder`](http://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html) is not.



### [剑指 Offer 58 - II. 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)





## Day4 查找算法（简单）

## Day5 查找算法（中等）

## 

# 剑指Offer

## 题目

Leetcode 03 数组中重复的数字   原地排序的思想， 关键点在于思考遍历的i值增减问题

#### [剑指 Offer 04. 二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

充分利用条件然后优化，过程里清楚需要思绪。

#### [剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

Python和Java里String不可变， C++里如何对String进行扩容

#### [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

考察的点： 递归的本质就是一个栈。

#### [剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

前序遍历和中序遍历结果，构建二叉树。 利用一个HashMap来映射位置，用分治思想进行解决。

pre: root left right

in: left root right

right: left right root

#### [剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

栈入队和出队

#### [剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/) & [剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

经典dp

#### [剑指 Offer 11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

O(n) -> O(log N)

可以优化到二分查找。 一系列问题： 排序数组的查找问题可以使用二分查找





[剑指 Offer 13](#13) 机器人的运动范围]         DFS/BFS + 回溯

剪绳子 动态规划/贪心算法  **未做出来**(18min)

- DFS

  ```java
  public int movingCount(int m, int n, int k) {
          boolean[][] visited = new boolean[m][n];
          return dfs(visited, m, n, k, 0, 0);
      }
  
      private int dfs(boolean[][] visited, int m, int n, int k, int i, int j) {
          if(i >= m || j >= n || visited[i][j] || bitSum(i) + bitSum(j) > k) return 0;
          visited[i][j] = true;
          return 1 + dfs(visited, m, n, k, i + 1, j) + dfs(visited, m, n, k, i, j + 1) ;
      }
  
      private int bitSum(int n) {
          int sum = 0;
          while(n > 0) {
              sum += n % 10;
              n /= 10; 
          }
          return sum;
      }
  ```

- 剪绳子

  - dp

    核心是dp数组的函数定义，还有自底向上的思想。

    困扰我的点，绳子该怎么分？分成多少部分？分成部分不确定还能用dp或者贪心思想吗？

    看题解后

    困扰的是dp[2] = 2； dp[3] = 3这个定义，为什么？其实这部分在之前定义为绳子长度为n的最大乘积基础上，还有另一层含义，作为更大系统的子系统部分的最大值。

    数学表达是max{x1,x2}

    ```java
        public int cutRope(int target) {
            if(target < 2)return 0;
            if(target == 2)return 1;
            if(target == 3)return 2;
            int dp[] = new int[target + 1];
            dp[0] = 0;
            dp[1] = 1;
            dp[2] = 2;
            dp[3] = 3;
            int max = 0;
            for(int i = 4; i < target + 1; ++i){
                max = 0;
                for(int j = 1; j <= i/2; ++j){
                    int cur = dp[j]*dp[i-j];
                    if(max < cur){
                        max = cur;
                    }
                    dp[i] = max;
                }
            }
            max = dp[target];
            return max;
        }
    ```

  - 贪心思想

    n >=5 尽量剪成长度为3的绳子。

    n = 4，剪成2+2

    为什么？其实背后有数学推导和证明，不太容易得出。但实在没思路，可以自底向上进行尝试

    `max =(int)(Math.pow(3,timesOfThree)*Math.pow(2,timesOfTwo));`

    这个小东西折腾了一会儿，类型匹配