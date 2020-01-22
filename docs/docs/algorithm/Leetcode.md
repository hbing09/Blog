# Leetcode 2020
# 100. Same Tree
Given two binary trees, write a function to check if they are the same or not.

    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
      if not p and not q:
        return True
      elif p and q:
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right) and p.val == q.val
      else:
        return False
----------

# 101. Symmetric Tree
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

    def isSymmetric(self, root: TreeNode) -> bool:
      if not root:
        return True
      return self.isMirror(root.left, root.right)
        
    def isMirror(self, left: TreeNode, right: TreeNode):
      if not left and not right:
        return True
      if not left or not right or left.val != right.val:
        return False
      return self.isMirror(left.left,right.right) and self.isMirror(left.right,right.left)
----------

# 102. Binary Tree Level Order Traversal
Given a binary tree, return the *level order* traversal of its nodes' values. (ie, from left to right, level by level).

    from collections import deque
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
      if not root:
        return None
      res = []
      queue = deque([root])
    
      while queue:
        cur_level = [] # hold the current level nodes
        size = len(queue)
        for i in range(size):
          node = queue.popleft()
          if node.left:
            queue.append(node.left)
          if node.right:
            queue.append(node.right)
          cur_level.append(node.val)
        res.append(cur_level)
      return res
----------

# 103. Binary Tree Zigzag Level Order Traversal
Given a binary tree, return the *zigzag level order* traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

    def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
      if not root:
        return None
      res = []
      stack = [root]
      flag = 1
      
      while stack:
        cur_level = []
        next_level = []
        for node in stack:
          cur_level.append(node.val)
          if node.left:
            next_level.append(node.left)
          if node.right:
            next_level.append(node.right)
        res.append(cur_level[::flag])
        
        stack = next_level    
        flag *= -1
      return res
----------

# 112. Path Sum
Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

    def hasPathSum(self, root: TreeNode, sum: int) -> bool:
      if not root:
        return None
      sum -= root.val
      if not root.left and not root.right:
        return sum == 0
      return self.hasPathSum(root.left, sum) or self.hasPathSum(root.right, sum)
----------

# 113. Path Sum II
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

    def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
      if not root:
        return [[]]
      if root.val == sum and not root.left and not root.right:
        return [[root.val]]
      sum -= root.val
      subSum = self.pathSum(root.left, sum) + self.pathSum(root.right, sum)
      return [[root.val] + i for i in subSum]
----------

# 543. Diameter of Binary Tree
Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the **longest** path between any two nodes in a tree. This path may or may not pass through the root.

    '''
    for whichever node, see what's the longestleft + longestright for it
    直径 = number of nodes - 1
    如何维持一个 max (longest) path，
    用 global 变量 count 每次 path 最多的点的个数，
    '''
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
      if not root:
        return 0
      self.nodes = 1
      self.depth(root)
      return self.nodes - 1
    def depth(self, node: TreeNode):
      if not node:
        return 0
      left = self.depth(node.left)
      right = self.depth(node.right)
      # remember the highest number of nodes used in some path
      self.nodes = max(self.nodes, left + right + 1)
      return max(left, right) + 1
----------

# 572. Subtree of Another Tree
Given two non-empty binary trees **s** and **t**, check whether tree **t** has exactly the same structure and node values with a subtree of **s**. A subtree of **s** is a tree consists of a node in **s** and all of this node's descendants. The tree **s** could also be considered as a subtree of itself.

    def isSubtree(self, s: TreeNode, t: TreeNode) -> bool:
      if not t:
        return True
      if not s:
        return False
      if self.isIdentical(s, t):
        return True
      return self.isSubtree(s.left, t) or self.isSubtree(s.right, t)
      
    def isIdentical(self, tree1: TreeNode, tree2: TreeNode):
      if not tree1 and not tree2:
        return True
      if not tree1 or not tree2:
        return False
      return tree1.val == tree2.val and self.isIdentical(tree1.left, tree2.left) and self.isIdentical(tree1.right, tree2.right)
----------

