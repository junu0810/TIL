- 문제
준규가 가지고 있는 동전은 총 N종류이고, 각각의 동전을 매우 많이 가지고 있다.
동전을 적절히 사용해서 그 가치의 합을 K로 만들려고 한다. 이때 필요한 동전 개수의 최솟값을 구하는 프로그램을 작성하시오.

- 입력
첫째 줄에 N과 K가 주어진다. (1 ≤ N ≤ 10, 1 ≤ K ≤ 100,000,000)
둘째 줄부터 N개의 줄에 동전의 가치 Ai가 오름차순으로 주어진다. (1 ≤ Ai ≤ 1,000,000, A1 = 1, i ≥ 2인 경우에 Ai는 Ai-1의 배수)

- 출력
첫째 줄에 K원을 만드는데 필요한 동전 개수의 최솟값을 출력한다.

<img width="1142" alt="image" src="https://user-images.githubusercontent.com/89199949/213617661-944299e6-7ddb-4858-beb1-1a60699ffdfe.png">


```js
const arr = require('fs').readFileSync('dev/stdin').toString().trim().split("\n");

let targetNum = Number(arr[0].split(" ")[1]);
let coinList = arr.slice(1,arr.length).map(el => {return Number(el)}).sort((a,b) => {return b-a});

let count = 0;

const changeCoin = (coin , List) => {
    List.forEach(el => {
        if(el <= coin){
            // 소숫점을 제외한 정수부분만의 몫을 구하고 싶을땐 parseInt를 사용하면 된다.
            count += parseInt(coin / el)
            coin = coin%el
        }
    })
}

changeCoin(targetNum, coinList)
console.log(count)
```
