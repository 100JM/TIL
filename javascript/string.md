String
=============
### '' / "" / 벡틱(`)
**''**(작은따옴표)는 html 코드를 작성하는데 용이하다.
```javascript
let html = '<div class="title">title</div>';
``` 
html 코드에 class와 같은 부분에 **""**(큰따옴표)로 된 내용이 주로 들어가기 때문   
**""**(큰따옴표)는 영어 문장을 작성하는데 좋다.
```javascript
let time = "It's a 5 o'clock.";
```
영어 문법상 **''**(작은따옴표)가 자주 쓰이기 때문   
**벡틱(`)**은 그냥 최고다.   
\${}로 변수를 표현하거나 표현식을 쓸 수 있어 훨씬 코드가 간결해진다.   
```javascript
let name = 'Tom Holland';
let intro = `My name is ${name}.` // My name is Tom Holland
let add = `2 더하기 3은 ${2+3}입니다.` // 2 더하기 3은 5입니다.
```
또한 여러줄을 포함 할 수 있다.
```javascript
let intro = `My job is
            Spider-Man.`;

// 백틱을 사용하지 않는다면?
let intro = "My job is\nSpider-Man.";

let intro = "My job is 
            Spider-man. // error
```
절대 벡틱써 !   

**진행중**