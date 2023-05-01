### `문제 설명`

H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과1에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

### `제한 사항`

과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.

논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

### `입출력 예`

<img width="153" alt="image" src="https://user-images.githubusercontent.com/84978165/235407432-60439924-ef84-4829-b787-0db40998cf4b.png">

#### 입출력 예 설명

이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.

----

### `ANS`

```python

def solution(citations):
    citations.sort()
    print(citations)
    hindex = 0
    while True:
        temph = 0 # hindex번 이상인용된 논문의 갯수
        for i in citations:
            if i >= hindex:
                temph += 1
        
        # break에 걸릴 경우 이전 hindex가 최대치라는 소리이므로 아래서 -1을 해줌
        if temph < hindex:
            break
        if len(citations) - temph > hindex:
            break
            
        hindex += 1
        
        
    answer = hindex - 1
    return answer

#[1, 4, 5]: 2 , 2번 이상 인용된 논문이 2편 이상[4,5]이고 나머지 논문은 2번 이하 인용
#[5, 6, 7]: 3, 3번 이상 인용된 논문이 3편[5,6,7]이고 나머지 논문은 3번이하 인용

```


<img width="475" alt="image" src="https://user-images.githubusercontent.com/84978165/235407517-44d4ca18-f36f-4127-a619-45df07c2a9d5.png">



