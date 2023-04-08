나머지 매개변수(Rest parameters) / 전개 구문(Spread syntax)
=============

### 나머지 매개변수 : Rest Parameters
함수에서 매개변수를 얻는 법은 2가지가 있다.   
첫 번째로는 **arguments**가 있고 두 번째로는 **나머지 매개변수\(...)**다.   
**arguments**란?   
함수내에서 이용 가능한 지역변수로 함수로 넘어온 모든 인수에 접근할 수 있다.   
length와 index를 가지고있어 배열로 생각할 수 있지만 배열 형태의 객체이므로 배열 내장 메소드는 사용이 불가능하다.
```javascript
function myName(name){
    console.log(name);
    console.log(arguments.length);
    console.log(arguments[0]);
    console.log(arguments[1]);
};

myName('Tom', 'Petter');
// 'Tom'
// 2
// 'Tom'
// 'Petter'
```
**ES6**를 사용할 수 있는 환경이라면 가급적 더 편리한 **나머지 매개변수**를 사용하는걸 권장한다.   
**나머지 매개변수** 점 3개를 찍고 배열 이름을 정하여 개수가 정해지지 않은 인수를 배열로 표현할 수 있다.   
인수로 아무것도 전달하지 않으면 undefined가 아닌 빈 배열이 나타단다.   
```javascript
let myName = (...name) => {
    console.log(name);
};

myName(); // []
myName('Tom'); // ['Tom']
myName('Tom', 'Petter'); // ['Tom', 'Petter']
```

**나머지 매개변수**는 **forEach**나 **reduce**같은 배열 메소드를 사용할 수 있다.
```javascript
/*전달 받는 인수를 모두 더하라*/

function addForEach(...num){
    let result = 0;
    num.forEach((n) => {
        result += n;
    });

    return result;
}

function addReduce(...num){
    let result = num.reduce((prev, cur) => prev + cur);
    console.log(result);
}

addForEach(1,2,3); // 6
addReduce(1,2,3) // 6
```

**나머지 매개변수**를 사용하여 생성자 함수 만들기.
```javascript
function User(name, age, ...skills){
    this.name = name;
    this.age = age;
    this.skills = skills;
}

let user1 = new User('Tom', 31, 'html', 'css');
let user2 = new User('Petter', 29, 'js', 'react');

console.log(user1);
// {name: 'Tom', age: 31, skills: Array(2)}
// user1.skills ['html', 'css']

console.log(user2);
// {name: 'Petter', age: 29, skills: Array(2)}
// user2.skills ['js', 'react']
```
주의할 점으로 **나머지 매겨변수**는 항상 인수들 중 마지막에 위차할 것 !   

### 전개 구문(Spread syntax) : 배열
```javascript
let arr1 = [1,2,3];
let arr2 = [4,5,6];

let result1 = [...arr1, ...arr2]; // [1, 2, 3, 4, 5, 6]
let result2 = [0, ...arr1, ...arr2, 7,8,9]; // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] 

/*arr,push(), arr.splice(), arr.concat() 등을 사용하지 않고도 편하게 작업할 수 있다.*/
```

### 전개 구문(Spread syntax) : 객체
```javascript
let user = {name : 'Tom'};

let newUser = {...user, age : 31}; // {name: 'Tom', age: 31}
```

### 전개 구문(Spread syntax) : 복제
**Object.assign()**울 사용하지 않고 간단하게 복제가 가능하다.
```javascript
let arr = [1,2,3];
let newArr = [...arr]; // [1,2,3]

let user = {name : 'Petter', age : 29};
let newUser = {...user}; // {name : 'Petter', age : 29}

/*Object.assign()을 사용한 것처럼 별개의 객체로 복제가 된다.*/
newUser.name = 'Tom';
console.log(user.name); // Petter
console.log(newUser.name); // Tom
```

**전개 구문** 예시
```javascript
/*arr1을 [4, 5, 6, 1, 2, 3] 으로 만들기*/
let arr1 = [1,2,3];
let arr2 = [4,5,6];

// 전개 구문 X
arr2.reverse().forEach((num) => {
    arr1.unshift(num);
});

console.log(arr1); // [4, 5, 6, 1, 2, 3]

// 전개 구문 사용
arr1 = [...arr2, ...arr1];

console.log(arr1); // [4, 5, 6, 1, 2, 3]


/*Object.assign()*/
let user = {name : 'Tom'};
let info = {age : 31};
let fe = ['js', 'react'];
let lan = ['Korean', 'English'];

// 전개 구문 X
let result = Object.assign(
    {}, 
    user, 
    info, 
    {
        skills : []
    }
);

fe.forEach((f) => {
    result.skills.push(f);
});

lan.forEach((l) => {
    result.skills.push(l);
});

console.log(result);
/*
{ 
    name : 'Tom',
    age : 31,
    skills : ['js', 'react', 'Korean', 'English']
}
*/

// 전개 구문 사용
let result = {
    ...user,
    ...info,
    skills : [...fe, ...lan]
};

console.log(result);
/*
{ 
    name : 'Tom',
    age : 31,
    skills : ['js', 'react', 'Korean', 'English']
}
*/
```
**전개 구문**을 사용하면 작업이 상당히 간단해진다.   
정말 편하다 !