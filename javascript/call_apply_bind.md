call / apply / bind
=============

### call
**call**메소드는 모든 함수에서 사용할 수 있으며 **this**를 특정값으로 지정할 수 있다.   
함수를 호출할 때 **call**을 사용하고  **this**로 사용할 객체를 넘기면 해당 함수가 주어진 객체의 메소드인것 처럼 사용할 수 있다.
```javascript
const user = {
    name : 'Tom'
};

function showName(){
    console.log(this.name);
};

showName(); // 여기서 this는 window
showName.call(user); // 'Tom'

function update(age, job){
    this.age = age;
    this.job = job;
};

update.call(user, 31, 'Spider-Man'); // {name: 'Tom', age: 31, job: 'Spider-Man'}
// 첫 번째 인수 : this로 사용될 값
// 두 번째, 세 번째 인수 : 함수가 사용할 매개변수
```

### apply
**apply**는 함수 매개변수를 처리하는 방법을 제와하면 **call**과 완전히 같다.   
**call**은 일반적인 함수와 마찬가지로 매개변수를 직접 받지만, **apply**는 매개변수를 **배열**로 받는다.
```javascript
const user = {
    name : 'Tom'
};

function update(age, job){
    this.age = age;
    this.job = job;
};

update.apply(user, [31, 'Spider-Man']); // {name: 'Tom', age: 31, job: 'Spider-Man'}
```
**apply**는 배열 요소를 함수 매개변수로 사용할 때 유용하다.
```javascript
const num = [1,2,3,4,5];

let maxNum = Math.max.apply(null, num); // 5
// let maxNum = Math.max(...num);
// let maxNum = Math.max.call(...num);
```

### bind
**bind**는 함수를 호출하는 것이 아닌 새로운 함수를 만들어 리턴 해준다.
```javascript
const user = {
    name : 'Petter',
    showName : function(){
        console.log(`Hi my name is ${this.name}`);
    }
};

let fn = user.showName;
fn(); // Hi my name is

let bindFn = user.showName.bind(user);
bindFn(); // Hi my name is Petter
// user.showName.call(user);
// user.showName.apply(user);
```
**react** 등의 프론트엔드에서 함수를 prop으로 전달하는 경우 **bind**를 사용하기도 한다.
```javascript
function showName(name){
    console.log(name);
};
<Component callback={() => showName('Petter');}>

<Component callback={showName.bind('Petter');}>
```
이처럼 함수와 인자를 모두 전달하기 위해 불필요한 함수를 추가하지 않아도 되어 편리하다.