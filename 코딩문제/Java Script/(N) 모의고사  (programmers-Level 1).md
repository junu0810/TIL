<출처 - https://programmers.co.kr/learn/courses/30/lessons/42840#>

- 수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.
1. 1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
2. 2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...,
3. 3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

1. 시험은 최대 10,000 문제로 구성되어있습니다.
2. 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
3. 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.



나의 풀이(1h) :

```js
function solution(answers) {
    //시험 찍은 순서 패턴을 정리 
    const hum1 = [1,2,3,4,5];
    const hum2 = [2,1,2,3,2,4,2,5];
    const hum3 = [3,3,1,1,2,2,4,4,5,5];
    //입력받은 정답의 배열을 순서대로 나열
    let anscopy = [...answers];
    
    //정답을 맞출때마다 count'사람수'를 +1 해준다.
    let count1 = 0;
    let count2 = 0;
    let count3 = 0;
    
    //찍은 순서배열을 사용하기 때문에 deepcopy를 통해 변수에 옮겨놓는다.
    let hum1copy = [...hum1];
    let hum2copy = [...hum2];
    let hum3copy = [...hum3];
    
    //정답 순서를 하나씩 훑어본다.
    for(let i=0; i<anscopy.length; i++){
    //정답 i번째 순서가 0번째 순서와 같을경우 count를 + 해준다.
        if(anscopy[i] === hum1copy[0]){
            count1++
            //비교뒤 정답 순서배열에서 비교한걸 없앤다.
            hum1copy.shift()
        }
        //정답 비교간 결과가 undefinded가 나올경우(정답배열은 남아 있지만 찍은 순서배열이 없어질경우)
        //다시한번 찍는 순서 비교배열에 다시한번 전체 배열을 할당해준다.
        else if((anscopy[i] === hum1copy[0]) === undefined){
            hum1copy = [...hum1]
        }
        //비교하고 같지 않을경우 비교대상의 배열만 없애서 다음 순서로 넘긴다. 
        else{
            hum1copy.shift()
        }
        
        
        if(anscopy[i] === hum2copy[0]){
            count2++
            hum2copy.shift()
        }
        else if((anscopy[i] === hum2copy[0]) === undefined){
            hum2copy = [...hum2]
        }
        else{
            hum2copy.shift()
        }
        
        
        if(anscopy[i] === hum3copy[0]){
            count3++
            hum3copy.shift()
        }
        else if((anscopy[i] === hum3[0]) === undefined){
            hum3copy = [...hum3]
        }
        else{
            hum3copy.shift()
        }
    }
    
    //가장 큰 결과값을 maxnum에 넣어준다.
    const maxnum = Math.max(count1,count2,count3);
    
    //결과를 닮은 배열을 생성
    const result = [];
    
    //싱글 스레드를 이용해 큰 결과값이랑 인원별 count값이랑 같을경우 결과배열에 push한다.
    //모두 같은결과값이라도 정상적으로 결과 배열에 담긴다.
    if(maxnum === count1){
        result.push(1)
    }
    if(maxnum === count2){
        result.push(2)
    }
    if(maxnum === count3){
        result.push(3)
    }
    
    //최종 result값을 넣어준다.
    return result
}
//테스트 케이스 5,6,7,9,11,12,15
```
