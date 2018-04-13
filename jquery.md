# 함수

자바스크립트의 함수는 일급 객체로, 코드 재용, 정보의 구성 및 은닉 등에 사용하는 모듈화의 근간이다.

## 함수 객체

함수는 객체이다. 따라서 프로토타입 체인이 있다.

``` javascript
var fn = function () {};

fn.__proto__ === Function.prototype;  // true
Function.prototype.__proto__ === Object.prototype;  // true
```

모든 프로토타입 객체는 함수 자체를 가리키는 `constructor` 속성이 있으므로, 함수도 마찬가지다.

``` javascript
Function.prototype.constructor === Function;  // true
```

## 함수 선언문

다음과 같이 함수를 선언하는 것을 함수 선언문이라고 한다.

``` javascript
function add(a, b) {
    return a + b;
}
```

## 함수 리터럴

다음과 같이 함수를 선언하는 것을 함수 리터럴이라고 한다.

``` javascript
var add = function (a, b) {
    return a + b;
};
```

- `function` 예약어 다음에 이름을 붙여도 되고 안 붙여도 된다. 붙이면 디버거에서 함수 이름이 보인다는 장점이 있다. 
- 호출시 전달하지 않은 매개변수는 `undefined`로 초기화 되고, 초과 전달된 매개변수는 무시된다.

## 반환

`return` 문을 이용해서 값을 반환할 수 있고, 반환값이 지정되지 않은 경우에는 `undefined`가 반환된다.

## 예외

`throw` 문을 이용해서 예외를 발생 시킬 수 있다. `name` 속성과 `message`  속성은 반드시 포함해야 하며, 추가 속성도 가능하다.

``` javascript
var raiseException = function () {
    throw {
        name: 'TypeError',
        message: 'some type error'
    };
};
```

`try`, `catch` 문으로 예외를 처리할 수 있다.

``` javascript
var tryCatch = function () {
    try {
        raiseException();
    } catch (e) {
        console.log(e.name);  // TypeError
        console.log(e.message);  // some type error
    }
};
```

## 함수 호출

모든 함수는 호출시 명시된 매개변수에 더해 `this`와 `arguments`라는 추가적인 매개변수 두 개를 받는다. 이 때 `this`는, 함수를 호출하는 4가지 방식에 따라서 다르게 초기화 된다.

- 메소드 호출 패턴
- 함수 호출 패턴
- 생성자 호출 패턴
- `apply`, `call` 호출 패턴

### 메소드 호출 패턴

함수를 객체의 속성으로 저장하는 경우, 이 함수를 메소드라고 부른다. 메소드를 호출할 때, `this`는 메소드를 포함하고 있는 객체에 바인딩, 즉, 객체 자체가 된다. 이렇게 객체 자체를 `this`에 바인딩하는 메소드를 퍼블릭 메소드라고 한다.

``` javascript
var myObject = {
    value: 0,
    increment: function (inc) {
        this.value += typeof inc === 'number' ? inc : 1;
    };
};

myObject.increment();
console.log(myObject.value);  // 1

myObject.increment(2);
console.log(myObject.value);  // 3
```

객체가 메소드 안의 `this`에 바인딩 되는 것은 메소드 호출시 일어나므로, `this`는 동적으로 다양하게 응용될 수 있다.

### 함수 호출 패턴

``` javascript
var sum = add(3, 4);
```

함수가 객체의 속성이 아닌 경우는 함수로서 호출되고, 이 경우 `this`는 전역 객체에 바인딩 된다. 이는 명백한 설계 오류로, 만약 바르게 설계되었다면 내부 함수의 `this`는 외부 함수의 `this`에 바인딩되었어야 할 것이다.

따라서 다음과 같이 사용할 경우 의도하지 않은 동작이 나타난다.

``` javascript
var myObject = {};

myObject.fn = function() {
    // this가 myObject를 참조할 것이라고 기대
    var innerFn = function() {
        console.log(this);
    };
    innerFn();
};

myObject.fn();  // Window {speechSynthesis: SpeechSynthesis, ...
```

이를 해결하고 싶을 경우 보통 다음과 같은 패턴을 사용한다.

