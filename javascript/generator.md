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

**진행중**