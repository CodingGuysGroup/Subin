### `Problem explain`

You are given an integer array nums with no duplicates. A maximum binary tree can be built recursively from nums using the following algorithm:

1.Create a root node whose value is the maximum value in nums.

2.Recursively build the left subtree on the subarray prefix to the left of the maximum value.

3.Recursively build the right subtree on the subarray suffix to the right of the maximum value.

4.Return the maximum binary tree built from nums.

----

### `문제 설명`

중복없는 정수형 배열 nums가 선언되어 있습니다. 최대 이진 트리는 nums로 부터 다음과같은 알고리즘을 따라 재귀적으로 설계됩니다.

1. nums배열의 최대값을 트리의 루트 노드로 생성합니다.

2. nums배열 최대값 인덱스의 왼쪽의 값들을 재귀적으로(1로 돌아감) left tree로 설계합니다.

3. nums배열 최대값 인덱스의 오른쪽의 값들을 재귀적으로(1로 돌아감)  right tree로 설계합니다.

4. nums배열로부터 최대 이진 트리를 반환합니다.


### `Constraints`

1. 1 <= nums.length <= 1000

2. 0 <= nums[i] <= 1000

3. All integers in nums are unique.

### `Input/Output Example`

|Input|Output|
|---|---|
|[3,2,1,6,0,5]	|[6,3,5,null,2,0,null,null,1]|

![image](https://user-images.githubusercontent.com/84978165/224588629-c13a4557-b063-45e0-9995-b708300d0f9c.png)


|Input|Output|
|---|---|
|[3,2,1]|[3,null,2,null,1]|

![image](https://user-images.githubusercontent.com/84978165/224588700-beefe6ef-9d9a-4426-b23b-32f542828566.png)


----

### `ANS`

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def constructMaximumBinaryTree(self, nums):
        if not nums:
            return
            
        mx = max(nums)
        index=nums.index(mx)
        root = TreeNode(mx)
        root.left = self.constructMaximumBinaryTree(nums[:index])
        root.right = self.constructMaximumBinaryTree(nums[index+1:])
        return root


```

<img width="595" alt="스크린샷 2023-03-09 205802" src="https://user-images.githubusercontent.com/84978165/224016477-474f2df9-cb7f-478a-bce9-96ee1a964121.png">


