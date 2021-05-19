# leetcode

# Goals

主要目的是为了给自己快速复习和查漏补缺进行食用。

这类笔记的要点就是要精简，不够精简的详细（说明大概率不会做），精简完了的可能会遗忘，需要时长巩固与复习，就是无聊的时候写一些，不会分析为什么再写。

采用的是小时间+高频词的复习方法

## Array

单纯的数组是没什么好提的，不过数组和链表作为最基础的数据结构，它们可以和很多东东结合，来变得有趣。比如，数组是以什么顺序排的？降序、无序或者升序？

我做过的题的一个简单预览：

1.Two Sum array + hashtable

| 4    | [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays) hard | Array+BinarySearch                  |
| ---- | ------------------------------------------------------------ | ----------------------------------- |
| 1    | [Two Sum](https://leetcode.com/problems/two-sum) easy        | Array+HashTable                     |
| 26   | [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array)easy | Array+TwoPointers                   |
| 34   | [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array)medium | Array+BinarySearch                  |
| 53   | [Maximum Subarray](https://leetcode.com/problems/maximum-subarray)easy | Array在线处理/DP                    |
| 56   | [Merge Intervals](https://leetcode.com/problems/merge-intervals)medium | Array+sort(Arrays.sort()的调用方法) |
| 80   | [Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii)Medium | Array+TwoPointers                   |
| 88   | [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array)Easy | Array+TwoPointers                   |
| 121  | [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock)Easy | Array+Dp                            |
| 122  | [Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii)Easy | Array+Dp                            |
| 289  | [Game of Life](https://leetcode.com/problems/game-of-life)Medium | 纯Array(有难度)                     |
| 581  | [Shortest Unsorted Continuous Subarray](https://leetcode.com/problems/shortest-unsorted-continuous-subarray)Medium | Array+TwoPointers(感觉这道题不错)   |
| 674  | [Longest Continuous Increasing Subsequence](https://leetcode.com/problems/longest-continuous-increasing-subsequence)Easy | Array+sliding window Or dp          |
| 941  | [Valid Mountain Array](https://leetcode.com/problems/valid-mountain-array)Easy | Array                               |
| 977  | [Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array) | Array+Sort(要你自己写)              |
| 1010 | [Pairs of Songs With Total Durations Divisible by 60](https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60)Medium | Array                               |

| 1437 | [Check If All 1's Are at Least Length K Places Away](https://leetcode.com/problems/check-if-all-1s-are-at-least-length-k-places-away)easy | Array                 |
| ---- | ------------------------------------------------------------ | --------------------- |
| 1539 | [Kth Missing Positive Number](https://leetcode.com/problems/kth-missing-positive-number)Easy | Array+Hash Table      |
| 1640 | [Check Array Formation Through Concatenation](https://leetcode.com/problems/check-array-formation-through-concatenation)Easy | Array Hash Table Sort |
| 1758 | [Minimum Changes To Make Alternating Binary String](https://leetcode.com/problems/minimum-changes-to-make-alternating-binary-string)Easy | Array Greedy          |
|      |                                                              |                       |

40min；回忆了几道题和列出了所做过的题的标签

## Tree

### 思考方式

树的基本框架的构建，是用BFS还是DFS，BFS怎么用，DFS的话是pre,in,post中的哪一个或者只是要对树进行单纯的遍历。结合树的类型一般的树，二叉树，二叉搜索树等。

方案的时间复杂度和空间复杂度是怎么样的。

难点：想清楚递归，递归终止条件，是否是大问题转化为小问题，每个小问题是否独立。

### 涉及到的题目

[leetcode110](#110)平衡二叉树 涉及到高度

[剑指Offer 32](#从上到下打印二叉树系列)从上到下打印二叉树 层序遍历+一些变形

[剑指Offer 07](#重建二叉树)重建二叉树 利用不同dfs结果的特点逆向进行思考

[剑指Offer 34](#二叉树中和为某一值的路径)二叉树中和为某一值的路径

[leetcode449](#449. Serialize and Deserialize BST)Serialize and Deserialize BST

[leetcode98](#98)Validate Binary Search Tree 中序遍历

[leetcode124](#124)Binary Tree Maximum Path Sum

[leetcode173](#173)Binary Search Tree Iterator

### 具体的题解

- leetcode<a name="110">110</a>

平衡二叉树 两种方法

自顶而下暴力解

自底而上（How: 后序遍历）+ 剪枝思想

4.8 again 写辅助函数的时候，采用DFS中的哪种模式？返回值为int的时候，终止条件，递归函数，返回值等如何思考。

- 剑指Offer 32 - I, II, III <a name="从上到下打印二叉树系列">从上到下打印二叉树系列 </a>

基本框架是层序遍历 --> Queue数据结构 --> 实现形式 `Array` Or `LinkedList` --> if `LinkedList` 注意 `LinkedList Interface`
API `addFirst` `addLast`

API调用 一般`Queue` `FIFO` 注意 `PriorityQueue` 和 `LIFO` `Queue` --> `Stack` --> Java `Deque`

|         | Throws exception          | Returns special value   |
| ------- | ------------------------- | ----------------------- |
| Insert  | [`add(e)`](#add(E))       | [`offer(e)`](#offer(E)) |
| Remove  | [`remove()`](#remove())   | [`poll()`](#poll())     |
| Examine | [`element()`](#element()) | [`peek()`](#peek())     |

分别的要求

一层的节点按照从左到右的顺序打印 简单层序遍历

同一层的节点按从左到右的顺序打印，每一层打印到一行 层序遍历中加一个for语句

第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推 Deque + 分类处理

- [剑指Offer 07]<a name = "重建二叉树"> 重建二叉树</a>(https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof)

  不会的：看题解 重构二叉树 编号07 思维：首先想清楚一个整理步骤 然后递进 分治思想进来啦， 最后的难点在于应用分治的边界选择问题3.23再刷不会**

  分治思想下的树的边界条件，左子树，右子树，从那开始，在哪结束，用什么方法能够让inorder和preorder两个数组进行联动起来？

  分治思想下的辅助方法怎么写，递归结束条件是什么，递归的实际含义是什么？子问题是怎么样的。</a>

```java
class Solution {
    int[] preorder;
    HashMap<Integer, Integer> hp = new HashMap<>();
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        this.preorder = preorder;
        for(int i = 0; i < inorder.length; i++){
            hp.put(inorder[i],i);
        }
        return helper(0,0, inorder.length-1);
    }
    public TreeNode helper(int root, int left, int right){
        if(left > right)return null;
        TreeNode node = new TreeNode(preorder[root]);
        int i = hp.get(preorder[root]);
        node.left = helper(root+1,left,i-1);
        node.right = helper(root + i - left + 1,i+1,right);
        return node;
    }
}
```

- [剑指Offer 34]<a name = "二叉树中和为某一值的路径"> 二叉树中和为某一值的路径</a>(https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof)

  回溯思想 : 先序遍历+记录

- [leetcode449]<a name = "449. Serialize and Deserialize BST">449. Serialize and Deserialize
  BST</a>(https://leetcode.com/problems/serialize-and-deserialize-bst/)

  serialize & deserialize

  ```java
  public class Codec {
  
      // Encodes a tree to a single string.
      StringBuilder sb = new StringBuilder();
      public String serialize(TreeNode root) {
          inorder(root);
          if(!sb.toString().equals("")){sb.deleteCharAt(sb.length()-1);}
          return sb.toString();
      }
      public void inorder(TreeNode root){
          if(root == null)return;
          sb.append(root.val);
          sb.append(",");
          inorder(root.left);
          inorder(root.right);
      }
  
      // Decodes your encoded data to tree.
  public TreeNode deserialize(String data) {
          if (data.isEmpty()) return null;
          Queue<String> q = new LinkedList<>(Arrays.asList(data.split(",")));
          return deserialize(q, Integer.MIN_VALUE, Integer.MAX_VALUE);
      }
      
      public TreeNode deserialize(Queue<String> q, int lower, int upper) {
          if (q.isEmpty()) return null;
          String s = q.peek();
          int val = Integer.parseInt(s);
          if (val < lower || val > upper) return null;
          q.poll();
          TreeNode root = new TreeNode(val);
          root.left = deserialize(q, lower, val);
          root.right = deserialize(q, val, upper);
          return root;
      }
  }
  
  ```

    - leetcode<a name="98">98</a>Validate Binary Search Tree

      一眼看出中序遍历，BST的中序遍历有数据值递增的性质。问题就转化为判断此树中序遍历后的结果是否为递增。

      容器储存遍历的结果——优化：1、参数上优化，加上min和max 2、用一个pre节点储存上一次遍历的值，与当前值进行比较。

    - leetcode<a name="124">124</a>Binary Tree Maximum Path Sum

      写出基本框架后，发现需要用一个全局变量max来处理路径的最大值。

      ```java
          //my code
          //适用条件：作为当前一个子树的maxSum传到子树所在的root节点
          //报错情况:[-3][-1]直接求root节点maxPathSum的情况未考虑
          public int maxPathSum(TreeNode root) {
              if(root == null)return 0;
              int left = maxPathSum(root.left);
              if(left < 0 )left = 0;
              int right = maxPathSum(root.right);
              if(right < 0)right = 0;
              return Math.max(Math.max(left + root.val + right, left), right);
          }
      ```

      ```c++
      //相似思路的题解代码
      int max = Integer.MIN_VALUE;
          public int maxPathSum(TreeNode root) {
              if (root == null) {
                  return 0;
              }
              dfs(root);
              return max;
          }
          public int dfs(TreeNode root) {
              if (root == null) {
                  return 0;
              }
              int leftMax = Math.max(0, dfs(root.left));
              int rightMax = Math.max(0, dfs(root.right));
              max = Math.max(max, root.val + leftMax + rightMax);
              return root.val + Math.max(leftMax, rightMax);
          }
      ```

        - leetcode<a name="173">173</a> Binary Search Tree Iterator

          一般的思路ArrayList储存每一个节点，hasNext(),next(), Time complexity: O(1) O(1) Space complexity:O(n)

          n- the node of the tree

          升级想法：Space complexity:O(h)    h-the height of the tree

          ```
          Before I come up with this solution, I really draw a lot binary trees and try inorder traversal on them. We all know that, once you get to a TreeNode, in order to get the smallest, you need to go all the way down its left branch. So our first step is to point to pointer to the left most TreeNode. The problem is how to do back trace. Since the TreeNode doesn't have father pointer, we cannot get a TreeNode's father node in O(1) without store it beforehand. Back to the first step, when we are traversal to the left most TreeNode, we store each TreeNode we met ( They are all father nodes for back trace).
          
          After that, I try an example, for next(), I directly return where the pointer pointing at, which should be the left most TreeNode I previously found. What to do next? After returning the smallest TreeNode, I need to point the pointer to the next smallest TreeNode. When the current TreeNode has a right branch (It cannot have left branch, remember we traversal to the left most), we need to jump to its right child first and then traversal to its right child's left most TreeNode. When the current TreeNode doesn't have a right branch, it means there cannot be a node with value smaller than itself father node, point the pointer at its father node.
          
          The overall thinking leads to the structure Stack, which fits my requirement so well.
          ```

          ```java
          public class BSTIterator {
              
              private Stack<TreeNode> stack;
              public BSTIterator(TreeNode root) {
                  stack = new Stack<>();
                  TreeNode cur = root;
                  while(cur != null){
                      stack.push(cur);
                      if(cur.left != null)
                          cur = cur.left;
                      else
                          break;
                  }
              }
          
              /** @return whether we have a next smallest number */
              public boolean hasNext() {
                  return !stack.isEmpty();
              }
          
              /** @return the next smallest number */
              public int next() {
                  TreeNode node = stack.pop();
                  TreeNode cur = node;
                  // traversal right branch
                  if(cur.right != null){
                      cur = cur.right;
                      while(cur != null){
                          stack.push(cur);
                          if(cur.left != null)
                              cur = cur.left;
                          else
                              break;
                      }
                  }
                  return node.val;
              }
          }
          ```

## Backtracking

### 学习参考

[fucking-algorithms](https://github.com/labuladong/fucking-algorithm/blob/master/%E7%AE%97%E6%B3%95%E6%80%9D%E7%BB%B4%E7%B3%BB%E5%88%97/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95%E8%AF%A6%E8%A7%A3%E4%BF%AE%E8%AE%A2%E7%89%88.md)

### 思想

**解决一个回溯问题，实际上就是一个决策树的遍历过程**。你只需要思考 3 个问题：

1、路径：也就是已经做出的选择。

2、选择列表：也就是你当前可以做的选择。

3、结束条件：也就是到达决策树底层，无法再做选择的条件。

代码方面，回溯算法的框架：

```python
result = []
def backtrack(路径, 选择列表):
    if 满足结束条件:
        result.add(路径)
        return
    
    for 选择 in 选择列表:
        做选择
        backtrack(路径, 选择列表)
        撤销选择
```

### 题目列表

[leetcode10](#10)正则表达式匹配

[leetcode51](#51)N皇后

[leetcode93](#93)复原IP地址

[leetcode46](#46)全排列

[剑指 Offer 12](#剑指 12)矩阵中的路径

[剑指 Offer 13](#剑指 13)机器人的运动范围

### 具体题解

- leetcode<a name="51">51</a>

  框架练习

  ```java
  class Solution {
      private List<List<String>> res = new ArrayList<>();
      /* 输入棋盘边长 n，返回所有合法的放置 */
      public List<List<String>> solveNQueens(int n) {
          // '.' 表示空，'Q' 表示皇后，初始化空棋盘。
          char[][] board = new char[n][n];
          for (int i = 0; i < n; i++) {
              for (int j = 0; j < n; j++) {
                  board[i][j] = '.';
              }
          }
          //回溯 (路径，选择列表)
          backtrack(board, 0);
          return res;
      }
      // 路径：board 中小于 row 的那些行都已经成功放置了皇后
      // 选择列表：第 row 行的所有列都是放置皇后的选择
      // 结束条件：row 超过 board 的最后一行// 触发结束条件
      public void backtrack(char[][] board, int row){
          //结束条件
          if(row == board.length){
              //将char转为List,并将结果添加到res中
              res.add(construct(board));
          }
          //做选择
          for(int col = 0; col < board.length; col++){
              //判断是否有效
              if(isValid(board, row, col)){
                  board[row][col] = 'Q';
                  backtrack(board, row + 1);
                  board[row][col] = '.';
              }
        }
      }
    public List<String> construct(char[][] board){
          List<String> path = new ArrayList<>();
        for (char[] each:board) {
              path.add(new String(each));
        }
          return path;
    }
      public boolean isValid(char[][] board, int row, int col){
        if(row < 0 || row >= board.length || col < 0 || col >= board.length)return false;
          //第row行
          for(int i = 0; i < board[0].length; i++){
              if(board[row][i] == 'Q'){
                  return false;
              }
          }
          //第col列
          for(int i = 0; i < board.length; i++){
              if(board[i][col] == 'Q'){
                  return false;
              }
          }
          //board[row][col]的两条对角线
          //right-up
          for(int i = row, j = col; i >= 0 && j < board[0].length; i--,j++){
              if(board[i][j] == 'Q'){
                  return false;
              }
          }
          //right-down
          for(int i = row, j = col; i < board.length && j >= 0; i++,j--){
              if(board[i][j] == 'Q'){
                  return false;
              }
          }
          //left-up
          for(int i = row, j = col; i >= 0 && j >= 0; i--,j--){
              if(board[i][j] == 'Q'){
                  return false;
              }
          }
          //left-down
          for(int i = row, j = col; i < board.length && j < board[0].length; i++,j++){
              if(board[i][j] == 'Q'){
                  return false;
              }
          }
          return true;
      }
  }
  ```

    - leetcode<a name="46">46</a>

      框架代码

      框架外的思考：

        - `List`接口具体用的类

        - `res.add()`时，要重新`new` 一个对象（放到常量池中），

          不`new`的话，全为空结果，从`cur`这个`reference variable`指向的常量，反映了回溯的特性（回到最初的起点）

```java
class Solution {
    private List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> permute(int[] nums) {
        List<Integer> cur = new ArrayList<>();
        backtrack(cur,nums);
        return res;
    }
    public void backtrack(List<Integer> cur, int[] nums){
        if(cur.size() == nums.length){
            res.add(new ArrayList<>(cur));
        }
        for(int i = 0; i < nums.length; i++){
            if(!cur.contains(nums[i])){
                //合法情况
                cur.add(nums[i]);
                backtrack(cur, nums);
                int index = cur.size() - 1;
                cur.remove(index);
            }
        }
    }
}
```

- 剑指 Offer<a name="12">12</a>

## DP

### 学习参考

- [fucking-alogorithms 系列](https://github.com/labuladong/fucking-algorithm/tree/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E7%B3%BB%E5%88%97)
- [算法概论 Sanjoy Dasgupta / Christos Papadimitriou / Umesh Vazirani]((https://book.douban.com/search/Sanjoy Dasgupta))

### 思想

**明确 base case -> 明确「状态」-> 明确「选择」 -> 定义 dp 数组/函数的含义**。

按上面的套路走，最后的结果就可以套这个框架：

```python
# 初始化 base case
dp[0][0][...] = base
# 进行状态转移
for 状态1 in 状态1的所有取值：
    for 状态2 in 状态2的所有取值：
        for ...
            dp[状态1][状态2][...] = 求最值(选择1，选择2...)
```

### 题目列表

​    [斐列纳波数列](#斐列纳波数列)

​    [凑零钱](#凑零钱)

​    [leetcode300](#最长递增子序列)

​    [剑指 Offer 14剪绳子](#剪绳子)

​    [leetcode 72编辑距离](#编辑距离)

​ 正则表达式、背包问题、矩阵相乘、最短路径问题、树中的独立积问题

### 具体题解

- <a name = "斐列纳波数列">斐列纳波数列</a>

  最简单+ `dp`思想明确 + `dptable`优化重复的子结构问题

- <a name = "凑零钱">凑零钱</a>

- <a name = "leetcode300">leetcode300最长递增子序列</a>

- <a name = "剪绳子">剪绳子</a>

  如何找到`dp`数组含义：如何确定状态和选择

  对于的正整数 n，当 n≥2 时，可以拆分成至少两个正整数的和。令 k 是拆分出的第一个正整数，则剩下的部分是 n−k，n−k
  可以不继续拆分，或者继续拆分成至少两个正整数的和。由于每个正整数对应的最大乘积取决于比它小的正整数对应的最大乘积，因此可以使用动态规划求解。

  创建数组 `dp`，其中`dp[i] `表示将正整数 i 拆分成至少两个正整数的和之后，这些正整数的最大乘积。特别地，0 不是正整数，1是最小的正整数，0和 1都不能拆分，因此 `dp`[0]`=dp`[1]=0。

  ```java
  class Solution {
      public int integerBreak(int n) {
          int[] dp = new int[n + 1];
          for (int i = 2; i <= n; i++) {
              int curMax = 0;
              for (int j = 1; j < i; j++) {
                  curMax = Math.max(curMax, Math.max(j * (i - j), j * dp[i - j]));
              }
              dp[i] = curMax;
          }
          return dp[n];
      }
  }
  ```


- <a name = "编辑距离">编辑距离</a>

  大问题如何拆分小问题，然后套框架，明确每一步的含义