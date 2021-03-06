<출처 - https://programmers.co.kr/learn/courses/30/lessons/42862 >
- 문제설명
점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 

1. 전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 
2. 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 
3. 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.
4. 여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 
남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.

나의풀이(1h) : 
```js
function solution(n, lost, reserve) {
//원본 배열 deepcopy 실행
    const lostcopy = [...lost].sort((a,b) => a-b);
    const reservecopy = [...reserve].sort((a,b) => a-b);
    
//조건4에 의해서 여벌 배열과 분실 배열에 둘다 존재할 경우 체육에 참여는 할 수 있지만 빌려주지는 못하기 때문에 두 배열에서 삭제    
    const filterlost = lostcopy.filter(el => {
        return !reserve.includes(el)
    })

    const filterreserve = reservecopy.filter(el => {
        return !lost.includes(el)
    })

//체육에 온전히 참여할 수 있는 인원 구하기 (총 인원 - 분실인원 - 여벌인원) 
//분실도 안하고 여벌도 없으면 아무 조건없이 참여할 수 있기때문에 온전히 참여 가능한 인원 확인
    let partperson = n-filterlost.length-filterreserve.length

//이중 For문을 활용해서 분실한 인원배열에 0번째 인덱스부터 여벌인원의 배열을 돌면서 빌려줄 수 있으면 같이 같이 하나의 배열로 묶여 이중 배열이 형성되도록 설정
//EX) lost: [2,4]   reserve:[1,3,5]  => [[1,2],[3,4],5]
    let ele;
for(let i=0; i<filterlost.length; i++){
    for(let y=0; y<filterreserve.length; y++){
    if((filterlost[i]-1 === filterreserve[y] || filterlost[i]+1 === filterreserve[y]) && !Array.isArray(filterreserve[y]) ){
     ele = filterreserve[y]
      filterreserve[y] = [ele,filterlost[i]]
      filterlost.shift()
    }
        }
    }
    
//체육복 분배계획이 끝나면 reserve배열에서 배열로 형성되어있으면 참여인원에 +2를 하고 아니면 +1을 하여 총 참여 가능한 인원을 구함
   filterreserve.forEach(el =>{
       if(Array.isArray(el)){
           partperson = partperson + 2
       }
       else {
           partperson++
       }
   })
//최종 참여가능한 인원 출력
    return partperson
    
}

//조건 4번을 제대로 유의안하고 분실한 인원에서 제거를 안하고 여벌의 인원에서만 제거를 해서 테스트를 통과 못했었음 (입력값 (5,[2,3,4], [1,2,3])을 통과못함) 
//조건을 잘 읽고 천천히 풀어보자
//모든 테스트 케이스 
```
