React - useEffect
---------

### useEffct
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
    console.log('I'm useEffect');
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
    console.log('I'm useEffect');
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
    console.log('I'm useEffect');
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
