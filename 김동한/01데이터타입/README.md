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

> 변수 선언
