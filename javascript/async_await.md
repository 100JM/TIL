async / await
=============

### async
**async**와 **await**을 사용하면 **Promise**에 then 메소드를 체인형식으로 호출하는 것보다 가독성이 좋아진다.   
함수 앞에 **async** 키워드를 붙혀주면 항상 **Promise**를 반환한다. 
```javascript
async function getName() {
    return 'Tom';
};

console.log(getName());
// Promise {<fulfilled>: 'Tom'}

async function getMyName() {
    return new Promise((res, rej) => {
        res('Petter');
    });
};

getMyName().then((name) => console.log(name)); // 'Petter'
```

### await
**await** 키워드는 **async** 함수 내부에서만 사용할 수 있다.   
**await** 옆에는 **Promise**가 오고 해당 **Promise**가 처리될 때 까지 기다린다.
```javascript
function getName(name) {
    return new Promise((res, rej) => {
        setTimeout(() => {
            res(name);
        }, 3000);
    });
};

async function showName() {
    const result = await getName('Petter');
    console.log(result);
};

showName();
// 3초뒤 'Petter'
```

**Promise**의 체인형식 then 메소드를 **async**, **await**으로 바꿔보자.   
예외처리에는 try /catch 문을 사용해주면 된다.
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
// fn1()
//     .then((result) => fn2(result))
//     .then((result) => fn3(result))
//     .then((result) => console.log(result))
//     .catch((err) => console.log(err))
//     .finally(() => {
//         console.log('end');
//         console.timeEnd('time-check');
//     });

async function start() {
    try {
        const result1 = await fn1();
        const result2 = await fn2(result1);
        const result3 = await fn3(result2);
        console.log(result3);
    } catch(err) {
        console.log(err);
    }

    console.log('end');
    console.timeEnd('time-check');
};

start();
// start, 1번 함수 실행, 2번 함수 실행, 3번 함수 실행, end
// time-check: 11024.880859375 ms
```

**promise.all** 또한 사용 가능하다.
```javascript
console.log('start');
console.time('time-check');

async function startAll() {
    try {
        const result = await Promise.all([fn1(), fn2(), fn3()]);
        console.log(result);
    } catch(err) {
        console.log(err);
    }

    console.log('end');
    console.timeEnd('time-check');
};

startAll();
// start, ['1번 함수 실행', '2번 함수 실행', '3번 함수 실행'], end
// time-check: 6006.072998046875 ms
```