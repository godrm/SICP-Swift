## 1장. 프로시저로 요약하는 방식 (Building Abstractions with Procedures)

```
The acts of the mind, wherein it exerts its power over simple ideas, are chiefly these three: 
1. Combining several simple ideas into one compound one, and thus all complex ideas are made. 
2. The second is bringing two ideas, whether simple or complex, together, and setting them by one another so as to take a view of them at once, without uniting them into one, by which it gets all its ideas of relations. 
3. The third is separating them from all other ideas that accompany them in their real existence: this is called abstraction, and thus all its general ideas are made.

—John Locke, An Essay Concerning Human Understanding (1690)
```

생각(아이디어)에 대한 인용문으로 시작한다. 인간은 단순한 생각들을 합쳐서 복합적인 생각으로 만들기도 하며, 단순하거나 복잡한 생각을 펼쳐놓고 관계를 살펴보기도 한다. 그리고 복잡한 생각이나 실체를 분리하고, 간추려서 요약(추상화, Abstraction)하기도 한다. 이 글은 추상화(Abstraction)에 대한 인지를 위해서 인용한 것 같다.

`추상화`라는 단어는 말 그대로 추상적이다. 복잡한 실체를 감추고 요약되어 있기 때문에 추상화 과정을 거친 표현은 구체적인 정보를 포함하지 않는다. 사람들이 뇌에서 떠올린 개념을 각자의 언어로 표현하는 순간에도 이미 말과 글로 요약되기 마련이다. 

이 책은 `추상화`라는 용어를 인용하면서 시작한다. 특히 번역서는 특히 한글로 풀어쓰는 경향이 강하기 때문에  추상화라는 한자어보다는 요약, 간추린 표현이 더 자주 등장한다. 이제 본문을 좀 더 읽어보자.

### 앞부분

#### 용어 정리 

##### 계산 프로세스 computational process 와 프로그램 Program

- 컴퓨터 내부에서 데이터를 조작하면서 하는 어떤 작업(일)
- 개발자가 지정해놓은 규칙을 따라 동작한다.
- 이 규칙의 묶음을 프로그램 Program 이라고 한다.

프로그램은 여러 개의 표현식 Symbolic expression을 포함하고, 각 표현식을 작성할 때 사용하는 언어를 프로그래밍 언어라고 한다.

##### 프로그램은 위험한가

프로그램을 작성하는 일 자체가 위험하지는 않지만, 프로그램을 사용하는 기계가 사람을 위험하게 만들 수도 있다. 
그래서 안전과 연결되는 일을 하는 기계에 들어가는 프로그램은 지식과 경험이 많은 개발자가 주의깊게 작성하도록 한다. 
책에 나오는 것처럼 산업 인프라 혹은 비행기, 기차에서 사용하는 프로그램의 기준은 훨씬 높다.

#### 리스프 Lisp과 스킴 Scheme

Lisp은 `LISt Processing` 리스트 처리라는 말의 약자로, 기호로 이루어진 데이터를 다루기 편리하도록 설계했다.
기계가 처리할 프로세스를 표현하기 위해 선택한 언어는 Lisp 계통의 스킴 Scheme 

이 책에서 Lisp 계열 언어를 중심으로 설명하는 이유는 다음과 같은 표현이 나온다.

```
The importance of this is that there are powerful program-design techniques that rely on the ability to blur the traditional distinction between “passive” data and “active” processes. As we shall discover, Lisp’s flexibility in handling procedures as data makes it one of the most convenient languages in existence for exploring these techniques. The ability to represent procedures as data also makes Lisp an excellent language for writing programs that must manipulate other programs as data, such as the interpreters and compilers that support computer languages.
```

