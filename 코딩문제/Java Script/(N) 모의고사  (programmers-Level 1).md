출처 


```js
function solution(answers) {
    const hum1 = [1,2,3,4,5];
    const hum2 = [2,1,2,3,2,4,2,5];
    const hum3 = [3,3,1,1,2,2,4,4,5,5];
    let anscopy = [...answers];
    
    let count1 = 0;
    let count2 = 0;
    let count3 = 0;
    
    let hum1copy = [...hum1];
    let hum2copy = [...hum2];
    let hum3copy = [...hum3];
    
    for(let i=0; i<anscopy.length; i++){
        if(anscopy[i] === hum1copy[0]){
            count1++
            hum1copy.shift()
        }
        else if((anscopy[i] === hum1copy[0]) === undefined){
            hum1copy = [...hum1]
        }
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
    
    const maxnum = Math.max(count1,count2,count3);
    
    const result = [];
    
    if(maxnum === count1){
        result.push(1)
    }
    if(maxnum === count2){
        result.push(2)
    }
    if(maxnum === count3){
        result.push(3)
    }
    
    return result
}
```
