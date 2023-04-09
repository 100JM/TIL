클로저(Closure)
=============

### 클로저란?
함수와 함수 렉시컬 환경의 조합.   
함수가 생성될 당시의 외부 변수를 기억하고 생성된 이후에도 계속 접근 할 수 있다.
```javascript
function makeAdd(x){
    return function(y){
        return x + y;
    }
};

let add1 = makeAdd(1);
console.log(add1(2)); // 3

let add5 = makeAdd(5);
console.log(add5(5)); // 10
console.log(add5(10)); // 15
```
add1과 add5 함수가 생성되면서 서로 다른 환경을 갖고 변수x를 기억하고있어 함수가 정상적으로 실행된다.\ (add1 = 1, add5 = 5)   

### 은닉화
함수 내부적으로 생성된 변수에는 직접적으로 접근을 할 수 없다.   
함수를 실행시켜 그 값을 변수에 담아 클로저를 생성함으로서 접근이 가능하다.   
즉 이러한 방식과 같이 직접적으로 변경되면 안되는 변수에 대한 접근을 막는 것을 은닉화라고한다.
```javascript
function countFunc(){
    let num = 0; // 은닉화

    return function(){
        return num++;
    }
};

let counter = countFunc();

console.log(counter()); // 0
console.log(counter()); // 1
console.log(counter()); // 2
```