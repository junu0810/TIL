<출처 - https://programmers.co.kr/learn/courses/30/lessons/64065>

- 셀수있는 수량의 순서있는 열거 또는 어떤 순서를 따르는 요소들의 모음을 튜플(tuple)이라고 합니다. 
n개의 요소를 가진 튜플을 n-튜플(n-tuple)이라고 하며, 다음과 같이 표현할 수 있습니다.

튜플은 다음과 같은 성질을 가지고 있습니다.

1. 중복된 원소가 있을 수 있습니다. ex : (2, 3, 1, 2)
2. 원소에 정해진 순서가 있으며, 원소의 순서가 다르면 서로 다른 튜플입니다. ex : (1, 2, 3) ≠ (1, 3, 2)
3. 튜플의 원소 개수는 유한합니다.
4. 원소의 개수가 n개이고, 중복되는 원소가 없는 튜플 (a1, a2, a3, ..., an)이 주어질 때(단, a1, a2, ..., an은 자연수), 이는 다음과 같이 집합 기호 '{', '}'를 이용해 표현할 수 있습니다.

{{a1}, {a1, a2}, {a1, a2, a3}, {a1, a2, a3, a4}, ... {a1, a2, a3, a4, ..., an}}

#### 예를 들어 튜플이 (2, 1, 3, 4)인 경우 이는
- {{2}, {2, 1}, {2, 1, 3}, {2, 1, 3, 4}}와 같이 표현할 수 있습니다. 
- 이때, 집합은 원소의 순서가 바뀌어도 상관없으므로
1. {{2}, {2, 1}, {2, 1, 3}, {2, 1, 3, 4}}
2. {{2, 1, 3, 4}, {2}, {2, 1, 3}, {2, 1}}
3. {{1, 2, 3}, {2, 1}, {1, 2, 4, 3}, {2}}

는 모두 같은 튜플 (2, 1, 3, 4)를 나타냅니다.
특정 튜플을 표현하는 집합이 담긴 문자열 s가 매개변수로 주어질 때, s가 표현하는 튜플을 배열에 담아 return 하도록 solution 함수를 완성해주세요.


나의 풀이(2h) :

```js
function solution(s) {
    //배열로 만들어 0과 마지막의 {}을 없애줍니다.
    let copy = [...s.slice(1,s.length-1)]
    let check = false 
    let ele = '';
    let element = [];
    let result = [];
    
    //{1},{2}사이의 구분되는 ','를 없애줍니다.
    copy = copy.filter((el,ind) => {
        if(el === ',' && copy[ind+1] === '{'){
            return false
        }
        else{
           return true
        }
    })

 
    for(let i=0; i<copy.length; i++){
        //중간에 숫자인 부분은 합쳐서 하나의 문자열로 만듭니다.
        if(check === true && copy[i] !== ',' && copy[i] !== '}') {
            ele += copy[i]
            continue
        }
        //만약 다음 인덱스 숫자가 있으면 element배열에 넣어서 다음 숫자를 만들어 줍니다.
        if(copy[i] === ','){
            element.push(Number(ele))
            ele = ''
            continue
        }
        //하나의 구간이 끝나면 element가 0일경우 구간에 하나의 숫자밖에 없으므로 ele에 만들어둔 숫자를 배열에 담아 result에 push 합니다.
        //아닐경우 element를 result에 push 합니다.
        if(copy[i] === '}'){
            if(element.length === 0){
                result.push([Number(ele)])
                ele = ''
                check=false
                continue
            }
            else{
            element.push(Number(ele))
            ele = ''
            result.push(element)
            element = []
            check=false    
            }
        }
        //'{'가 시작되면 check를 true로 두어 숫자를 만들기 시작합니다.
        if(copy[i] === '{'){
            check = true
            continue
        }
    }
    //배열이 끝났다면 sort를 활용해 구간의 길이순을 오름차순으로 정렬합니다.
    result = result.sort((a,b) => a.length - b.length)
    const answer = [];
    //정렬이 끝났다면 answer에 포함되어있지 않은 숫자를 answer에 push하여 배열을 만듭니다.
    result.forEach(el => {
        for(let i=0; i<el.length; i++){
            if(!answer.includes(el[i])){
                answer.push(el[i])
            }
        }
    })
    return answer
}
```
