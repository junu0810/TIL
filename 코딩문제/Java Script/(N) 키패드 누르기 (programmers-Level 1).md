<출처 - https://programmers.co.kr/learn/courses/30/lessons/77484>

- 문제설명 
이 전화 키패드에서 왼손과 오른손의 엄지손가락만을 이용해서 숫자만을 입력하려고 합니다.
맨 처음 왼손 엄지손가락은 * 키패드에 오른손 엄지손가락은 # 키패드 위치에서 시작하며, 엄지손가락을 사용하는 규칙은 다음과 같습니다.

1. 엄지손가락은 상하좌우 4가지 방향으로만 이동할 수 있으며 키패드 이동 한 칸은 거리로 1에 해당합니다.
2. 왼쪽 열의 3개의 숫자 1, 4, 7을 입력할 때는 왼손 엄지손가락을 사용합니다.
3. 오른쪽 열의 3개의 숫자 3, 6, 9를 입력할 때는 오른손 엄지손가락을 사용합니다.
4. 가운데 열의 4개의 숫자 2, 5, 8, 0을 입력할 때는 두 엄지손가락의 현재 키패드의 위치에서 더 가까운 엄지손가락을 사용합니다.
5. 만약 두 엄지손가락의 거리가 같다면, 오른손잡이는 오른손 엄지손가락, 왼손잡이는 왼손 엄지손가락을 사용합니다.

나의 풀이(1h 20M) :
```js
function solution(numbers, hand) {
   const handler = [0,0]
   const result = []
   const midnum = [2,5,8,0]
   while(numbers.length !== 0){
       if(numbers[0] === 1 || numbers[0] === 4 || numbers[0] === 7){
           handler[0] = numbers[0]
           result.push('L');
           numbers.shift();
       }
       else if(numbers[0] === 3 || numbers[0] === 6 || numbers[0] === 9){
           handler[1] = numbers[0]
           result.push('R');
           numbers.shift();
       }
       else{
           if(!midnum.includes(handler[0]) && !midnum.includes(handler[1])){
               
           }else{
               let leftnum = Math.abs(handler[0] - numbers[0])
           let rightnum = Math.abs(handler[1] - numbers[0])
          if(leftnum > rightnum){
              handler[1] = numbers[0];
              numbers.shift();
              result.push('R');
          }
          else if(leftnum < rightnum){
              handler[0] = numbers[0];
              numbers.shift();
              result.push('L');
          }
          else{
              if(hand === 'right'){
              handler[1] = numbers[0];
              numbers.shift();
              result.push('R');
              }
              else{
              handler[0] = numbers[0];
              numbers.shift();
              result.push('L');
              }
           }
          }
       }
   }
    let resultstring = '';
    for(let i=0; i<result.length; i++){
        resultstring  = resultstring + result[i]
    }
    return resultstring
}
//무한 loop가 된다...
```
