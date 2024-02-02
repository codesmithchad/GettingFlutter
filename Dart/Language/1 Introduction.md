# Introduction to Dart

> [dart.dev/language](https://dart.dev/language)

## Hello World

## Variables

Dart 코드는 type-safe 하면서도 타입을 특정하지 않고 추론하여 var를 사용해 선언할 수 있다.

## Control flow statements

## Functions

'=>' 구문을 통해 하나의 상태를 가지는 펑션을 쉽게 표현할 수 있다.
이 문법은 특히 anonymous function(swift의 closure)을 매개변수로 전달할 때 유용하다.

## Comments

## Imports

## Classes

## Enums

enum 선언
```
enum Planet {
    mercury(planetType: PlanetType.terrestrial, moons: 0, hasRings: false),
    venus(planetType: PlanetType.terrestrial, moons: 0, hasRings: false),
    // ···
    uranus(planetType: PlanetType.ice, moons: 27, hasRings: true),
    neptune(planetType: PlanetType.ice, moons: 14, hasRings: true);

    /// A constant generating constructor
    const Planet(
        {required this.planetType, required this.moons, required this.hasRings}

    /// All instance variables are final
    final PlanetType planetType;
    final int moons;
    final bool hasRings;

    /// Enhanced enums support getters and other methods
    bool get isGiant =>
        planetType == PlanetType.gas || planetType == PlanetType.ice;
}
```

enum 사용
```
final yourPlanet = Planet.earth;

if (!yourPlanet.isGiant) {
    print('Your planet is not a "giant planet".');
}
```

## Inheritance

extends 구문으 사용하여 상속
```
class Orbiter extends Spacecraft {
    // ...
}
```

## Mixins

Mixin을 여러 클래스 구조에서 통해 코드를 재사용 할 수 있다.
```
mixin Piloted {
    int astronauts = 1;

    void describeCrew() {
        print('Number of astronauts: $astronauts');
    } 
}
```

```
class PilotedCraft extends Spacecraft with Poloted {
    // ...
}
```

PilotedCraft에서 describeCrew() 함수를 사용할 수 있게 된다.

## Interface and abstract classes

콘크리트 클래스의 의도에 따라 추상 클래스를 생성할 수 있다.

```
abstract class Describable { 
    void describe();

    void describeWithEmphasis() {
        print('=========');
        describe();
        print('=========');
    } 
}
```

Describable을 확장한 클래스는 describeWithEmphasis()를 가져야 하며 이 메서드는 해당 클래스에서 정의한 describe()메섣를 호출해야 한다.

## Async

async와 await를 사용하여 콜백 지옥을 피하고 코드의 가독성을 높일 수 있다

```
const oneSecond = Duration(seconds: 1);
// ···
Future<void> printWithDelay(String message) async {
    await Future.delayed(oneSecond);
    print(message);
}
```
위 코드는 (then을 사용해) 아래와 같이 표현할 수도 있다.

```
Future<void> printWithDelay(String message) {
    return Future.delayed(oneSecond).then((_) {
        print(message);
    });
}
```

> `Future<T>`는 T 또는 에러를 반환하는 비동기 함수를 의미

아래와 같이 async, await를 활용하면 가독성 좋은 비동기 코드의 작성이 가능하다.
```
Future<void> createDescriptions(Iterable<String> objects) async {
    for (final object in objects) {
        try {
            var file = File('$object.txt');
            if (await file.exists()) {
                var modified = await file.lastModified();
                print(
                    'File for $object already exists. It was modified on $modified.')
                continue;
            }
        await file.create();
        await file.writeAsString('Start describing $object in this file.');
        } on IOException catch (e) {
            print('Cannot create description for $object: $e');
        } 
    }
}
```

또한 `async*`을 사용하여 가독성있는 빌드 stream을 구성할 수 있다.
(async*는 제너레이터 함수로 여러개 갑승ㄹ 비동기로 생성할 때 사용한다. return 대신 yield를 사용하여 값을 반환한다.)
async 함수는 비동기 작업을 수행하고 완료 결과를 반환
async*은 비동기로 여러 값을 생성하여 호출자에게 전달한다.
위의 샘플은 for loop를 통해반복적인 작업을 수행하므로 아래와 같이 async*가 사용 가능하다.

```
Stream<String> report(Spacecraft craft, Iterable<String> objects) async* {
    for (final object in objects) {
        await Future.delayed(oneSecond);
        yield '${craft.name} flies by $object';
    }
}
```
## Exceptions

## Important concepts
* null safety를 활성화해두었다면 명시적으로 지정하지 않으면 변수는 null을 포함할 수 없다. 타입 뒤에 ?를 붙이는 것으로 nullable로 선언이 가능하다.
* Dart는 List<Object>와 같은 generic type을 지원한다.
* Dart는 public, protected, private 같은 접근 제한자를 제공하지 않는다. 식별자가 언더스코어로 시작한다면 private으로 간주한다.