Object - methods / Computed property
=============
### 1. Computed property(계산된 프로퍼티)   
객체를 선언하는 순간에도 변수를 활용하여 프로퍼티를 할당할 수 있다.   
```javascript
let a = 'lastName';

const user = {
    firstName : 'Tom',
    [a] : 'Holland' // lastName : 'Holland'
    //대괄호로 묶어 위와 같이 표시하면 문자열 'a'가 아닌 변수 a에 할당된 값이 들어간다.
    //이를 computed property(계산된 프로퍼티)라 부른다.
}
```

식 자체를 넣는 것도 가능하다.
```javascript
let a = 'my'

const user = {
    [31 + 1] : 32,
    [a + 'name'] : 'Spider-Man'
}
// user {32: 32, myname: 'Spider-Man'}
```

### 2. Object - methods(객체에서 사용할 수 있는 메소드)
#### 2-1 Object.assign() : 객체 복제   
```javascript
const user = {
    name : 'Petter',
    job : 'Spider-Man'
}

const newUser = user; // 복제 X
```
위와 같은 방법으로 복제가 될까?   
정답은 아니다.   
user 변수에는 객체 자체가 들어가 있는 것이 아니라 객체가 저장되어 있는 메모리의 주소인 객체에 의한 참조값이 저장된다.   
때문에 객체가 복제되는 것이 아니라 같은 객체에 접근하게 되어 newUser에서 name값을 바꾸면 user의 name값도 바뀌게된다.   
그렇다면 어떻게 할까?   
**Object.assign()** 메소드를 사용하자.   
```javascript
const newUser = Object.assign({}, user);

{} + {name : 'Petter', job : 'Spider-Man'}
// 첫번째 인자값 객체에 두번째부터 들어오는 객체들이 병합되어 객체가 복제된다.
```
**예시**   
```javascript
const newUser = Object.assign({mind : 'friendly neighborhood'}, user);
// newUser {mind: 'friendly neighborhood', name: 'Petter', job: 'Spider-Man'}

/*만약 병합을 하는데 key가 같다면 덮어쓰게 된다.*/
const newUser = Object.assign({name : 'Tom'}, user);
// newUser {name: 'Petter', job: 'Spider-Man'}

/*2개 이상의 객체도 병합할 수 있다.*/
const user = {
    mind : 'friendly neighborhood'
}
const info1 = {
    name : 'Petter'
}
const info2 = {
    job : 'Spider-Man'
}

Object.assign(user, info1, info2);
// {mind: 'friendly neighborhood', name: 'Petter', job: 'Spider-Man'}
```
**진행중...**