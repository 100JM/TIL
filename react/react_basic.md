React 핵심 - 컴포넌트, JSX, 속성, 상태 등
==========

### 컴포넌트
컴포넌트는 잠재적으로 재사용이 가능한 구성 요소로 리액트 개발자가 생성할 수 있고 차후에 혼합하여 전반적인 UI를 구축할 수 있다.   
결국 리액트 애플리케이션은 컴포넌트를 결합하여 만들어지는 것이다.   
컴포넌트는 HTML과 경우에 따라 CSS코드, 관련된 자바스크립트 로직 등을 감싼다고 볼 수 있다.   
이로 인해 복잡한 사용자 인터페이스를 관리하기 쉽도록 작게 분리하여 다른 위치에서도 사용할 수 있게 해준다.   
컴포넌트 접근 방식의 가장 큰 장점이다.   
- 재사용성
- 관심사의 분리 : 단일책임으로 복잡성↓, 가독성↑, 협업 & 오류 수정에 용이
- 리액트에서 컴포넌트로 인식되기 위해 함수의 이름이 대문자로 시작해야하며 렌더링 가능한 값이 반환 되어야한다.

### JSX
JSX는 JavaScript Syntax Extension, 즉 JavaScript 문법 확장자를 의미한다.   
이 확장자는 개발자가 자바스크립트 파일 내에 HTML 마크업 코드를 작성하여 HTML 요소를 설명하고 생성할 수 있게 해준다.   
JSX는 브라우저에는 사용할 수 없지만 브라우저에 도달하기 전에 개발 서버에서 변환되어 보다 편리하게 UI를 생성할 수 있다.   
- 반드시 부모 요소 하나가 감싸는 형태여야 한다.   
  → Virtual DOM에서 컴포넌트 변화를 감지할 때 효율적인 비교를 위해 컴포넌트 내부는 하나의 DOM 트리 구조로 이루어져야 하는 규칙
```javascript
// div 태그로 감싸기
function App() {
  return(
    <div>
      <h2>Hello</h2>
      <h2>World</h2>
    </div>
  )
}

// Fragment(<></>)로 감싸기
function App() {
  return(
    <Fragment>
      <h2>Hello</h2>
      <h2>World</h2>
    </Fragment>
  )
}

function App() {
  return(
    <>
      <h2>Hello</h2>
      <h2>World</h2>
    </>
  )
}
```

- JSX 안에서도 중괄호로 자바스크립트 표현식을 사용할 수 있다.
```javascript
function App() {
  const name = 'Tom';
  return(
    <>
      <h2>Hello</h2>
      <h2>{name}</h2>
    </>
  )
}
```

### props
props는 properties의 줄임말로 상위 컴포넌트가 하위 컴포넌트에 값을 전달할때 사용한다.   
props는 객체이며 하위 컴포넌트에서 props.이름(key)으로 접근할 수 있다.
- 하위 컴포넌트 입장에서 props는 읽기 전용이다.(수정 불가)
- 상위 컴포넌트에서 props를 변경하면 해당 props를 사용하고 있는 하위 컴포넌트가 리렌더링된다.

```javascript
// 상위 컴포넌트
import Header from './components/Header';
function App() {
  return(
    <>
      <Header name="Tom"/>
    </>
  );
}

// 하위 컴포넌트
function Header(props) {
  return(
    <header>
      <h2>{props.name}</h2>
    </header>
  )
}
```

- 구조분해할당도 가능하다.
```javascript
// 상위 컴포넌트
import Header from './components/Header';
function App() {
  const info = {
    name: 'Tom',
    age: 18
  }

  return(
    <>
      <Header {...info}/>
    </>
  );
}

// 하위 컴포넌트
function Header({name, age}) {
  return(
    <header>
      <h2>{name}</h2>
      <h2>{age}</h2>
    </header>
  )
}
```

- children prop : 리액트에서 설정한 내장 prop으로 컴포넌트 사이 내용(택스트)을 의미한다.
```javascript
// 상위 컴포넌트
import Header from './components/Header';
function App() {
  return(
    <>
      <Header>My name is Tom</Header>
    </>
  );
}

// 하위 컴포넌트
function Header(props) {
  return(
    <header>
      <h2>{props.children}</h2> // <h2>My name is Tom</h2>
    </header>
  )
}
```

- props를 단일 객체로 그룹화 : ...을 사용하여 하나의 객체에 props로 분류되는 모든 것을 모아온다.
```javascript
// 상위 컴포넌트
import Header from './components/Header';
function App() {
  return(
    <>
      <Header id="basicHeader" className="headerClass">
        My name is Tom
      </Header>
    </>
  );
}

// 하위 컴포넌트
function Header({children, ...props}) {
  return(
    <header {...props}> // <header id="basicHeader" className="headerClass">
      <h2>{children}</h2>
    </header>
  )
}
```

- 기본값 설정
```javascript
// 상위 컴포넌트
import Header from './components/Header';
function App() {
  return(
    <>
      <Header id="basicHeader" className="headerClass">
        My name is Tom
      </Header>
    </>
  );
}

// 하위 컴포넌트
function Header({children, ...props, HeaderContainer = 'div'}) {
  return(
    <HeaderContainer> // <div>로 작동
      <header {...props}> // <header id="basicHeader" className="headerClass">
        <h2>{children}</h2>
      </header>
    </HeaderContainer>
  )
}
```

### useState
리액트 Hook중 하나인 useState는 컴포넌트의 상태를 편하게 생성하고 관리할 수 있는 도구이다.   
state 생성과 동시에 가져야할 초기값을 useState 함수에 인자로 넣어주면 state와 setState를 배열 형태로 리턴해준다.
```javascript
const [state, setState] = useState(); // [현재 상태, 상태 업데이트 함수] 
```
컴포넌트의 현재 상태 값은 state 변수에 담겨져있고, setState함수를 이용해 변경할 수 있다.(state & setState는 마음대로 지정 가능)   
state가 변경되면 해당 컴포넌트는 다시 렌더링이 된다.