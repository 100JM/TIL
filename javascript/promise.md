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
        console.log(result);
    },
    function(err){ // 거부 되었을때
        console.log(err);
    }
);
```
   
**then** 이외에 사용할 수 있는것은 **catch**와 **finally**이다.   
**catch**는 **reject**인 경우에만 실행된다.   
**catch**문을 사용하면 가독성도 더 좋고 첫 번째 함수를 실행했을때 나오는 error를 잡아줄 수 도 있기때문에 사용하는 것이 더좋다.   
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