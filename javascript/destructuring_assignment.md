구조 분해 할당(Destructuring assignment)
=============

### 구조 분해 할당 ?
구조 분해 할당 구문은 배열이나 객체의 속성을 분해하여 그 값을 변수에 담을 수 있게 하는 표현식이다.   

### 배열 구조 분해
```javascript
let users = ['Tom', 'Petter', 'MJ'];

let [user1, user2, user3] = users;
// 아래와 같은 코드와 똑같은 의미이다.
// let user1 = users[0];
// let user2 = users[1];
// let user3 = users[2];

console.log(user1); // 'Tom'
console.log(user2); // 'Petter'
console.log(user3); // 'MJ;

let str = 'Tom-Petter-MJ';

let [user1, user2, user3] = str.split('-');

console.log(user1); // 'Tom'
console.log(user2); // 'Petter'
console.log(user3); // 'MJ;
```

### 배열 구조 분해 : 기본값
해당하는 값이 없을 경우 undefined가 할당되며 오류를 방지하기 위해 기본값을 설정할 수 있다.
```javascript
let [a, b, c] = [1,2]; // a = 1, b = 2, c = undefined

let [a=3, b=5, c=5] = [1,2];
console.log(a); // 1
console.log(b); // 2
console.log(c); // 5
/*값이 undefined일 경우만 기본값이 할당된다.*/
```

### 배열 구조 분해 : 일부 반환값 무시
공백과 쉼표를 이용해서 필요하지 않은 배열의 요소를 무시할 수 있다.
```javascript
let [user1, ,user2] = ['Tom', 'Holland', 'Petter'];

console.log(user1); // 'Tom'
console.log(user2); // 'Petter'
```

### 배열 구조 분해 : 바꿔치기
구조 분해를 통해 임의의 변수를 만들지 않고 요소들의 값을 서로 바꿀 수 있다.
```javascript
let a = 1;
let b = 2;
let c = a;
a = b;
b = c; 

/*위처럼 불필요한 임의의 변수를 만들지 않아도 된다.*/
[a, b] = [b, a];
```

### 객체 구조 분해
객체 또한 구조 분해 할당이 가능하다.
```javascript
let user = {name : 'Tom', age : 31};
let {name, age} = user;
// let name = user.name;
// let age = user.age;

console.log(name); // 'Tom'
console.log(age); // 31
```

변수명을 꼭 프로퍼티의 key값으로 사용해야 하는 것은 이니다.   
새로운 변수명으로 할당이 가능하다.
```javascript
let user = {name : 'Tom', age : 31};
let {name : userName, age : userAge} = user;

console.log(userName); // 'Tom'
console.log(userAge); // 31
```

기본값도 배열과 마찬가지로 할당 가능하며 undefined 일때만 기본값이 할당된다.
```javascript
let user = {name : 'Tom', age : 31};
let {name, age, gender = 'male'} = user;
// 'Tom', 31, 'male'

let info = {
    name : 'Petter',
    age : 31,
    job : 'Spider-Man'
}

let {name, age, job = 'Venom'} = info;
console.log(job); // Spider-Man
```