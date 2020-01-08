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

### 1.1.2 이름과 환경

프로그래밍 언어로 표현하는 것 중에 가장 중요한 일이 계산 객체 computational object에 다른 이름을 붙이는 것이다. 이 때 이름은 `상수 constant`라고 하고, 계산 객체는 변수의 `값 value`이라고 한다. 참고로 `변수 variable`에 대해서는 뒤에 다시 설명한다.

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

### 1.1.3 조합combinations 표현 실행하기

절차대로 일하는 순서를 정하는 데 고려해야 할 것들을 정리하고 있다. 

조합 표현을 실행하는 순서는 다음과 같다.
1. 조합 표현에서 부분 표현을 먼저 실행한다
2. (스위프트 기준) 조합 표현에서 가운데 있는 표현이 연산을 위한 프로시저이고, 나머지 표현이 인자에 해당하는 값이 된다. 인자 값에 대해 프로시저를 적용해서 조합 표현의 값을 계산한다. 

앞에서 설명했던 것처럼 부분 표현에 대한 값을 계산할 때도 같은 절차를 따른다. 반복해서 조합 표현을 계산하다보면 자연스럽게 귀납법recusive이 된다. 귀납법은 특정한 단계에서 동일한 반복해서 규칙을 다시 따르게 된다. 

이렇게 깊이 겹쳐서 중첩된 표현식을 반복해서 계산하는 절차가 복잡한 절차를 단순하게 만드는 데 도움을 준다. 

```swift
(2 + (4 * 6)) * ((3 + 5) + 7)
```

실제로 스위프트 실행기에 위의 코드를 입력하면 컴파일러 에러가 나오거나 실행이 10초 넘게 걸린다. 이유는 컴파일러가 타입 추론하는 데 실패하기 때문이다. 다음과 같이 Int() 타입이라는 것을 명시적으로 표시해야 제대로 동작한다.

```swift
Int(2 + (4 * 6)) * Int((3 + 5) + 7)
```

이 식을 그림1.1처럼 나무 모양 Tree로 표현하면, 부분 표현식을 계산하는 프로세스가 잘 드러난다. 

