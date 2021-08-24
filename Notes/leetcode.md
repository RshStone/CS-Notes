# leetcode

# Goals

主要目的是为了给自己快速复习和查漏补缺进行食用。

这类笔记的要点就是要精简，不够精简的详细（说明大概率不会做），精简完了的可能会遗忘，需要时长巩固与复习，就是无聊的时候写一些，不会分析为什么再写。

采用的是小时间+高频词的复习方法

换个角度思考

学不下去的时候。

探索人类的智慧，这是我学习的一个动力。无论是以前对杨振宁、爱因斯坦等人的崇拜。

计算机科学的初衷。丰富的学习资源，先进的开源理念，让教育资源尽可能平等。

我这样的普通人也可以沉浸其中，自得其乐。

当然，经济上很重要，一份还算不错的收获，对个人来说就是这样子啊。

![image-20210626210359371](C:/Users/ASUS/AppData/Roaming/Typora/typora-user-images/image-20210626210359371.png)

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

4

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int length1 = nums1.length, length2 = nums2.length;
        int totalLength = length1 + length2;
        if (totalLength % 2 == 1) {
            int midIndex = totalLength / 2;
            double median = getKthElement(nums1, nums2, midIndex + 1);
            return median;
        } else {
            int midIndex1 = totalLength / 2 - 1, midIndex2 = totalLength / 2;
            double median = (getKthElement(nums1, nums2, midIndex1 + 1) + getKthElement(nums1, nums2, midIndex2 + 1)) / 2.0;
            return median;
        }
    }

    public int getKthElement(int[] nums1, int[] nums2, int k) {
        /* 主要思路：要找到第 k (k>1) 小的元素，那么就取 pivot1 = nums1[k/2-1] 和 pivot2 = nums2[k/2-1] 进行比较
         * 这里的 "/" 表示整除
         * nums1 中小于等于 pivot1 的元素有 nums1[0 .. k/2-2] 共计 k/2-1 个
         * nums2 中小于等于 pivot2 的元素有 nums2[0 .. k/2-2] 共计 k/2-1 个
         * 取 pivot = min(pivot1, pivot2)，两个数组中小于等于 pivot 的元素共计不会超过 (k/2-1) + (k/2-1) <= k-2 个
         * 这样 pivot 本身最大也只能是第 k-1 小的元素
         * 如果 pivot = pivot1，那么 nums1[0 .. k/2-1] 都不可能是第 k 小的元素。把这些元素全部 "删除"，剩下的作为新的 nums1 数组
         * 如果 pivot = pivot2，那么 nums2[0 .. k/2-1] 都不可能是第 k 小的元素。把这些元素全部 "删除"，剩下的作为新的 nums2 数组
         * 由于我们 "删除" 了一些元素（这些元素都比第 k 小的元素要小），因此需要修改 k 的值，减去删除的数的个数
         */

        int length1 = nums1.length, length2 = nums2.length;
        int index1 = 0, index2 = 0;
        int kthElement = 0;

        while (true) {
            // 边界情况
            if (index1 == length1) {
                return nums2[index2 + k - 1];
            }
            if (index2 == length2) {
                return nums1[index1 + k - 1];
            }
            if (k == 1) {
                return Math.min(nums1[index1], nums2[index2]);
            }
            
            // 正常情况
            int half = k / 2;
            int newIndex1 = Math.min(index1 + half, length1) - 1;
            int newIndex2 = Math.min(index2 + half, length2) - 1;
            int pivot1 = nums1[newIndex1], pivot2 = nums2[newIndex2];
            if (pivot1 <= pivot2) {
                k -= (newIndex1 - index1 + 1);
                index1 = newIndex1 + 1;
            } else {
                k -= (newIndex2 - index2 + 1);
                index2 = newIndex2 + 1;
            }
        }
    }
}

