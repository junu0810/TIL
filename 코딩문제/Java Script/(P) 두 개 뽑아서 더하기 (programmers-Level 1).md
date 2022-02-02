<출처 - https://programmers.co.kr/learn/courses/30/lessons/68644>

문제 설명
- 정수 배열 numbers가 주어집니다. 
- numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 하도록 solution 함수를 완성해주세요.

나의 풀이(40M) :
```js
function solution(numbers) {
    //원본 배열을 deepcopy 합니다.
    const numarr = [...numbers];
    //결과를 담을 배열 선언
    const result =[];
    
    //for문을 활용해서 배열의 하나씩 빼서 part변수에 담습니다. 
    for(let i=0; i<numbers.length; i++){
        let part = numarr[0]
        numarr.shift()
        
        //forEach문을 활용해서 result문에 없는 값일 경우 배열내의 값들을 더해서 push해 줍니다.
        numarr.forEach(el => {
            let element = el + part
            if(!result.includes(element)){
                result.push(element)
            }
        })
    }
    return result.sort((a,b) => a - b)
}
//유의사항 :: numarr를 shift하기 때문에 for문의 값은 원본 배열을 설정하여 모든 배열을 돌도록 선언한다. 
```
