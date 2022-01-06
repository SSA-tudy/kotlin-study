# 코틀린에서의 when 식에 대해
<br>

## 동등성
> 동등성 : 타입마다 다르지만, 대부분의 타입은 인스턴스 내부의 값들이 모두 같다면 동등하다고 한다!
> 
>
> [동일성과 동등성 참고 링크](https://joont.tistory.com/143)
<br><br>

### 자바에서의 동등성

- 자바에서 동등성은 `o1.equals(o2)` 메소드 또는 `Objects.equals(o1, o2)` 메서드로 확인할 수 있다.
```java
Object a = new Person("경운");
Object b = new Person("경운");

System.out.println(a.equals(b)); // Person 클래스에 equals 메소드가 재정의 되어있냐 아니냐에 따라 결과가 다름!
```
- 어떤 클래스가 equals() 메소드를 재정의하지 않았다면,
  가장 상위 클래스인 Object 클래스의 equals() 메소드를 그대로 상속받게 되고,
  이 경우 `두 객체가 완전히 같은 지 - 주소 비교(동일성)`를 비교하게 된다!

<br><br>

### 코틀린에서의 동등성
- 코틀린에서의 동등성은 `o1.equals(o2)` 메소드 또는, `==` 연산자로 확인할 수 있다
  자바에서는 `==` 연산자가 동일성을 비교하지만, 코틀린에서는 동등성을 비교한다! (코틀린에서 동일성은 `===` 연산자)

  ```kotlin
  val a: String = "apple"
  val b: String = "apple"
  
  println(a.equals(b)) // true
  println(a == b) // true
  println(a === b) // false
  ```
- 코틀린에서도 어떤 클래스가 equals() 메소드를 재정의하지 않았다면,
  가장 상위 클래스인 Any 클래스의 equals() 메소드를 그대로 상속받게 되고,
  이 경우 `두 객체가 완전히 같은 지 - 주소 비교(동일성)`를 비교하게 된다!
- 코틀린에서 equals() 메소드를 override 하는 법

  ```kotlin
  class TestClass(val num: Int) {
      override fun equals(others: Any?): Boolean {
          // equals 동작 로직 구현 예시
          return if(other is TestClass)
          	other.num == this.num
          else
          	false
      }
  }
  ```
<br><br>

### 대표적인 타입들의 동등성

> 이 부분은 자바/코틀린 기준으로 작성했습니다!
> <br>
> 
> (코틀린의 모든 컬렉션 API는 자바의 컬렉션 API와 동일합니다! - 코인액 104-105p)
<br>

1. String: 두 문자열의 내용이 완전히 같다면 동등하다.

   ```java
   // example
   
   String a = "apple";
   String b = "apple";
   
   System.out.println(a.equals(b)); // true
   System.out.println(Objects.equals(a, b)); // true
   ```
<br>

2. List<T>: 각 인덱스에 해당하는 내용(객체)들끼리 모두 서로 `동등` 하다면 동등하다. (당연히 각 리스트의 길이는 같아야 함!)

   ```java
   // example
   
   List<String> a = List.of("apple", "banana", "kiwi");
   List<String> b = List.of("apple", "banana", "kiwi");
   List<String> c = List.of("apple", "kiwi", "banana");
   
   System.out.println(a.equals(b)); // true
   System.out.println(a.equals(c)); // false, 포함하는 내용들은 같지만, 순서가 다르기 때문에 false!
   ```
<br>

3. Set<T>: 비교하는 집합이 비교당하는 집합의 원소들로만 구성되어 있다면 동등하다, 순서 상관 없고 당연히 길이는 서로 같아야 함!

   ```java
   // example
   
   Set<String> a = Set.of("apple", "banana", "kiwi");
   Set<String> b = Set.of("apple", "banana", "kiwi");
   Set<String> c = Set.of("apple", "kiwi", "kiwi");
   
   System.out.println(a.equals(b)); // true
   System.out.println(a.equals(c)); // true, 순서는 다르지만, 구성 원소가 같기 때문에 true
   ```
<br>

4. Map<K, V>: 비교하는 맵이 비교당하는 맵의 `키-값 쌍`들로만 구성되어 있다면 동등하다.

   ```java
   // example
   
   Map<Integer, String> a = Map.of(1, "one", 2, "two", 3, "three");
   Map<Integer, String> b = Map.of(1, "one", 2, "two", 3, "three");
   Map<Integer, String> c = Map.of(1, "one", 2, "two", 3, "three");
   
   System.out.println(a.equals(b)); // true
   System.out.println(a.equals(c)); // true, 순서는 다르지만, 구성 키-값쌍이 같기 때문에 true
   ```

5. Array: `equals() 메소드가 재정의가 되어 있지 않으므로`, 비교하는 배열과 비교 당하는 배열이 완전 같아야 동등

   ```java
   int[] a = new int[] {1, 2, 3};
   int[] b = new int[] {1, 2, 3};
   
   System.out.println(a.equals(b)); // false, 순서와 값이 모두 같아도 두 배열이 다른 객체기 때문에 false
   ```
<br><br>

## 코틀린의 when 식에서의 동등성 사용

> (코틀린 인 액션 - 81p)
>
> 코틀린의 when 식에서 인자 값과 매칭이 되는 값을 찾을 때는, 동등성을 비교하며 찾는다고 한다.



```kotlin
/**

실제로 돌아가는 코드는 아니고, 이해를 돕기 위한 코드입니다.
arg: 	  sampleClass의 instance
	 	  일반적인 로직에서는 whenTest 메서드를 통해 들어온 인자인 num1과 num2로 구성된 컬렉션 또는 객체일 것입니다.
	 
case<n> : SampleClass의 instance
		  
arg에 매칭되는 case를 찾을 때 SampleClass의 equals() 메소드를 사용합니다!
만약 매칭되는 것이 없는 경우 else로 빠집니다!

그리고, 만약 SampleClass가 배열이거나, equals() 메소드가 재정의되지 않은 클래스인 경우,
절대 매칭이 될 수 없기 때문에 항상 else로 빠질 것입니다!
(equals() 메소드가 재정의 되지 않아 동등성을 비교할 때 동일성을 비교하게 되기 때문)

*/

fun whenTest(num1: Int, num2: Int) {
    // 매칭되는 
    when(arg: SampleClass) {
        case1: SampleClass -> println("case1");
        case2: SampleClass -> println("case2");
        case3: SampleClass -> println("case3");
        case4: SampleClass -> println("case4");
        case5: SampleClass -> println("case5");
        ...
        else -> println("case6")
    }
}
```

