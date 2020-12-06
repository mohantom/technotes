9 Zhang Algo
-----------------

## Introduction
面试不是考试，可以要求提示，思路，引导。
将来的同事，能否一起愉快工作，code review要轻松
面试考察的变成基本功：
	Bug free 更重要
1.	程序风格（缩进，括号，变量）
2.	Coding习惯（异常检查，边界处理）
3.	沟通（让面试官时刻明白你的意图）
4.	测试（主动写出合理的Testcase）
a.	A+b: Normal numbers, Small number, very big number, exception data (String instead of Integer)
b.	Test if there are branches
想清楚再写
考察基本算法：二分法，分制，宽度压缩，递归，iterator/stack/queue
刷题时总结、归类相似题
找出适合同一类题目的模板程序

## 1	Subsets
Given a set of distinct integers, return all possible subsets.
	All possible -> depth first
Search -> DFS, BFS
DFS -> divided & conquer, permutation, subsets
 
[] -> [1] -> [1,2] -> [1, 2, 3], 然后回溯(backtracking)
Subsets
Subsets II
[1,2,2] -> all possible distinct combinations
 

排列组合模板
几乎所有的搜索问题，根据具体要求进行改动；什么时候输出，那些情况需要跳过。
- Combinations
    - Combination sum
    - Letter combination of a phone number
    - Palindrome partitioning
    - Restore IP address

- Permutations
    - permutations
    - permutations2

多联系，与面试官愉快交谈（一起合作解决面试问题，而非争论不休）
理解而不是背诵，时间用在刀刃上（KMP，红黑树，AVL, ACM竞赛题）
找事做，而不是等待分配任务

Why this company?? Talk about culture, slogan (found it on their website)
Tech idea conflict with other member/manager
Why leave: future growth opportunity, like the stuff/business here, other people also say good things here


## 2 Binary search
如果需要优化O(n)的时间复杂度，那么只能是O(log n)的二分法。
Recursion: 可能stack overflow, 每次调用都需要占用新的空间。
能用非递归就用非递归，如果问题比较复杂就用递归。

```shell script
public int binarySearch(int[] nums, int target) {
    if (nums == null || nums.length == 0) {
        return -1;
    }

    int start = 0, end = nums.length - 1;
    while (start + 1 < end) {
        int mid = start + (end - start) / 2;  // start+end may overflow
        if (nums[mid] == target) {
            end = mid;
        } else if (nums[mid] < target) {
            start = mid;
        } else {
            end = mid;
        }
    }
    if (nums[start] == target) {
        return start;
    }
    if (nums[end] == target) {
        return end;
    }
    return -1;
}
```


// typical one
```shell script
int found = -1;
while(left <= right) {
    if(nums[mid] == target) {
        found = mid;
        break;
    } else if (target < nums[mid]) {
        right = mid - 1;
        mid = (left + right) / 2;

    } else {
        left = mid + 1;
        mid = (left + right) / 2;
    }
}
return found;
```


typical one 不能用过来找last position of a range

### 4点要素
1.	Start + 1 < end
2.	Mid = Start + (end -start) / 2
3.	A[mid] ==, <, >
4.	A[start], A[end] ? target

- Search for a range
- Search a 2D matrix
- First bad version
- Find peak element
- If to find all peaks -> O(n); now only one peak -> binary search
- Search insert position
- Search a 2D matrix II
- Sqrt(x)

Double/float实数的二分：
```shell script
while(end – start > 1e-6) {
}
return start;
```


- Find minimum in rotated sorted array
- Search in rotated sorted array
- Search in a big sorted array with O(log k)
- Wood cut

 

## 3 Binary tree & divide and conquer
 
Both recursion and iterative
Binary tree preorder traversal

// version 1: recursive, O(n)
//Version 2: Divide & Conquer, O(n2), 有返回值
```shell script
public ArrayList<Integer> preorderTraversal(TreeNode root) {
   ArrayList<Integer> result = new ArrayList<Integer>();
   // null or leaf
   if (root == null) {
      return result;
   }

   // Divide
   ArrayList<Integer> left = preorderTraversal(root.left);
   ArrayList<Integer> right = preorderTraversal(root.right);

   // Conquer, n*O(n)
   result.add(root.val);
   result.addAll(left);	// addAll takes more time
   result.addAll(right);
   return result;
}
```


divide and conquer example: merge sort, quick sort, most of binary tree problem
Binary tree inorder traversal
Binary tree postorder traversal

几乎所有二叉树的问题都可以用分治法解决
Maximum depth of binary tree
// D&C, O(n) since we traverse every node
```shell script
public static int maxDepth(TreeNode root) {
    if(root == null)
        return 0;

    return Math.max(maxDepth(root.left) + 1, maxDepth(root.right) + 1);
}
```


- balanced binary tree
- lowest common ancestor from binary search tree

