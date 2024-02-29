참조형 & 기본형
=============

### 참조형과 기본형
String, Number, boolean은 모두 **기본형(Primitive type)**이다.   
자바스크립트의 기본형 값의 특징은 변경할 수  없다는 점이다.
```javascript
let name = 'Tom';
name = 'Tom Holland';

name = name.concat(' Holland');

// 재할당을 하면 기존의 값은 삭제되고 새로운 문자열이 생성된다.
```

객체를 다룰 때는 다르다.   
자바스크립트 객체는 **참조형(Reference Type)** 값이며 이는 변수에 값을 저장할 때 값 자체를 저장하는것이 아니라, 해당 값의 메모리 주소를 저장한다.   
만약 push를 호출하면 자바스크립트에서 해당 주소를 찾아 그 주소의 값을 열어 배열을 확인한 후 메모리에 있는 해당 배열에 새 원소를 추가한다.   
메모리의 배열은 수정되지만 주소는 변하지 않는것이다.
```javascript
const name = ['Tom', 'Holland'];
name.push('Spider-Man');
``` 
따라서 const에 저장된 객체는 재할당 할 수는 없지만 객체는 주소를 참조해 액세스된다는 점을 활용해 메모리 주소에 있는 값을 조작할 수 있다.
