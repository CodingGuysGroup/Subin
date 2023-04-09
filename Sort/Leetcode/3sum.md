### `Problem explain`

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

----

### `문제 설명`

정수형 배열 nums가 주어졌을 때 배열안에서 합이 0이되는 세개의 인덱스를 구해서 배열로 반환, 각각의 삼중합 배열은 이중 배열에 넣어서 반환하며 삼중합이 0이되는 배열들은 겹치면 안됨

----

### `Constraints`

3 <= nums.length <= 3000

-105 <= nums[i] <= 105

### `Input/Output Example`

## Example 1:

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter
```
## Example 2:

```
Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.

```
## Example 3:

```
Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.
```
----

### `ANS`

실패한 풀이(시간초과)
```python
class Solution(object):
    def threeSum(self, nums):
        # [-1,0,1,2,-1,-4]
        # [[-1,-1,2],[-1,0,1]]
        # i != j, i != k, and j != k
        ans = []
        nums.sort()
        lennum = len(nums)
        for i in range(lennum-2):
            if nums[i] > 0:
                break
            for j in range(i+1,lennum-1):
                k = 0 - (nums[i] + nums[j])
                if k in nums[j+1:lennum+1]:
                    k = nums.index(k)
                    if [nums[i],nums[j],nums[k]] not in ans:
                        ans.append([nums[i],nums[j],nums[k]])
                    #print("{},{},{}".format(i,j,k))
        #print(ans)
        return ans                     
```

실패해서 구글링해서 찾아본 정답

```python
class Solution(object):
    def threeSum(self, nums):
        # [-1,0,1,2,-1,-4]
        # [[-1,-1,2],[-1,0,1]]
        # i != j, i != k, and j != k
        ans = []
        nums.sort()
        lennum = len(nums)
        for i in range(lennum-2):
            if i>0 and nums[i] == nums[i-1]:
                continue
            j = i+1
            k = lennum-1
            while j < k:
                # [-4,-1,-1,0,1,2]
                tsum = nums[i] + nums[j] + nums[k]
                if tsum < 0: # 음수면 왼쪽 포인터 오른쪽 이동
                    j += 1
                elif tsum > 0: # 양수면 오른쪽 포인터 왼쪽 이동
                    k -= 1
                else: 
                    ans.append([nums[i],nums[j],nums[k]])

                    # 왼쪽 포인터가 오른쪽 포인터를 넘어설 경우 빠져나감
                    while j<k and nums[j] == nums[j+1]:
                        # 왼쪽 포인터와 같은 수가 나올때까지 왼쪽 포인터를 오른쪽으로 이동
                        j += 1
                    while j<k and nums[k] == nums[k-1]:
                        # 오른쪽 포인터와 같은 수가 나올때까지 오른쪽 포인터를 왼쪽으로 이동
                        k -= 1
                    j += 1
                    k -= 1
                    #print("{},{},{}".format(i,j,k))
        #print(ans)
        return ans
        
                        
```




