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
// key가 심볼형인 프로퍼티들은 건너뛴다. 유일성 보장 !
```
즉 심볼은 특정 객체에 원본 데이터를 건드리지 않고 속성을 추가할 수 있다.
```javascript
const user = {
    name : 'Petter',
    job : 'Spider-Man',
}

const realName = Symbol('realName');
user[realName] = 'Tom';
// {name: 'Petter', job: 'Spider-Man', Symbol(realName): Symbol(realName)}

//다른사람이 만든 객체나 모르는 곳에서 keys, values, entries 같은 메소드가 실행되는 객체에 내가 원하는 속성을 추가할 수 있다.
```

**진행중...**