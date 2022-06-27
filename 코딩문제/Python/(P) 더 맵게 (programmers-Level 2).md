<출처 - https://programmers.co.kr/learn/courses/30/lessons/42626>

- 문제설명

Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.

Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 

모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

- 제한사항 

1. scoville의 길이는 2 이상 1,000,000 이하입니다.
2. K는 0 이상 1,000,000,000 이하입니다.
3. scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
4. 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.

나의 풀이(1h 50M) :
```python
import heapq

def solution(scoville, K):
    count = 0
    heapq.heapify(scoville)    
    
    while scoville[0] <= K and len(scoville) > 1:
        ele1 = heapq.heappop(scoville)
        ele2 = heapq.heappop(scoville)
        heapq.heappush(scoville, ele1 + (ele2 *2))
        count += 1
        
        if len(scoville) == 1 and scoville[0] < K:
            return -1 
            
    return count  
```
- 최초 문제를 풀었으나 효용성에서 문제가 풀리지 않았었음
- python의 heapq 모듈을 사용해서 문제를 푸니 효용성 문제가 해결되었음
(참고 - https://www.daleseo.com/python-heapq/ )
