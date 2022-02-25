<출처 - https://programmers.co.kr/learn/courses/30/lessons/42888>
- 문제설명

카카오톡 오픈채팅방에서는 친구가 아닌 사람들과 대화를 할 수 있는데, 본래 닉네임이 아닌 가상의 닉네임을 사용하여 채팅방에 들어갈 수 있다.
신입사원인 김크루는 카카오톡 오픈 채팅방을 개설한 사람을 위해, 다양한 사람들이 들어오고, 
나가는 것을 지켜볼 수 있는 관리자창을 만들기로 했다. 채팅방에 누군가 들어오면 다음 메시지가 출력된다.
```
"[닉네임]님이 들어왔습니다."
```
채팅방에서 누군가 나가면 다음 메시지가 출력된다.
```
"[닉네임]님이 나갔습니다."
```
채팅방에서 닉네임을 변경하는 방법은 다음과 같이 두 가지이다.
채팅방을 나간 후, 새로운 닉네임으로 다시 들어간다.
채팅방에서 닉네임을 변경한다.
닉네임을 변경할 때는 기존에 채팅방에 출력되어 있던 메시지의 닉네임도 전부 변경된다.

```
예를 들어, 채팅방에 "Muzi"와 "Prodo"라는 닉네임을 사용하는 사람이 순서대로 들어오면 채팅방에는 다음과 같이 메시지가 출력된다.
```

## 입력값
```
["Enter uid1234 Muzi", "Enter uid4567 Prodo","Leave uid1234","Enter uid1234 Prodo","Change uid4567 Ryan"]
```

나의 풀이(1h) :
```js
function solution(record) {
    //들어온 인원들의 uuid를 통해 닉네임을 객체로 만들기 
    const userObj = {};
    const actionArr = [];
    const result =[];
    
    //userObj에 user의 uuid로 닉네임을 저장한다.
    //uuid로 최신화된 닉네임이 유지된다.
    
    record.forEach(el => {
        const userAction = el.split(' ') 
        if(userAction[0] === 'Enter'){
            userObj[userAction[1]] = userAction[2]
        }
        else if(userAction[0] === 'Change'){
            userObj[userAction[1]] = userAction[2]
        }
        })
    
    //user의 활동을 기반으로 최신화된 닉네임이 저장된 user의 닉네임을 사용해서 resultarr에 저장한다.
    
    record.forEach(el => {
         const userAction = el.split(' ') 
         
        if(userAction[0] === 'Enter'){
            result.push(`${userObj[userAction[1]]}님이 들어왔습니다.`)
        }
        else if(userAction[0] === 'Leave'){
            result.push(`${userObj[userAction[1]]}님이 나갔습니다.`)
        }
    })
    
    return result
}
```
