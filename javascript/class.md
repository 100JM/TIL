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

<img src = "../img/class.png" width = "30%" height = "30%">  

**생성자 함수**로 생성된 user는 객체 내부에 showName이 있고, **Class**로 생성된 newUser는 **prototype** 내부에 있다.