// D&C: O(n); getPath -> O(height) [worst is O(n), best is O(log n)
```shell script
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode node1, TreeNode node2) {
    if (root == null || root == node1 || root == node2) {
        return root;
    }

    // Divide
    TreeNode left = lowestCommonAncestor(root.left, node1, node2);
    TreeNode right = lowestCommonAncestor(root.right, node1, node2);

    // Conquer
    if (left != null && right != null) {
        return root;
    }
    if (left != null) {
        return left;
    }
    if (right != null) {
        return right;
    }
    return null;
}
```


- [ ] binary tree maximum path sum from root to leaf
- [ ] binary tree maximum path sum (from any node), hard
	review
	use inner class to return several results

- LC102 binary tree level order traversal
BFS, use queue
```shell script
    public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
        ArrayList result = new ArrayList();

        if (root == null) {
            return result;
        }

        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            ArrayList<Integer> level = new ArrayList<Integer>();
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode head = queue.poll();
                level.add(head.val);
                if (head.left != null) {
                    queue.offer(head.left);
                }
                if (head.right != null) {
                    queue.offer(head.right);
                }
            }
            result.add(new ArrayList<>(level));
        }

        return result;
    }
}
```
 

- LC107 binary tree level order traversal II
	add(0, level) //add to the first position of ArrayList
- LC103 binary tree zigzag level oder traversal

binary tree level order traversal by DFS
迭代搜索（算法已淘汰）
BFS needs a queue which takes space (heap, faster). DFS takes stack space, but more time.

- Validate binary search tree
    Review code
    By Traverse: concise
    By D&C:  easy to understand
- Search range in BST
- Inorder successor in BST:
	Given a BS and a node in it, find the in-order successor of that node
```shell script
public class Solution {
   public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
      TreeNode successor = null;
      while (root != null && root.val != p.val) {
         if (root.val > p.val) {
            successor = root;
            root = root.left;
         } else {
            root = root.right;
         }
      }

      if (root == null) {
         return null;
      }

      if (root.right == null) {
         return successor;
      }

      root = root.right;
      while (root.left != null) {
         root = root.left;
      }

      return root;
   }
}

```



Implement iterator of BST
	背诵题, next(), hasNext()
	 

- Search range in BST
- Insert a node in BST
给定一棵二叉查找树和一个新的树节点，将节点插入到树中。
你需要保证该树仍然是一棵二叉查找树。
样例
给出如下一棵二叉查找树，在插入节点6之后这棵二叉查找树可以是这样的：
  2             2
 / \           / \
1   4   -->   1   4
   /             / \ 
  3             3   6

- Remove a node in BST

## 4 Dynamic programming
Triangle
1.	Traverse, DFS
 
Permutation: O(n!)
Triangle: every node has 2 choices to go down -> O(2n)
2.	D&C
 
Correction: Return Math.max(A[x][y] + divideConquer(x + 1, y), A[x][y] + divideConquer(x+1, y+1));
但是仍然是O(2n)
3.	D&C + memorization
 
Above has O(n2), n 是层数
Dynamic planning: 解决重复计算的搜索。
4.	不用递归，自底向上的动态规划
 
O(n2)

5.	自顶向下的动态规划
 

动态规划
什么情况下可能是动态规划？
满足下面3个条件之一：
1.	Maximum/minimum
2.	Yes/no 存不存在（或者最优方案）
3.	Count(*) (所有方案的个数， 不是具体方案)
不是动态规划的情况：
1.	题目要求出所有“具体”的方案，而非方案个数：palindrome-partitioning
2.	输入数是一个“集合”而不是“序列”: longest-consecutive-sequence
4个要素：
1.	状态state：灵感，创造力，存储小规模问题的结果
2.	方程function: 状态之间的联系
3.	初始化 initialization
4.	答案 answer: 终点

常见4中类型
1.	Matrix DP (15%)
2.	Sequence (40%)
3.	Two sequences DP (40%)
4.	Others (5%)

Matrix DP
	State: f[x][y] 表示我从起点走到坐标x, y…
	Function: 研究走到x,y 这个点之前的一步
	Initialize: 起点
	Answer: 终点
- LC64 Minimum path sum
对2维DP，初始化第0行和第0列

- LC62 Unique paths
- Unique paths II

Sequence
- Climbing stairs
- Jump game
Is it possible to jump from start to end?
	State: f[i] 代表我能否从起点跳到第i个位置
	Function: f[i] = OR(f[j], j < i && j 能跳到i)
	Initialize: f[0] = true;
	Answer: f[n-1]

- Jump game II
Reach the last index in the minimum number of jumps.
	State: f[i] 代表到这个位置需要最少几步
	Function: f[i] = Min(f[j] + 1, j < i && j能跳到i)
	Initialize: f[0] = 0;
	Answer: f[n-1]
