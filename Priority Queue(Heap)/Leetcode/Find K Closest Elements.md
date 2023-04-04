### `Problem explain`

Given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The result should also be sorted in ascending order.

An integer a is closer to x than an integer b if:

|a - x| < |b - x|, or

|a - x| == |b - x| and a < b


----

### `문제 설명`

정렬된 정수형 배열 arr과 두 정수 k, x가 입력값으로 주어졌을 때, 배열에서 x에 가장 가까운 정수를 k개 반환하세요. 결과 또한 오름차순으로 정렬된 배열이여야만 합니다.

다음과 같은 경우 정수 a는 정수 b보다 x에 더 가깝습니다.

|a - x| < |b - x|, or

|a - x| == |b - x| and a < b

----

### `Constraints`

1 <= k <= arr.length

1 <= arr.length <= 104

arr is sorted in ascending order.

-104 <= arr[i], x <= 104

### `Input/Output Example`

## Example 1:

```
Input: arr = [1,2,3,4,5], k = 4, x = 3
Output: [1,2,3,4]
```

## Example 2:

```
Input: arr = [1,2,3,4,5], k = 4, x = -1
Output: [1,2,3,4]
```
----

### `ANS`

```python
class Solution(object):
    def findClosestElements(self, arr, k, x):
        # 배열에서 x에 가장 가까운 정수 k개를 배열로 반환
        hq = []
        for i in range(len(arr)):
            hq.append([abs(arr[i]-x),i]) # [|값-x|, 인덱스]
        hq.sort()
        answer = []
        for i in range(k):
            answer.append(arr[hq[i][1]])
        answer.sort()
        return answer
        """
        :type arr: List[int]
        :type k: int
        :type x: int
        :rtype: List[int]
        """
```

<img width="446" alt="image" src="https://user-images.githubusercontent.com/84978165/229794164-914a8a3d-0398-45b6-b86d-871d0e494e05.png">


---

```python
# 이분탐색(binary_search) 사용?
```


