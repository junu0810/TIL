###  이진탐색(Binary Search)

1. 정렬되어 있는 데이터 배열에서 특정한 값을 찾아내는 알고리즘이다. 
2. 배열의 중간값을 시작으로 찾고자하는 값이 기준값보다 큰지 작은지를 따지며 위치를 찾는 방법이다.
3. 검색 원리상 정렬된 리스트에만 사용할 수 있다는 단점이 있다.
4. 하지만, 검색이 반복될 때마다 목표값을 찾을 확률은 두 배가 되므로 속도가 빠르다는 장점이 있다.



#### 1. 방법
<img width="452" alt="스크린샷 2022-02-03 오후 3 56 47" src="https://user-images.githubusercontent.com/89199949/152295898-51de01a6-aab6-4797-8941-d8cca0e9f3a2.png">


```js
예시)배열이 [2,5,7,8,11,13,17,19,23,29] 이고 찾고자 하는 값이 17일경우 

- 먼저 배열의 중간 값을 찾는다. 
11이라는 값이 도출된다. 

- 11을 기준으로 찾고자 하는값이 6보다 큰지 작은지 확인한다.
값이 큰것을 확인 하였으므로 왼쪽으로는 탐색을 안해도 된다.

- 11보다 큰 값들중 다시 중간 기준점을 잡는다. 
19가 도출되었다.

- 19가 도출되었다면 찾고자 하는값이 기준점과 큰지작은지 확인한다.
찾고자하는값이 19보다는 작으므로 기준값보다 오른쪽 값들은 탐색을 안해도 된다.

- 중갑값들중 다시 기준을 잡는다.
이때, 기준값이 찾고자 하는값과 같으므로 기준값의 위치를 출력한다.

```

#### 2. 전체 탐색과의 비교

다음 배열에서 target(두번쨰 인수값)을 찾아라 

([1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17] , 13)

binarySearch를 활용한 내 풀이(1h 40M) :
```js
function binarySearch(arr, target,started) {
    if(arr.length <= 2 && arr.indexOf(target) !== false){
      return arr.indexOf(target)
    }
    let start;
    let end = arr.length;
  
    started === undefined ? start = 0 : start = started;
  
    const copy = [...arr];
  
    // let middle = Number((arr.length/2).toFixed())-1
    let middle = Math.ceil(arr.length/2)-1
  
    if(copy[middle] > target){
      let slicearr = copy.slice(0,middle)
      return binarySearch(slicearr,target,start)
    }
    else if(copy[middle] < target){
      let slicearr = copy.slice(middle,end)
     return binarySearch(slicearr,target,middle+start)
    }
    else if(copy[middle]  === target){
      return start+middle
    }
  };

```
전체 탐색을 할 겨우 풀이:
```js
function usuallySearch(arr, target){
    const copy = [...arr];
    for(let i=0; i<copy.length; i++){
        if(arr[i] === target){
            return i
        }
    }

}
```

시간비교

<img width="229" alt="스크린샷 2022-02-03 오후 10 43 37" src="https://user-images.githubusercontent.com/89199949/152379820-ae5772b4-04f9-4c09-b54b-8c3facc869e1.png">

<img width="229" alt="스크린샷 2022-02-03 오후 10 43 45" src="https://user-images.githubusercontent.com/89199949/152379830-62d14b9a-2c01-44bc-b772-992a3fa65451.png">

- 시간이 절약이 되는것을 확인 하였고 자세한 시간은 구동환경에따라 상이 할 수 있다.

