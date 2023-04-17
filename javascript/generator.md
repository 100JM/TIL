Generator
=============

### Generator란?
**Generator**는 함수의 실행을 중간에 멈췄다가 재개할 수 있는 기능이다.   
function 옆에 *을 넣어서 만들고 내부에 **yield** 키워드를 사용하며 이를 이용해 함수의 실행을 멈춘다.   
**Generator** 함수를 실행하면 **Generator**객체가 반환되며 **next**, **return**, **throw** 메서드를 가지고있다.
```javascript
function* fn() {
    yield 1;
    yield 2;
    yield 3;
    return 'end';
}

const gFn = fn();
```

### next()
**next**를 호출하면 가장 가까운 **yield**문을 만날때까지 실행하고 데이터 객체를 반환한다.   
반환되는 데이터 객체로는 value와 done을 갖으며 value는 **yield** 오른쪽에 있는 값이고 생략한다면 **undefined**이다.    
done은 함수코드가 끝났는 지를 나타낸다.
```javascript
function* fn() {
    console.log('Tom');
    yield 'Holland';

    console.log('Petter');
    console.log('Parker');
    yield 'Spider-Man';

    return 'end';
};

const gFn = fn();

gFn.next();
// 'Tom'
// {value: 'Holland', done: false}

gFn.next();
// 'Petter'
// 'Parker'
// {value: 'Spider-Man', done: false}

gFn.next();
// {value: 'end', done: true}
```

### return() / throw()
**return**을 호출하면 그 즉시 done속성 값이 true가 된다.
```javascript
function* fn() {
    console.log('Tom');
    yield 'Holland';

    console.log('Petter');
    console.log('Parker');
    yield 'Spider-Man';

    return 'end';
};

const gFn = fn();

gFn.return('finish');
// {value: 'finish', done: true}
```

**throw**도 마찬가지로 done을 true로 바꾸며 catch문을 실행한다.
```javascript
function* fn() {
    try{
        console.log('Tom');
        yield 'Holland';

        console.log('Petter');
        console.log('Parker');
        yield 'Spider-Man';

        return 'end';
    }catch(e){
        console.log(e);
    }
};

const gFn = fn();

gFn.throw(new Error('Err...'));
// 49037:1 Uncaught Error: Err... at <anonymous>:18:11
```

### Generator === iterable
**iterable**이란 반복이 가능하다는 뜻으로 몇가지 조건이 있다.   
- **Symbol.iterator** 메소드가 구현되어있어야 하며 이 메소드를 호출한 결과를 **iterator**라고한다.   
- **iterator**는 value와 done 속성을 반환하는 **next**메서드를 가진다.   
배열 또한 **iterable**하다고 볼 수 있다.
```javascript
const arr = [1,2,3];
const it = arr[Symbol.iterator]();

it.next();
// {value: 1, done: false}

it.next();
// {value: 2, done: false}

it.next();
// {value: 3, done: false}

it.next();
// {value: undefined, done: true}
```

**Generator**는 **iterable**객체이며 **iterable**은 **for of**를 통해 순회할 수 있다.
```javascript
function* fn(){
    yield 1;
    yield 2;
    yield 3;
};

const it = fn();

/*Generator에서 Symbol.iterator를 실행한 값이 자기 자신이다.*/
it === it[Symbol.iterator](); //true

for(let i of it) {
    console.log(i);
};
// 1, 2, 3

/*문자열도 가능할까?*/
const name = 'Tom';
const n = name[Symbol.iterator]();

for(let i of n) {
    console.log(i);
};
// 'T', 'o', 'm'
```

### next()에 인수 전달
```javascript
function* add() {
    const num1 = yield '첫 번째를 숫자 입력하세요';
    console.log(num1);

    const num2 = yield '두 번째를 숫자 입력하세요';
    console.log(num2);

    return num1 + num2;
};

const fn = add();

fn.next();
// {value: '첫 번째를 숫자 입력하세요', done: false}

fn.next(1);
// 1
// {value: '두 번째를 숫자 입력하세요', done: false}

fn.next(2);
// 2
// {value: 3, done: true}
```

### Generator는 값을 미리 만들어 두지 않는다.
**Generator**는 필요할 때만 값을 연산해주기 때문에 아래와 같은 무한반복자를 만들어 사용해도 브라우저가 뻗지 않는다.
```javascript
function* fn(){
    let num = 0;
    while(true){
        yield num++;
    }
};

const a = fn();

a.next(); // {value: 0, done: false}
a.next(); // {value: 1, done: false}
a.next(); // {value: 2, done: false}
```

### yield*
**yield** 옆에 *을 붙혀 반복가능한 다른 객체를 불러올 수 있다.
```javascript
function* gen1() {
    yield 'T';
    yield 'o';
    yield 'm';
};

function* gen2() {
    yield 'My name is';
    yield* gen1();
};

/*구조분해할당을 사용하면 for of와 마찬가지로 done이 true가 될때까지 값을 펼쳐주는 역할을 한다.*/
console.log(...gen2());
// My name is T o m
```

**Generator**는 다른 작업을 하다가 다시 돌아와서 **next**를 해주면 진행이 멈췄던 부분부터 이어서 실행할 수 있다는 장점이 있다.