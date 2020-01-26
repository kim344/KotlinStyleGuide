Kotlin Style Guide
=================


Kotlin 코드를 이해하기 쉽고 명확하게 작성하기 위한 스타일 가이드입니다.  

본 문서에 나와있지 않은 규칙은 아래 문서를 따릅니다.

- [Kotlin Coding Conventions](https://kotlinlang.org/docs/reference/coding-conventions.html)

- [Kotlin 스타일 가이드](https://developer.android.com/kotlin/style-guide)

# 목차

- [소스 파일](#소스-파일)

    - [이름 지정](#이름-지정)
    - [특수문자](#특수문자)
    - [구조](#구조)

- [형식 지정](#형식-지정)
    - [중괄호](#중괄호)
    - [공백](#공백)
    - [특정 구성](#특정-구성)
    - [문서](#문서)

## 소스 파일
---

- 모든 소스 파일은 UTF-8로 인코딩되어야합니다.

### 이름 지정

- 소스 파일에 최상위 클래스가 하나 뿐인 경우 파일 이름에 대소문자를 구분하는 이름과 `.kt` 확장자가 반영되어야 합니다.  
 그렇지 않고 소스 파일에 최상위 수준 선언이 여러 개 있는 경우 파일의 내용을 설명하는 이름을 선택하고 PascalCase를 적용한 다음 `.kt`확장자를 추가합니다.

```kotlin
// MyClass.kt
class MyClass { }
```
```kotlin
// Bar.kt
class Bar { }
fun Runnable.toBar(): Bar = // ...
```
```kotlin
// Map.kt
fun <T, O> Set<T>.map(func: (T) -> 0): List<O> = // ...
fun <T, O> List<T>.map(func: (T) -> 0): List<O> = // ...
```
### 특수문자

#### 공백 문자

`ASCII 수평 공백 문자(0x20)`는 줄 마침 표시 시퀀스를 제외하고 소스 파일의 모든 부분에 나타나는 유일한 공백문자입니다. 이 내용의 의미는 다음과 같습니다.
- 문자열과 문자 리터럴의 모든 다른 공백 문자는 이스케이프 처리됩니다.    

- 탭 문자는 들여쓰기에 사용되지 않습니다.

#### 특수 이스케이프 시퀀스

특수 이스케이프 시퀀스가 있는 모든 문자의 경우 (`\b`,`\n`,`\r`,`\t`,`\'`,`/"`,`\\`,`\$`)이 시퀀스가 해당하는 유니코드(예: `\u000a\`) 이스케이프 대신 사용됩니다.

#### 비ASCII 문자
나머지 비ASCII 문자의 경우 실제 유니 코드 문자(예: `∞`) 또는 동등한 유니코드 이스케이프(예: `\u221e`)가 사용됩니다. 코드를 
**쉽게 읽고 이해할 수 있도록**
선택해야 합니다. 유니코드 이스케이프는 모든 위치의 인쇄 가능한 문자에 권장되지 않으며 문자열 리터럴 및 주석 외부에서 사용하지 않는 것이 좋습니다.  

|예|토론|
|:-----------------------------------|:-----------|
| val unitAbbrev = "μs"    | 최고: 주석 없이도 완벽하게 이해됩니다.|
| val unitAbbrev = "\u03bcs" // μs	|나쁨: 이스케이프를 인쇄 가능한 문자와 함께 사용할 이유가 없습니다.|
| val unitAbbrev = "\u03bcs"`	|나쁨: 독자가 이해할 수 없습니다.|
|return "\ufeff" + content	|좋음: 인쇄할 수 없는 문자에 이스케이프를 사용하고 필요한 경우 주석으로 처리합니다.|

### 구조

`.kt`파일은 다음과 같은 순서로 구성됩니다.

- 저작권 및/또는 라이선스 헤더(선택사항)

- 파일 수준 주석

- Package 문

- Import문

- 최상위 수준 선언

빈 줄을 하나만 사용하여 각 섹션을 구분합니다.

#### 저작권/라이선스

파일에 저작권 또는 라이선스 헤더가 포함된 경우 맨 위에 여러 줄로 주석을 넣어야 합니다.

```
/*
 * Copyright 2017 Google, Inc.
 *
 * ...
 */
```

`KDoc 스타일` 또는 한 줄 주석을 사용하지 마세요.

```
 /**
  * Copyright 2017 Google, Inc.
  *
  * ...
  */
```

```
 // Copyright 2017 Google, Inc.
 //
 // ...
```

#### 파일 수준 주석

`user-site target` 파일을 포함하는 주석은 헤더 주석과 패키지 선언 사이에 배치됩니다.

#### Package 문

package 문은 열 제한을 받지 않으며 줄바꿈되지 않습니다.

#### Import 문

클래스, 함수 및 속성의 import 문은 단일 목록으로 그룹화되고 ASCII 정렬됩니다.

모든 유형의 와일드 카드 가져오기는 
**허용되지 않습니다.**

package 문과 마찬가지로 import 문은 열 제한을 받지 않으며 줄바꿈되지 않습니다.

#### 최상위 수준 선언

`.kt` 파일은 최상위 수준에서 하나 이상의 유형, 함수, 속성 또는 유형 별칭을 선언할 수 있습니다.  

파일의 내용은 단일 테마에 중점을 두어야 합니다. 예를 들어 여러 수신기 유형에 관해 동일한 연산을 실행하는 확장 함수 집합 또는 단일 공개 유형이 있습니다. 관련 없는 선언은 자체 파일로 분리되어야 하며 단일 파일 내 공개 선언은 최소화되어야 합니다.

파일 콘텐츠의 수와 순서에는 명시적인 제한이 적용되지 않습니다.

소스 파일은 일반적으로 위에서 아래로 읽습니다. 즉, 일반적으로 순서가 더 높은 선언을 이해하면 순서가 더 낮은 선언을 이해할 수 있도록 순서가 지정됩니다. 파일에 따라 콘텐츠의 순서를 다르게 지정할 수 있습니다. 마찬가지로 세 개의 파일에 각각 속성 100개, 함수 10개, 클래스 1개를 포함할 수 있습니다.

각 클래스에서 
**특정한**
논리적 순서를 사용한다는 것이 중요합니다. 요청이 있으면 유지관리 담당자가 설명해 드릴 수 있습니다. 예를 들어 새 함수가 클래스의 끝에 습관적으로 추가되지 않습니다. 그러면 논리적 순서가 아닌 `'추가가된 날짜순'`으로 순서가 지정되기 때문입니다.

#### 클래스 멤버 정렬

클래스 내 멤버의 순서는 최상위 수준 선언과 동일한 규칙을 따릅니다.

## 형식 지정

---

### 중괄호

`else if/else` 분기가 없고 한 줄에 들어가는 `when` 분기 및 `if`문 본문에는 중괄호가 필요하지 않습니다.

```kotlin
if (string.isEmpty()) return

when (value) {
    0 -> return 
    // ...
}
```

`if`,`for`,`when` 분기, `do` 및 `while`문의 경우 본문이 비어 있거나 단일 문만 포함하는 경우에도 중괄호가 필요합니다.

```kotlin
if (string.isEmpty())
    return // WRONG!

if (string.isEmpty()){
    return // Okay
}
```

#### 비어 있지 않은 블록

비어 있지 않은 블록과 블록 형식 구문의 경우 중괄호는 K&R(Kermighan and Ritchie) 스타일 (`'이집트 대괄호'`)을 따릅니다.

- 여는 중괄호 앞에 줄바꿈이 없습니다.

- 여는 중괄호 뒤에 줄바꿈이 있습니다.

- 닫는 중괄호 앞에 줄바꿈이 있습니다.

- 중괄호로 구문이 종료되거나 함수, 생성자 또는 named 클래스의 본문이 종료되는 경우에만 닫는 중괄호 뒤에 줄바꿈이 있습니다. 예를 들어 중괄호 뒤에 `else`또는 쉼표가 오는 경우 중괄호 뒤에 줄바꿈이 `없습니다`.

```kotlin
return Runnable {
    while (condition()){
        foo()
    }
}

retrun object : MyClass(){
    override fun foo(){
        if(condition()){
            try {
                something()
            } catch (e: ProblemException){
                recover()
            }
        } else if (otherCondition()){
            somethingElse()
        } else{
            lastThing()
        }
    }
}
```

다음은 `enum` 클래스에 대한 몇 가지 예외입니다.

#### 빈 블록

빈 블록 또는 블록 형식 구문은 K&R 스타일이어야 합니다.

```kotlin
try{
    doSomething()
} catch (e: Exception) {} // WRONG!
```

```kotlin
try{
    doSomething()
} catch (e: Exception) {

} //Okay
```

#### 표현식

표현식으로 사용되는 `if/else` 조건문에서는 전체 표현식이 한 줄에 들어가는 경우에만 중괄호를 생략할 수 있습니다.

```kotlin
val value = if (string.isEmpty()) 0 else 1 // Okay
```

```kotlin
val value = if (string.isEmpty()) // WRONG!
                0
            else
                1
```

```kotlin
val value = if (string.isEmpty()) { // Okay
    0
} else {
    1
}
```

#### 들여쓰기

새 블록 또는 블록 형식 구문이 열릴 때마다 들여쓰기가 4칸씩 증가합니다. 블록이 끝나면 들여쓰기가 이전 들여쓰기 수준으로 돌아갑니다. 들여쓰기 수준은 블록 전체에서 코드와 주석에 모두 적용됩니다.

#### 한 줄에 한 구문

각 문 다음에 줄바꿈이 옵니다. 세미콜론은 사용되지 않습니다.

#### 줄바꿈

코드의 열 제한은 100자입니다. 아래 언급된 경우를 제외하고 아래 설명된 대로 이 제한을 초과하는 줄은 줄바꿈 되어야 합니다.

예외:

- 열 제한을 준수할 수 없는 줄(예:KDoc의 긴 URL)

- `package` 및 `import` 문

- 잘라서 셀에 붙여넣을 수 있는 주석의 명령줄

#### 줄바꿈 위치

우선적으로 줄바꿈은 더 높은 구문 수준에서 하는 것이 좋습니다. 기타정보:

- 비대입 연산자에서 줄이 끊기면 기호 앞에서 줄바꿈됩니다.

    - 이는 다음 `'연산자 형식'`기호에도 적용됩니다.

    - 점 구분자(`.`)

    - 멤버 참조의 두 콜론(`::`)

- 대입 연산자에서 줄이 끊기면 기호 뒤에서 줄바꿈됩니다.

- 메서드 또는 생서자 이름은 뒤에 오는 열린 관호( `'('` )에 연결된 상태로 유지됩니다.

- 쉼표(`','`)는 앞에 오는 토큰에 연결된 상태로 유지됩니다.

- 람다 화살표(`'->'`)는 앞에 오는 인수 목록에 연결된 상태로 유지됩니다.

```
★ 참고:줄바꿈의 기본 목표는 코드를 명확히 보여주는 것이며, 코드를 최대한 적은 수의 줄에 표시할 필요는 없습니다.
```

#### 함수

함수 서명이 한 줄에 들어가지 않으면 각 매개변수 선언을 한 줄에 하나씩 표시합니다. 이 형식으로 정의된 매개변수에서는 단일 들여쓰기(+4)를 사용해야 합니다. 닫는 괄호(`')'`)및 반환 유형은 추가 들여쓰기 없이 한 줄에 하나씩 입력됩니다.

```kotlin
fun <T> Iterable<T>.joinToString(
    separator : CharSequence = ", ",
    prefix: CharSequence = "",
    postfix: CharSequence = ""
): String {
    // ...
}
```

##### 표현식 함수

함수에 표현식이 하나만 포함되는 경우 `식 함수`로 표현될 수 있습니다.

```kotlin
override fun toString(): String {
    return "Hey"
}
```

```kotlin
override fun toString(): String = "Hey"
```

식 함수가 블록을 여는 경우에만 이 함수를 여러 줄로 줄바꿈해야 합니다.

```kotlin
fun main() = runBlocking{
    // ..
}
```

그렇지 않은 경우 식 함수가 증가하여 줄바꿈이 필요한 경우 일반 함수 본문, `return`선언 및 일반 식 줄바꿈 규칙을 대신 사용합니다.

#### 속성

속성 이니셜라이저가 한 줄에 들어가지 않을 경우 등호(`'='`)뒤에서 줄바꿈하고 들여쓰기를 사용합니다.

```kotlin
private val defaultCharset: Charset? =
        EncodingRegistry.getInstance().getDefaultCharsetForPropertiesFiles(file)
```

`get`및/또는 `set` 함수를 선언하는 속성은 일반 들여쓰기(+4)를 적용하여 한 줄에 하나씩 입력해야 합니다. 함수와 동일한 규칙을 사용하여 형식을 지정합니다.

```kotlin
var directory: File? = null
    set(value) {
        // ...
    }
```

읽기 전용 속성에서는 한 줄에 들어가는 더 짧은 구문을 사용할 수 있습니다.

```kotlin
val defaultExtension: String get() = "kt"
```

### **공백**

#### 수직

빈 줄이 하나 표시됩니다.

- 클래스의 연속하는 멤버 `사이`:속성, 생성자, 함수, 중첩 클래스 등

    - **예외**: 두 개의 연속하는 속성 사이에 다른 코드가 없는 경우 두 속성 사이의 줄바꿈은 선택사항입니다. 그런 줄바꿈은 속성의 논리적 그룹을 만들고 속성을 지원 속성(있는 경우)과 연결하는 데 필요한 경우에 사용됩니다.

    - **예외**:열거형 상수 사이의 줄바꿈은 아래에서 설명합니다.

- 코드를 논리 하위 섹션으로 구성하는데 `필요한 경우`식 사이에 줄바꿈을 넣습니다.

- 함수의 첫 번째 문 앞, 클래스의 첫 번째 멤버 앞 또는 클래스의 마지막 멤버 뒤에 `선택적으로` 줄바꿈을 넣습니다(권장하지도 권장하지 않지도 않음).

- 이 문서의 다른 섹션(예: 구조 섹션)에 필요한 경우에 줄바꿈을 넣습니다.

여러 개의 빈 줄을 연속으로 사용할 수 있지만 권장하지 않으며 필요하지도 않습니다.

#### 수평

언어 또는 다른 스타일 규칙에 필요한 경우와 리터럴, 주석 및 KDoc를 제외하면 단일 ASCII 공백이 다음 위치에만 표시됩니다.

- 예약어(예: `if`, `for` 또는 `catch`)는 해당 줄에서 뒤에 오는 여는 괄호(`'('`)와 구분됩니다.

```kotlin
// WRONG!
for(i in 0..1){
}
```

```kotlin
// Okay
for (i in 0..1){
}
```

- 예약어(예: `else` 또는 `catch`)는 해당 줄에서 앞에 오는 닫는 중괄호(`'}'`)와 구분됩니다.

```kotlin
// WRONG!
}else {
}
```

```kotlin
// Okay
} else {
}
```

- 여는 중괄호(`'{'`) 앞

```kotlin
// WRONG!
if (list.isEmpty()){
}
```

```kotlin
// Okay
if (list.isEmpty()){
}
```

- 2진 연산자의 양쪽

```kotlin
// WRONG!
val two = 1+1
```

```kotlin
// Okay
val two = 1 + 1
```

이는 다음 `'연산자 형식'`기호에도 적용됩니다.

- 람다 식의 화살표(`'->'`)

```kotlin
// WRONG!
ints.map { value->value.toString() }
```

```kotlin
// Okay
ints.map { value -> value.toString() }
```

단, 다음은 제외:

- 멤버 참조의 두 콜론(`'::'`)

```kotlin
// WRONG!
val toString = Any :: toString
```

```kotlin
// Okay
val toString = Any::toString
```

- 점 구분자(`'.'`)

```kotlin
// WRONG!
it . toString()
```

```kotlin
// Okay
it.toString()
```

- 범위 연산자(`'..'`)
```kotlin
// WRONG
for (i in 1 .. 4) print(i)
```

```kotlin
// Okay
for (i in 1..4) rpint(i)
```

- 기본 클래스 또는 인터페이스를 지정하기 위해 클래스 선언에 사용된 경우나 일반 제약조건의 `where`절에 사용된 경우에만 콜론(`':'`)앞에 줄바꿈을 넣습니다.

```kotlin
// WRONG!
class Foo: Runnable
```

```kotlin
// Okay
class Foo : Runnable
```

```kotlin
// WRONG
fun <T: Comparable> max(a: T, b: T)
```

```kotlin
// Okay
fun <T : Comparable> max(a: T, b: T)
```

```kotlin
//WRONG
fun <T> max(a: T, b: T) where T: Comparable<T>
```

```kotlin
// Okay
fun <T> max(a: T, b: T) where T : Comparable<T>
```

- 쉼표(`','`)또는 콜론(`':'`) 뒤

```kotlin
// WRONG!
val oneAndTwo = listOf(1,2)
```

```kotlin
// Okay
val oneAndTow = listOf(1, 2)
```

```kotlin
// WRONG!
class Foo :Runnable
```

```kotlin
// Okay
class Foo : Runnable
```

- 줄 끝 주석을 시작하는 이중 슬래시(`'//'`)의 양쪽 여러 개의 공백이 허용되지만 필수는 아닙니다.

```kotlin
// WRONG!
var debugging = false//disabled by default
```

```kotlin
// Okay
var debugging = false // disabled by default
```

이 규칙은 행의 시작 부분이나 끝 부분에 추가 공백이 필요하거나 금지되는 것으로 해석되지 않으며, 내부 공백만 설명합니다.

### **특정 구성**

#### Enum 클래스

함수와 상수에 대한 문서가 없는 열거형은 필요에 따라 한 줄로 서식 지정할 수 있습니다.

```kotlin
enum class Answer { YES, NO, MAYBE }
```

열거형의 상수가 별도의 줄에 배치되는 경우 상수가 본문을 정의하는 경우를 제외하고 빈 줄이 필요하지 않습니다.

```kotlin
enum class Answer {
    YES,
    NO,

    MAYBE {
        override fun toString() = """¯\_(ツ)_/¯"""
    }
}
```

enum 클래스는 클래스이므로 모든 다른 클래스 서식 지정 규칙이 적용됩니다.

#### 주석

멤버 또는 유형 주석은 주석 처리된 구문 바로 앞에 별도의 줄로 입력됩니다.

```kotlin
@retention(SOURCE)
@Target(FUNCTION, PROPERTY_SETTER, FIELD)
annotation class Global
```

인수가 없는 주석은 한 줄로 입력할 수 있습니다.

```kotlin
@JvmField @Volatile
var disposable: Disposable? = null
```

인수가 없는 주석이 하나만 있는 경우 선언과 동일한 줄에 입력할 수 있습니다.

```kotlin
@Volatile var disposable: Disposable? = null

@Test fun selectAll() {
    // ...
}
```

#### 암시적 변환/속성 유형

식 함수 본문 또는 속성 이니셜라이저가 스칼라 값이거나 반환 유형을 본문에서 명확히 추론할 수 있는 경우 생략할 수 있습니다.

```kotlin
override fun toString(): String = "Hey"
// becomes
override fun toString() = "Hey"
```

```kotlin
private val ICON: Icon = IconLoader.getIcon("/icons/kotlin.png")
// becomes
private val ICON = IconLoader.getIcon("/icons/kotlin.png")
```

라이브러리를 작성할 때 명시적 유형 선언은 공개 API의 일부인 경우에만 유지됩니다.

### 이름 지정

식별자에는 ASCII 문자와 숫자만 사용하며, 아래 언급된 소수의 경우에는 밑줄로 표시됩니다. 따라서 각 유효 식별자 이름은 정규 표현식 `/w+`과 일치합니다.

예제 `name`,`mName`,`s_name` 및 `kName`에 표시된 것과 같은 특수 접두사 또는 접미사는 지원 속성의 경우를 제외하고 사용되지 않습니다.

#### 패키지 이름

패키지 이름은 모두 소문자이며 연속 단어는 밑줄 없이 연결됩니다.

```kotlin
// Okay
package com.example.deepspace
// WRONG!
package com.example.deepSpace
// WRONG!
package com.example.dee_space
```

#### 유형 이름

클래스 이름은 Pascal표기법으로 작성되며 일반적으로 명사 또는 명사구입니다. 예를 들면 `Character` 또는 `ImmuableList`가 있습니다. 또한 인터페이스 이름은 명사 또는 명사구(예: `List`)이지만, 형용사 또는 형용사구(예: `Readable`)를 대신 사용하는 경우도 있습니다.

테스트 클래스의 이름은 테스트 중인 클래스의 이름으로 시작하고 `Test`로 끝납니다. 예를 들면 `HashTest` 또는 `HashIntegrationTest`가 있습니다.

#### 함수 이름

함수 이름은 camel표기법으로 작성되며 일반적으로 동사 또는 동사구 입니다. 예를 들면 `sendMessage`또는 `stop`이 있습니다.

이름의 논리적 구성 요소를 구분하기 위해 테스트 함수 이름에 밑줄을 표시할 수 있습니다.

```kotlin 
@Test fun pop_emptyStack() {
    // ...
}
```

#### 상수 이름

상수 이름에는 UPPER_SNAKE_CASE(모두 대문자)를 사용하며 밑줄로 단어를 구분합니다. 상수란 정확히 무엇일까요?

상수는 맞춤 `get` 함수가 없는 `val` 속성이며 내용을 세부적으로 변경할 수 없고 함수에 감지할 수 있는 부작용이 없습니다. 여기에는 변경할 수 없는 유형과 이 유형의 변경할 수 없는 컬렉션뿐만 아니라 스칼라와 문자열도 포함됩니다(`const`(으)로 표시된 경우). 인스턴스의 관찰 가능한 상태가 변경될 수 있는 경우 해당 인스턴스는 상수가 아닙니다. 객체를 변경하지 않으려는 것만으로는 충분하지 않습니다.

```kotlin
const val NUMBER = 5
val NAMES = listOf("Alice", "Bob")
val AGES = mapOf("Alice" to 35, "Bob" to 32)
val COMMA_JOINER = Joiner.on(",") // Joiner is immutable
val EMPTY_ARRAY = arrayOf()
```

이러한 이름은 일반적으로 명사 또는 명사구입니다.

상수 값은 `object` 내부 또는 최상위 선언으로만 정의할 수 있습니다. 상수의 요구 사항을 충족하지만 `class`의 내부에 정의된 값은 상수가 아닌 이름을 사용해야 합니다.

스칼라 값인 상수는 `const`변경자를 사용해야 합니다.

#### 상수가 아닌 이름

상수가 아닌 이름은 camel표기법으로 작성됩니다. 이는 인스턴스 속성, 로컬 속성, 매개변수 이름에 적용됩니다.
```kotlin
val variable = "var"
val nonConstScalar = "non-const"
val mutableCollection: MutableSet = HashSet()
val mutableElements = listOf(mutableInstance)
val mutableValues = mapOf("Alice" to mutableInstance, "Bob" to mutableInstance2)
val logger = Logger.getLogger(MyClass::class.java.name)
val nonEmptyArray = arrayOf("these", "can", "change")
```

이러한 이름은 일반적으로 명사 또는 명사구입니다.

##### 지원 속성

지원 속성이 필요한 경우 밑줄 처리된 접두사를 제외하고 이름이 실제 속성의 이름과 정확히 일치해야 합니다.

```kotlin
private var _table: Map? = null

val tabe: Map
    get() {
        if (_table == null) {
            _table = HashMap()
        }
        return _table ?: throw AssertionError()
    }
```

#### 유형 변수 이름

각 유형 변수의 이름은 다음 두 스타일 중 하나로 지정됩니다.
- 단일 대문자, 필요에 따라 단일 숫자가 뒤에 옴(예:`E`,`T`,`X`,`T2`)

- 클래스에 사용된 형식으로 된 이름, 대문자 `T`가 뒤에 옴(예: `RequestT`, `FooBarT`)

#### 카멜 표기법

영어 구를 카멜 표기법으로 합리적으로 변환할 수 있는 다양한 방법이 있습니다.(예: 'IPv6','iOS'와 같은 두문자어 또는 일상적이지 않은 구성이 있는 경우). 예측 가능성을 개선하려면 다음 스키마를 사용합니다.

구문 형식의 이름으로 시작:

1. 구문을 일반 ASCII로 변환하고 모든 아포스트로피를 삭제합니다. 예를 들어 'Müller’s algorithm'이 'Muellers algorithm'으로 변환될 수 있습니다.

2. 공백 및 나머지 구두점(일반적으로 하이픈)에서 분할하여 이 결과를 단어로 나눕니다. **권장**:단어에 일반적인 용도의 카멜 표기법이 이미 있는 경우 이 단어를 구성요소로 분할합니다. 예를 들어 
'AdWords'는 'ad words'로 분할됩니다. 'iOS'와 같은 단어는 실제로 카멜 표기법이 아니며, 어떤 규칙도 따르고 있지 않으므로 이 권장 사항이 적용되지 않습니다.

3. 모두 소문자(두문자어 포함)인 경우 다음 중 하나를 수행합니다.

    - 파스칼 표기법을 적용하려면 각 단어의 첫 글자를 대문자로 시작합니다.

    - 카멜 표기법을 적용하려면 첫 단어를 제외한 각 단어의 첫 글자를 대문자로 시작합니다.

4. 마지막으로 모든 단어를 단일 식별자로 결합합니다.

원래 단어의 대소문자는 거의 무시됩니다.

|구문 형식|올바름|올바르지 않음|
|:-------|:----|:-----------|
|'XML HTTP 요청'|XmlHttpRequest|XMLHTTPRequest|
|'새 고객 ID'|newCustomerId|newCustomerID|
|'내부 스톱워치'|innerStopwatch|innerStopWatch|
|'iOS에서 IPv6 지원'|supportsIpv60nIos|supportsIPv60nIOS|
|'YouTube 가져오기 도구'|YouTubeImporter|YoutubeImporter*|  

(* 허용되지만 권장되지 않음)  

```
★ 참고:영어에서 일부 단어는 하이폰으로 모호하게 연결되어 있습니다. 예를 들어 'nonempty'와 'non-empty'가 모두 올바르므로 checkNonempty 및 checkNonEmpty' 메서드 이름도 모두 올바릅니다.
```

### 문서

#### 형식 지정

다음 예제에는 KDoc블록의 기본 형식이 나와 있습니다.

```kotlin
/**
 * Multiple lines of KDoc text are written here,
 * wrapped normally...
 */
 fun method(arg: String) {
     // ...
 }
```
 
 다음은 단일 행의 예입니다.

```kotlin
 /** An especially short bit of KDoc. */
```

기본 형식은 항상 허용됩니다. 주석 마커를 포함하여 전체 KDoc 블록이 한 줄에 들어가는 경우 단일 줄 형식이 대체될 수 있습니다. 이는 블록 태그가 없는 경우(예: `@return`)에만 적용됩니다.

##### 단락

단일 공백 행,즉 정렬될 선행 별표(`'*'`)만 포함하는 행은 단락 사이와 블록 태그 그룹(있는 경우) 앞에 표시됩니다.

##### 블록 태그

사용된 표준 '블록 태그'는 `@constructor`, `@receiver`, `@param`, `@property`, `@return`, `@throws`, `@see` 순으로 표시되며, 빈 설명으로 표시되지 않습니다. 블록 태그가 한 줄에 들어가지 않는 경우 연속된 줄은 `@` 위치에서 4칸 들여쓰기 됩니다.
 
#### 요약 프래그먼트

각 KDoc 블록은 요약 프래그먼트로 시작합니다. 이 프래그먼트는 클래스, 메서드 색인과 같은 특정 컨텍스트에 표시되는 텍스트의 유일한 부분이므로 매우 중요합니다.

프래그먼트는 명사구 또는 동사구이며 전체 문장이 아닙니다. '`A 'Foo' is a...`'또는 '`This method returns...`'로 시작하지 않고 완전한 명령문(예: `Save the record.`)을 형성할 필요도 없습니다. 하지만 프래그먼트는 전체 문장인 것처럼 대문자 및 구두점 처리됩니다.

#### 사용

최소한 KDoc은 모든 `public` 유형과 그런 유형의 모든 또는 `protected` 멤버에 제공되며, 아래와 같은 몇 가지 예외가 있습니다.

##### 예외: 설명이 필요 없는 함수

'foo 반환'을 제외하고 실제로 달리 언급할 가치가 없는 경우 KDoc는 '단순하고 명확한'함수(예: `getFoo`) 및 속성(예:`foo`)에 대한 선택사항입니다.

이 예외를 인용하여 일반적인 독자가 알아야 하는 관련 정보 생략을 정당화하는 것은 적절하지 않습니다. 예를 들어 `getCanonicalName`함수 또는 `cononicalName` 속성에서 일반 독자가 '표준 용어'의 의미를 모를 수도 있는 경우 `//* Returns the canonical name. */`이라고 하는 근거를 알려주는 문서를 생략해서는 안 됩니다.

##### 예외:재정의

KDoc가 상위 유형 메서드를 재정의하는 메서드에 항상 존재하는 것은 아닙니다.