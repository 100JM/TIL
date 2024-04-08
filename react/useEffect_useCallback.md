React - useEffect & useCallback
========

useEffct
---------
컴포넌트의 Lifecycle을 3가지로 분류해보자.   
1. 컴포넌트 마운트
2. 컴포넌트 업데이트(리렌더링)
3. 컴포넌트 언마운트
   
useEffect는 이러한 생명주기 사이사이에 간섭을 줄 수 있는 Hook이다.   

### useEffect 형태
useEffect는 실행할 함수코드 & 의존성 배열, 2가지의 인수를 받으며 컴포넌트가 렌더링 된 후에 실행된다.   

1. 기본
```jsx
import React, { useEffect } from 'react';

function App() {
  useEffect(() => {
    console.log('I am useEffect');
  })

  return (
    // 컴포넌트
  )
}
```

의존성 배열이 없는 경우 컴포넌트가 랜더링 될 때마다 side effect가 실행된다.

2. 빈 의존성 배열
```jsx
import React, { useEffect } from 'react';

function App() {
  useEffect(() => {
    console.log('I am useEffect');
  }, [])

  return (
    // 컴포넌트
  )
}
```

비어있는 의존성 배열이 있을 경우 컴포넌트가 마운트 될 때 한번만 실행된다.

3. 값이 있는 의존성 배열
```jsx
import React, { useEffect } from 'react';

function App() {
  useEffect(() => {
    console.log('I am useEffect');
  }, [dependency])

  return (
    // 컴포넌트
  )
}
```

배열 내의 값이 변경될 때마다 실행된다.   
의존성 값이 state라면 당연히 컴포넌트도 다시 렌더링된다.

### clean up
useEffect에 return문으로 함수를 추가하여 clean up 함수를 추가할 수 있다.   
이는 메모리 정리 및 오류를 방지하는데 도움이 된다.
```jsx
import React, { useEffect } from 'react';

function App() {
  useEffect(() => {
    const timer = setInterval(() => {
      console.log('timer');
    }, 1000);

    return () => {
      clearInterval(timer);
    }
  }, [dependency])

  return (
    // 컴포넌트
  )
}
```

useEffect의 return문, 즉 clean up function은 두 가지 경우에 실행된다.   
1. 컴포넌트 언마운트
   - 컴포넌트가 DOM에서 제거될 때 실행되어 메모리 누수를 방지하고 컴포넌트 리소스를 정리할 수 있다.
2. side effect 실행 전
   - 의존성 배열에 있는 값이 변경되어 side effect가 다시 실행되기 전에 이전 side effect의 효과를 정리한다.
   
useCallback
-----------
자바스크립트의 함수는 객체의 한 종류이다.   
```javascript
const consoleFunction = (str) => {
   console.log(str);
}
```
위 코드를 보면 consoleFunction 변수에 함수 객체가 할당되어 있다.   
이는 리액트에서 컴포넌트가 다시 렌더링된다면 완전히 새로운 함수가 생성됨을 의미한다.   
말했듯이 **자바스크립트에서 함수는 객체** 이기 때문이다.   
같은 모양과 같은 값이더라도 자바스크립트의 객체는 이를 동일하다고 여기지 않는다.   
결국 불필요한 렌더링이 발생할 수 있는 상황이 생기는 것이다.  
또한 함수를 useEffect같은 훅에서 의존성으로 추가한다면 상황에따라 무한루프를 유발할 위험도 있으며 최적화면에서도 좋지 않을거라 보인다.

useCallback은 함수를 재사용하여 이러한 점들을 개선할 수 있게 해주고 컴포넌트 성능을 최적화 시켜주는 Hook이다.   
1. 이벤트 핸들러 함수의 잦은 재생성
2. 하위 컴포넌트에 props로 전달되는 함수의 잦은 재생성
3. 렌더링 최적화가 필요한 경우

### useCallback 사용
useCallback도 useEffect와 같이 2개의 인자를 받는다.
```jsx
import React, { useEffect, useCallback } from 'react';

function App() {

   const consoleFunction = useCallback(() => { console.log('useCallback') }, [dependency]);

   return (
      // 컴포넌트
   )
}
```

consoleFunction 안에있는 함수는 App 컴포넌트가 렌더링 될 때 만들어져 해당 함수의 주소가 들어간다.   
그 다음 렌더링부터는 함수를 재생성하는 것이 아니라 기억된 주소를 가지고 재사용하는 것이다.   
만약 의존성 배열안에 값이 있다면 해당 값이 변경될때만 안에있는 함수를 재생성하게 된다.