바로 능동적인 `프로세스`와 수동적인 `데이터`를 구분하는 일반적인 절차지향 프로그래밍 방식보다 `프로시저(또는 함수)`를 `데이터`처럼 다룰 수 있는 유연한 언어적인 특성 때문이다.
이런 특징은 객체지향 패러다임과 함수형 패러다임을 모두 갖춘 현대적인 언어들에서도 공통적으로 찾아볼 수 있는 장점이다. 
그래서 이 글에서는 마찬가지 기준으로 스위프트를 활용해서 설명하려고 한다.

덧붙여서 Swift로 프로그램을 작성하는 과정도 매우 즐거운 일이다. 

### 목차

[1.1 The Elements of Programming](#head1.1)

[1.2 Procedures and the Processes They Generate](#head1.2)

[1.3 Formulating Abstractions](#head1.3)


## <a name="head1.1"></a> 1.1 프로그래밍할 때 필요한 것들 The Elements of Programming

프로그램을 표현하기 좋은 언어는 단지 컴퓨터가 할 일을 표현하는 것이 아니다. 프로그래밍 언어가 표현할 수 있는 방법이 다양하면, 컴퓨터가 처리할 프로세스에 대한 개발자의 생각을 적절하게 표현할 수 있다. 간단한 생각들을 모아서 복잡한 생각을 표현하는 방식으로 프로그래밍 언어 활용하는 것에 집중해보자. 

훌륭한 언어들은 다음과 같은 매커니즘을 제공한다.

- 기초 표현 primitive expressions : 언어에서 가장 단순한 것들을 표현

- 조합 수단 means of combination : 간단한 것들을 합쳐서 복잡한 것을 만듦

- 추상화 수단 means of abstraction : 복잡한 것에 이름을 붙여 요약 

우리는 프로그래밍 과정에서 `프로시저`와 `데이터`를 다룬다. 현대 언어에서는 엄밀하게 두 개를 구분할 필요가 없어지고 있는 추세다. 특히 스위프트나 코틀린, 러스트처럼 최근에 만들어진 훌륭한 언어들이 많아졌다. 

데이터와 프로시저 모두 기초 표현으로 활용할 수 있고, 데이터나 프로시저 여러 개를 합쳐서 조합할 수도 있다. 1장에서는 주로 프로시저 관섬에서 데이터를 다루는 방식을 설명한다.

### 1.1.1 표현식 Expressions

프로그래밍을 배우기 시작하기 좋은 방법으로 그 언어 개발 환경을 직접 실행해보는 것이다. 터미널에서 바로 스위프트 코드를 넣으면 실행할 수 있는 환경이나 웹 브라우저에서도 바로 코드를 실행할 수 있는 환경이 많아있다. 직접 스위프트 표현식을 넣으면, 표현식을 계산 evaluating 해서 결과를 표시해 준다. 

10진수 같은 숫자 값을 표현하는 식도 기초 표현 중에 하나다. 스위프트 REPL에 숫자 값을 넣으면 값을 그대로 출력한다. Xcode Playground 나 iPad Playground 에서도 출력값을 확인할 수 있다. 

```swift
486
$R0: Int = 486
```

숫자 값을 나타내는 표현식에 `+`, `-` 같은 사칙 연산을 위한 기호를 덧붙여서 조금더 복잡한 조합을 표현할 수 있다. `숫자에 연산 기호를 적용 application한다`는 의미로 읽는다.

```swift
137 + 349
$R1: Int = 486

1000 - 334
$R2: Int = 666

5 * 99
$R3: Int = 495

10 / 5
$R4: Int = 2

2.7 + 10
$R5: Double = 12.699999999999999
```

스위프트에서는 이렇게 연산할 데이터 - 피연산자 operand와 계산을 위한 프로시저 - 연산자 operator를 조합해서 조합식 combination을 만들 수 있다. 조합식에 대한 계산 결과는 프로시저에 해당하는 연산자에 계산할 인자값 argument를 적용해서 계산한다.

원문에서는 Lisp 기반으로 설명하기 때문에 앞쪽 표기 prefix notation 방식으로 되어 있지만, 스위프트에서 연산은 수학 표기 방식과 비슷한 중간 표기 infix notation 방식이다. 

Lisp처럼 앞쪽 표기를 사용하면 인자가 많아져도 그대로 적용할 수 있다는 장점이 있다. 스위프트에서는 중간 표기 방식을 사용하기 때문에 할 수 없다.

```lisp
(+ 21 35 12 7)
> 75

(+25 4 12)
> 200
```

스위프트에서는 표현식이 다음과 같이 달라진다. `+` 연산자 표기를 더 많이 반복해서 표현해야만 한다.

```swift
21 + 35 + 12 + 7
$R6: Int = 75
```

이렇게 연산자가 많아지는 경우에는 여러 겹으로 엮어서 처리해야 하는 경우가 생길 수 있다. 

```swift
(3 * 5) + (-10 + 6)
$R7: Int = 11
(3 * ((2 * 4) + (3 + 5))) + ((10 - 7) + 6)
$R8: Int = 57
```

표현식이 깊어져서 겹쳐써도 실행기는 전혀 실수없이 동작한다. 괄호를 정확하게 계산하는 단위를 묶어서 표시하면 충분하다. 반면에 사람은 조금만 식이 복잡해지면 실수로 계산을 틀릴 가능성이 있다. 실제로 이 예시를 작성하면서도 2번이나 잘못 입력했다.

```swift
(3 * 
    ( (2 * 4) +
        (3 + 5)
    )
) +
    ( (10 - 7) +
        6
    )
```

사람이 표현식을 읽을 때 도움을 주기 위해서 인자를 중심으로 줄을 맞추고 알맞게 들여쓰는 방식을 예쁜 출력 pretty-printing 이라고 한다. 실행기는 표현식이 어떻게 쓰여있더라도 상관없이 표현식을 읽고, 계산하고, 출력하는 일을 되풀이 read-eval-print loop 한다. 터미널에서 코드를 입력하고 바로바로 실행결과를 알려주는 환경을 `REPL`라고 부른다. 

1.1.2 이름과 환경

프로그래밍 언어로 표현하는 것 중에 가장 중요한 일이 계산 객체 computational object에 다른 이름을 붙이는 것이다. 이 때 이름은 `상수 constant`라고 하고, 계산 객체는 변수의 `값 value`이라고 한다. 

```swift
let size = 2
size: Int = 2
```

이렇게 size라는 이름으로 2라는 값을 (다른 이름으로) 나타낼 수 있다. 
아래처럼 여러 가지 값에 다른 이름을 붙일 수도 있다.

```swift
let pi = 3.141592
pi: Double = 3.1415920000000002

let radius = 10.0
radius: Double = 10

pi * (radius * radius)
$R0: Double = 314.1592

let circumference = 2 * pi * radius
circumference: Double = 62.83184
```

이렇게 `let`을 사용하면 `circumference`라는 이름으로 둘레를 계산하는 복합 연산compound operation을 다르게 표현할 수 있다. 컴퓨터 하드웨어나 소프트웨어 프로그램은 값이나 표현식을 다 풀어서 복잡하게 쓰기 보다는, 조금 덜 복잡한 내용을 합쳐서 더 복잡한 것으로 만든다. 

이렇게 어떤 값에 기호symbol로 이름을 붙였다가 다시 그 이름으로 이전에 지정한 값을 찾아서 사용할 수 있다는 것은 REPL 실행기에 이름과 값을 짝지어서 저장하는 기억장치memory가 있다는 의미다. 이런 기억장치를 `실행 환경environment`라고 하고, 여기서 실행 환경은 가장 바깥쪽에 있는 전체 환경global environment을 의미한다. 책 뒷부분에서 계산 과정에서 사용하는 환경이 여러 개 더 있다는 것을 알게 된다.

1.1.3 조합 combination 표현



## <a name="head1.2"></a> 1.2 Procedures and the Processes They Generate



## <a name="head1.3"></a> 1.3 Formulating Abstractions