``` javascript
var myObject = {};

myObject.fn = function() {
    var self = this;
    
    var innerFn = function() {
        console.log(self);
    };
    
    innerFn();
};

myObject.fn();  // Object { fn: ....
```

### 생성자 호출 패턴

함수를 `new` 문과 함께 호출하는 방법이다. 이 경우 함수의 프로토타입 객체의 `constructor` 속성을 이용해 호출한다.

``` javascript
var Quo = function (string) {
    this.status = string;
};

Quo.prototype.getStatus = function () {
    console.log(this.status);
};

var myQuo = new Quo('confused');
myQuo.getStatus();  // confused
```

`new` 문은 클래스 기반 언어를 떠올리게 만들어서 프로그래머에게 혼란을 준다. 자바스크립트는 프로토타입 기반 언어이고, `new` 문은 프로토타입 기반의 언어를 사용하는데 적절한 방법이 아니다.

### `apply`, `call` 호출 패턴

함수도 객체이기 때문에 메소드를 가질 수 있다. `apply`, `call` 메소드는 자바스크립트의 모든 함수에 포함되어 있는 메소드이다. 첫 번 째 매개변수로 함수 안에서 `this`에 묶이게 될 값을 넘길 수 있다. `apply`, `call`의 차이점은 다음과 같다.

- `apply`: 호출하려고 하는 함수의 매개변수들의 배열을 두 번 째 매개변수로 넘긴다. (`arguments`)
- `call`: 호출하려고 하는 함수의 매개변수들을 두 번 째, 세 번 째 ... 매개변수로 넘긴다.

아래 세가지 호출은 같다.

``` javascript
var add = function (a, b) {
    return a + b;
};

add(3, 4);  // 7
add.apply(null, [3, 4]);  // 7
add.call(null, 3, 4);  // 7
```

첫 번 째 매개변우에 `null` 혹은 `undefined`를 넣을 경우 자동으로 전역 객체에 바인딩 된다. (non-strict mode의 경우)

객체의 컨텍스트(`this`)를 마음대로 설정할 수 있으므로, 다른 객체의 메소드를 훔쳐(?) 쓰는 것도 가능하다.

``` javascript
var myStatus = {
    status: 'WOW'
};

Quo.protoype.getStatus.apply(myStatus);  // WOW
```

객체 구조만 맞다면 얼마든지 동적으로 메소드를 재사용할 수 있다.

## 기본 타입에 기능 추가 (프로토타입 확장)

프로토타입을 이용해서 기본 타입을 확장할 수 있다. 모든 숫자(`Number`) 타입에 음수면 올림, 양수면 버림을 하는 메소드를 추가해보자.

``` javascript
Number.prototype.integer = function () {
    var methodName = this < 0 ? 'ceil' : 'floor';
    return Math[methodName](this);
};

console.log((-10 / 3).integer());  // -3
```

다음과 같은 메소드를 함수(`Function`) 타입에 추가하면 기능 확장시 `.prototype`을 반복해서 써줄 필요가 없다.

``` javascript
Function.prototype.addMethod = function (name, fn) {
    if (!this.prototype[name]) {
        this.prototype[name] = fn;
    } else {
        console.log('method already exists');
    }
};

Number.addMethod('integer', function () {
    var methodName = this < 0 ? 'ceil' : 'floor';
    return Math[methodName](this);
});
```

이미 같은 이름의 속성이 있는 경우 덮어쓰지 않도록 조치했다.

## 매개변수 배열

함수 호출시 추가적인 매개변수로 `this`와 함께 `arguments` 배열을 사용할 수 있다. 이 배열은 함수를 호출 할 때 전달된 모든 매개변수를 담고 있는 배열이다.

이 배열을 이용하면, 호출시 넘어오는 매개변수의 개수가 정해지지 않은 동적인 함수를 만들 수 있다.

``` javascript
var sum = function () {
    var i, sum = 0;
    
    for (i = 0; i < arguments.length; i += 1) {
        sum += arguments[i];
    }
    
    return sum;
};

console.log(sum(4, 8, 15, 16, 23, 42));  // 108
```

