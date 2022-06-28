<출처 - https://programmers.co.kr/learn/courses/30/lessons/92334>
- 문제설명
신입사원 무지는 게시판 불량 이용자를 신고하고 처리 결과를 메일로 발송하는 시스템을 개발하려 합니다. 무지가 개발하려는 시스템은 다음과 같습니다.

1. 각 유저는 한 번에 한 명의 유저를 신고할 수 있습니다.
2. 신고 횟수에 제한은 없습니다. 서로 다른 유저를 계속해서 신고할 수 있습니다.
3. 한 유저를 여러 번 신고할 수도 있지만, 동일한 유저에 대한 신고 횟수는 1회로 처리됩니다.
4. k번 이상 신고된 유저는 게시판 이용이 정지되며, 해당 유저를 신고한 모든 유저에게 정지 사실을 메일로 발송합니다.
5. 유저가 신고한 모든 내용을 취합하여 마지막에 한꺼번에 게시판 이용 정지를 시키면서 정지 메일을 발송합니다.


나의 풀이(1h 30M) :
```js
function solution(id_list, report, k) {

    let reportcopy = []
    const idcopy = [...id_list]
    const listObj = {};
    let resultObj = {}
    //listObj = {'신고받은 사람': [['신고한사람'], '신고당한 횟수']}
    idcopy.forEach(el => {
        listObj[el] = [[],0]
        resultObj[el] = 0
    })
    
   
    report.forEach(el => {
      let ele =  el.split(' ')
      
      //신고는 한대상에 대해 중복이 안되므로 걸러준다.신고한사람 리스트에 없으면 아래 코드를 돌린다.
       if(!listObj[ele[1]][0].includes(ele[0])){
           //신고한 사람 리스트에 추가한다.
            listObj[ele[1]][0].push(ele[0])
           //신고받은 횟수를 증가시킨다
            listObj[ele[1]][1]++
       }
    })
    //idcopy의 순대로 신고받은 횟수를 출력한다.
    
    let result = []
    for(let i in listObj){
       if(listObj[i][1] >= k){
           listObj[i][0].forEach(el=>{
               resultObj[el]++
           })
       }
    }   
    
    idcopy.forEach(el =>{
        result.push(resultObj[el])
    })
    return result
}    
```
