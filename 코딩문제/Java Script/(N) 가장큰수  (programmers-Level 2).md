<출처 - https://programmers.co.kr/learn/courses/30/lessons/42746>

- 문제설명

0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.
나의 풀이(1h 25M) :
```js
function solution(numbers) {

function permutation(arr, selectNum) {
  let elearr = [];
  if (selectNum === 1) return arr.map((v) => [v]);

  arr.forEach((v, idx, arr) => {
    const fixer = v;
    const restArr = arr.filter((_, index) => index !== idx);
    const permuationArr = permutation(restArr, selectNum - 1);
    const combineFixer = permuationArr.map((v) => [fixer, ...v]);
    elearr.push(...combineFixer);
  });
  return elearr;
}
    
    const resultarr = permutation(numbers,numbers.length)
    const result = resultarr.map(el => {
       const element =  el.reduce((el,ele) => {
            return el+ele
        },'')
       
       return Number(element)
    })
    return `${Math.max(...result)}`
}
```
