<출처 - https://programmers.co.kr/learn/courses/30/lessons/12951>
- 문제설명

JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 문자열 s가 주어졌을 때, 
s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

예시)"3people unFollowed me" =>	"3people Unfollowed Me"


나의 풀이(1h 15M) :
```js
function solution(s) {
    const arr = s.split(' ');
    const resultarr = [];
    
    for(let i=0; i<arr.length; i++){
      let elementarr = arr[i].split('')
      
      if(elementarr.length === 0){
          resultarr.push('')
      }
      
      else if(Number(elementarr[0]) === undefined){
          elementarr = elementarr.map(el => {
              return el.toLowerCase()
          })
          elementarr = elementarr.reduce((el,ele) => {
              return el+ele
          },'')
          resultarr.push(emementarr)
          continue
      }
      else{
          elementarr = elementarr.map(el => {
              return el.toLowerCase()
          })
          elementarr[0] = elementarr[0].toUpperCase()
          elementarr = elementarr.reduce((el,ele) => {
              return el+ele
          },'')
          resultarr.push(elementarr)
      }
      
    }
    return resultarr.reduce((el,ele) => {
        return el+' '+ele
    })
}
```
