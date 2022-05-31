- this
this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수다.

this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를
참조할 수 있다.

- 함수를 호출하면 arguments 객체와 this가 암묵적으로 함수 내부에 전달된다.
이때 this를 지역 변수처럼 사용할 수 있다.
단, this가 가리키는 값은 함수 호출 방식에 의해 동적으로 결정된다.
메서드 내에서 정의한 중첩 함수도 일반 함수로 호출되면 중첩 함수 내부의 this에는 전역 개체가 바인딩 된다.

```
global.value = 1;

const obj = {
  value: 100,
  foo: function () {
    console.log(this.value); // 100

    function bar() {
      console.log(this.value); // 1
    }
    bar();
  },
};

obj.foo();
```