- House robber

others

递归 vs DP
都有分治，但是DP有处理重复的。
如果矩阵可以朝4个方向走 -> 循环依赖 -> 不能用DP
- Palindrome partition II
review
- Minimum cuts for a palindrome partitioning of string s.
 
如果不是跟坐标相关的动态规划，一般有N个数/字符，就开N+1个位置的数组，第0个位置单独留出来做初始化。
Coins in a line??
区间型动态规划 (getIsPalindrome())
- Word break
 

何时用一维、二维DP
矩阵DP
分割DP
如果限制了分割的字符串的（为k），那么要用二维。
F[i][j] = 前i个字符，切成j个单词，是否可行。
如果没有限制，f[i]就可以了。
区间DP
	i-j 二维
两个序列的DP
	二维
Two sequences DP

 
- Longest common subsequence??
review
- Longest common substring??

- Edit distance, hard

- Distinct subsequence, hard

- Interleaving string, hard

- Backpacks
- Backpacks II
- Minimum adjustment cost??
- k-sum??
- coins in a line iii
- scramble string, hard

## 5 Linked list
Use dummy node if head may change
Remove duplicates from list
Remove duplicates from list II
Reverse linked list
Reverse linked list II
Rotate list
Partition list
Sort list
O(nlogn)
原地排序 in place, 稳定排序 stable
	Heap sort: need a heap
Merge sort
quick sort
reorder list
Linked list 本身是in place

Linked list cycle
Linked list cycle II
Merge k-sorted list, hard
Copy list with random pointer, hard
Convert sorted list to binary search tree
	In O(n)
Longest increasing subsequence

## 6 Arrays and numbers
3-step reversion
Recover rotated sorted array??
Rotate string??
Merge sorted array
Median of two sorted arrays, hard
Review: 前缀和
Maximum subarray
Review solution on jiuzhang.com/solution/maximum-subarray
Best time to buy and sell stock
Maximum subarray II
	Left[i], right[j], get the max from two sum in arrays
Maximum subarray III??
Minimum Size Subarray Sum
Maximum subarray difference??
Subarray sum??
Sum == 0
Subarray sum closest??
Sum closest to 0
2-Sum
HashMap
If sorted, use left and right pointer (similar to the water container)
3-Sum
Sort, then 2-sum => O(n2)
2-Sum closest??
3-Sum closest
4-Sum
A+b+c+d  = target
HashMap: sum(a,b) -> List(a, b pairs) => O(n3)

k-sum
不要求
Partition array??
Partition array by odd and even??
Sort letters by case??
Sort colors
Counting sort??
Interleaving positive and negative numbers??

## 7 Data structure
MinStack
Implement a queue by two stacks
时间复杂度是算平均值，不是最坏的情况O().
Largest rectangle in histogram, hard
Use stack 递增栈: solutions/largest-in-histogram
Max tree, hard
递减栈
HashMap: Array can be a simple HashMap
```shell script
// takes O(key.length())
Int hashfunc(String key) {
	// md5 is too slow
	Int sum = 0; 
	For (int I = 0; I < key.length(); i++) {
		sum = sum * 33 + (int)(key.charAt(i));
		sum = sum % HASH_TABLE_SIZE;
	}
	Return sum;
}
```

 
Closed hashing does not support “delete”
Rehashing:  全部重新算一遍Hash code

Longest consecutive sequence, hard
“For in for” is not necessarily O(n2), need to look at if in/out stack once or not

LRU cache, hard
Least recently used
HashMap + LinkedList

- Heap
特殊binary tree, in an dynamic array
Left child: i*2, right child: i*2+1
- Max heap, min heap
- Min heap: left, right > root
- BST: left < root, right >= root 
BST对插入、删除需要O(logn), 而且code不好写。
- Priority queue: delete root
	Siftup, siftdown
需要学会自己实现heap
Median number, hard

## 8 Graph and search
- LC133: Clone graph
    BFS = queue + HashMap (record isVisited)
    DFS is not good, which needs recursion, it may be too deep. 
- Topological sorting
InDegree(入度): number of edges pointing to the node

### BFS use cases:
- 从一个点找到所有点
- 寻找图上2个点之间的距离
- find the shortest path in a simple graph

Will need queue and a map (or set)

Find the connected component in the undirected graph

#### Time complexity
O(m), m is the number of edeges

### DFS: 找出所有方案（不是方案个数）
不需要position, 但是要判断前一个是否已经加入list

#### Time complexity
方案总数*每个方案的代价

- Permutations: O(n! * n): 
- subsets: O(2^n * n)

Permutations II
How to check duplicates
N-Queens, hard