> `arguments`는 사실 배열이 아니고 배열 같은 객체이다. `length`라는 속성은 있지만 일반적인 배열이 가지는 메소드들은 없다.

## 재귀 호출

재귀 함수는 자기 자신을 호출하는 함수를 말한다. 하나의 문제를 유사한 하위 문제로 나눌 수 있고, 같은 해결 방법으로 처리할 수 있을 때 사용할 수 있는 강력한 기법이다.

웹 브라우저의 DOM 트리를 순회하는 기능을 재귀를 이용해 만들어 보자.

``` javascript
var walkDOM = function (node, fn) {
    fn(node);  // do something with this node
    node = node.firstChild;
    
    while (node) {
        walkDOM(node, fn);
        node = node.nextSibling;
    }
};
```

자바스크립트에서는 꼬리 재귀 최적화를 제공하지 않는다.

> 재귀호출을 바로 반환하는 방법으로 진행되는 재귀 호출을 꼬리 재귀라고 한다. 몇몇 언어에서는 이런 꼬리 재귀를 속도를 개선하는 방법으로 자동 대체한다.

## 유효 범위 (Scope)

### 실행 컨텍스트 (Execution Context)

실행 컨텍스트는 흔히 이야기하는 콜 스택(Call Stack)과 같은 말이다. 함수가 호출될 때 같이 생성되고, 다음과 같은 것들을 포함한다.

- 변수 생성
- `this`, `arguments` 생성
- **스코프 생성 !!**

### 함수 스코프

자바스크립트는 **오로지 함수 스코프만 존재하고 블록 스코프가 없다**. 이는 프로그래머에게 충분히 혼란을 줄 수 있다. 따라서 보통의 언어에서 변수는 사용하기 직전에 선언되는 것을 선호하는 반면, 자바스크립트에서는 함수의 시작 부분의 변수를 모두 선언하는 것을 선호하는 편이다. (호이스팅에 의한 혼란 방지 차원)

``` javascript
var foo = function () {
    var a = 3, b = 5;
    
    var bar = function () {
        var b = 7, c = 11;
        // 2) a === 3, b === 7, c === 11
        a += b + c;
        // 3) a === 21, b === 7, c === 11
    };
    
    // 1) a === 3, b === 5
    bar();
    // 4) a === 21, b === 5
};
```

> ES6의 `let`, `const`는 블록 스코프를 가진다.
 
### 렉시컬 스코프 (Lexical Scope)

자바스크립트는 렉시컬 스코프의 규칙을 따른다. 렉시컬 스코프 규칙은 **콜 스택과 관련 없이** 소스코드가 작성된 컨텍스트를 기준으로 스코프를 정의하고, 런타임에 이것을 변경하지 않는 것을 말한다. 예를 들어,

``` javascript
var x = 'global';

function foo() {
    var x = 'local';
    bar();
}

function bar() {
    console.log(x);
}

foo();  // global
bar();  // global
```

와 같은 결과가 나온다. 만약 자바스크립트가 렉시컬 스코프가 아닌 동적 스코프(콜 스택에 따라 스코프 체인이 변경됨)의 규칙을 따랐다면, 결과는 다음과 같을 것이다.

``` javascript
foo();  // local
bar();  // global
```

### 스코프 체인 (Scope Chain)

방금 본 두 가지 규칙에 따라 알 수 있듯이, 함수가 실행될 때마다 함수 범위를 가지는 렉시컬 스코프가 생성된다. 그리고 생성된 스코프는 자기 바로 상위 스코프를 참조하는데, 이것이 스코프 체인이다.

방금 위의 예제에서 `bar` 함수가 전역 변수 `x`를 참조할 수 있는 이유는 무엇일까? 바로 `bar`가 실행되면서 생성된 스코프가 바로 상위 스코프인 전역 스코프를 참조하고 있기 때문이다.

