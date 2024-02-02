# Operators

> [dart.dev/language/operators](https://dart.dev/language/operators)

|Description|Operator|Associativity|
|---|---|---|
|unary postfix(단항연산자 접미사)|	expr++ &nbsp; expr-- &nbsp; () &nbsp; [] &nbsp; ?[] &nbsp; . &nbsp; ?. &nbsp; !	|None|
|unary prefix|	-expr &nbsp; !expr &nbsp; ~expr &nbsp; ++expr &nbsp; --expr &nbsp; await expr	|None|
|multiplicative|	* &nbsp; / &nbsp; % &nbsp; ~/	|Left|
|additive|	+ &nbsp; -	|Left|
|shift|	<< &nbsp; >> &nbsp; >>>	|Left|
|bitwise AND|	&	|Left|
|bitwise XOR|	^	|Left|
|bitwise OR	| \| |Left|
|relational and `type test`|	>= &nbsp; > &nbsp; <= &nbsp; < &nbsp; as &nbsp; is &nbsp; `is!`	|None|
|equality|	== &nbsp; !=   	|None|
|logical AND|	&&	|Left|
|logical OR| \|\|	|Left|
|if null|	??	|Left|
|conditional|	expr1 ? expr2 : expr3	|Right|
|`cascade`|	..    ?..	|Left|
|assignment|	= &nbsp; *= &nbsp; /= &nbsp; += &nbsp; -= &nbsp; &= &nbsp; ^= &nbsp; etc.|Right|

## Operator precedence example


## Arithmetic operators
* ~/ : 나눈 값의 인티저 결과만 리턴한다.

* Dart에는 전위 연산자와 후위 연산자가 있다.
후위 연산자는 변수를 사용한 후 값을 1 증감시키고
전위 연산자는 값을 1 증감시킨뒤 변수에 사용한다.
    ```
    var num = 5;
    print(num++); // 출력: 5
    print(num);   // 출력: 6
    ```

    ```
    var num = 5;
    print(++num); // 출력: 6
    print(num);   // 출력: 6
    ```


## Equality and relational operators


## Type test operators
* as: 타입 캐스팅
* is: 객체가 특정 타입이 맞다면 true를 리턴
* is!: 객체가 특정 타입이 아니라면 true를 리턴

## Assignment operators
* 아래와 같은 방법으로 null또는 값을 할당할 수 있다.
```
b ??= value;
```

## Logical operators


## Bitwise and shift operators


## Conditional expressions
null 여부를 판단하여 표현하는 경우 ??를 사용할 수 있다.
```
String playerName(String? name) => name ?? 'Guest';
```

```
// ?: operator를 사용한 조금 긴 버전
String playerName(String? name) => name != null ? name : 'Guest';

// if-else를 사용한 매우 긴 버전
String playerName(String? name) {
  if (name != null) {
    return name;
  } else {
    return 'Guest';
  }
}
```

## Cascade notation
한 객체의 순차적인 명령을 수행할 수 있도록 해준다.
```
var paint = Paint()
  ..color = Colors.black
  ..strokeCap = StrokeCap.round
  ..strokeWidth = 5.0;
```

아래와 같이 nest cascade로 응용이 가능하다.
```
final addressBook = (AddressBookBuilder()
      ..name = 'jenny'
      ..email = 'jenny@example.com'
      ..phone = (PhoneNumberBuilder()
            ..number = '415-555-0100'
            ..label = 'home')
          .build())
    .build();
```

하지만 아래와 같이 실제 객체를 리턴하는 함수의 경우 주의해야 한다.
(void를 리턴하는 write함수도 ..write('foo')로 사용되어야 한다.)
```
var sb = StringBuffer();
sb.write('foo')
  ..write('bar'); // Error: method 'write' isn't defined for 'void'.
```

## Other operators

* ?[]: fooList?[1]은 fooList의 인덱스 1번을 요청하면 null이 아닌경우 인티저 1을 전달한다.