# 173. Binary Search Tree Iterator
Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.
Calling `next()` will return the next smallest number in the BST.

    '''
         4
       2   7
     1  3 6  8
     
    这样一个二叉搜索树，先依次让4->2->1入栈，每次调用next函数则让一个元素出栈。
    第一次调用next的时候１出栈。
    第二次调用next的时候２出栈，因为２有右子树，因此让２的右子树３入栈
    第三次调用next的时候３出栈
    第四次调用next的时候４出栈，并且４有右子树，但是此时４的右子树并不是最小结点，他还有左子树，因此一直遍历到左子树的叶子结点，依次入栈。
    
    重复以上操作即可。
    平均时间复杂度还是O(1)，空间复杂度降为O(h)。
    '''
    class BSTIterator:
      def __init__(self, root: TreeNode):
          # for a given node, 把最左边的树枝放进stack
          # 初始只让左子树入栈直到最左结点
          # 每次结点出栈的时候再把他的右子树入栈，这样就可以达到O(h)的时间复杂度
          self.stack = []
          while root:
              self.stack.append(root)
              root = root.left   
      def next(self) -> int:
          """
          @return the next smallest number
          """
          node = self.stack.pop()
          temp = node.right
          while temp:
              self.stack.append(temp)
              temp = temp.left
          return node.val    
      def hasNext(self) -> bool:
          """
          @return whether we have a next smallest number
          """
          return len(self.stack) > 0
----------

# 109. Convert Sorted List to Binary Search Tree
Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.
For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

    def sortedListToBST(self, head: ListNode) -> TreeNode:
        if not head:
            return None
        if not head.next:
            return TreeNode(head.val)
        
        prev= None
        slow = fast= head
        
        while fast and fast.next:
            prev = slow
            fast = fast.next.next
            slow = slow.next
        
        if prev:
            prev.next = None
        
        root = TreeNode(slow.val)
    
        root.left = self.sortedListToBST(head)
        root.right = self.sortedListToBST(slow.next)
        return root
----------

# 99. Recover Binary Search Tree
Two elements of a binary search tree (BST) are swapped by mistake.
Recover the tree without changing its structure.

    def recoverTree(self, root: TreeNode) -> None: # iterative inorder
        if not root:
            return
        stack = []
        x = y = prev = None
        
        
        while stack or root:  # stack 或者 root 有一个有值就行
            while root:
                stack.append(root)
                root = root.left
            root = stack.pop()
            if prev and prev.val > root.val: # 找到需要被交换的两次
                y = root     
                if x is None:
                    x = prev  
                else:
                    break
            prev = root
            root = root.right
        x.val, y.val = y.val, x.val
----------

# 450. Delete Node in a BST
Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.
Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

**Note:** Time complexity should be O(height of tree).

    def deleteNode(self, root: TreeNode, key: int) -> TreeNode:
        if not root:
            return None
        if root.val == key:
            if not root.left and not root.right:
                return None
            elif root.right:
                root.val = self.post(root)
                root.right = self.deleteNode(root.right, root.val)
            else:
                root.val = self.prev(root)
                root.left = self.deleteNode(root.left, root.val)
        elif root.val > key:
            root.left = self.deleteNode(root.left, key)
        else:
            root.right = self.deleteNode(root.right, key)        
        return root
    
    def post(self, root):
        root = root.right
        while root.left:
            root = root.left
        return root.val
    
    def prev(self, root):
        root = root.left
        while root.right:
            root = root.right
        return root.val
----------

# 91. Decode Ways
A message containing letters from `A-Z` is being encoded to numbers using the following mapping:

    'A' -> 1
    'B' -> 2
    ...
    'Z' -> 26

Given a **non-empty** string containing only digits, determine the total number of ways to decode it.

    def numDecodings(self, s: str) -> int:
        if not s:
            return 1
        dp = [0 for x in range(len(s) + 1)]
        # base case
        dp[0] = 1
        dp[1] = 0 if s[0] == "0" else 1
        
        for i in range(2, len(s) + 1):
            # one step jump
            if s[i - 1] != "0":
                dp[i] = dp[i - 1]
            
            #two step jump
            if 10 <= int(s[i - 2: i]) <= 26:
                dp[i] += dp[i - 2]
                
        return dp[-1]
