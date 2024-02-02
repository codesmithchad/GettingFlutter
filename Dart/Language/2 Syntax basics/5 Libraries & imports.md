# Libraries & imports

> [dart.dev/language/libraries](https://dart.dev/language/libraries)

import와 library 지시자들은 모듈을 만들거나 공유 가능한 코드베이스를 만들 수 있게 해준다. 라이브러리는 API 뿐만 아니라 유닛의 보안도 제공해 준다. (언더스코어로 시작하는 식별자는 라이브러리 내에서만 접근 가능하다.) Dart 파일과 그 부속은 라이브러리로 사용하지 않더라도 모두 라이브러리이다.

## Using libraries
import를 지정할때는 특정 라이브러리의 URI만을 필요로 한다. 빌트인 라이브러리의 경우 URI에 `dart:`이라는 스키마를 사용하면 된다.
다른 라이브러리인 경우 파일 시스템 경로나 `package:` 스키마를 사용할 수 있다. 
`package:` 스키마는 pub tool같은 패키지 메니저에서 제공되는 라이브러리를 특정하는데 사용한다.
```
import 'package:test/test.dart';
```

### Specifying a library prefix
식별자가 충돌하느 서로 다른 라이브러리를 import 하는 경우 하나 또는 양 라이브러리에 프리픽스를 통해 특정할 수 있다.
예를 들어 library1과 library2 양쪽에 Element라는 클래스를 소유한 경우 아래와 같이 사용할 수 있다.
```
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

// Uses Element from lib1.
Element element1 = Element();

// Uses Element from lib2.
lib2.Element element2 = lib2.Element();
```

### Importing only part of a library
라이브러리에서 특정 파트만 import 하고 싶다면 아래와 같이 사용할 수 있다.
```
// foo만 import
import 'package:lib1/lib1.dart' show foo;

// foo를 제외한 모두 import
import 'package:lib2/lib2.dart' hide foo;
```

#### Lazily loading a library
지연 로딩을 통해 필요에 따라 웹앱의 라이브러리 로드를 지연시킬 수 있다.
아래와 같은 경우 지연 로딩이 필요할 것이다.
* 웹앱의 시작 시간을 줄이려 할 때
* A/B 테스트를 진행할 때 (예를 들어 서로 다른 알고리즘을 비교하고자 할 때)
* 자주 사용되지 않는 기능이나 화면, 다이얼로그를 로드할 때

라이브러리를 지연 로드하려면 `deffered as`를 사용하여 import 한다.
```
import 'package:greetings/hello.dart' deferred as hello;
```

라이브러리에서 loadLibrary()를 사용하려면 아래와 같이 라이브러리의 identifier를 이용한다.
```
Future<void> greet() async {
  await hello.loadLibrary();
  hello.printGreeting();
}
```
위 코드에서 await 키워드는 라이브러리가 로드 될때까지 실행을 지연시킨다.
라이브러리가 한번 로드되고 나면 이후 loadLibrary()를 문제없이 여러번 호출할 수 있다.

지연 로딩을 사용할 때 아래의 사항에 유의하자.
* 라이브러의 상수는 해당 라이브러리가 로드되기 전까지 상수로서 존재하지 않는다.
* 지연 라이브러리의 타입을 사용할 수 없다. 대신 인터페이스 타입을 지연 라이브러리와 import한 파일 양쪽을 import한 라이브러리로 옮기는 것을 고려해야 한다.
* Dart는 암묵적으로 deffered as namespace로 지정한 네임스페이스에 loadLibragy()를 네임 스페이스에 추가한다. loadLibragy() 함수는 `Future` 타입을 리턴한다.



### The library directive


## Implementing libraries