![javascript-lexical-scope-chain](http://i.imgur.com/VwfKlqu.png)

> 이미지 출처: [http://techslides.com/understanding-javascript-closures-and-scope](http://techslides.com/understanding-javascript-closures-and-scope)

### 호이스팅 (Hoisting)

실행 컨텍스트를 설명할 때, 함수가 실행되면서 변수를 생성한다고 했었다. 즉, 함수가 실행 될 때, `var`로 선언된 변수와 함수 선언문으로 선언된 함수는 **위로 끌어올려진다.** 다음 코드를 보자.

``` javascript
function foo() {
    x = 2;
    var x;
    console.log(x);
}

foo();  // 2
```

이 코드는 사실 다음과 같다.

``` javascript
function foo() {
    var x;
    x = 2;
    console.log(x);
}

foo();  // 2
```

어렵지 않다. 그럼 다음을 보자.

``` javascript
function foo() {
    console.log(x);
    var x = 2;
}

foo();  // undefined
```

음? `ReferenceError`가 발생한 것도 아니고, 2가 출력된 것도 아니다. 왜? 다음을 보면 이해 된다.

``` javascript
function foo() {
    var x;
    console.log(x);
    x = 2;
}

foo();  // undefined
```

함수 선언문은 호이스팅이 된다.

``` javascript
fn();  // CALL

function fn() {
    console.log('CALL');
}
```

그러나 함수 리터럴은 생각한대로 동작하지 않는다.

``` javascript
fn();  // fn of object is not a function

var fn = function () {
    console.log('CALL');
};
```

왜냐하면 사실 저 코드는 다음과 같기 때문이다.

``` javascript
var fn;

fn();  // fn of object is not a function

fn = function () {
    console.log('CALL');
};
```

 `fn`을 호출하려고 할 때 `fn`은 함수가 아니라 단순히 선언된 변수일 뿐이니 `fn`은 함수가 아니라는 메세지를 보게된다.

## 클로저 (Closure)

클로저는 보통 이렇게 설명되곤 한다.

> 자신이 선언된 스코프를 캡쳐(기억, 참조 등등...)하는 함수

밑도 끝도 없이 이 설명만 들으면 의미가 잘 와닿지 않을수도 있다. 그런데 사실 위에서 렉시컬 스코프와 스코프 체인을 설명할 때 이미 똑같은 말을 했다. **"함수가 실행될 때 스코프를 생성하고, 그 스코프는 소스코드 상에서 바로 상위 스코프를 참조한다."**

그러니까, 저 설명에 따르면 사실 모든 함수는 클로저이다. 왜냐하면 모든 함수의 스코프는 자기가 선언된 바로 상위 함수의 렉시컬 스코프를 참조하고 있기 때문이다. 그러나 보통은, 우리는 모든 함수를 클로저라고 부르지 않는다.

보통은 다음과 같을 때, 이 함수를 클로저라고 부른다.

``` javascript
var color = 'red';

function foo() {
    var color = 'blue';
    
    function bar() {
        console.log(color);
    }
    
    return bar;
}

var baz = foo();
baz();  // blue
```

함수 `foo`가 콜 스택에서 pop 되었는데도 'blue' 값이 사라지지 않고 남아있는 이상한(?) 동작처럼 보인다. 콜 스택과 연관지어서 생각하기 때문에 그렇다. 다음 그림을 보자.

![javascript-closure](http://image.toast.com/aaaadh/alpha/2016/techblog/gcclosure.png)

> 이미지 출처: [http://meetup.toast.com/posts/86](http://meetup.toast.com/posts/86)

위의 렉시컬 스코프와 스코프 체인의 정의에 따라, 함수가 항상 선언된 곳을 기준으로 바로 상위의 스코프를 참조하고 있다는 것만 알면 너무나 당연한 결과이다. 이를 잘못 이해하면 다음과 같은 오동작을 야기할 수 있다.

``` javascript
var addHandlers = function (nodes) {
    var i;
    for (i = 0; i < 10; i += 1) {
        nodes[i].onclick = function (e) {
            alert(i);
        };
    }
};
```

아마 핸들러마다 1부터 10까지의 숫자를 띄워주려는 의도였으나, 실은 어떤 노드를 클릭해봐도 모두 10이 출력된다. 왜냐하면 `onclick` 속성에 연결된 함수들이 참조하는 변수는 모두 같은 상위 스코프의 `var i`이기 때문이다. (즉, 모두 같은 상위 스코프를 공유하고 있다.)

의도대로 동작하게 하고 싶다면 다음과 같이 하면 된다.

``` javascript
var addHandlers = function (nodes) {
    var i;
    for (i = 0; i < 10; i += 1) {
        nodes[i].onclick = function (i) {
            return function (e) {
                alert(i);
            };
        }(i);
    }
};
```

즉시 실행 함수를 추가해서 상위 스코프를 공유하지 않도록 했다.

> 클로저를 사용하면, 사라졌어야 할 상위 렉시컬 스코프를 계속해서 유지하게 되므로 자칫 메모리 누수의 원인이 되기도 한다.
>
> 참고: [Beware of the closure memory leak in Javascript](http://heichwald.github.io/2016/01/10/memory-leak-closure-javascript.html)

### 은닉화

클로저는 보통 은닉화(private 변수)에 자주 쓰인다. 다음을 보자.

``` javascript
var Quo = function (status) {
    this._status = status;
};

Quo.prototype.getStatus = function () {
    return this._status;
};

var q = new Quo('my status');
console.log(q._status);  // my status
console.log(q.getStatus());  // my status
```

`new` 문을 쓰는 방법으로는 은닉화가 불가능하다. 하지만 클로저를 사용하면 은닉화가 가능하다.

``` javascript
function quo(status) {
    var _status = status;
    
    return {
        getStatus: function () {
            return _status;
        };
    };
}

var q = quo('my status');
console.log(q._status);  // undefined
console.log(q.getStatus());  // my status
```

클로저를 이용한 은닉화는 모듈 개념과 같다. 따라서 이를 적극적으로 활용하면 자바스크립트의 최대 단점 중 하나인 전역 변수 사용을 최소화할 수 있다.

### 커링

클로저를 이용하면 함수형 프로그래밍 기법 중 하나인 커링을 구현할 수 있다. 커링이란 n개의 매개변수를 받는 함수를 1개의 매개변수를 받는 함수 n개로 쪼개어 함수의 호출 체인으로 처리하는 방법이다.

``` javascript
Function.prototype.curry = function () {
    var args = Array.prototype.slice.apply(arguments),
        self = this;
    
    return function () {
        return self.apply(null, args.concat(Array.prototype.slice.apply(arguments));
    };
};

var add = function () {
    // arguments의 합
};

var add1 = add.curry(1);

console.log(add1(6));  // 7
```

## 연속 호출 (Cascade)

만약 어떤 메소드의 반환값이 `this`라면 이런식의 호출이 가능할 것이다.

``` javascript
getElement('myElement').move(50, 50).width(100).height(100) ...
```

이것 자체가 별로 특별한 것은 아니다. 다만 이런 연속 호출을 비동기로 한다면 ES6의 Promise와 유사한 모양이 된다.

## 콜백

보통의 동기식 작업은 다음과 같다.

``` javascript
response = sendSync(request);
doAfter(response);
```

자바스크립트에서는 일반적으로 콜백 패턴을 사용해서 이것을 비동기 작업으로 바꿀 수 있다.

``` javascript
sendAsync(request, function (response) {
    doAfter(response);
});
```

> 자바스크립트에서는 비동기 패턴이 매우 일반적이고 흔하게 사용된다. 이런 이벤트 드리븐 방식을 쉽게 사용하는 것이 가능한 이유는 모든 브라우저에 자바스크립트 런타임과 별개로 이벤트 루프와 태스크 큐가 있기 때문이다.

> 참고: [Philip Roberts: Help, I’m stuck in an event-loop](https://vimeo.com/96425312)

## 참고한 페이지

- [자바스크립트의 스코프와 클로저](http://meetup.toast.com/posts/86)
- [JavaScript : Scope 이해](http://www.nextree.co.kr/p7363)
- [JavaScript 클로저(Closure)](https://hyunseob.github.io/2016/08/30/javascript-closure)
- [JavaScript에서 커링 currying 함수 작성하기](http://www.haruair.com/blog/2993)
- [JavaScript 모나드](http://www.haruair.com/blog/2986)
