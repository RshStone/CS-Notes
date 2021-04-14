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



# Tree

## 思考方式

树的基本框架的构建，是用BFS还是DFS，BFS怎么用，DFS的话是pre,in,post中的哪一个或者只是要对树进行单纯的遍历。结合树的类型一般的树，二叉树，二叉搜索树等。

方案的时间复杂度和空间复杂度是怎么样的。

难点：想清楚递归，递归终止条件，是否是大问题转化为小问题，每个小问题是否独立。

## 涉及到的题目

[leetcode110](#110)平衡二叉树     涉及到高度

[剑指Offer 32](#从上到下打印二叉树系列)从上到下打印二叉树   层序遍历+一些变形

[剑指Offer 07](#重建二叉树)重建二叉树   利用不同dfs结果的特点逆向进行思考

[剑指Offer 34](#二叉树中和为某一值的路径)二叉树中和为某一值的路径 

[leetcode449](#449. Serialize and Deserialize BST)Serialize and Deserialize BST   

[leetcode98](#98)Validate Binary Search Tree    中序遍历

[leetcode124](#124)Binary Tree Maximum Path Sum  

[leetcode173](#173)Binary Search Tree Iterator

## 具体的题解



- leetcode<a name="110">110</a>

平衡二叉树  两种方法 自顶而下暴力解 自底而上 + 剪枝思想 

4.8 again 写辅助函数的时候，采用DFS中的哪种模式？返回值为int的时候，终止条件，递归函数，返回值等如何思考。

- 剑指Offer 32 - I, II, III <a name="从上到下打印二叉树系列">从上到下打印二叉树系列 </a>

基本框架是层序遍历

分别的要求

一层的节点按照从左到右的顺序打印                            简单层序遍历

同一层的节点按从左到右的顺序打印，每一层打印到一行       层序遍历中加一个for语句     

第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推                                           Deque + 分类处理

- [剑指Offer 07]<a name = "重建二叉树"> 重建二叉树</a>(https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof) 

  不会的：看题解 重构二叉树 编号07  思维：首先想清楚一个整理步骤 然后递进 分治思想进来啦， 最后的难点在于应用分治的边界选择问题3.23再刷不会**

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

- [leetcode449]<a name = "449. Serialize and Deserialize BST">449. Serialize and Deserialize BST</a>(https://leetcode.com/problems/serialize-and-deserialize-bst/)

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
    
      

