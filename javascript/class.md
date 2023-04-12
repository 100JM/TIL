Class
=============

**Class**는 ES6에 추가된 객체를 생성하기 위한 템플릿이다.   
**생성자 함수**와 **Class**를 비교해보자.
```javascript
// 생성자 함수
const User = function(name, age){
    this.name = name;
    this.age = age;
    this.showName = function(){
        console.log(this.name);
    };
};

const user = new User('Tom', 31); // User {name: 'Tom', age: 31, showName: ƒ}

// Class
class NewUser {
    constructor(name, age){
        this.name = name;
        this.age = age;
    }
    showName(){
        console.log(this.name);
    }
};

const newUser = new NewUser('Petter', 29); // NewUser {name: 'Petter', age: 29}
```
**Class**에는 **constructor**가 있으며 이는 객체를 만들어주는 메소드다.   
또한 showName과 같이 **Class**내에 정의한 메소드는 생성된 객체의 **prototype**에 저장된다.

<img src = "../img/class.png" width = "40%" height = "40%">  

**생성자 함수**로 생성된 user는 객체 내부에 showName이 있고, **Class**로 생성된 newUser는 **prototype** 내부에 있다.   
**생성자 함수**에서도 **Class**처럼 구현하기 위해선 아래와 같이 변경하면 된다.
```javascript
const User = function(name, age){
    this.name = name;
    this.age = age;
    // this.showName = function(){
    //     console.log(this.name);
    // };
};

User.prototype.showName = function(){
    console.log(this.name);
};
```
그렇다면 단순히 문법의 편의성을 위해서 **Class**가 탄생한 것일까?   
**생성자 함수**의 경우 **new** 연산자를 적지 않더라도 에러가 발생하지 않는다.   
하지만 **Class**는 TypeError가 발생하여 실수를 사전에 방지할 수 있다.

<img src = "../img/class_typeError.png" width = "50%" height = "50%">   

newUser의 **constructor**를 보면 **Class**라고 명시되어 있어 **Class**를 통해 생성되었다는 것을 알 수 있고 이러한 경우 **new**없이 호출하면 에러가 발생하도록 설계되어있다.

<img src = "../img/class_constructor.png" width = "40%" height = "40%">    

---

**Class**와 **생성자 함수**는 상속을 하는 키워드도 다르다.   
**생성자 함수**에서 **prototype**을 사용했다면 **Class**는 **extends** 키워드를 사용한다.
```javascript
class Car{
    constructor(color){
        this.color = color;
        this.wheels = 4
    }
    drive(){
        console.log('drive...');
    }
    stop(){
        console.log('stop');
    }
};

class Bmw extends Car{
    park(){
        console.log('park');
    }
};

const x5 = new Bmw('black');
x5.color; // 'black'
x5.drive(); // 'drive...'
x5.stop(); // 'stop'
x5.park(); // 'park'
```
   
---

**Class**에는 **메소드(method) 오버라이딩**과 **생성자(constructor) 오버라이딩**이 있다.   
**메소드 오버라이딩**은 상속받는 **Class**에서 부모 **Class**와 같은 이름의 메소드를 정의하게 되면 덮어쓰게 된다.   
만약 부모의 메소드를 계속 이용하면서 확장하고 싶다면 **super** 키워드를 사용하면 된다.
```javascript
class Bmw extends Car{
    park(){
        console.log('park');
    }
    stop(){
        super.stop();
        console.log('off');
    }
};

const x5 = new Bmw('black');
x5.stop(); // 'stop' 'off'
```
**생성자 오버라이딩**을 하기 위해선 항상 **super** 키워드로 부모 **Class**의 **constructor**를 실행해 주어야 한다.   
또한 제대로 동작하기 위해서는 자식 **Class**의 **constructor**에 동일한 인수를 받는 작업이 필요하다.
```javascript
class Bmw extends Car{
    constructor(color){
        super(color);
        this.owner = 'Tom';
    }
    park(){           
        console.log('park');
    }      
};

const x5 = new Bmw('black');
x5.owner; // 'Tom'
```