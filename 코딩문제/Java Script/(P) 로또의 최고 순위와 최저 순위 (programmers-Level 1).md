<출처 - https://programmers.co.kr/learn/courses/30/lessons/77484>
- 문제설명
로또를 구매한 민우는 당첨 번호 발표일을 학수고대하고 있었습니다. 하지만, 민우의 동생이 로또에 낙서를 하여, 일부 번호를 알아볼 수 없게 되었습니다.
당첨 번호 발표 후, 민우는 자신이 구매했던 로또로 당첨이 가능했던 최고 순위와 최저 순위를 알아보고 싶어 졌습니다.

1. 알아볼 수 없는 번호를 0으로 표기하기로 하고, 
2. 구매한 로또 번호 6개가 44, 1, 0, 0, 31 25라고 가정해보겠습니다. 
3. 당첨 번호 6개가 31, 10, 45, 1, 6, 19라면, 당첨 가능한 최고 순위와 최저 순위의 한 예는 아래와 같습니다.

|당첨 번호	31	10	45	1	6	19	결과
|최고 순위 번호	31	0→10	44	1	0→6	25	4개 번호 일치, 3등
|최저 순위 번호	31	0→11	44	1	0→7	25	2개 번호 일치, 5등

나의 풀이(50M) :
```js
function solution(lottos, win_nums) {
    const copylotto = [...lottos]
    const copywin =[...win_nums]
    let count = 0;
    
    const filterarr = copylotto.map(el =>{
        if(el !==0){
           return copywin.includes(el)
        }
        else{
            return 0
        }
    })
    
    let max = 0;
    let min = 0;
    filterarr.forEach(el =>{
        if(el === true || el === 0){
            max++
        }
        if(el === true){
            min++
        }
    })
    
    const grade ={
        6:1,
        5:2,
        4:3,
        3:4,
        2:5,
    }
    return [ grade[max] ? grade[max] : 6 , grade[min] ? grade[min] : 6 ]
}

//모든 테스트 케이스 통과
```
