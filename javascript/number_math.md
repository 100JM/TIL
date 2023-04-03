숫자(Number)와 수학(Math)
=============
### 1. toString을 통해 10진수를 2진수/16진수로 표현할 수 있다.
```javascript
let num = 255;

/*2진수 표현*/
num.toString(2); // '11111111'

/*16진수 표현*/
num.toString(16); // 'ff'
```

### 2. Math : 수학과 관련된 프로퍼티와 메소드를 가지고 있는 자바스크립트 내장 객체
#### 2-1 Math.ceil() : 올림 / Math.floor() : 내림 / Math.round() : 반올림
**ceil**과 **floor** 둘다 소수점 숫자에 상관없이 올리거나 내리고 **round**는 5보다 작으면 내리고 크면 올린다.
```javascript
let num1 = 2.9;
let num2 = 2.1;

Math.ceil(num1) // 3
Math.ceil(num2) // 3

Math.floor(num1); // 2
Math.floor(num2); // 2

Math.round(num1) // 3
Math.round(num2) // 2
```

#### 2-2 toFixed() : 소수점 자릿수 표현
원하는 자릿수에서 반올림하여 표현할 수 있다.
```javascript
let rate = 30.1264;

/*소수부 갯수보다 큰 숫자를 넣으면 0으로 채워준다*/
rate.toFixed(2); // '30.13'
rate.toFixed(6); // '30.126400'
```
정말 유용한 메소드이지만 한가지 주의할 점이 있다.   
**toFixed**는 문자열로 반환한다는 것이다.   
필요에 따라 **Number**를 이용해 숫자로 변환하여 사용하자.
```javascript
let rate = 30.1264;

rate.toFixed(2); // '30.13'
Number(rate.toFixed(2)); // 30.13
```
#### 2-3 isNaN() : NaN 판별
NaN인지 아닌지 판별하는 법은 **isNaN**이 유일하다.   
```javascript
isNaN('x'); // true
isNaN(31); // false
Number('x'); // NaN
```

#### 2-4 parseInt() : 문자열을 숫자로 변환
**Number**와 **parseInt**의 차이점은 **parseInt**는 문자가 혼용되어 있어도 동작을한다.   
읽을 수 있는 부분까지 진행 후 문자를 만나면 반환한다.   
하지만 문자가 먼저 시작한다면 NaN을 반환한다.
```javascript
let margin = '10px';

parseInt(margin); // 10
Number(margin); // NaN

parseInt('f3'); // NaN
```
또한 **parseInt**는 두번째 인수를 받아서 진수를 지정할 수 있다.
```javascript
let redColor = 'f3';

parseInt(redColor); // NaN
parseInt(redColor, 16); // 243

parseInt('11', 2); // 3
parseInt('11', 10); // 11
```   

#### 2-5 parseFloat() : parseInt와 동일하게 동작하지만 소수점 자리까지 변환
```javascript
let per = '29.9%';

parseFloat(per); // 29.9
parseInt(per); // 29
```

#### 2-6 Math.random() : 0~1 사이 무작위 숫자 생성
```javascript
Math.random(); // 0.9114765076335309
Math.random(); // 0.44012832900685495
Math.random(); // 0.7558516676180345
```
만약 1~100 사이 임의의 숫자를 뽑고 싶다면 ?   
```javascript
Math.floor(Math.random()*100)+1 // 29
/*+1을 해주는 이유
    floor로 소수점을 버렸을 때 0이 나올 수 있기 때문에 최솟값인 1을 더해준다.
*/
```

#### 2-7 Math.max() / Math.min() / Math.abs() : 최댓값 / 최솟값 / 절대값 구하기
```javascript
Math.max(1,4,-1,5,9); // 9
Math.min(1,4,-1,5,9); // -1
Math.abs(-1) // 1
```

#### 2-8 Math.pow() : 제곱 구하기
```javascript
/*2의 10승*/
Math.pow(2, 10); // 1024
```
#### 2-9 Math.sqrt() : 제곱근 구하기
```javascript
/*루트 16 = 4*/
Math.sqrt(16); // 4
```