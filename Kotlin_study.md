# Kotlin</br>
형변환 : 하나의 변수에 지정된 자료형을 다른 자료형으로 변경하는 기능 <br/>
명시적 형변환: 변환될 자료형을 개발자가 직접 지정함<br/>
암시적 형변환: 변수 할당 시 자료형을 지정하지 않아도 자동으로 형변환 가능
<br/>
## 배열
```
var intArr = arrayOf(1,2,3,4,5)
```
배열에 들어갈 값 저장<br/>
```
var nullArr = arrayOfNulls<Int>(5)
``` 
크기가 5이고 null값으로 채워진 배열 생성
<>안에 배열에 할당할 자료형 지정
처음 선언 시 전체크기 변경이 불가능하지만 한번 선언해두면 빠른 입출력이 가능함.

<br/>

## 반복문
- do while: 최초한번은 do에서 조건없이 실행한 후 while로 조건체크
	-> 반드시 한번 실행해야하는경우에 사용
- for문
증가값을 1이아닌 다른값으로 정하기 step사용
```
for(i in 0..9 step 3){} 0 -> 3 -> 6 -> 9
```

- 흐름제어<br/>
  break : 반복문 내의 구문이 실행되는 중간에 즉시 반복문 종료<br/>
continue : 다음 반복조건으로 즉시 넘어가는 역할
다중 반복문에서 사용시 레이블 지정 후 모든 반복문에 continue 또는 break 적용 가능
  
  ```
  loop@for (i in 1..10){
	  for(j in 1..10){
    if(i == 1 && j == 2) break@loop
		  }
	    }
  ```
  
레이블이 달린 반복문을 기준으로 즉시 break함

<br/>

## 클래스<br/>
- '값'과 그 값을 사용하는 '기능'들을 묶어놓은 것<br/>
- 인스턴스를 만드는 틀이다<br/>
	- 인스턴스 : 클래스를 이용해서 만들어내는 서로 다른 속성의 객체를 지칭하는 용어<br/>
- 클래스 생성자 : 새로운 인스턴스를 만들기 위해 호출하는 특수한 함수<br/>
	- init : 인스턴스 생성시 구문을 수행하는 기능<br/>
	- this : 인스턴스 자신의 속성이나 함수를 호출하기 위해 클래스 내부에서 사용되는 키워드<br/>
	- 기본 생성자 : 클래스를 만들 때 기본으로 선언<br/>
	- 보조 생성자 : 필요에 따라 추가적으로 선언, 기본 생성자와 다른형태의 생성자 제공 인스턴스 생성 시 편의 제공 및 추가적인 기능 수행, constructor 사용<br/>
- 보조 생성자를 만들 때는 반드시 기본 생성자를 통해 속성을 초기화 해줘야 함<br/>
- 보조 생성자가 기본 생성자를 호출하도록 하려면 콜론(:) 을 붙인 후 this 라는 키워드를 사용하고 기본 생성자가 필요로 하는 파라미터를 괄호안에 넣어주면 됨<br/>
```
    class Person(var name: String, val birthYear: Int){
	    init{}
	  constructor(name: String): this(name, 1997) //기본 생성자가 필요로하는 파라미터를 괄호안에 넣음 
```
사용시
```
	fun main(){
		var a = Person("박보영", 1990) //기본 생성자 사용
		var d = Person("이루다") //보조 생성자 사용, 보조 생성자 사용시 init 구문 실행후 constructor 구문 실행함
```

=> 기본 생성자, 보조 생성자를 이용해 다양한 방법으로 인스턴스를 생성하는 법을 제시함으로써 편의를 제공함

<br/>

## 클래스의 상속
- 상속이 필요한 경우: 이미 존재하는 클래스를 확장하여 새로운 속성이나 함수를 추가한 클래스를 만들어야 할때, 여러개의 클래스를 만들었을때, 클래스들의 공통점을 뽑아 코드 관리를 편하게 해야할 때
- 수퍼 클래스 : 속성과 함수를 물려주는 역할
- 서브 클래스 : 물려받는 역할 
- 수퍼 클래스 역할을 하기위해서는 클래스 생성시 open을 붙여주어야함<br/>
```
open class Animal (var name: String, var age: Int){}
```

