생성자 함수
=============
### 1. 생성자 함수
**객체를 생성하는 역할을 하는 함수를 생성자 함수라고 한다.**
```javascript
function User(firstName, lastName){
    this.firstName = firstName;
    this.lastName = lastName;
}
// 생성자 함수는 붕어빵틀 이라고 생각하면 이해가 쉽다

let user1 = new User('Tom', 'Holland'); // User {firstName: 'Tom', lastName: 'Holland'}
let user2 = new User('Spider', 'Man'); // User {firstName: 'Spider', lastName: 'Man'}
// 필요한 재료(firstName, lastName)를 넣어 만들어낸 객체는 붕어빵
```

### 2. 생성자 함수 동작원리
```javascript
function User(firstName, lastName){

    this = {}; // 2.빈 객체를 생성한 후 this에 할당

    this.firstName = firstName;
    this.lastName = lastName; // 3.this에 프로퍼티 추가

    return this; // 4.this를 반환
}

new User() // 1.생성자 함수 실행

//실제로 2, 4번은 코드에 존재하지 않지만 알고리즘이 실행해준다.
//생성자 함수는 첫 글자를 대문자로 하는 것이 관례이다.
```

**예시**
```javascript
function User(firstName, lastName){

    // this = {};

    this.firstName = firstName;
    this.lastName = lastName;
    this.sayMyName = function(){
        console.log(`My name is ${firstName} ${lastName}`)
    }
    // return this;
}

 let user = new User('Tom', 'Holland'); // User {firstName : 'Tom', lastName : 'Holland'. sayMyName : ƒ}
    // new 키워드를 사용하지 않으면 undefined, 즉 객체가 할당되지 않는다.
    
user.firstName // Tom
user.lastName // Holland
user.sayMyName(); // My name is Tom Holland
```