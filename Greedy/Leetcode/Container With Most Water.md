### `Problem explain`

You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

----

### `문제 설명`

n의 길이를 가진 정수형 array 'height'가 주어진다.

이곳에는 수직으로 그려진 선들이 height 배열의 요소만큼 높이를 가지고 수직으로 평면에 놓여져 있다.

넓이가 가장 큰 값이 도출되게 하는 두 라인을 구하라

두 라인은 경사가 지면 안된다. 즉, 이 말은 두 라인을 구했을 때 길이가 짧은 한쪽의 라인이 구하려는 넓이의 높이가 된다.



----

### `Constraints`

n == height.length

2 <= n <= 10^5 # BIG O표기법에서 O(N)은 10000이다. 즉, O(N)을 적어도 열번정도만 반복해야 하며, O(N^2), O(NlogN)으로 구현해서는 안된다는 소리이다.

0 <= height[i] <= 10^4

### `Input/Output Example`

![image](https://github.com/CodingGuysGroup/Subin/assets/84978165/40352c2a-be12-4425-b6fd-bf62dcc605a9)

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. 
In this case, the max area of water (blue section) the container can contain is 49.
```

----

## `ANS`

### 첫 시도에는 Y축을 기준으로 가장 긴 라인을 기준으로 왼쪽, 오른쪽을 탐색하였으나 [1,2,1], [1,2,4,3] 같은 예제들은 Y축에 구애받지 않는다.

### 다음 시도로써 X축을 기준으로 생각하였으며, 투 포인터를 사용해 X축의 길이에 대해서 그리디 알고리즘을 구현하려 하였다.

### 투 포인터의 또한 첫 시도에는 start와 end 포인터를 0부터 시작했으나, 그리디 알고리즘은 가장 최적인 답을 근시안적으로 택하는 알고리즘이므로

### 생각을 바꾸어 양 끝으로 포인터를 바꾸었고 한칸씩 높이에 따라 안쪽으로 당기며 그리디를 구현하였다.


```python
class Solution(object):
    def maxArea(self, height):
        # 10^5라는 소리는 O(N)*10 안에는 구현해야한다는 소리
        # O(N^2)은 절대 안됨

        # 1. 세로가 길어야 높이의 최댓값이 커지며, 넓이의 최댓값 또한 커짐
        # 2. 가로가 길어야 넓이의 최댓값이 커짐

        x_len = len(height)
        st = 0
        en = x_len-1
        max_area = 0

        while True:
            if st > en:
                break
            x_tmp = en - st
            #print("en:{}, st:{}".format(en,st))
            y_tmp = 0
            if height[st] < height[en]:
                y_tmp = height[st]
            else:
                y_tmp = height[en]
            tmp_area = x_tmp * y_tmp
            if max_area < tmp_area:
                max_area = tmp_area
            #print("{}*{} = {}".format(x_tmp,y_tmp,max_area))
            #print("height(en):{}, height(st):{}".format(height[en],height[st]))
            #print()

            if height[st] < height[en]:
                st += 1
            else:
                en -= 1
        # [2,3,4,5,18,17,6]
        return max_area

''' 
## 실패한 답안이다.
        # height => y축 기준
        cursor = 0
        maxheight = max(height)
        maxidx = height.index(maxheight)

        maxarea = 0
        # right move
        for i in range(maxidx+1,len(height)):
            tmparea = (i - maxidx)*height[i]
            if maxarea < tmparea:
                maxarea = tmparea

        # left move
        for i in range(maxidx-1,0,-1):
            tmparea = (i - maxidx)*height[i]
            if maxarea < tmparea:
                maxarea = tmparea
'''

```

<img width="452" alt="image" src="https://github.com/CodingGuysGroup/Subin/assets/84978165/cba40a1b-f7e8-44e6-9973-7c3fafb5abc3">