![1.1 조합 표현에 대한 값을 모두 펼쳐 보여주는 그림](https://github.com/godrm/SICP-Swift/blob/master/images/1.1.png?raw=true)

나무 모양에서 계산해야 하는 값은 가지branch로, 연산자는 마디node로, 가장 끝에 나오는 마지막 마디 terminal node에는 숫자와 연산자를 표시한다. 앞에서 설명한 조합 표현 계산 프로세스로 설명해보면 나무 마지막 마디부터 차례차례 윗 단계로 올라가며 계산한다. 그러면서 같은 절차를 여러 번 반복하는 귀납적인 재귀recursion로 계산한다. 

나무 그림 마지막 마디에 위치한 숫자나 내장 연산자built-in operator 표현 식을 계산할 때 규칙을 살펴보자.

- 숫자 표현식 값은 여러 숫자가 모인 값
- 내장 연산자 값은 해당 연산자가 의미하는 계산 동작을 미리 조합해 놓은 명령들
- 나머지 다른 이름 값은 `환경`에 지정해 놓은 객체 

여기서 핵심은 환경에 따라서 표현 식에서 사용하는 이름에 대한 의미가 달라질 수 있다는 것이다. 스위프트 실행기에서 `x`라는 이름이나 `+`라는 연산 이름을 정의하지 않았다면 아무런 의미가 없다. 3장에서 프로그램 실행을 위한 문맥 context를 결정하는 환경에 다시 설명한다. 

지금까지 설명한 계산 규칙으로는 표현식에 이름을 붙이지는 못한다. `let pi = 3.141592` 표현에서 `let`이라는 프로시저가 있어서 pi 와 3.141592 인자 값으로 계산한다는 것이 아니다. let은 pi라는 이름으로 값을 대신할 뿐이다. 

계산을 위한 규칙만으로 값을 계산하지 못하기 때문에 계산 규칙을 설명해 놓는 문법이 필요한다. 이런 문법을 특별한 형태 special form이라고 부른다. let만 설명을 했지만 앞으로 여러 종류의 표현식을 보게 된다. 이런 표현식들을 모아서 프로그래밍 언어의 문법syntax을 만든다. 

### 1.1.4 복합 프로시저 compound procedure

지금까지 훌륭한 프로그래밍 언어가 갖고 있는 요소들을 정리했다. 복잡한 절차를 포함하는 복합적인 연산을 요약해서 다른 이름을 붙이는 `프로시저 만들기`에 대해 알아볼 차례다. 

`제곱`을 어떻게 표현하는지로 설명한다. 제곱하는 계산 방식을 말로 설명하면 '어떤 값을 제곱하는 것은 같은 값을 두 번 곱한다.'는 말이다. 이 말을 코드로 표현해보자.

```swift
func square(_ x : Int) -> Int { x * x }
```

위의 코드를 풀어서 읽어보면 다음과 같이 해석할 수 있다. 영어와 달리 한국어는 어순이 반대라서 읽기 어려운 측면도 있다. 

![1.2 프로시저 문법](https://github.com/godrm/SICP-Swift/blob/master/images/1.2.png?raw=true)


이렇게 선언하면 이미 있던 다른 프로시저를 요약하고 합쳐서 `square`라는 이름으로 복합 프로시저가 생긴다. 이 프로시저는 정의한 데로 같은 값을 두 번 곱해서 제곱을 계산한다. 위에 정의한 코드를 읽어보면, 곱할 값을 x라는 지역 이름local name으로 부른다. 이런 표현은 평소에 사용하는 자연 언어에서 대명사와 비슷한 표현이다. 

프로시저를 선언하는 과정은 두 단계로 인지해야만 한다. 이름이 없는 상태로 새로운 복합 프로시저를 만드는 것과 이렇게 만든 프로시저에 `square`라는 이름을 붙이는 두 단계를 구분해야 한다. 나중에는 이름이 없는 프로시저만 만들어서 사용하기도 한다. 

프로시저를 선언하는 문법은 다음 형식이다. 

```swift
func <name>(<formal parameters>) {
<body>
}
``` 

<name>은 환경에서 프로시저를 구분하는 이름Symbol이다.
<formal parameters>는 프로시저가 넘겨받는 인자를 구분하는 지역 이름들이다.
<body>는 프로시저를 부를 때마다 계산하는 규칙을 표현한다. 프로시저에 인자를 넘기면 지역에만 있는 인자 이름을 해당 값으로 바꾼 다음에 계산해서 값을 구한다. 
<formal parameters>는 () 소괄호로 구분하고, <body>는 {} 중괄호로 구분한다.
프로시저를 부를 때는 <body>는 생략하고 () 괄호에 인자 값만 전달한다. 

```swift
square(21)
$R0: Int = 441

square(2 + 5)
$R1: Int = 49

square(square(3))
$R2: Int = 81
```

square를 만들면서 *라는 기본 연산 프로시저를 사용한 것처럼 square도 다른 프로시저를 정의할 때 사용할 수도 있다. 

```swift
func sumOfSquares(x: Int, y: Int) -> Int { 
    square(x) + square(y) 
}

sumOfSquares(x: 3, y:4)
$R3: Int = 25
```

더 확장해보면 sumOfSquares도 다른 프로시저를 정의할 때 사용할 수 있다.

```swift
func foo(a: Int) -> Int {
    sumOfSquares(x: a+1, y: a*2)
}

foo(a: 5)
$R4: Int = 136
```

### 1.1.5 교체 방식substitution model로 프로시저 실행하기



## <a name="head1.2"></a> 1.2 Procedures and the Processes They Generate



## <a name="head1.3"></a> 1.3 Formulating Abstractions



