상속과 프로토타입
=============

객체에는 자신이 프로퍼티를 가지고 있는지 확인하는 **hasOwnProperty**라는 함수가 있다.
```javascript
const user = {
    name : 'Tom'
};

user.hasOwnProperty('name'); // true
user.hasOwnProperty('age'); // false
```
그렇다면 **hasOwnProperty** 함수는 어디에서 오는 걸까?   
바로 여기에 있다.   
<img src = "../img/prototype.png" width = "30%" height = "30%">
