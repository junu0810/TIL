- 문제설명
<그림 1>과 같이 9×9 격자판에 쓰여진 81개의 자연수 또는 0이 주어질 때, 이들 중 최댓값을 찾고 그 최댓값이 몇 행 몇 열에 위치한 수인지 구하는 프로그램을 작성하시오.
예를 들어, 다음과 같이 81개의 수가 주어지면
<img width="456" alt="image" src="https://user-images.githubusercontent.com/89199949/212590624-1e205425-49c3-42f4-b1c4-b1c3572d6e5e.png">
이들 중 최댓값은 90이고, 이 값은 5행 7열에 위치한다.

- 입력
첫째 줄부터 아홉 번째 줄까지 한 줄에 아홉 개씩 수가 주어진다. 주어지는 수는 100보다 작은 자연수 또는 0이다.

- 출력
첫째 줄에 최댓값을 출력하고, 둘째 줄에 최댓값이 위치한 행 번호와 열 번호를 빈칸을 사이에 두고 차례로 출력한다. 최댓값이 두 개 이상인 경우 그 중 한 곳의 위치를 출력한다.


<img width="1141" alt="image" src="https://user-images.githubusercontent.com/89199949/212590734-0d84201a-45bd-4853-b845-7cbce4f45555.png">


```js
var fs = require('fs');
const arr = require('fs').readFileSync('dev/stdin').toString().trim().split("\n");

let numArr = arr.map(el => {
    return el.split(" ").map(ele => {
        return Number(ele)
    })   
})

let resultArr = [];
numArr.forEach((el,ind) => {
    
    let maxNum = Math.max(...el)
    let maxNumInd = el.indexOf(maxNum)

    return resultArr.push([maxNum, ind, maxNumInd])
})

let result = [0];
resultArr.forEach(el => {
    if(result[0] <= el[0]){
        result = el
    }
})
console.log(result[0])
console.log(result[1]+1,result[2]+1)

```
