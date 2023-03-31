변수 - hoisting, tdz, scope
=============

### 1. 변수는 let, const, var 가 있다.

**var**는 한번 선언된 변수를 다시 선언할 수 있다.
```javascript
var name = 'Tom';
console.log(name); // Tom

var name = 'Holland';
console.log(name); // Holland
```

**let**은 재선언이 불가능하다.
```javascript
let name = 'Tom';
console.log(name); // Tom

let name = 'Holland';
console.log(name); // error !
```

**var**는 선언하기 전에 사용할 수 있다.
```javascript
console.log(name); // undefined
var name = 'Tom';
```
**why? var**로 선언한 변수는 실제로는 이동하지 않지만 최상위로 끌어올려진 것처럼 동작(호이스팅 Hoisting)하기 때문이다.   
*호이스팅(Hoisting) : 스코프 내부 어디서든 변수 선언은 최상위에 선언된 것 처럼 행동*   
*선언은 호이스팅 되지만 할당은 그렇지 않아 undefined로 찍힌다*   
```javascript
var name;
console.log(name); // undefined
name = 'Tom';
```

**let**의 경우엔 error가 발생한다.
```javascript
console.log(name); // ReferenceError !
let name = 'Holland';
```
그렇다고 **let**이 호이스팅 되지 않는 것은 아니다.   
**let, const**는 **Temporal Dead Zone(TDZ)**의 영향을 받기 때문이다.   
```javascript
console.log(name); // TDZ
const name = 'Spider-Man'; // 선언 및 할당
console.log(name); // 사용 가능
```
이는 코드를 예측 가능하게 하고 전제적인 버그를 줄일 수 있다.

### 2. 변수의 생성과정

**선언 단계 - 초기화 단계 - 할당 단계**

**var**는 선언과 초기화 단계가 동시에 진행된다.   
1.선언 및 초기화 단계   
2.할당 단계   
*초기화 : undefined를 할당 해주는 단계*   

**let**은 선언과 초기화 단계가 분리되어 진행된다.   
1.선언 단계 - 호이스팅되며 선언 단계가 진행   
2.초기화 단계 - 실제 코드에 도달했을때 진행   
3.할당 단계   

**const**는 선언과 할당이 동시에 되어야한다.   
1.선언 + 초기화 + 할당   

```javascript
var name;
name = 'Tom';

let name2;
name2 = 'Holland';

const name3;
name3 = 'Spider-Man'; // error !
```

### 3. 스코프

**var** : 함수 스코프(function-scoped)   
**let, const** : 블록 스코프(block-scoped) - 모든 코드블록에서 선언된 변수는 코드블록 내에서만 유요하며 외부에선 접근할 수 없다.   
즉 코드블록 내부에서 선언된 변수는 지역 변수다.   
*함수, if문, for문, while문, try/catch문 등*   

**var**는 if문 밖에서 사용이 가능하지만 **let, const**는 불가능하다.   
*var가 유일하게 벗어날 수 없는 스코프는 함수라고 생각하자*   
```javascript
const age = 31;
if(age > 29) {
    var im = 'old';
}
console.log(im); // old

function fullName(name, name2){
    var myName = name + name2;
}
fullName('Tom', 'Holland');
console.log(myName); // ReferenceError !
```
