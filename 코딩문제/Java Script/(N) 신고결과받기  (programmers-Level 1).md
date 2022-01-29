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
    const reportcopy = [...report];
    const idcopy = [...id_list]
  
  //filter로 같은 부분을 지워준다.
    const filterarr =[];
    reportcopy.forEach(el =>{
        if(!filterarr.includes(el)){
            filterarr.push(el)   
        }
    })    
  //listObj에는 key값에 신고당한 인원명 value에는 신고받은 횟수를 입력
  //checkObj에는 key값에는 신고한 인원명 value에는 신고한 인원의 list를 배열로 입력 
    const listObj = {};
    const checkObj = {};
    filterarr.forEach(el => {
        let element = el.split(' ');
        if(!checkObj[element[1]]){
            checkObj[element[1]] = 1
        }
        else{
            checkObj[element[1]]++
        }
        
        if(!listObj[element[0]]){
            listObj[element[0]] = [element[1]]
        }
        else{
            listObj[element[0]].push(element[1])
        }
    })
    
   //listObj와 checkObj를 for-in문으로 돌면서 신고당한 횟수가 k보다 크고 listObj에 신고한 대상에 인원이 포함되어 있으면 resultObj에 입력해준다. 
    const resultObj ={};
    for(let key in checkObj){
        for(let person in listObj){
            if(checkObj[key] >= k && listObj[person].includes(key)){
                if(!resultObj[person]){
                    resultObj[person] = 1
                }
                else{
                    resultObj[person]++
                }
            }   
        }
    }
   //result에 idcopy에 map을 사용해서 id_list순대로 메일을 받을 횟수를 result배열에 순서대로 할당해준다. 
    const result = idcopy.map(el => {
        if(!resultObj[el]){
            return 0
        }
        else{
            return resultObj[el]
        }
    })
    return result
}

//testCase => 3,11,15,21 미통과
```
