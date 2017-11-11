# 함수(Function)

## 즉시실행함수(IIFE - Immediately-invoked function expression)

함수를 정의함과 동시에 바로 실행하는 함수를 즉시 실행 함수라고 한다.

```js
    (function (name) {
        console.log(name)
   }) ('jeongeun'); // 'jeongeun'
```

즉시 실행 함수는 최초 한 번의 실행만을 필요로 하는 초기화 코드나, 외부에 공유되면 안되는 코드,
전역 공간의 오염없이 수행하기 위한 방법으로 많이 사용에 자주 사용한다.
함수 리터럴을 괄호()로 둘러싸준 다음, 함수가 바로 호출될 수 있게 () 괄호 쌍을 추가해주면 된다.
이때 괄호 안에 값을 추가해주면 즉시 실행 함수의 인자로 바로 넘길 수 있다.


## 인자, 매개변수

### 매개변수(Parameters)

함수 외부의 값(인자 or 인수)을 받아 함수 내부에 값(데이터)을 넘겨 주는 중간 역할(매개체)을 하는 변수를
매개변수(파라미터)라고 한다.
소괄호() 안에 작성, 콤마로 구분하여 다수의 파라미터를 작성할 수 있다.


### 인자(Arguments)

인자(argument)는 함수 내부로 유입되는 입력 값을 의미하는데, 어떤 값을 인자로 전달하느냐에 따라서
함수가 반환하는 값이나 메소드의 동작방법을 다르게 할 수 있다.

```js
function testParameter(a, b ,c) {

	console.log(a + b + c);
}

testParameter(1, 2, 3); // 6
```

### arguments 객체(Arguments Object)

자바스크립트에서는 유입되는 인자의 수가 함수에서 요구하는 수와 달라도 에러가 발생하지 않는다.
그렇다고 인자들이 그냥 버려지는것이 아니라 arguments라는 구조체에 인자 정보가 저장되어
사용할 수 있는데 이러한 인자의 정보를 관리하는 것이 arguments 객체이다.

```js
function argTest (a, b) {
  console.dir(arguments);
    return a + b;
}

//Arguments(3)
//0 : 1
//1 : 2
//2 : 3
//callee :ƒ argTest(a, b)
//length : 3
//Symbol(Symbol.iterator) : ƒ values()
//__proto__ : Object

argTest(1, 2); // 3
argTest(1, 2, 3); // 3
```
arguments 객체는 배열과 비슷한 구조체에 저장되지만 배열은 아니다.
저장된 인자는 숫자 인덱스로 접근할 수 있으며 length 속성을 사용하면 저장된 인수의 개수를 알 수 있다.


## 유효범위(Scope)

유효범위는 변수의 사용이 유효한(가능한) 범위.
변수는 지역(local), 전역(Global)로 나눌 수 있다.

```js
var global = 'global'; // 전역변수

function func(){
  var local = 'local'; // 지역변수
}
```

```js
var value = 'global';
function func(){
	var value = 'local';
	console.log(value); // local
}
func();
console.log(value); // global
```
func 안에서 지역변수 value를 호출. 이떄는 자신의 영역 (local scope)안에서 해당 변수 (value)를 먼저 찾는다.
자신의 영역(local Scope)안에 value가 있으므로 자신의 value를 콘솔에 찍어주었음.
자바스크립트는 기본적으로 외부에서 내부에 접근할 수 없음. 내부에서는 외부로의 접근이 가능.
떄문에 밖에서 console.log(value) 실행하면 func안에 value는 볼 수 없어 자신의 영역 (global)의 value를 찍은 것.


## 렉시컬(Lexical)

소스코드가 작성되는 시점에 유효범위가 결정되는 것을 렉시컬이라 표현.

```js
var name = 'abc'; // 전역에 abc 변수 선언

function print(){
  console.log(name);
}
function getName(){
	var name = 'innerName';
	print(); // abc
}
getName();
```

print() 함수를 호출. 결과 abc
getName함수 안에서 실행되어 getName의 name을 예상.
print라는 함수는 getName의 밖에 선언(전역)
print()가 실행되면 자신의 로컬 영역에서 name을 한번 찾을테고 없으니
자신이랑 가까운 글로벌 영역으로 올라가 글로벌의 name를 찍는 것.


## 호이스팅(Hoisting)

함수 선언이 소스코드에서 해당 함수를 실행하는 부분보다 뒤에 있다 하더라도 함수 선언을 '끌어올리는 것(hoist)'이다.
함수 호이스팅이 발생하는 원인은 자바스크립트 변수 생성과 초기화(선언과 할당)가 분리되어 진행되기 때문.

함수 선언은 코드가 실행될 때 컨텍스트 상단에 끌여올려진다.
함수를 호출하는 코드가 함수를 선언한 코드보다 앞에 있어도 에러가 발생하지 않는다.

함수 표현식은 변수를 통해서만 함수를 참조하기 때문에 호이스팅 되지 않는다.


### 함수 표현식에서의 함수 호이스팅
```js
console.log(sum(10, 10));   // uncaught type error!

var sum = function (num1, num2) { return num1 + num2;
}
console.log(sum(10, 10));   // 20
```

### 함수 선언문에서의 함수 호이스팅
```js
console.log(sum(10, 10));    // 20

function sum(num1, num2) {
    return sum1 + sum2;
}
```


## 콜백(Callback)
함수를 다른 함수의 인자로 전달할 경우 전달되는 함수를 콜백 함수라고 한다.
콜백 함수는 직접 정의할 수도 있고 이미 자바스크립트에 기본 탑재된 것이어도 된다.
콜백 함수는 로직을 분리하고 코드 기반을 가능한 한 재사용 할 수 있게 유지하는 데 도움된다.

주로 특정 이벤트가 발생했거나 특정 시점에 도달했을때 호출되어 자주 사용된다.


### 이벤트 리스너로 사용

```js
$("#btnStart").click(function(){
       alert("클릭되었습니다.");
});
```

### 타이머 실행 함수로 사용

```js
setInterval(function(){
   alert("1초마다 한 번씩 실행되요");
}, 1000);
```

### Ajax 결과값을 받을 때 사용

```js
$.get("http://luxlab.co.kr/", function(){
       alter("정상적으로 서버 통신이 이뤄졌습니다.");
});
```

### jQuery 애니메이션 완료

```js
$("#target").animate ({
       left:100,
       opacity:1
},2000,"easeoutQuint", function(){
       alert("애니메이션이 완료되었습니다.");
     });
```


## 클로저

클로저(closure)는 내부함수가 외부함수의 지역변수에 접근 할 수 있지만 외부함수의 실행이 끝나서
외부함수가 소멸된 이후에도 내부함수가 외부함수의 변수에 접근 할 수 있는 것을 말한다.

```js
function aaa(){
   var a = 100;
   var b = 200;

  function bbb(){
    var b = 2000;
    console.log(a);
    console.log(b);
	}
   bbb();
}
 aaa();

// 100
// 2000
```

```js
function aaa(){
 var a = 100;

  var bbb = function() {
    console.log(a);
    }

  return bbb;
}

var ccc = aaa();
 ccc();

// 100
```
