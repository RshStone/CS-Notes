# 剑指Offer

## 题目

[剑指 Offer 13](#13) 机器人的运动范围]         DFS/BFS + 回溯

剪绳子 动态规划/贪心算法  **未做出来**(18min)



## 题解

- 剑指 Offer<a name = "13">13</a>

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