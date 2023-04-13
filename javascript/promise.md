Promise
=============

### Promise란 ?
**Promise**는 자바스크립트 비동기 처리에 사용되는 객체다.   
여기서 자바스크립트의 비동기 처리란 **특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 자바스크립트의 특성**을 의미한다.
```javascript
const pr = new Promise((resolve, reject) => {
    // code
})
```
**new Promise**로 생성하며 인수로 함수를 전달 받는데 **resolve**는 성공, **reject**는 실패했을 때 실행되는 함수다.   
이렇게 어떠한 작업이 완료되고 실행되는 함수를 **callback**함수라고 한다.

### Promise의 3가지 상태(states)
**Promise**의 상태란 처리 과정을 의미한다.   
**Promise**를 생성하고 종료될 때까지 3가지 상태를 갖는다.   
- Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태로 result는 undefined이다.
- Fulfilled(이행) : 비동기 처리가 완료되어 resolve를 호출하면 Fulfilled가 된다. 이때 result는 resolve 함수로 전달된 값이다.
- Rejected(실패) : 비동기 처리가 실패하면 즉 reject가 호출되면 Rejected가 되며 result는 reject로 전달된 error이다.

### then / catch / finally
**then**을 이용하여 resolve와 reject를 처리할 수 있다.
```javascript
const pr = new Promise((resolve, reject) => {

    let isTrue = true;

    setTimeout(() => {
        if(isTrue){

            resolve('success');
        }else{
            reject('fail');
        }
    }, 3000)
});

pr.then(
    function(result){ // 이행 되었을때
        console.log(result); // 'success'
    },
    function(err){ // 거부 되었을때
        console.log(err); // 'fail'
    }
);
```
   
**then** 이외에 사용할 수 있는것은 **catch**와 **finally**이다.   
**catch**는 reject인 경우에만 실행된다.   
**catch**문을 사용하면 가독성도 더 좋고 첫 번째 함수를 실행했을때 나오는 error를 잡아줄 수 도 있기때문에 사용하는 것이 더 좋다.   
```javascript
pr.then(
    function(result){ 
        console.log(result);
    }
).catch(
    function(err){
        console.log(err);
    };
);
```
   
**finally**는 이행이든 거부든 처리가 완료되면 항상 실행된다.   
로딩 화면 같은 것을 없앨 때 유용하다.
```javascript
pr.then(
    function(result){ 
        console.log(result);
    }
).catch(
    function(err){
        console.log(err);
    }
).finally(
    function(){
        console.log('end');
    }
);
// 'success'
// 'end'
```

### callback hell에서 벗어나기
아래와 같이 1,2,3번 함수를 실행하는 로직을 **Promise**를 사용하지 않고 구현 한다면 로직이 추가될수록 뎁스가 깊어지면서 callback hell, 콜백 지옥에 빠지게 된다.
```javascript
const fn1 = (callback) => {
    setTimeout(() => {
        console.log('1번 함수 실행');
        callback();
    }, 3000)
};

const fn2 = (callback) => {
    setTimeout(() => {
        console.log('2번 함수 실행');
        callback();
    }, 6000)
};

const fn3 = (callback) => {
    setTimeout(() => {
        console.log('3번 함수 실행');
        callback();
    }, 2000)
};



console.log('start');
console.time('time-check');

fn1(function(){
    fn2(function(){
        fn3(function(){
            console.log('end');
            console.timeEnd('time-check');
        })
    })
});
// start, 1번 함수 실행, 2번 함수 실행, 3번 함수 실행, end
// time-check: 11027.3369140625 ms
```
**callback**함수가 아닌 **Promise**를 사용하여 구현해보자.   
아래와 같이 **Promise**들이 연결되는 것을 **Promise chaining**이라 한다.
```javascript
const fn1 = () => {
    return new Promise((res, rej) => {
        setTimeout(() => {
            res('1번 함수 실행');
        },3000);
    });
};

const fn2 = (msg) => {
    console.log(msg);
    return new Promise((res, rej) => {
        setTimeout(() => {
            res('2번 함수 실행');
        },6000);
    });
};

const fn3 = (msg) => {
    console.log(msg);
    return new Promise((res, rej) => {
        setTimeout(() => {
            res('3번 함수 실행');
        },2000);
    });
};

console.log('start');
console.time('time-check');

fn1()
    .then((result) => fn2(result))
    .then((result) => fn3(result))
    .then((result) => console.log(result))
    .catch((err) => console.log(err))
    .finally(() => {
        console.log('end');
        console.timeEnd('time-check');
    });
// start, 1번 함수 실행, 2번 함수 실행, 3번 함수 실행, end
// time-check: 11042.4560546875 ms
```