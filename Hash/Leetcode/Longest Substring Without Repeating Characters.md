### `Problem explain`

Given a string s, find the length of the longest substring without repeating characters.
----

### `문제 설명`

문자열 s가 주어졌을 때, 반복되는 문자가 없는 가장 긴 substring의 길이를 구하세요.
----

### `Constraints`

1. 0 <= s.length <= 5 * 104

2. s consists of English letters, digits, symbols and spaces.

### `Input/Output Example`

|Input|Output|
|---|---|
|pwwkew|3|

=> 'wke'

|Input|Output|
|---|---|
|abcabcbb|3|

=> 'abc'

|Input|Output|
|---|---|
|dvdf|3|

=> 'vdf'

----

### `ANS`

```python
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        dict = {}
        substr = ""
        maxlen = 0
        for i in range(0,len(s)):
            if dict.get(s[i],-1) == -1: # 사전에 정의되지 않았다면
                dict[s[i]] = i # 사전에 정의
                substr += s[i]
                if maxlen < len(substr):
                        maxlen = len(substr)
            else: # 사전에 정의되어 있다면
                if s[i] == s[i-1]: # 바로전 단어와 같을 경우 pwwkew / 현재는 pw[w]
                    substr = "" # "pw" -> ""
                    substr += s[i] # "" -> "w"
                else: # 바로전 단어와 다를 경우 => dvdf, ckilbkd, abba
                    if s[i] not in substr:
                        substr += s[i]
                    else:
                        idx = substr.index(s[i]) # 현재 단어의 인덱스를 구해서
                        substr = substr[idx+1:] # 그 인덱스의 왼쪽을 전부 짜름 
                        substr += s[i] # 다시 해당하는 단어 +
            if maxlen < len(substr):
                maxlen = len(substr)

        return maxlen

```

<img width="409" alt="image" src="https://user-images.githubusercontent.com/84978165/226494074-30847943-88a8-4bee-863f-ed1c986e2194.png">



