<출처 - https://programmers.co.kr/learn/courses/30/lessons/87390>

- 정수 n, left, right가 주어집니다. 다음 과정을 거쳐서 1차원 배열을 만들고자 합니다.

n행 n열 크기의 비어있는 2차원 배열을 만듭니다.

i = 1, 2, 3, ..., n에 대해서, 다음 과정을 반복합니다.

1행 1열부터 i행 i열까지의 영역 내의 모든 빈 칸을 숫자 i로 채웁니다.

1행, 2행, ..., n행을 잘라내어 모두 이어붙인 새로운 1차원 배열을 만듭니다.

새로운 1차원 배열을 arr이라 할 때, arr[left], arr[left+1], ..., arr[right]만 남기고 나머지는 지웁니다.

정수 n, left, right가 매개변수로 주어집니다. 주어진 과정대로 만들어진 1차원 배열을 return 하도록 solution 함수를 완성해주세요.



나의 풀이(1h) :

```js
풀이1) 
function solution(n, left, right) {

    let background = []
    
    for(let i=0; i<n; i++){
      let arr = new Array(n).fill(0)
      background.push(arr)  
    }
    
    let input = 1
    let low = [0,0]
    let col = [0,0]
    
    for(let i=0; i<n; i++){
        for(let y=0; y<=i; y++){
            background[low[0]][low[1]] = input
            low[1]++
        }
        
        for(let z=0; z<=i; z++){
            background[col[0]][col[1]] = input
            col[0]++
        }
        low = [input,0]
        col = [0,input]
        input++
    }
    let resultarr = [];
    background.forEach(el => {
       resultarr = resultarr.concat(el)
    })
    return resultarr.slice(left,right+1)
}

풀이2)
    
    let back = [];
    let count = 1
    for(let i=1; i<=n; i++){
        let ele = [];
        for(let y=1; y<=n; y++){
            if(i <= y){
                ele.push(y)
            }
            else{
                ele.push(count)
            }
            count
        }
        back.push(ele)
        count++
    }
   let resultarr = [];
   back.forEach(el =>{
       resultarr = resultarr.concat(el)
   })
   return resultarr.slice(left,right+1)   
```
문제가 풀리지 않는것은 아니나 시간초과가 결과가 몇개씩 나온다.
시간 복잡도를 다시한번더 생각해보면 좋을거 같다.
시간 복잡도가 아닌 2차원배열로 전체를 만들고 값을 찾으려고 하면 너무 많은 시간이 소요된다. 
left와 right값으로 규칙성을 찾아서 (left+a) ~ (right+a) 만큼 생성해야한다.

