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