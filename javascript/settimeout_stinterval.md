setTimeout / setInterval
=============

### setTimeout
일정 시간이 지난 후 함수를 실행한다.
```javascript
function showName(){
    console.log('My name is Petter');
};

setTimeout(showName, 3000); // 1000 = 1초
// 3초뒤 'My name is Petter'
```
함수에 전달할 인수가 필요하다면 시간 뒤에 적어주면 된다.
```javascript
function showName(name){
    console.log(`My name is ${name}`);
};

setTimeout(showName, 3000, 'Petter');
```
**setTimeout**은 TIME ID를 반환하는데 이것을 이용하면 **cleatTimeout** 함수를 통해 예정된 스케줄을 취소할 수 있다.
```javascript
function showName(name){
    console.log(`My name is ${name}`);
};

const timeId = setTimeout(showName, 3000, 'Petter');

clearTimeout(timeId);
```

### setInterval
일정 시간 간격으로 함수를 반복한다.
```javascript
function showName(name){
    console.log(`My name is ${name}`);
};

setInterval(showName, 3000, 'Petter');
// 3초마다 'My name is Petter' 반복
```
중간에 중단하고 싶다면 **clearInterval**을 사용하면 된다.
```javascript
let num = 1;

function count5(){
    console.log(`${num++}초가 지났습니다.`);

    if(num > 5){
        clearInterval(timeId);
    }
}

let timeId = setInterval(count5, 1000);
```

주의할 점으론 딜레이를 0으로 설정해도 바로 실행되지 않는다.
```javascript
setTimeout(function(){
    console.log(1);
}, 0);

console.log(2);
// 1이 아닌 2가 먼저 찍힌다.
// 2
// 1
```
이유는 현재 진행중인 스크립트가 종료된 이후 스케줄링 함수를 실행하기 때문이다.   
또한 브라우저는 기본적으로 4ms 혹은 그이상의 대기시간이 있다.