- 상속시 규칙 : 서브클래스는 수퍼클래스에 존재하는 속성과 '같은 이름'의 속성을 가질 수 없음 , 서브 클래스가 생성될 때 반드시 수퍼클래스의 생성자까지 호출해야함
- 서브클래스 : 클래스 선언 뒤에 콜론(:)을 붙이고 수퍼 클래스의 생성자를 호출할 수 있도록 해주면 됨<br/>
```
class Dog (name: String, age: Int) : Animal ( name, age, "개") // var 또는 val 사용X, 콜론뒤에 수퍼 클래스의 생성자 호출
```

사용시<br/>
```
fun main(){
	var a = Animal("별이",5,"개")
	var b = Dog("별이",5)
	a.introduce()
	b.introduce()	//Dog 클래스에서도 Animal 클래스를 상속받았기 때문에 Animal 클래스 내에있는 함수 사용가능
}
```

=> 클래스의 상속은 클래스를 더 구조적으로 다룰 수 있게 해줌 but 지나친 상속구조는 코드를 더 어렵게만듦

<br/>

## 오버라이딩
- 서브클래스에서 수퍼클래스와 같은 이름과 형태로 된 함수의 내용을 다시 구현가능<br/>
  - Animal 클래스를 상속받는 Tiger클래스 생성
``` 
	open class Animal {
		open fun eat(){	//open을 사용하면 오버라이드가 가능해짐
			println("음식을 먹습니다.")
			}
		}
	class Tiger : Animal() {
		override fun eat(){		//오버라이드를 통해 똑같은 함수 재정의 가능
			println("고기를 먹습니다")
			}
		}
```

<br/>

## 추상화
- 선언부만 있고 기능이 구현되지 않은 추상함수, 추상함수를 포함하는 추상클래스로 구성<br/>
```
abstract class Animal{
	abstract fun eat()
}
```
- 추상클래스는 미완성 클래스이기 때문에 단독으로는 인스턴스를 만들 수 없음, 따라서 반드시 서브클래스에서 상속을 받아 abstract표시가 된 함수들을 구현해줘야함<br/>
```
class Rabbit : Animal(){		//Animal 클래스 상속받음
	override fun eat(){		//abstract 함수 오버라이드하고 구현
		println("당근을 먹습니다")
		}
	}
```

<br/>

## 인터페이스
- 추상함수, 일반함수, 속성으로 이루어짐 but 인터페이스는 생성자를 가질 수 없음, 구현부가 있는 함수 -> open 함수로 간주
- 구현부가 없는 함수 -> abstract 함수로 간주<br/>
	-> 인터페이스 내의 모든 함수를 서브클래스에서 구현 및 재정의 가능
	-> 한번에 여러 인터페이스를 상속받을 수 있음

<br/>

## 스코프(범위)
- 패키지 내부 / 클래스 내부 / 함수 내부
- 스코프 규칙 : 스코프 외부에서는 스코프 내부의 멤버를 '참조연산자(.)'로만 참조가능, 동일 스코프 내에서는 멤버들 '공유' 가능, 하위 스코프에서는 상위 스코프의 멤버 재정의 가능
- 접근제한자 : 스코프 외부에서 스코프 내부에 접근할 때 그 권한을 제어할 수 있는 기능
	-> public, internal, private, protected
- 패키지 스코프 : public(기본값) - 어떤 패키지에서도 접근 가능, internal - 같은 모듈 내에서만 접근 가능, private - 같은 파일 내에서만 접근 가능
- 클래스 스코프 : public(기본값), private - 클래스 내부에서만 접근 가능, protected - 클래스 자신과 상속받은 클래스에서만 접근 가능

<br/>