```



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

  不会的：看题解 重构二叉树 编号07 思维：首先想清楚一个整理步骤 然后递进 分治思想进来啦， 最后的难点在于应用分治的边界选择问题

  **3.23再刷不会****

  **7.3再刷用递归解决如何用递归没有思考出来** 根节点索引的root+i-left+1是怎么来的，好像有点明白了
  
  [105. 从前序与中序遍历序列构造二叉树 - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
  
  相似题目练习巩固
  
  （**难点还在于递归边界条件的选取**）
  
  分治思想下的树的边界条件，左子树，右子树，从那开始，在哪结束，用什么方法能够让inorder和preorder两个数组进行联动起来？
  
  分治思想下的辅助方法怎么写，递归结束条件是什么，递归的实际含义是什么？子问题是怎么样的。</a>

```java
//7.3重写的代码，注释代表了部分思考过程    
int preorder[];
    HashMap<Integer, Integer> hp = new HashMap();
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        this.preorder = preorder;
        for(int i = 0; i < inorder.length; i++){
            hp.put(inorder[i],i);   //hashMap put() not add hashSet add 
        }
        return recur(0,0,inorder.length - 1);
    }
    //Three parameters
    //root: add node with index root
    //left and right: the boundary condition of inorder
    public TreeNode recur(int root, int left, int right){
        //terminal condition test
        // why not >=  image the situation pre[3] in[3] the res will be null
        if(left > right)return null;
        TreeNode res = new TreeNode(preorder[root]);
        int index = hp.get(preorder[root]);
        res.left = recur(root + 1, left, index - 1 );
        res.right = recur(root + index - left + 1 , index + 1, right );
        //root 0 index 1 left 0  boundary test  (confused root + index - left + 1)
        // index - left + 1 根+左有多少个节点 + root 表示从root 开始 数起到右子树的根节点
        return res;
    }


    //结果问题
    int[] postorder;
    HashMap<Integer, Integer> hp = new HashMap();
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        this.postorder = postorder;
        for(int i = 0; i < inorder.length; i++){
            hp.put(inorder[i],i);
        }
        return recur(inorder.length - 1, 0, inorder.length - 1);
    }
    public TreeNode recur(int root, int left , int right){
        if(left > right || root < 0)return null;
        TreeNode res = new TreeNode(postorder[root]);
        int index = hp.get(postorder[root]);
        res.left = recur( root - right + left,left, index - 1);
        //root 4 left 0 right 4 index 1
        //index - left + 1  l到index有多少个节点（包括index）
        //r - l 子树有多少个节点 
        res.right = recur(root - 1, index + 1, right);
        return res;
    }
//root - right + index - 1 wrong -- > right  index = hp.get(postorder[right])wrong
[15,13,20,7]
[15,13,7,20]
		20 
	13  	7
15
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