----------

# 62. Unique Paths
A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).
The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).
How many possible unique paths are there?

    def uniquePaths(self, m: int, n: int) -> int:
        if not m or not n:
            return 0
        cur = [1] * n
        for i in range(1, m):
            for j in range(1, n):
                cur[j] += cur[j - 1]
        return cur[-1]
----------

# 116. Populating Next Right Pointers in Each Node
You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

    struct Node {
      int val;
      Node *left;
      Node *right;
      Node *next;
    }

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.
Initially, all next pointers are set to `NULL`.

    class Solution:
      def connect(self, root: 'Node') -> 'Node':
          if not root:
              return root
          leftmost = root
          while leftmost.left:
              curr = leftmost
              while curr:
                  curr.left.next = curr.right
                  if curr.next:
                      curr.right.next = curr.next.left
                  curr = curr.next
              leftmost = leftmost.left
          return root
      
      def connect1(self, root: 'Node') -> 'Node':
          from collections import deque
          queue = deque()
          if not root:
              return root
          queue.append(root)
          while queue:
              size = len(queue)
              for i in range(size):
                  node = queue.popleft()
                  if i < size - 1:
                      node.next = queue[0]
                  if node.left:
                      queue.append(node.left)
                  if node.right:
                      queue.append(node.right)
          return root
----------

# 76. Minimum Window Substring
Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

    **Example:**
    Input: S = "ADOBECODEBANC", T = "ABC"
    Output: "BANC"
    **Note:**
    - If there is no such window in S that covers all characters in T, return the empty string `""`.
    - If there is such window, you are guaranteed that there will always be only one unique minimum window in S.
    '''
    j    0123456789    i   012
    S = "ADOBECODEB", T = "ABC"
    分析：
    1. Find the first window that contains all letters in t;
    2. Keep expanding the window to the right by 1 char at a time, reducing left side if possible.
    3. Make sure that THE ACTIVE WINDOW ALWAYS CONTAINS ALL LETTERS IN t. 
    4. In this case, every time the window is expanded, only the new char need to be checked.
    要 track 的4 个变量， remaining missing, position of previous first match, start and end position
    '''
    def minWindow(self, s: str, t: str) -> str:
        need = collections.Counter(t)    # >>> need = Counter({'A': 1, 'B': 1, 'C': 1})
        missing = len(t)
        left, right, i = 0, 0, 0
        for j, char in enumerate(s, 1):
            if need[char] > 0:
                missing -= 1    # 找到对应的 char， missing -1 --> missing = 0时，存在潜在的解 
            need[char] -= 1     # 无论 char 在不在 need 里，都进行-1
                                # after matching all chars, then looking for the start
            if missing == 0:             
                while need[s[i]] < 0:    # need[s[i]] < 0 表示 i 不是 t 里的元素
                    need[s[i]] += 1      # 逐步缩小 i 和 j 的范围，找到 min window                   
                    i += 1               # [i, j] 是当前区间，[left, right]是理想区间
                if right == 0 or j - i < right - left:  
                    left, right = i, j   # 如果找到更小的[i, j]，把这个区间赋给[left, right]
                need[s[i]] += 1          # update to be ready for next window
                missing += 1
                i += 1                   
        return s[left: right]
----------

# 560. Subarray Sum Equals K
Given an array of integers and an integer **k**, you need to find the total number of continuous subarrays whose sum equals to **k**.

    **Example 1:**
    Input:nums = [1,1,1], k = 2
    Output: 2


    # hashmap    key: prefixSum[j] - k,    value : prefixSum[i - 1]
    def subarraySum(self, nums: List[int], k: int) -> int:
        prefixSum = {}
        sum = 0
        count = 0
        prefixSum[0] = 1
        for i in range(len(nums)):
            sum += nums[i]
            if sum - k in prefixSum:
                count += prefixSum[sum - k]
            prefixSum[sum] = prefixSum.setdefault(sum, 0) + 1 
        return count