## 람다함수
- 함수를 변수형태로 사용 가능, 컬렉션의 조작이나 스코프 함수의 사용에도 도움이 됨<br/>
```
fun main(){
	var a = {str: String -> println("${str}")}	//타입 자동추론
	a("hello")
	}
```

<br/>

## 스코프 함수
- 함수형 언어의 특징을 더 편리하게 사용할 수 있도록 기본 제공하는 함수들
  - apply, run, with, also, let<br/>

```
class Book(var name: String, var price: Int){
	fun discount(){
		price -= 200
	}
}

fun main(){
	var price = 5000

	var a = Book("코틀린",10000).apply{	// apply를 사용하면 변수가 생성되자마자 조작된 인스턴스를 변수에 바로 넣어줄 수 있음
		name = "[초특가]" + name
		discount()		//참조 연산자 없이 사용가능
		}

	var b = Book("코틀린",10000).also{	// also는 apply와 역할이 유사하지만 it을 사용함으로써 인스턴스내의 속성에만 접근하도록 한다
		it.name = "[초특가]" + it.name
		discount()		
		}

	a.run{
		println("상품명: ${name}, 가격: ${price}원")	// run은 반환값을 가지는 특성이 있음
	}
	a.let{
		println("상품명: ${it.name}, 가격: ${it.price}원")	// it을 사용함으로써 price가 main함수에 선언된 변수가아닌 인스턴스내의 price속성을 가르키고있음을 알려줌
	}
}
```

=> 스코프함수는 인스턴스의 속성이나 함수를 scope 내에서 깔끔하게 분리하여 사용할 수 있다는 점 때문에 코드의 가독성 향상가능

<br/>

## object
- 생성자없이 직접 객체를 만들어냄, 여러개의 객체가 필요하지않을때 사용 <br/>
-> 싱글톤 패턴으로 인스턴스를 단 하나만 만들어 사용하도록 하는 패턴<br/>
```
object Counter{
	var count = 0
	fun countUp(){
		count++
	}
}
fun main(){
	println(Counter.count)	//따로 변수를 만들지않고 object를 그대로 가져와서 사용가능
	Counter.countUp()
```

=> 오브젝트로 선언된 객체는 최초 사용시 자동으로 생성되며 이후에는 코드 전체에서 공용으로 사용 가능
- companion object : 클래스의 인스턴스 기능은 그대로 사용하면서 인스턴스간에 공용으로 사용할 속성 및 함수를 별도로 만드는 기능<br/>
```
class FoodPoll (val name: String){
	companion object{
		var total = 0
	}
	var count = 0
	fun vote(){
		total++
		count++
	}
}
fun main(){
	var a = FoodPoll("짜장")
	var b = FoodPoll("짬뽕")
	}
```
=> FoodPoll 클래스의 count 변수는 인스턴스변수가 생성될때 마다 0으로 초기화되지만 total 변수는 공유하고있는 값이므로 초기화 되지않음

<br/>

## 옵저버 패턴
- 인터페이스를 사용하여 클래스간의 신호를 주고받음<br/>
```
interface EventListner{
	fun onEvent(count: Int)
}

class Counter(var listner: EventListner){		//신호를 발생시킴
	fun count(){
		for(i in 1..100){
			if(i%5 == 0) listner.onEvent(i)	// 조건에 만족할때마다 이벤트를 실행시킴

class EventPrinter: EventListner{	// onEvent 함수가 실행되면 기능을 수행하는 역할
	override fun onEvent(count: Int){	// 인터페이스의 추상함수를 재정의함
		print("${count}-")
		}
```

<br/>

## 컬렉션
- Set : List와 달리 순서가 정렬되지 않으며 중복 허용이 되지 않음 => 인덱스를 통해 객체 참조 불가, contains로 set안에 데이터가 존재하는지 확인만 가능
- Map : 객체를 넣을때 그 객체를 찾아낼 수 있는 Key를 쌍으로 넣어주는 컬렉션, key,value로 구성, 같은 key에 새로운 value를 넣으면 기존의 객체가 대체됨<br/>
```
val a = mutableMapOf("레드벨벳" to "음파음파")	// key와 value를 to로 연결시킴
```

