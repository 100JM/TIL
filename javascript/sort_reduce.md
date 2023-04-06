arr.sort() / arr.reduce()
=============

### arr.sort()
배열 재정렬, 배열 자체가 변경된다.
```javascript
let arr = [1,5,3,2,4];
let arr2 = ['A', 'D', 'C', 'B', 'E'];

arr.sort(); // [1, 2, 3, 4, 5]
arr2.sort(); // ['A', 'B', 'C', 'D', 'E']
```
주의 할 점으로 자바스크립트는 배열안에 있는 숫자들은 유니코드 문자로 취급하기 때문에 아래와 같은 문제가 생긴다.
```javascript
let arr = [13, 21, 5, 7];

arr.sort(); // [13, 21, 5, 7]
```
정확한 비교를 하기 위해 로직을 담은 함수를 인수로 넣자.
```javascript
let arr = [13, 21, 5, 7];

let newArr = arr.sort((a, b) => {
    return a - b;
    // a가 b보다 크면 양수 작으면 음수 같으면 0
    // 양수 : a > b
    // 음수 : b < a
    // 0 : a = b
    // 양수라면 b를 앞으로, 음수라면 a를 앞으로, 0이라면 아무일도 일어나지 않는다.
});

console.log(newArr); // [5, 7, 13, 21]
```

### arr.reduce()
배열의 요소들을 순회하며 반복적인 연산을 하는 메소드이다.   
인수로 함수를 받는다.   
(누적 계산값, 현재값) => {return 계산값};   
   
배열의 모든 수 합치기 예시
```javascript
/*forEach를 사용한다면?*/
let arr = [1,2,3,4,5];

let sum = 0;
arr.forEach((num) => {
    sum += num;
});

console.log(sum); // 15

/*reduce를 사용하기*/
const result = arr.reduce((prev, cur) => {
    // prev : 누적 값
    // cur : 현재 값
    return prev + cur;
    // prev(초기 값 0) + cur(배열의 첫 번째 요소 1) = 1
    // prev(누적 값 1) + cur(배열의 두 번째 요소 2) = 2
    // 이런식으로 배열의 요소를 순회
}, 0 /*초기 값*/);

console.log(result); // 15
```

**map**이나 **filter** 대신 **reduce**를 사용해보자.
```javascript
/*배열 요소 중 성인만 추출*/
let userList = [
    {name : 'Tom', age : 20},
    {name : 'Petter', age : 30},
    {name : 'Holland', age : 15},
    {name : 'Parker', age : 10}
]

let result = userList.reduce((prev, cur) => {
    if(cur.age > 19){
        prev.push(cur.name);
    }
    return prev;
}, []);

console.log(result); // ['Tom', 'Petter']
```

**배열을 컨트롤할 때 map, forEach, reduce 등 상황에 맞게 알맞는 메소드를 잘 활용하도록 노력하자.**