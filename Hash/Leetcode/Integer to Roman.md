### `Problem explain`

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

|Symbol|Value|
|---|---|
|I|1|
|V|5|
|X|10|
|L|50|
|C|100|
|D|500|
|M|1000|

For example, 2 is written as II in Roman numeral, just two one's added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. 

Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 

X can be placed before L (50) and C (100) to make 40 and 90. 

C can be placed before D (500) and M (1000) to make 400 and 900.

Given an integer, convert it to a roman numeral.

----

### `문제 설명`

로마 숫자는 I, V, X, L, C, D 및 M의 7가지 기호로 표시됩니다.

|Symbol|Value|
|---|---|
|I|1|
|V|5|
|X|10|
|L|50|
|C|100|
|D|500|
|M|1000|

예를 들어, 2는 로마 숫자에서 II로 표기되며, 단지 두 개의 1을 더한 것입니다. 12는 XII로 표기되며, 간단히 X + II입니다. 숫자 27은 XXVII로 표기되며, 이는 XX + V + II입니다.

로마 숫자는 일반적으로 왼쪽에서 오른쪽으로 큰 순서로 씁니다. 그러나 4의 숫자는 IIII가 아닙니다. 대신 숫자 4는 IV로 씁니다. 1이 5보다 앞에 있기 때문에 빼면 4가 됩니다. 같은 원리가 IX로 쓰여진 숫자 9에도 적용됩니다. 빼기가 사용되는 경우는 6가지입니다.

V(5)와 X(10) 앞에 I를 배치하여 4와 9를 만들 수 있습니다.

X는 L(50)과 C(100) 앞에 배치하여 40과 90을 만들 수 있습니다.

C는 D(500)와 M(1000) 앞에 배치되어 400과 900을 만들 수 있습니다.

정수가 주어지면 로마 숫자로 변환하십시오.

![image](https://user-images.githubusercontent.com/84978165/228226332-9fa99ffc-f834-4d29-b64e-267e7fda1696.png)


----

### `Constraints`

1 <= num <= 3999

### `Input/Output Example`

## Example 1:

```
Input: num = 3
Output: "III"
Explanation: 3 is represented as 3 ones.
```
## Example 2:

```
Input: num = 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.

```
## Example 3:

```
Input: num = 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```
----

### `ANS`

```python
from collections import deque

# 사전에 치환되는 로마자를 넣음
roman = {}
roman[1] = 'I'
roman[5] = 'V'
roman[10] = 'X'
roman[50] = 'L'
roman[100] = 'C'
roman[500] = 'D'
roman[1000] = 'M'

deq = deque()
def setRoman(sym, temp):
    # 1994
    # 4(5), 90(50), 900(500), 1000(5000)
    if temp / (5*sym) == 1: # 5,6,7,8,9
        if temp % (5*sym) == 4*sym: # 9(IX)
            deq.append(roman[sym]) # I
            deq.append(roman[temp+sym]) # X
        else:
            deq.append(roman[5*sym])
            temp %= 5*sym # 5,6,7,8
            temp /= sym 
            for i in range(temp):
                deq.append(roman[sym])
    else: # 1,2,3,4,10(*sym)
        if temp % (5*sym) == 4*sym: # 4(IV)
            deq.append(roman[sym])
            deq.append(roman[temp + sym])
        else: # 1,2,3
            temp /= sym # 20,30, 1000
            for i in range(temp):
                deq.append(roman[sym])

class Solution(object):
    def intToRoman(self, num):
        sym = 1
        temp = 0
        # 1994 => 4, 90, 900, 1000 반대로 나오게
        # 1994 => 1000, 900, 90, 4
        # 58 => 50, 8
        temparray = deque()
        while num != 0:
            temp = num % 10 * sym
            temparray.appendleft([sym,temp])
            sym *= 10
            num /= 10

        for i in temparray:
            # 1000
            # 900
            # 90
            # 4 
            # 에 대한 로마숫자를 전역 deq에 담는 함수
            setRoman(i[0],i[1])

       # print(deq)

        retstr = ""
        for i in deq:
            retstr += i

        deq.clear()
        
        return retstr
        
        # I=1 / IV = 4, IX = 9 , XLIX = 49
        # X=10 / XL = 40, XC = 90
        # C=100 / CD = 400, CM = 900
```

<img width="409" alt="image" src="https://user-images.githubusercontent.com/84978165/226494074-30847943-88a8-4bee-863f-ed1c986e2194.png">



