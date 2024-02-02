# Metadata

> [dart.dev/language/metadata](https://dart.dev/language/metadata)

Metadata는 코드에 추가적인 정보를 지정할 때 사용한다.
@으로 시작하며 컴파일 타임 상수로 deprecated나 상수 생성자 호출에 사용한다.
Dart에서는 [@Derecated](https://api.dart.dev/stable/3.2.6/dart-core/deprecated-constant.html), [@deprecated](https://api.dart.dev/stable/3.2.6/dart-core/deprecated-constant.html), [@override](https://api.dart.dev/stable/3.2.6/dart-core/override-constant.html), [@pragma](https://api.dart.dev/stable/3.2.6/dart-core/pragma-class.html) 등이 사용 가능하다.

* @deprecated는 메세지를 지정하고 싶지 않을 경우 사용하지만 deprecate의 의도가 드러나지 않으므로 사용하지 않는 편이 좋겠다.

아래와 같이 사용자 지정 어노테이션으로 할용할 수 있다. 
(todo 어노테이션을 직접 만들어서 써야하다니...)

* define
```
class Todo {
  final String who;
  final String what;

  const Todo(this.who, this.what);
}
```

* use
```
@Todo('Dash', 'Implement this function')
void doSomething() {
  print('Do something');
}
```