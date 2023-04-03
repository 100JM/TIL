심볼(Symbol)
=============
### 1. Symbol
**심볼은 유일한 식별자이다.**
```javascript
const a = Symbol(); // new를 붙히지 않는다.
const b = Symbol();

console.log(a); // Symbol()
console.log(b); // Symbol()

a === b; // false
a == b; // false
```

**심볼을 객체의 key로 사용하기**
```javascript
const id = Symbol('id');

const user = {
    name : 'Petter',
    job : 'Spider-Man',
    [id] : 'myId'
}
// {name: 'Petter', job: 'Spider-Man', Symbol(id): 'myId'}

Object.keys(user); // ['name', 'job']
Object.values(user); // ['Petter', 'Spider-Man']
Object.entries(user); // [Array(2), Array(2)]
/*key가 심볼형인 프로퍼티들은 건너뛴다. 유일성 보장 !*/
```
즉 심볼은 특정 객체에 원본 데이터를 건드리지 않고 속성을 추가할 수 있다.
```javascript
const user = {
    name : 'Petter',
    job : 'Spider-Man',
}

/*다른사람이 만든 객체나 모르는 곳에서 keys, values, entries 같은 메소드가 실행되는 객체에 내가 원하는 속성을 추가하여 숨길 수 있다.*/
const realName = Symbol('name');
user[realName] = 'Tom';
// {name: 'Petter', job: 'Spider-Man', Symbol(name): 'Tom'}

/*description으로 심볼을 생성할 때 지정한 이름을 알 수 있다.*/
realName.description; // 'Tom'
```

### 1-1 Symbol.for() : 전역 심볼
**하나**의 심볼만 보장받을 수 있다. 없으면 만들고, 있으면 가져오기 때문이다.   
Symbol 함수는 매번 다른 Symbol 값을 생성하지만, Symbol.for() 메소드는 하나를 생성한 뒤 키를 통해 같은 Symbol을 공유한다.
```javascript
const name1 = Symbol.for('Petter Parker');
const name2 = Symbol.for('Petter Parker');

name1 === name2; // true

/*Symbol.for()는 keyFor 메소드를 통해 지정한 이름을 가져올 수 있다.*/
Symbol.keyFor(name1); // 'Petter Parker'
```
### 1-2 숨겨진 Symbol key 보는 법
```javascript
const id = Symbol('id');

const user = {
    name : 'Petter',
    job : 'Spider-Man',
    [id] : 'myId'
}

Object.getOwnPropertySymbols(user); // [Symbol(id)]
Reflect.ownKeys(user); // ['name', 'job', Symbol(id)]
```

### 1-3 Symbol을 사용하는 간단한 상황 예시
```javascript
/*다른 개발자가 만든 객체*/
const user = {
     name : 'Petter Parker',
     job : 'Spider-man'
}

/*내가 작업*/
const myFunc = Symbol('myFunc');

user[myFunc] = function() {
    console.log('나만 보는 메세지');
}
 
/*사용자가 보는 메세지*/
for(let key in user){
    console.log(`His ${key} is ${user[key]}`);
}
// His name is Petter Parker
// His job is Spider-man
// 내가 추가한 심볼은 사용자에게 전혀 영향을 주지 않는다.

user[myFunc](); // 나만 보는 메세지
// 다른 사람이 작업한 객체의 프로퍼티를 덮어 쓸 일도 없어 원하는 속성을 추가하는데 용이하다 !
```