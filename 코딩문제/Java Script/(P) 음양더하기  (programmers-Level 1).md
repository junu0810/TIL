<출처 - https://programmers.co.kr/learn/courses/30/lessons/68644>

- 문제설명

어떤 정수들이 있습니다. 
이 정수들의 절댓값을 차례대로 담은 정수 배열 absolutes와 이 정수들의 부호를 차례대로 담은 불리언 배열 signs가 매개변수로 주어집니다.
실제 정수들의 합을 구하여 return 하도록 solution 함수를 완성해주세요.

- 제한사항
1. absolutes의 길이는 1 이상 1,000 이하입니다.
2. absolutes의 모든 수는 각각 1 이상 1,000 이하입니다.
3. signs의 길이는 absolutes의 길이와 같습니다.
4. signs[i] 가 참이면 absolutes[i] 의 실제 정수가 양수임을, 그렇지 않으면 음수임을 의미합니다.
로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 하도록 solution 함수를 완성해주세요.

나의 풀이(40M) :
```js
function solution(absolutes, signs){
    const sum = 0;
    const copy = [...absolutes];
    const signcopy = [...signs]
    let resultarr = [];
    
    copy.forEach(el => {
        if(signcopy[0] === true){
            resultarr.push(el)
            signcopy.shift()
        }
        else{
            resultarr.push(-el)
            signcopy.shift()
        }
    })
    const result = resultarr.reduce((el,ele) => {
       return el+ele
    },0)
    return result
}
```
