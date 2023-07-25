<p align="center">
  <img src="https://github.com/giljihun/Nomad_Dart-Flutter/assets/75918176/593c53fb-1471-461c-96b8-6fe9d0e0fe19" alt="image">
</p>

<p align="center">
다트. 뭐 어쩔
</p>

[0. Why Dart?](#0.-Why-Dart?)

[1. Variables](#1.-Variables)

[2. Data Types](#2.-Data-types)


# #0. Why Dart?

dart 는 두 개의 컴파일러를 가지고 있다

-> **JIT, AOT**

**<JIT 컴파일러>**
dart VM 사용
코드의 결과를 바로 보여준다.
가상머신에서 동작중이라 조금 느리지만 많은 디버깅 옵션도 지원.
**개발중에만 사용하며 배포에는 사용하지 않음.**

**<AOT 컴파일러>**
네이티브(arm, x86, x64), 웹(js)
시스템에 맞게 최적화된 바이너리를 생성하므로 컴파일에 많은 시간이 걸린다.
**최종 배포시 사용.**



* **null safety** 특성을 가진다.

* c나 java에서 null 참조하면 오류 발생.

* flutter, dart 둘 다 google 에서 개발 한 것이다 즉 flutter 의 성능 향상을 위해 dart 를 변경 하는 것도 가능하다.

* flutter 가 처음 나왔을 때 AOT 컴파일러 는 없었다. flutter 팀의 요청에 의해 dart 팀에서 개발 한 것.

<br>
<br>
<br>

# #1. Variables


### #1-1. main함수

**main함수는 모든 Dart 프로그램의 Entry point이다.**
main 함수에서 쓴 코드가 호출된다. **(만약 main이 없다면 실행이 되지 않음)**
**dart는 자동으로 세미콜론을 붙여주지 않기 때문에 직접 붙여야 한다. (일부러 세미콜론을 안 쓸 때가 있기 때문)**



### #1-2. 변수를 만드는 2가지 방법

\```
void main() {
var name = "pizza"; // 방법 1
String name = "chicken"; // 방법 2
name = "chicken ";
}
\```
**함수나 메소드 내부에 지역변수를 선언할 때는 var를 사용하고**
**class에서 변수나 property를 선언할 때는 타입을 지정해준다.**  (Dart Guide에 명시)



### #1-3. Dynamic 타입

여러가지 타입을 가질 수 있는 변수에 쓰는 키워드이다. **(해당 변수의 타입을 알 수 없을 때 주로 사용)**
**변수를 선언할 때 dynamic을 쓰거나 값을 지정하지 않으면 dynamic 타입을 가진다.**
\```
void main(){
dynamic name;
var name2; 
}
\```



### #1-3. Null Safety

개발자가 null 값을 참조할 수 없도록 하는 것이다.
**String뒤에 ?를 붙여줌으로서 name이 String 또는 null이 될 수 있다고 명시해준 것.**
**기본적으로 모든 변수는 non-nullable(null이 될 수 없음).**
\```
void main() {
String? name = "hello";
name = null;
}
\```



### #1-4. final 변수

**var대신 final로 변수를 만들게 되면 이 변수는 수정할 수 없게 된다.**
**자바스크립트의 const랑 비슷하다.**
\```
void main() {
final name = "pizza";
**name = "ham"; // can't do this**

final String username = "tom";
**name = "tom2"; // can't do this**
}
\```



### #1-5. late 변수

**초기 데이터 없이 먼저 변수를 생성하고 추후에 데이터를 넣을 때 주로 사용한다.**
flutter로 data fecthing을 할 때 유용하다.

**Ex) late 변수를 만들고, API에 요청을 보낸 뒤에 API에서 값을 보내주면 그 응답값을 late변수에 넣어 사용할 수 있다.**
\```
void main() {
late final String name;

print(name); // name 변수에 접근 불가 (데이터를 안넣어서. 당연쓰.)
}
\```



### #1-6. const 변수

dart에서 const는 compile-time constant를 만들어준다.

**const는 컴파일할 때 알고 있는 값을 사용해야 한다.**
**만약 어떤 값인지 모르고, 그 값이 API로부터 오거나 사용자가 화면에서 입력해야 하는 값이라면 그건 const가 아닌 final이나 var가 되어야 한다.**

\```
void main() {
const name = "tom"; // 컴파일 시점에 바뀌지 않는 값
final username = fetchAPI(); // 컴파일 시점에 바뀌는 값
}
\```
const: 컴파일 시점에 바뀌지 않는 값 (상수)
final: 컴파일 시점에 바뀌는 값 (API에서 받아온 값, 사용자 입력값)



### #1-7. RECAP

변수를 만드는 2가지 방법
\```dart
void main() {
var name = "pizza"; // 방법 1
name = "chicken ";
String name2 = "chicken"; // 방법 2
}
\```

**final: 값을 재할당하지 못하는 변수를 만듦**
**dynamic type: 어떤 타입의 데이터가 들어올 지 모를 때 사용함**
**const: 컴파일 할 때 값을 알고 있는 변수**
**final: 런타임 중에 만들어질 수 있는 변수**
**late: final, var, String같은 것들 앞에 써줄 수 있는 수식어로서 어떤 데이터가 올 지 모를 때 사용한다.**


<br>
<br>
<br>

# #2. Data types



### #2-1. 기본 데이터 타입

**아래 타입을 포함한 거의 대부분의 타입들이 객체로 이루어져 있다. (함수도 객체)**
**이것이 Dart가 진정한 객체 지향 언어로 불리는 이유이다.**
\```
void main() {
String name = "tom";
bool isPlay = true;
int age = 10;
double money = 52.55;
num x = 12;
num y = 1.2;
}
\```



### #2-2. Lists

dart에서 lists를 선언하는 것은 두 가지 방법이 있다.

\```
void main(){
int case1 = [1,2,3,4,5]; (var도 가능)
List case2 = [1,2,3,4,5];
}
\```
**dart의 유용한 점은 `collection if`와 `collection for`을 지원하는 것.**

**collection if를 사용하면 `존재할 수도 안할 수도 있는 요소를 가지고 올 수 있다.`**

\```dart
void main(){
var giveMeSix = true;
int case1 = [
1,
2,
3,
4,
5,
if(giveMeSix) 6,
];
// 아래와 같은 기능.
if(giveMeSix){
case1.add(6);
}
}
\```



### #2-3. String interpolation(문자열 보간)

$달러 기호를 붙이고 사용할 변수를 적어주면 된다.
만약 무언가를 계산하고 싶다면 ${ } 형태로 적어주면 된다.
\```
void main(){
var name = "tom";
var age = 10;
var greeting = "hello $name, I'm ${age + 5}";
}
\```



### #2-4. Collection For

Dart는 조건문(if) 및 반복(for)을 사용하여 컬렉션을 구축하는 데 사용할 수 있는 컬렉션 if 및 컬렉션 for도 제공합니다.

**컬렉션이란 List, Set, Map, ... 이런 애들을 말함!**

\```
void main() {
var oldFriends = ["nico", "lynn"];
var newFriends = [
"tom",
"jon",
for (var friend in oldFriends) "❤️ $friend",
];

print(newFriends); // [tom, jon, ❤️ nico, ❤️ lynn]
}
\```



### #2-5. Maps

일반적으로 맵은 key와 value를 연결하는 객체입니다. 

키와 값 모두 모든 유형의 객체가 될 수 있습니다. 

각 키는 한 번만 발생하지만 동일한 값을 여러 번 사용할 수 있습니다.

\```
var gifts = {
// Key: Value
'first': 'partridge',
'second': 'turtledoves',
'fifth': 'golden rings'
};

// Map 생성자를 사용하여 동일한 객체를 만들 수 있습니다.
var gifts2 = Map();
gifts2['first'] = 'partridge';
gifts2['second'] = 'turtledoves';
gifts2['fifth'] = 'golden rings';
\```

> 여기서도 var로 변수를 만드는데 아주 유용하긴 한듯..

### #2-6. Sets

Set에 속한 모든 아이템들이 유니크해야될 때 사용한다.
유니크할 필요가 없다면 List를 사용하면 된다.
\```
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};
\```

> **Dart에서 set에 순서가 있다.**
> **print({1,2,3}=={3,2,1}); ---> false**
> **파이썬은 True.**

