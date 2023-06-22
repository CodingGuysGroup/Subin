
### `Problem explain`

You are given the root of a binary search tree (BST), where the values of exactly two nodes of the tree were swapped by mistake.

Recover the tree without changing its structure.

<img width="407" alt="image" src="https://github.com/CodingGuysGroup/Subin/assets/84978165/877dd1fc-7402-4870-937c-4bbaa68ea0f3">

<img width="444" alt="image" src="https://github.com/CodingGuysGroup/Subin/assets/84978165/45996a56-9466-42cc-9624-1e061e88ed1c">



----

### `Constraints`

The number of nodes in the tree is in the range [2, 1000].

-231 <= Node.val <= 231 - 1

----


```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution(object):
    def recoverTree(self, root):

        # root = [3,1,4,null,null,2]는 다음과 같은 형식
        # TreeNode{val: 3, 
        # left: TreeNode{val: 1, left: None, right: None}, 
        # right: TreeNode{val: 4, left: TreeNode{val: 2, left: None, right: None}, right: None}}

        # left의 val은 얼만큼 트리가 뻗어나가든 상위 node의 val보다 작아야 함
        # right의 val 또한 상위 node의 val보다 커야 함

        self.tempAnode, self.tempBnode, self.prev = None, None, TreeNode(float('-inf')) 
        def recover(node): # root = [3,1,4,null,null,2]
            if node:
                recover(node.left) 
                if self.prev.val >= node.val: 
                    # 이전 노드가 현재 노드보다 크거나 같을 경우
                    # left, root
                    # root, right
                    self.tempAnode = self.tempAnode or self.prev
                    self.tempBnode = node
                self.prev = node
                recover(node.right)
        recover(root)   
        self.tempAnode.val, self.tempBnode.val = self.tempBnode.val, self.tempAnode.val

'''
        root_val = root.left
        index=root.index(root_val)
        root = TreeNode(root_val)
        root.left = self.recoverTree(root[:index])
        if root.left > root.val:
            leftidx = nums.index(root.left)
            idx = nums.index(root.val)
            nums[idx], nums[leftidx] = nums[leftidx], nums[idx]
        root.right = self.recoverTree(root[index+1:])
        if root.right < root.val:
            rightidx = nums.index(root.right)
            idx = nums.index(root.val)
            nums[idx], nums[leftidx] = nums[rightidx], nums[idx]
            '''   
            

```



