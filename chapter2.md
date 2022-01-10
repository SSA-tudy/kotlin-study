# 1. 코틀린이란 무엇이며, 왜 필요한가?

## 💡Question

1. (64p) 타입으로 변수 선언을 시작하면 타입을 생략할 경우 식과 변수 선언을 구별할 수 없다의 의미는?
- 자바에선 int a = 10이런식으로, 코틀린에서 생략하고 a = 10 대입인지, 새로운 변수 할당인지 구분할 수 없다
- 파이썬
    - 식 = 값으로 대체되는 것
    - 문장 = 값으로 대체되지 않는 것
- 자바 Person 클래스 있고, 인스턴스 하나 만들면 Person p = new Person(); 이러는데 new Person(); 치면 식
- 예를들어 val answer: Int = 42 이러면 Int생략 해도 되고 안해도 되고, 앞에 하면 모호해질듯?

<br>

2. (65p) 변수의 타입 추론 시 double 타입의 0을 할당하고 싶으면 0.0을 대입해야하나?
- yes


<br>


3. (66p) (자바에서는 final 키워드를 사용하면 변수 선언과 동시에 반드시 초기화를 해줘야 했지만) 코틀린은 val을 사용해서 변수를 선언할 때 선언과 대입을 분리해도 될까?
- 함수 내에서는 가능


<br>

4. (69p) JavaBean 클래스란?
- 특별한 종류의 POJO
- [https://2jinishappy.tistory.com/324](https://2jinishappy.tistory.com/324)

<br>

---

5. (72p) private 접근 제한자가 있어도 공개된 getter, setter를 모두 가지면 public과 다를 게 없다. 코틀린은 심지어 프로퍼티에 직접 접근할 수 있다. 캡슐화를 더 잘 구현하려면 어떻게 해야할까?
- [https://codechacha.com/ko/kotlin-property/](https://codechacha.com/ko/kotlin-property/)
- private 변수는 getter/setter 생성 x
- val은 getter만

<br>

6. (60p)함수 파라미터에 var, val을 안 붙이면 어떻게 될까
- 인수로 var 넣으면 함수 내에서 val로 바뀜
- 자바 메소드로 넘겨주는 방식 공부(call by value)

<br>

7. (81p) when 구문을 사용할 때 setOf로 동등성을 판단한다고 했다. 동등성 vs 동일성의 차이, Set collection이 아니어도 동등성으로 판단할까?
- [역스경](https://github.com/SSA-tudy/kotlin-study/blob/main/%EC%BD%94%ED%8B%80%EB%A6%B0%EC%97%90%EC%84%9C%EC%9D%98%20when%20%EC%8B%9D%EC%97%90%20%EB%8C%80%ED%95%B4.md)
