## 데이터 타입

> 데이터 타입의 종류

![데이터타입](../img/%EB%8D%B0%EC%9D%B4%ED%84%B0%ED%83%80%EC%9E%85.png)

```js
기본형[=원시형](primitive type) - Number, String, boolean, null, undefined, Symbol(ES6)

참조형(reference type) - Object, Array, Function, Date, RegExp(정규표현식), Map(ES6), WeakMap(ES6), Set(ES6), WeakSet(ES6)
```

읽자마자 조금 생소한 부분들이 있었다. ES6부터 추가 된 Map, WeakMap, Set, WeakSet, Symbol 이다. 이를 간단히 정리하고 넘어간다.

### Symbol

[참고한 블로그](https://it-eldorado.tistory.com/149)

```js
함수를 호출하여 생성가능(값의 변경이 불가능한 기본형)

심볼의 가장 큰 특징은 호출할 때 마다 고유한 심볼이 생성되는것이다.

const sym1 = Symbol();
const sym2 = Symbol();
const sym3 = Symbol('foo');
const sym4 = Symbol('foo');

console.log(sym1 === sym1);  // true
console.log(sym1 === sym2);  // false
console.log(sym3 === sym4);  // false

심볼은 객체의 프로퍼티 키로 사용된다.

심볼은 기본적으로 고유하기 때문에 어느 프로퍼티와도 충돌하지 않는다.

const obj = {};

const sym1 = Symbol();
const sym2 = Symbol('foo');
const sym3 = Symbol('foo');

obj[sym1] = 'propertyValue1';
obj[sym2] = 'propertyValue2';
obj[sym3] = 'propertyValue3';  // no conflict with sym2

console.log(obj);  // {Symbol(): 'propertyValue1', Symbol(foo): 'propertyValue2', Symbol(foo): 'propertyValue3'}

console.log(obj[sym1]);  // propertyValue1
console.log(obj[sym2]);  // propertyValue2
console.log(obj[sym3]);  // propertyValue3
```

#### Map

[참고한 블로그](https://medium.com/@hongkevin/js-5-es6-map-set-2a9ebf40f96b)

```js
우리가 평소에 알던 Array.prototype.map()과 완전히 다른 것이니 혼동하지말자.

간단하게 보자면 Map()도 객체의 한 종류이고, 기존에 쓰던 Object와 비교하여 메커니즘만 조금 다르다.

Key값을 이용하여 get(), set()으로 값을 수정할 수 있고, key들은 중복될 수 없다.

Map과 Object의 큰 차이점은 길이를 알 수 있다는 점이다.

기존 Object의 길이를 알려면 안에 들어있는 요소들을 카운트해야되지만, Map의경우 size()를 통하여 크기를 알 수 있다.

Map은 for-of 형태로 key, value를 뽑을 수 있다.

for(var [key, value] of MapObject) {
  console.log(k, v);
};

// 새로운 map 을 만들고 map 에 key, value 엔트리를 추가
let me = new Map();
me.set('name', 'elice');
me.set('generation', 3);
console.log(me.get('generation'); // 3

// 대괄호를 사용해서 map 을 선언하는 방법
이중 배열형태로 들어가 Array로 착각 할 수 있으나, 객체형이다.

const subject = new Map(
  [
    ["01", "HTML-CSS"],
    ["02", "JavaSCript"],
    ["03", "MongoDB"],
    ["04", "React"],
  ]
);

// 새로운 map 을 만들고 그 데이터를 기존의 [key, value] 페어컬렉션으로 채움
let you = new Map().set('name', 'paul').set('age', 34);
console.log(you.get('name')); // 'paul'

// has(): 주어진 key 가 존재하는지 확인
console.log(me.has('name')); // true

// size: map 에 담겨진 엔트리의 개수를 조회
console.log(you.size); // 2

// delete(): 엔트리를 삭제
me.delete('age');
console.log(me.has('age')); // false

// clear(): 모든 엔트리를 삭제
you.clear();
console.log(you.size); // 0
```

#### Set

```js
Set() 은 value 들로 이루어진 컬렉션(“집합”이라는 표현이 적절)
Array 와는 다르게 Set 은 같은 value 를 2번 포함할 수 없음
따라서 Set 에 이미 존재하는 값을 추가하려고 하면 아무 일도 없음

// 비어있는 새로운 set 을 만듬
let setA = new Set();

// 새로운 set 을 만들고 인자로 전달된 iterable 로 인자를 채움
let setB = new Set().add('a').add('b');
setB.add('c'); // setB = {'a', 'b', 'c'}
console.log(setB.size); // 3

// has(): 주어진 값이 set 안에 존재할 경우, true 를 반환
// indexOf() 보다 빠름. 단, index 가 없음
console.log(setB.has('b')); // true

// set 에서 주어진 값을 제거
setB.delete('b');
console.log(setB.has('b')); // false

// set 안의 모든 데이터를 제거
setB.clear();
console.log(setB.size); // 0
```

#### WeakMap

```js
Map과 상당히 비슷한 자료구조이지만, 위크맵은 반드시 Key를 객체로 지정해야한다.

let weakMap = new WeakMap(); //weakMap 선언

let object={ name: 'elice' };
weakMap.set(object, 'hi!');
weakMap.set('string', 'hi!'); // error!

// 위크맵의 키로 사용된 객체를 참조하는 것이 아무것도 없다면 해당 객체는 메모리와 위크맵에서 자동으로 삭제됩니다.
let john = { name: "John" };
let weakMap = new WeakMap();
weakMap.set(john, "...");
john = null; // 참조를 덮어씀
```

#### WeakSet

```js
WeakSet은 Set과 다르게 객체만 저장할 수 있다.

저장된 값이 null이 된다면, 가비지 컬렉터가 자동으로 삭제시킨다.

let weakSet = new WeakSet(); // weakSet 선언

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

weakSet.add(john); // weakSet에 데이터를 추가
weakSet.add(pete);
weakSet.add(john);

console.log(weakSet.has(john)); // true
weakSet.delete(john); //weakSet 데이터 삭제
console.log(weakSet.has(john)); // false

console.log(weakSet.has(pete)); // true
pete=null;
console.log(weakSet.has(pete)); // false
```

<br>
<br>

> 메모리와 데이터

```
기본형은 불변성을 가진다.

Q) 기본형 숫자 10을 담은 변수 a에 다시 15를 담으면 a의 값은 15로 변한다. 변하지 않는다는건 어떤 의미인가 ?

A) 숫자의 경우 자바스크립트는 8바이트(64비트)를 구분없이 확보하고, 비트는 고유한 식별자를 지닌다. 바이트는 비트의 식별자로 위치를 파악한다.
   이는 메모리 주솟값을 통해 서로 구분하고 연결할 수 있다는 뜻이다. (여기까지가 교재의 답변이다 아래는 정리자의 사견이 포함되어있다)

   위의 설명을 토대로 기본형의 불변성을 완전히 이해 못할것이다.
   a는 초기에 10을 담고있고 이 값은 여전히 남는다. 이 값은 재활용되어 계속 사용할 수 있다.
   하지만 a에 15를 담는다는 것은 a를 10에서 15로 바꾸는게 아니라 새로운 데이터 영역에 15를 만들고 그 값을 다시 할당하는 것이다.
   결국 10과 15는 완전히 다른 데이터이므로, 이는 기본형의 불변성을 설명하는데 뒷받침할 수 있다.
```

<br>
<br>

> 식별자와 변수

```
변수 - 변할 수 있는 수, 변할 수 있는 데이터

식별자 - 어떤 데이터를 식별하는 데 사용하는 이름, 즉 변수명
```

<br>
<br>

> 변수 선언, 데이터 할당

```js
불변성에 대하여 조금 자세히 정리할 수 있는 섹션같다.

var a = 'abc'; 다음과 같은 변수를 선언하고 값으로 'abc'를 넣어준다.

a의 값이 바뀐다면, 우리는 이전값을 지우지 않고 새로운 메모리영역에 새로운 값을 넣는다고 했다.

이를 기반으로 불변성을 입증했고, 변수가 데이터의 메모리 주소를 참조하는 것을 그림으로 보자.
```

![데이터할당1](../img/%EB%8D%B0%EC%9D%B4%ED%84%B0%ED%95%A0%EB%8B%B91.png)

```js
변수를 생성하기 위해 1003이라는 주소를 가지는 영역에 변수를 생성한다.

마찬가지로 'abc'라는 값도 데이터 영역에 5004라는 주소로 따로 할당한다.

1003은 값으로 5004라는 주소를 가지고있다.
```

![데이터할당2](../img/%EB%8D%B0%EC%9D%B4%ED%84%B0%ED%95%A0%EB%8B%B92.png)

```js
'abcdef'로 값을 수정한다면, 새로운 데이터 영역 5005에 'abcdef'라는 값을 넣는다.

기존에 5004를 참조하던 값은 새로운 주소인 5005를 바라보기 때문에

var a = 'abcdef'; 가 성립이된다.
```

<br>
<br>

> 불변 값

```js
변수(Variable)와 상수(Constant)를 구분하는 성질은 변경 가능성이다.

바꿀 수 있으면 변수, 바꿀 수 없으면 상수이다.

변수 영역 메모리에 다른 데이터를 재할당할 수 있는지 여부를 따진다.

기본형 데이터인 숫자, 문자열, boolean, null, undefined, Symbol 모두 불변값이다.
```

> 가변 값

```js
기본형 데이터는 모두 불변값이다.

Q) 그럼 참조형 데이터는 모두 가변값일까 ?
A) 기본적인 성질은 가변값인 경우가 많지만, 설정에 따라 변경 불가능한 경우도 있고, 아예 불변값으로 활용하는 방안도 있다.

객체의 변수는 기본형 데이터와 다르게 객체의 변수(프로퍼티) 영역이 별도로 존재한다는 점이다.

자신의 주소를 참조하는 변수의 개수를 참조 카운트라하며, 카운트가 0이되면 가비지 컬렉터에의해 수거된다.

[Case 1]
var a = 10;
var b = a;
b = 15

[Case 2]
var obj1 = {c: 10, d:'ddd'}
var obj2 = obj1;
obj2.c = 20;

Case 1의 경우 b가 15라는 새로운 값을 참조하므로 데이터 자체가 바뀌는것을 알 수 있다.

반대로 Case 2의 경우에 obj1, obj2 모두 객체 영역을 바라보고 그 객체 영역이 새로운 값의 주소로 바뀌기 때문에

두 객체는 값이 달라지지 않는다. (obj2를 새롭게 할당한다면 값이 바뀔 수 있다. ex: obj2 = {c: 20, d: 'ddd'} )
```

> 불변 객체

```js
어떤 객체를 복사할 때 객체 내부의 모든 값을 복사해서 완전히 새로운 데이터를 만들고자 할 때,

기본형 데이터일 경우에는 그대로 복사하면 되지만 참조형 데이터는 다시 그 내부의 프로퍼티들을 복사해야한다.

간단하게 JSON.parse(JSON.stringify(target)) 형태로 JSON 문법으로 표현된 문자열로 전환했다가 다시 JSON 객체로 바꾸는 방법이다.

이 방법은 숨겨진 프로퍼티인 __proto__ 나, getter/setter 등과 같이 JSON으로 변경할 수 없는 프로퍼티들은 모두 무시한다.
```

<br>
<br>

> undefined와 null

```js
자바스크립트에서 없음을 나타내는 값 두가지는 undefined와 null이다.

undefined는사용자가 지정할 수도 있지만, 값이 존재하지 않을 때 자바스크립트 엔진이 자동으로 부여하는 경우도 있다.

[자바스크립트 엔진이 자동으로 부여하는 경우]

사용자가 응당 어떤 값을 지정할 것이라고 예상되는 상황임에도 실제로는 그렇게 하지 않았을 때.

1. 값을 대입하지 않은 변수, 즉 데이터 영역의 메모리 주소를 지정하지 않은 식별자에 접근할 때
2. 객체 내부의 존재하지 않는 프로퍼티에 접근하려고 할 때
3. return 문이 없거나 호출되지 않는 함수의 실행 결과

es6에선 let, const는 undefined를 할당하지 않으며, 접근할 수 없다.

'비어있음'을 명시적으로 쓰고싶다면 null을 사용하자. 애초에 null의 목적이다.

한가지 주의할점은 typeof null은 object이며, 이는 자바스크립트 자체 버그이다.

어떤 변수의 값이 null인지 확인할때는 일치연산자(===)를 사용해야한다. 동등연산자로는 판별할 수 없다.

var n = null;
console.log(n == undefined); //true
console.log(n == null); //true
console.log(n === undefined); //false
console.log(n === null); //true
```