- [Dynamic programming - Wikipedia](https://en.wikipedia.org/wiki/Dynamic_programming)

- [fucking-alogorithms 系列](https://github.com/labuladong/fucking-algorithm/tree/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E7%B3%BB%E5%88%97)
- [算法概论 Sanjoy Dasgupta / Christos Papadimitriou / Umesh Vazirani]((https://book.douban.com/search/Sanjoy Dasgupta))

**基础知识**:

​	

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

​	

 正则表达式、背包问题、矩阵相乘、最短路径问题、树中的独立积问题

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

- 通配符匹配

  做多了会发现是dp题目，二维的dp Table在脑袋里徐徐展开。找到dp公式。不过初次看的时候，肯定会想到暴力解法。问题的难点在于"*"这个怎么办。从位置来看又有左，中，右三种情况，也可能没有。

  failed to test "adceb", *a*b

  仔细对比会发现最右边那一项`dp[i][j-1]`两个式子都一样。那么，`dp[0][j - 1] || dp[1][j-1] || ... || dp[i-1][j-1]`是否等价于`dp[i-1][j]`呢？你会发现很容易证明是等价的：假如p(0, j -1)可以匹配s(0, i - 1)的某个子串s(0, k) （k <= i - 1），而p[j]刚好是"*"，所以刚好可以适配配剩下的部分，即p(0, j)可以适配s(0, i - 1)，反之亦然。

  当p[j]为星号时，“p(0, j -1)可以匹配s(0, i - 1)的某个子串s(0, k)” 与 “p(0, j)可以匹配s(0, i - 1)”互为充要条件。

  最有意思的是，把全部或上的思路，其实是很顺势而为的，因为“*”可以匹配0到n个任意字符嘛，所以p的前半部分只要能匹配s的任意一个短串就行（哪怕是空串），这样这个理论形成一个整体。比较巧的是，这个“整体”是可以拆的，拆分办法就是前面所说的拿掉最后一项，剩下的一大堆或居然有个等价的结果、而且它已经被计算出来了。

  ```c++
  class Solution
  {
  public:
      bool isMatch(string s, string p)
      {
          int j=0;
  	for(int star=0,i=0, last=0;i<s.length();){
  		if(j<p.size() && (s[i]==p[j] || p[j]=='?')){
  			++i;
  			++j;}
  		else if(j<p.size() && p[j]=='*'){
  			last=i;
  			star=++j;}
  		else if(star!=0){
  			i=++last;
  			j=star;}
  		else return 0;
  		}
  		for(; j<p.size() && p[j]=='*'; ++j);
  		return j==p.size();
    }
  };
  
  作者：sunt
  链接：https://leetcode-cn.com/problems/wildcard-matching/solution/0-ms-88mb-c-bao-li-by-sunt/
  来源：力扣（LeetCode）
  著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
  ```

  

```c++
class Solution {
    std::unordered_map<std::string,bool> memo;
    bool is_match(std::string& s, std::string& p, int i, int j) {

        std::string index = std::to_string(i) + std::to_string(j);

        auto it = memo.find(index);
        if (it != memo.end()) return it->second;
        
        //if (memo.count(index)) return memo[index];

        while (i < s.size() && j < p.size()) {
            // match one any character pointers both move forward
            if (p[j] == '?') { 
                i++; j++;
            }
            // extactly match one characters
            else if (p[j] >= 'a' && p[j] <= 'z') {
                // if failed, memorize the result
                if (s[i] != p[j]) { 
                    index = std::to_string(i) + std::to_string(j); memo[index] = false;
                    return false;
                }
                i++; j++;
            }
            // if we encounter * match substrings with length greater than or equal to zero
            else if (p[j] == '*') {
                // there are more pattern characters to be processed
                if (j+1 < p.size()) {
                    // here we handle the remaining text and pattern as subproblem
                    for (int k = i; k < s.size(); ++k) {
                        index = std::to_string(k) + std::to_string(j+1);
                        // if this subproblem has been conquered before, fetch the result
                        auto it2 = memo.find(index);
                        if (it2 != memo.end()) return it2->second;
                        // otherwise go through the pain
                        bool sub_res = is_match(s, p, k, j+1);
                        memo[index] = sub_res;
                        if (sub_res) {
                            // if any submatch succeeds the whole match also succeeds
                            index = std::to_string(i) + std::to_string(j); memo[index] = sub_res;
                            return sub_res;
                        }
                    }
                    // othewise we have failed at index i and j respectively 
                    index = std::to_string(i) + std::to_string(j); memo[index] = false;
                    return false;
                }
                // * is the last character in the pattern 
                // we can happily match to the end
                else {
                    index = std::to_string(i) + std::to_string(j); memo[index] = true;
                    return true; 
                }
            }
        }

        // the remaining pattern consists of all *
        if (j < p.size()) { while (j < p.size() && p[j] == '*') j++; }

        bool res = (i == s.size() && j == p.size());
        index = std::to_string(i) + std::to_string(j); memo[index] = res;

        return res;
    }
public:
    bool isMatch(string s, string p) {
        if (s.size() == 0) {
            for (int i = 0; i < p.size(); ++i) {
                if (p[i] != '*') return false;
            }
            return true;
        }
        return is_match(s, p, 0, 0);
    }
};

作者：00010001
链接：https://leetcode-cn.com/problems/wildcard-matching/solution/bao-li-di-gui-bei-wang-lu-by-00010001-n4jd/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

```c++
p中没有 *，那就直接判断两个字符串是否相等，这里我写了isEqual函数来判断
如果p的第一个字符不是*，需要判断p的第一颗*前面的字符，是否与s对应的相等长度的字符完全相等，这里我写了rightHalfStar函数来判断
普通情况：找到两个相邻的之间的子字符串，判断s从上一次匹配到的位置之后的子字符串中是否含有该子字符串，期间储存好s对应的匹配位置，和两颗的位置
更新s中匹配到的位置，更新*的位置
结束


class Solution {
public:
    bool leftHalfStar(string s, string p)
    {
        if (s.size() < p.size()) return false;
        int i = s.size() - 1;
        int j = p.size() - 1;
        while(j >= 0)
        {
            if (p[j] == '?')    
            {
                j--;
                i--;
                continue;
            }
            if(p[j--] != s[i--])    return false;
        }
        return true;
    }
    bool rightHalfStar(string s, string p)
    {
        if (s.size() < p.size())    return false;
        for (int i = 0; i < p.size(); i++)
        {
            if (p[i] == '?')    continue;
            if (p[i] != s[i])   return false;
        }
        return true;
    }
    bool isEqual(string s, string p)
    {
        if (s.size() != p.size())   return false;
        for (int i = 0; i < s.size(); i++)
        {
            if (p[i] == '?')    continue;
            if (p[i] != s[i])   return false;
        }
        return true;
    }
    int isIncludeP_WithouStar(string s, string p)
    {
        if (s.size() < p.size()) return -1;
        int nextStart = 0;
        int theLoop = 0;
        while (nextStart < s.size())
        {
            for (theLoop; theLoop < p.size(); theLoop++)
            {
                if(p[theLoop] == '?')   continue;
                if(p[theLoop] != s[nextStart + theLoop])
                {
                    nextStart++;
                    break;
                }
            }
            if(theLoop == p.size()) return nextStart;
            theLoop = 0;
        }
        return -1;
    }
    bool isMatch(string s, string p) {
        if (s == "")
        {
            for(int i = 0; i < p.size(); i++)
            {
                if (p[i] != '*') return false;
            }
            return true;
        }
        //找到第一个*的idx
        int firstStar = -1;
        for (int i = 0; i < p.size(); i++)
        {
            if (p[i] == '*')
            {
                firstStar = i;
                break;
            }
        }
        //1. 如果没有 * ，直接来判断是否s == p，(？的情况就直接continue)
        if (firstStar == -1)
        {
            return isEqual(s,p);
        }
        
        //lastMatchPos记录上一次匹配的位置
        int lastMatchPos = 0;
        //2. 如果第一颗* 不是首位的话，需要判断*前字符是否跟s对应长度的完全相等
        if (firstStar != 0)
        {
            string startStr = p.substr(0,firstStar);
            if (!rightHalfStar(s,startStr)) return false;
            lastMatchPos = firstStar;
        }
        // 3. 普通情况，找到两个星星之间的子字符串，与 s上一次匹配到的位置之后的子字符串 进行匹配
        int secondStar = firstStar + 1;
        while(secondStar < p.size())
        {
            //找到第二颗*
            while(secondStar < p.size())
            {
                if(p[secondStar] == '*')    break;
                secondStar++;
            }
            //如果两颗*紧挨着，直接往后移位
            if (firstStar == secondStar - 1)
            {
                firstStar = secondStar++;
                continue;
            }
            //如果没有第二颗*，直接判断，最后一个*后面的字符串，是否跟s的末尾相同长度的字符串相等
            if (secondStar == p.size())
            {
                return leftHalfStar(s.substr(lastMatchPos),p.substr(firstStar + 1));
            }
            //strToMatch是提取出来的 两个*之间的字符串
            string strToMatch = p.substr(firstStar+1,secondStar-firstStar-1);
            //获取第一次匹配到的s的子字符串中的索引位置
            int strMatchPos = isIncludeP_WithouStar(s.substr(lastMatchPos),strToMatch);
            if (strMatchPos == -1)  return false;
            //索引位置需要加上 上一次匹配到的位置，转换到完整的s的索引
            strMatchPos += lastMatchPos;
            //更新匹配到的s的索引位置
            lastMatchPos = strMatchPos + strToMatch.size();
            //继续寻找 下一个  两颗*之间的字符串进行匹配
            firstStar = secondStar++;
        }
        return true;
    }
};


作者：jia-116
链接：https://leetcode-cn.com/problems/wildcard-matching/solution/bao-li-pi-pei-jian-dan-gao-xiao-by-jia-116/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```



## N-Sum-Questions

### 学习参考

​	[算法小抄nsum篇](https://mp.weixin.qq.com/s?__biz=MzAxODQxMDM0Mw==&mid=2247485789&idx=1&sn=efc1167b85011c019e05d2c3db1039e6&chksm=9bd7f755aca07e43405baeac62c76b44d8438fe8a69ae77e87cbb5121e71b6ee46f4c626eb98&mpshare=1&scene=23&srcid=0618PKDQJlp2X65llKoRcMsL&sharer_sharetime=1623980156037&sharer_shareid=d7abcec3b52761e13ec0050e123143a7#rd)

犯的错误： List是个接口，`ArrayList`是一个具体的实现类；

​	`HashMap`是一个Map，两种类型

​	List<List>类型里面如果加List;List不能消除，内存池放的是List指向的变量。

```java
public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    Arrays.sort(nums);
    for (int i = 0; i + 2 < nums.length; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) {              // skip same result
            continue;
        }
        int j = i + 1, k = nums.length - 1;  
        int target = -nums[i];
        while (j < k) {
            if (nums[j] + nums[k] == target) {
                res.add(Arrays.asList(nums[i], nums[j], nums[k]));
                j++;
                k--;
                while (j < k && nums[j] == nums[j - 1]) j++;  // skip same result
                while (j < k && nums[k] == nums[k + 1]) k--;  // skip same result
            } else if (nums[j] + nums[k] > target) {
                k--;
            } else {
                j++;
            }
        }
    }
    return res;
}
```

非常秒，将三维的3sum转化为使用双指针的2sum，类似采用了二分查找

思想需要慢慢体会。

## Binary Search



# 周赛

## Weekly Contest 251

- 如何将一个多位的整数按位相加， ps: 整数如果超过int取值范围呢

- 将字符（值是整数）转化为整数 

  ```
  Character.getNumericValue('z')   --> 35  使用条件 单纯将 0-9 numeric Value of character convert to int  不过为什么不用 '1' - '0' 来转换成整数呢?
  
  ```

  将String 转化为 char array 最后 再将char array 转化成String

## **Weekly Contest 255**

Find Greatest Common Divisor of Array:

```c++
//找公因数代码，我没写出来，很妙    
private int getGCD(int a, int b){
        if(b % a == 0) return a;
        else return getGCD(b % a, a);
}
```

Find Unique Binary String

我的思路：位运算，玄学找规律，但找错了，仔细想很容易找出反例。

(Code能力，怎么暴力枚举出来)



