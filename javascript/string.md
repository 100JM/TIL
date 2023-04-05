String
=============
### '' / "" / 벡틱(`)
**''** \(작은따옴표)는 html 코드를 작성하는데 용이하다.
```javascript
let html = '<div class="title">title</div>';
``` 
html 코드에 class와 같은 부분에 **""** \(큰따옴표)로 된 내용이 주로 들어가기 때문   
   
**""** \(큰따옴표)는 영어 문장을 작성하는데 좋다.
```javascript
let time = "It's a 5 o'clock.";
```
영어 문법상 **''** \(작은따옴표)가 자주 쓰이기 때문   

**벡틱** \(`)은 그냥 최고다.   
\${}로 변수를 표현하거나 표현식을 쓸 수 있어 훨씬 코드가 간결해진다.   
```javascript
let name = 'Tom Holland';
let intro = `My name is ${name}.` // 'My name is Tom Holland'
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

### length : 문자열 길이
배열의 길이를 구하는 것과 같이 문자열의 길이를 구할 수 있다.   
또한 문자열도 \[숫자]로 특정 위치에 접근이 가능하다.   
하지만 배열과 다르게 한 문자만 바꾸는 것은 허용되지 않는다.
```javascript
let name = 'Tom Holland';

name.length; // 11
name[0]; // 'T'

name[0] = 'B';
console.log(name); // 'Tom Holland'
```

### toUpperCase() / toLowerCase()
문자가 영어일 경우 대소문자 변환이 가능하다.
```javascript
let intro  = 'Hi my name is Tom Holland';

intro.toUpperCase(); // 'HI MY NAME IS TOM HOLLAND'
intro.toLowerCase(); // 'hi my name is tom holland'

let name = '피터 Parker';

name.toUpperCase(); // '피터 PARKER'
```

### indexOf(text)
문자를 인수로 받아 해당 위치를 반환한다.   
문자가 여러 개일 경우 첫 번째 문자의 위치만 반환하며 문자가 존재하지 않을 경우 -1을 반환한다.  
주의할 점으로 대소문자를 구분하기 때문에 구분 없이 찾고 싶다면 **toUpperCase** 혹은 **toLowerCase**를 활용하자.
```javascript
let job = 'Spider-Man';

job.indexOf('Man'); // 7
job.indexOf('man'); // -1
job.toLowerCase().indexOf('man'); // 7
```

### str.slice(n, m)
**slice**는 n\(시작점)부터 m까지\(포함하지 않음) 문자를 반환한다.   
m\(두 번째 인자)가 없으면 문자열 끝까지, 음수이면 끝에서부터 세어 반환한다.
```javascript
let text = 'abcdefg';

text.slice(2); // 'cdefg'
text.slice(0,5); // 'abcde'
text.slice(2,-2); // 'cde'
```

### str.substring(n, m)
**substring**은 n과 m사이에 위치하고 있는 문자를 반환한다.   
n과 m이 바뀌어도 동작하며 음수는 허용하지 않는다.\(0으로 인식)   
```javascript
let text = 'abcdefg';

text.substring(2, 5); // 'cde'
text.substring(5, 2); // 'cde'
```

### str.substr(n, m)
**substr**은 n부터 m개를 반환한다.   
```javascript
let text = 'abcdefg';

text.substr(2, 5); // 'cdefg'
text.substring(-5, 2); // 'cd'
```

### str.trim()
**trim**은 앞뒤 공백을 제거해준다.   
의도적으로 앞뒤에 공백을 넣는 경우는 거의 없기 때문에 보통 사용자로부터 뭔가를\(검색어..등) 입력 받을 때 사용한다.
```javascript
let coding = ' coding is fun ';

coding.trim(); // 'coding is fun'
```

**진행중...!**