### 컬렉션 함수
- 컬렉션에 일반함수 또는 람다 함수 형태를 사용하여 for문 없이도 컬렉션 내 아이템 순회하며 참조가능, 구조 변경도 가능<br/>
```
collection.forEach{	// forEach를 사용하여 컬렉션 내 모든 아이템 순서대로 참조 가능
	println(it)
	}

collection.filter{		// filter를 사용하여 컬렉션 내 아이템 중 조건에 맞는 값만 반환
	it < 4
	}```

collection.map{		// 컬렉션 내에 값들을 조건대로 변경함
	it*2
	}

collection.any { it == 0}	// 하나라도 조건에 맞으면 true
collection.all { it == 0}	// 모두 조건에 맞으면 true
collection.none { it == 0}	// 하나도 조건에 맞지 않으면 true

collection.first()	// 첫번째 객체 반환(조건이 있는경우 조건에 맞는 첫번째 객체 반환)
collection.last()	// 마지막 객체 반환
객체가 없는경우를 대비해 firstOrNull / lastOrNull 사용
collection.count()	// 모든 객체의 수 반환
```

=> 컬렉션 함수 사용 시 반복문 및 조건문을 대체가능하다는 장점이 있다

```
collection.associateBy{it.name}	// 객체에서 key를 추출하여 map으로 변환하는 함수, 여기에선 name이 key가 됨
collection.groupBy{it.name}		// 객체에서 특정 값을 key로 추출하여 해당 값을 가진 객체끼리 묶는것
collection.partition{it.birthYear > 2002}	// 조건에 따라 true, false 그룹으로 나눔, 두 그룹은 Pair의 first,second가 됨

collection.flatMap{
	listOf(it*3, it+3)	// 아이템마다 새로운 컬렉션을 생성하면 이를 합쳐서 하나의 컬렉션으로 반환함
}
collection.getOrElse(1){50}	// () 안의 값(1)이 컬렉션의 인덱스(1) 에 존재할경우 그 값을 반환하고 없을경우 {50} 을 그 인덱스에 넣음
collection1 zip collection2	// 두 컬렉션에 포함된 아이템을 1:1 로 Pair 클래스의 객체로만들어 List에 넣어 반환함, List의 개수는 크기가 작은 컬렉션의 크기를 따라감
```

<br/>

## 문자열을 다루는 함수<br/>
```
fun main(){
	val test1 = "Test.Kotlin.String"

	test1.length	// 문자열의 크기 반환
	test1.toLowerCase()	//문자들을 소문자로 변환
	test1.toUpperCase()	//문자들을 대문자로 변환

	val test2 = test1.split(".")	// .을 기준으로 문자열을 나눠서 배열에 담음
	test2.joinToString()		// 배열의 문자열을 합침, ()안에 특정 문자가 있다면 이 문자를 넣어 합침
	
	test1.substring(5..10)	// 5번째부터10번째까지 문자만 반환
	test1.isNullOrEmpty()	// 문자열이 Null이거나 비어있으면 true 반환(공백(ex.) space, Tab 등)을 비어있는 상태로 보지않음)
	test1.isNullOrBlank()	// 문자열이 Null이거나 비어있으면 true 반환(공백을 비어있는 상태로 봄)

	test1.startsWith("Te")	// 문자열이 Te로 시작할시 true반환
	test1.endsWith("ng")	// 문자열이 ng로 끝날시 true반환
	test1.contains("kotlin")	// 문자열이 kotlin 포함시 true반환
}
```
<br/>

## 동기 / 비동기
- 동기 : 요청한 결과가 한 자리에서 동시에 일어남, 결과가 주어질 때 까지 아무것도 못하고 대기해야함
- 비동기 : 요청과 결과가 동시에 일어나지 않음, 결과가 주어지는데 시간이 걸리더라도 그 시간 동안에 다른 작업을 할 수 있음
