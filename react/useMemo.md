# useMemo와 useCallback: React 성능 최적화 훅

React 애플리케이션의 성능을 최적화하기 위해 `useMemo`와 `useCallback` 훅을 사용하는 방법에 대해 알아보자.  
이 두 훅은 컴포넌트가 불필요하게 다시 렌더링되는 것을 방지해 성능을 향상시키는 데 중요한 역할을 한다.

---

## useMemo

`useMemo`는 메모이제이션된 값을 반환하는 훅이다. 
특정 값이 변경될 때까지 이전에 계산된 값을 재사용할 수 있게 하며, 이는 비용이 많이 드는 계산을 최적화하는 데 유용하다.

### 사용법

```javascript
import React, { useMemo } from 'react';

const MyComponent = ({ num }) => {
  const squaredNum = useMemo(() => {
    console.log('Calculating squared number...');
    return num * num;
  }, [num]);

  return <div>Squared Number: {squaredNum}</div>;
};
```
### 설명
- `useMemo`의 첫 번째 인자는 계산 함수.
- 두 번째 인자는 의존성 배열로, 이 배열의 값이 변경될 때만 계산 함수가 호출된다.
- 위 예제에서는 num이 변경될 때만 제곱 값이 다시 계산된다.

---

## useCallback
`useCallback`은 메모이제이션된 콜백 함수를 반환하는 훅이다. 
콜백 함수가 필요 없는 재생성을 방지하여, 자식 컴포넌트에 전달할 때 참조 동일성을 유지할 수 있다.

### 사용법

```javascript
import React, { useCallback } from 'react';

const MyComponent = ({ onClick }) => {
  return <button onClick={onClick}>Click Me</button>;
};

const ParentComponent = () => {
  const handleClick = useCallback(() => {
    console.log('Button clicked');
  }, []);

  return <MyComponent onClick={handleClick} />;
};

```
### 설명
- `useCallback`의 첫 번째 인자는 콜백 함수.
- 두 번째 인자는 의존성 배열로, 이 배열의 값이 변경될 때만 콜백 함수가 재생성된다.
- 위 예제에서는 의존성 배열이 비어 있어, `handleClick` 함수는 컴포넌트의 수명 동안 변경되지 않는다.

---

### useMemo와 useCallback의 차이점
|특정|useMemo|useCallback|
|:---|:---|:---|
|반환 값|메모이제이션된 값|메모이제이션된 함수|
|주 사용 사례|계산 비용이 높은 값을 메모이제이션하여 성능 최적화|동일한 함수 참조를 유지하여 불필요한 렌더링 방지|
|의존성 배열|값이 변경될 때까지 계산 함수를 재실행하지 않음|의존성이 변경되지 않는 한 함수 참조가 변경되지 않음|