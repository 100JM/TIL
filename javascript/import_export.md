import & export
=============

script 태그에 type="module"로 설정하면 해당 파일은 모듈로서 동작하게된다.
```html
<script src="app.js" type="module">
```

### 모듈이란?
JavaScript 코드를 담고 있는 파일이다.   
다만 일반적인 JavaScript 파일과는 다른 차이점을 가지고 있다.
- import 혹은 export 구문을 사용할 수 있다.
- 별다른 처리를 해주지 않아도 엄격 모드로 동작한다.
- 모듈의 가장 바깥쪽에서 선언된 이름은 전역 스코프가 아니라 **모듈 스코프**에서 선언된다.

### 모듈 스코프
모듈 내부의 가장 바깥 스코프에서 이름을 선언하더라도, 전역 스코프가 아니라 모듈 스코프에서 선언된다.   
모듈 스코프에 선언된 이름은 export 해주지 않는다면 해당 모듈 내부에서만 접근할 수 있다.   
```javascript
// util.js
let apiKey = 'Is api key';

// app.js
import {apiKey} from './util.js';

console.log(apiKey); // undefined
```

### import & export
모듈 스코프에서 정의된 이름은 export 구문을 통해 다른 파일에서 사용할 수있다.   
단순히 값을 저장하고 있는 변수뿐만 아니라, 함수나 클래스도 export를 통해 여러 모듈에서 재사용할 수 있다.   
```javascript
// util.js
let apiKey = 'Is api key';
function add(x, y) {
    return x+y;
}

export {apiKey, add};
```

```javascript
// app.js
import {aptKey, add} from './util.js';

console.log(apiKey); // Is api key
console.log(add(1, 2)); // 3
```

- 선언과 동시에 export
```javascript
export let name = 'Tom';
export let job = 'Spider-Man';
```

- default export   
export default 구문을 통해 모듈을 대표하는 하나의 값을 지정하고 그 값을 불러와 사용할 수 있다.
```javascript
// util.js
function add(x, y) {
  return x + y;
}

export let name = 'Tom';

export default add;
```

```javascript
// app.js
import add from './util.js';

console.log(add(1, 2)); // 3
```

- 다른 이름으로 import & export 하기   
default export와 일반적인 export를 동시에 가져올 수 있으며 이름뒤에 as를 붙혀서 다른 이름으로 사용할 수도 있다.
```javascript
// app.js
import add, {name as myName} from './util.js';

console.log(add(1, 2)); // 3
console.log(myName); // Tom
```