Palindrome partitioning
显式图搜索： matrix, graph
隐式图搜索：permutation, subset (combination)
切的位置: solutions/palindrome-partitioning
Combination sum
Combination sum II
Word ladder
BFS
Word ladder II, hard
BFS + DFS
找所有的方案：DFS
最短方案：
列出每个点到终点的距离, BFS
每个点每走一步，必须离终点更近。DFS

 
BFS: m, n 是边数

Data stream median, hard
Priority queue
Kth largest element in an array
Kth smallest element in BST

Implement Trie
强化班，题目一般比较难


九章算法加强
--------------
## 九章算法1 FLAG算法面试难度提高？如何准备？
Two sum
2 pointers
Two sum II
Given an array of integers, count the number of pairs that the sum of the pair is larger than a target number
Triangle count, hard
http://www.lintcode.com/en/problem/triangle-count/
 

N个非排序数组中第k大元素
有多个数组

N个非排序数组中第k大元素，k比较小，一个电脑装不下全部数组
 

O(k log n)

N个非排序数组中第k大元素，k比较大，一个电脑装不

Find the insertion position that’s larger than x
```shell script
while
	if a[mid] < target
		i = mid + 1;
	else a[mid] >= target
		i = mid – 1; 
		ans = mid;
```


 

## Data structure I
Union find
数组表示关系
1.	查询 Find, O(n)
 
HashMap<Integer, Integer> father = new HashMap<>();
2.	合并, O(n)
 

关于集合合并
判断在不在一个集合
Find the connected component in the undirected graph

Find the weak connected component in the directed graph

Compressed find, O(1)
Every node points to the root directly
 
合并 （compressed find）
 

- umber of Islands岛屿的个数
2D matrix, m x n
(x,y) -> x*n + y = p
X = p / n, y = p % n

- Number of Islands II

- Graph valid tree
Tree: no cycle
用并查集判断有无环

Trie
Retrieve, 字典树
1.	虚根
2.	26叉树
HashMap and Trie have O(k), k = length of word
Trie save more space than HashMap
需要一个个字符查找
 

Word search II
Add and search word
设计算法获得IP到城市的Map

Scan-line 区间拆分
Number of airplanes in the sky
 
变种1：开会需要多少会议室
变种2：火车需要多少轨道


## 数据结构2
Heap
- Trapping rain water

- Trapping rain water II
- Container in 3D
Heap 辅助记录外围柱子，快速找到最小值
Follow up: 都是从外围向里面灌水

Building outline
扫描线

Hash heap
Maxheap
Minheap
	Left: 2i + 1, right 2i+2
	Parent: (i-1)/2
	Sift-up, sift-down, pop (get the top/min), n*log(n)
Linked HashMap: to delete a node, log(n)
Duplicated node: use count
Similar to LRU: use Hash to find the element quickly

Data stream median

Sliding window median
Follow up from data stream median

Deque
Can pop from top or bottom

Sliding window maximum
Use Hashheap -> O(n*logn)
[1, 2, 7, 7, 5, 8]
	[7, 7, 5]
Deque: 单调递减的队列 -> O(n)

## 两个指针
Container with most water

Partition
Quick sort
Kth largest element
Quick select, O(n)
Nuts & bolts problem
 

前向型或追击型指针
Minimum size subarray sum
 

- Longest substring without repeating characters

- Minimum window substring

- Longest substring with distinct at most k characters
 

The smallest difference
两个数组，两个指针

## 动态规划1
House robber
1.动态规划的空间优化：滚动数组
 

 
 

Maximal square
 

3.	局部最优和全局最优实现时间优化
Global and local 实现时间的优化
Maximum subarray

Maximum product subarray

Best time to buy and sell stock IV (review)
 
 
4.	记忆化搜索
博弈类问题
Longest increasing continuous subsequence

Longest increasing continuous subsequence II

什么时候使用记忆化搜索？
	状态转移特别麻烦，不是顺序性。
	初始化状态不是很容易找到。

## 动态规划2
博弈类
Coins in a line
N coins, two players take turn to take 1 or 2 coins. The player who takes the last coin wins.
 
使用了recursion。
也可以用loop

Coins in a line II
Array of coins. The player who takes the most value wins.
 
因为有flag[x], O(n)

Coins in a line III
N coins in a line. Two players take turns to take a coin from one of the ends of the line. The player with the larger amount of money wins.
 

区间类DP
Stone-game
 
Scramble string (review)
 

 

### 背包类DP
Backpack
Size [2,3,5,7[, backpack size 11 => [2,3,5] and max fill is 10.
 
Backpack 马甲
把一个数组[1,2,4,5,6]尽量平分

Backpack II
Item size [2,3,5,7], value [1,5,2,4]
Backpack size 10, maximum value 10
 

Minimum adjustment cost

 
背包：有限制大小

## Follow up 问题
K sum

Find peak element

Find peak element II 

Kth largest element

Kth smallest number in sorted matrix

 

Subarray sum
 
