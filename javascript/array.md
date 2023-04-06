Array
=============
### 배열의 기본 메소드
- push() : 뒤에 삽입
- pop() : 뒤에 삭제
- unshift() : 앞에 삽입
- shift() : 앞에 삭제

### arr.splice(n, m)
- 특정 요소 삭제 : n부터 m개
```javascript
let arr = [1,2,3,4,5];

arr.splice(1,2);
console.log(arr); // [1,4,5] 
```
- 특정 요소 삭제 후 추가   
세 번째 인자로 추가할 요소를 넣는다.
```javascript
let arr = [1,2,3,4,5];

arr.splice(1,2,'Spider-Man','Venom');
console.log(arr); // [1, 'Spider-Man', 'Venom', 4, 5] 
```
arr.splice(n, 0, x)와 같이 두 번째 인자에 0을 넣으면 아무것도 삭제하지 않고 추가 가능하다.
```javascript
let arr = ['나는','입니다.'];

arr.splice(1,0,'스파이더맨');
console.log(arr); // ['나는', '스파이더맨', '입니다.']
```
- 변수를 선언하면 삭제된 요소를 반환할 수 있다.
```javascript
let arr = [1,2,3,4,5];

let result = arr.splice(1,2);
console.log(result); // [2, 3]
```

### arr.slice(n, m)
n부터 m까지 반환, **String.slice**와 마찬가지로 m은 포함하지 않는다.   
괄호안에 아무것도 넣지 않으면 배열이 복사된다.
```javascript
let arr = [1,2,3,4,5];
arr.slice(1,4); // [2, 3, 4]

let arr2 = arr.slice();
console.log(arr2); // [1, 2, 3, 4, 5]
```

### arr.concat(arr2, arr3..)
배열을 합쳐서 새배열을 반환한다.   
배열이 아닌 각각의 데이터를 전달해도 배열로 합쳐진다.
```javascript
let arr = [1,2];

arr.concat([3,4]); // [1, 2, 3, 4]
arr.concat([3,4], 5, 6); // [1, 2, 3, 4, 5, 6]
```
### arr.forEach(fn) : 배열 반복
**forEach**는 함수를 인수로 받고 함수는 3개의 매개변수가 있는데 첫 번째는 해당 요소, 두 번째는 인덱스, 세 번째는 해당 배열 자체를 의미한다.   
```javascript
let user = ['Petter Parker', 'Spider-Man', 'Venom'];

user.forEach((name, i) => {
    console.log(`${i+1}. ${name}`);
});
// 1. Petter Parker
// 2. Spider-Man
// 3. Venom
```

### arr.indexOf() / lastIndexOf()
문자열의 **indexOf**와 마찬가지로 인자의 인덱스를 반환하며 없을 시 -1를 반환한다.   
두 번째 인자값을 넣으면 해당 위치에서부터 찾는다.   
뒤에서부터 찾고싶으면 **lastIndexOf**를 사용하면 된다.
```javascript
let arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'D'];

arr.indexOf('D'); // 3
arr.indexOf('D', 4); // 7
arr.lastIndexOf('D'); // 7
```

### arr.includes()
굳이 인덱스가 필요없고 포함하는지만 확인하려면 **includes**를 사용하는 것이 좋다.   
포함하면 true, 포함하지 않으면 false를 반환한다.
```javascript
let arr = [1,2,3];

arr.includes(1); // true
arr.includes(4); // false
```

 **진행중..**