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
arr.splice(n, 0, x)와 같이 두 번째 인자에 0을 넣으면 아무것도 삭제하지 않고 추가가 가능하다.
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

**진행중...!**