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

위의 코드를 풀어서 읽어보면 다음과 같이 해석할 수 있다. 한국어는 영어와 어순이 반대라서 읽기 어렵다. `어떤 값의 제곱을 계산하려면, 그 값을 두 번 곱해서 구한다` 정도로 읽을 수 있다. 

![1.2 프로시저 문법](https://github.com/godrm/SICP-Swift/blob/master/images/1.2.png?raw=true)


이렇게 프로시저를 선언하면 이미 있던 다른 프로시저를 요약하고 합쳐서 `square`라는 이름으로 복합 프로시저가 생긴다. 이 프로시저는 정의한 데로 같은 값을 두 번 곱해서 제곱을 계산한다. 위에 정의한 코드를 읽어보면, 곱할 값을 x라는 지역 이름local name으로 부른다. 이런 표현은 평소에 사용하는 자연 언어에서 대명사와 비슷한 표현이다. 

프로시저를 선언하는 과정은 두 단계로 인지해야만 한다. 이름이 없는 상태로 새로운 복합 프로시저를 만드는 것과 이렇게 만든 프로시저에 `square`라는 이름을 붙이는 두 단계를 구분해야 한다. 나중에는 이름이 없는 프로시저만 만들어서 사용하기도 한다. 

**<노트>**

```
스위프트에서는 이런 계산 절차를 선언한 프로시저를 `함수`라고 부른다. 오래된 프로그래밍 언어 중에서는 명확하게 프로시저와 함수를 구분했다. 특히 2000년대 이후에 사용하는 현대 프로그래밍 언어에서는 프로시저를 그냥 함수라고 부르는 경향이 두드러진다. 파스칼Pascal 같은 언어에서는 리턴값이 없는 절차는 프로시저라고 부르고, 리턴값이 있는 절차는 함수라고 부르기도 한다. 

이 글에서는 원문에서 설명하는 계산 절차를 의미하는 프로시저를 더 강조하기 위해서 프로시저로 표현한다. 
```

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

### 1.1.5 교체 방식substitution model으로 프로시저 실행하기

직접 선언한 프로시저를 실행하는 과정은 기본 연산 프로시저를 실행하는 것과 동일하다. 모든 부분 표현 값을 구한 다음에, 연산자에 인자로 넣고 계산하면 된다. 

복합 프로시저를 적용하는 규칙은 다음과 같다.

> 복합 프로시저를 인자에 맞추는 것은, 프로시저 내부에 있는 모든 매개변수를 인자 값으로 바꾼 다음에 실행하는 것이다. 

`foo(a: 5)` 표현식을 실행하는 과정을 살펴보자.

앞에서 foo() 프로시저 내부는 `sumOfSquares(x: a+1, y: a*2)`로 선언했다. 
여기에 인자값 5는 `sumOfSquares(x: 5+1, y: 5*2)`로 `a` 자리에 값으로 교체된다. 
이렇게 표현식이 sumOfSquares() 라는 연산자와 피연산자 두 개를 합쳐놓은 조합combination이 된다. 마지막 노드에 해당하는 피연산자 표현식부터 값을 계산해서 인자 값으로 결정한다. `5 + 1`은 6이 되고, `5 * 2`는 10이 된다. 이제 sumOfSquares 프로시저에서 인자x는 6, 인자y는 10을 적용한다. sumOfSquares() 함수는 귀납적으로 `square(6) + square(10)` 표현식으로 바뀐다. square() 함수를 다시 적용하면 `(6 * 6) + (10 * 10)`으로 바뀌고, 괄호부터 곱셈을 하고 나면 `36 + 100`으로 바뀐다. 마지막에는 136이 된다. 

프로시저를 적용하면서 교체하는 방식에 대해 설명했다. 하지만 두 가지 꼭지를 짚고 넘어가야 한다.

- 여기서 설명한 교체 방식은 프로시저를 적용 과정을 설명을 위한 것일 뿐이고, 실행기가 정말로 이렇게 동작하는 것은 아니다. 프로시저를 실행하면서 매개 변수를 인자 값으로 문자 그대로 바꾸지는 않는다. 대신 프로시저 지역 환경에 인자 이름을 넣고 계산하는 방식으로 동작한다. 3장과 4장에서 실행기를 만드는 방법을 살펴볼 때 더 깊이 설명한다.

- 책에서는 실행기가 어떻게 동작하는 지 차례대로 보여주다가 5장에 가서 완벽한 실행기와 번역기를 보여준다. 교체 방식은 계산 모형model of computation 중에 하나로, 표현식을 계산하는 과정 evaluation process을 설명하기 위한 출발선일 뿐이다. 이후에는 더 복잡한 계산 방법을 사용하게 된다. 

##### 인자 먼저 계산법 대 순서대로 계산법

바로 앞서 설명한 인자 값부터 먼저 구하는 계산 방식을 '인자 먼저 계산법 applicative-order evaluation' 이라고 한다. 표현식에 대한 값을 구하는 방법이 연산자를 적용하기 전에 모든 인자값을 적용하는 것만 있는 게 아니다. 값이 필요한 상황까지 피연산자를 계산하지 않고 식 자체를 매개변수 대신 바꾸다가 (더 펼치지 못하는) 마지막에 기본 연산으로만 구성한 표현식으로 값을 계산하는 방법도 있다. 순서대로 계산하는 방식으로 계산해보자.

`f(5)`를 프로시저 정의에 따라서 펼쳐보면 다음과 같다. 

```swift
sumOfSquares(x:5 + 1, y: 5 * 2)
square(5 + 1) + square(5 * 2)
(5 + 1)*(5 + 1) + (5 * 2)*(5 * 2)
```

그리고 귀납법을 적용하면 다음과 같다.
```swift
(6 * 6) + (10 * 10)
     36 + 100
        136
```

지금 설명한 계산 절차와 다르지만 결과값은 동일하다. 이처럼 계산식을 끝까지 펼친 다음에 줄이는 계산 방법을 순서대로 계산법 normal-order evaluation 이라고 한다. Lisp 실행기는 인자 먼저 계산법을 적용한다. 

교체 방식으로 계산해서 결과 값을 구할 수 있는 경우에는, 다른 계산 방식을 사용해도 동일한 결과값이 나온다. 그렇지 않은 경우는 연습 문제 1.5에서 확인할 수 있다. 

Lisp은 인자 먼저 계산하는 방식으로 동작한다. 그래서 (5+1)이나 (5*2)처럼 같은 식을 여러 번 반복해서 계산하지 않는다. 그 이유는 더 빠르게 동작하고, 교체 방식으로 동작하지 않는 프로시저가 있을 순서대로 계산하는 방식이 더 복잡하기 때문이다. 하지만 순서대로 계산하는 방식도 가치가 있기 때문에 3장과 4장에서 설명한다. 

### 1.1.6 조건 표현식

조건에 따라서 계산 표현하는 방법을 정리한다. 예를 들어 음수인지, 0인지, 양수인지 조건에 따라 다르게 계산하고 싶을 때 표현하는 방법이 필요하다.

이처럼 경우의 수가 나눠지는 case analysis 경우에 스위프트에서는 switch-case 문법을 사용한다. 

```swift
func abs(x: Int) -> Int {
    switch x {
        case x where x > 0:
            return x
        case x where x < 0:
            return -x
        default:
            return 0
    }
}
```

조건 표현식 중에 switch-case 구문 문법은 다음과 같다.

```swift
switch control expression {
case pattern 1:
    statements
case pattern 2 where condition:
    statements
case pattern 3 where condition,
     pattern 4 where condition:
    statements
default:
    statements
}
```

switch 예약어 다음에는 제어를 위한 표현식 control expression이 있고, 그 아래에는 여러 조건을 case로 표현하는 절cluase이 나온다. 조건 식을 계산하는 방법은 간단하다. 먼저 pattern에 나오는 값을 구하고, control expression과 비교해서 참인지 비교한다. 뒤에 where절이 있는 경우는 condition 조건까지 비교해서 참인 경우에 해당 조건의 statements 표현식을 계산한다. 거짓이면 아래 다음 case 조건으로 내려간다. 마지막까지 조건이 모두 거짓인 경우는 default 구문 아래 statments를 실행한다. 논리식으로 모든 조건을 표현하지 않은 경우는 컴파일러가 에러를 표시한다.

절대값을 계산하는 프로시저를 다른 방식으로 만들어보자.

```swift
func abs(x: Int) -> Int {
    if x < 0 {
        return -x
    }
    else {
        return x
    }
}
```

switch-case 구문과 비슷하지만 조건식을 표현하기 위해 if 구문을 활용할 수 있다. switch-case가 조건이 여러 개인 경우에 사용한다면, if 구문은 조건이 두 개 뿐일 때 사용하기 좋은 문법이다. 물론 아래처럼 if 구문 문법을 보면 switch-case 구문처럼 여러 조건을 비교할 수 있지만, 권장할 만한 표현은 아니다. 

```swift
if condition 1 {
    statements //to execute if condition 1 is true
} else if condition 2 {
    statements //to execute if condition 2 is true
} else {
    statements //to execute if both conditions are false
}
```

실행기가 if 구문 계산할 때 condition 1 조건을 먼저 계산한다. 그 답이 참이라면 {} 괄호 내부 statements를 실행하고, 거짓이면 아래 조건을 계산한다. abs()를 계산하기 위해 사용한 기본 비교 표현과 복잡한 논리나 판단을 할 수도 있다. 논리 연산에 사용하는 기본 연산은 다음과 같이 세 가지가 있다. 

- (`<e1>` **&&** `<e2>` **&&** ... `<en>`)

논리식 <e>를 왼쪽에서 오른쪽으로 차례대로 계산한다. 그 중에 거짓으로 판단하는 <e>가 나오면 and 식은 거짓이 되고, 나머지 <e>값은 계산하지 않는다.

- (`<e1>` **||** `<e2>` **||** ... `<en>`)

논리식 <e>를 왼쪽에서 오른쪽으로 계산한다. 그 중에 참이라 판단하는 <e>가 나오면 or 식은 참이 되고, 나머지 <e>값은 계산하지 않는다. 

- (**!** `<e1>`)

<e>가 참이면 not 식은 거짓을, 거짓이면 참을 뒤집는다.

이 중에서 and 와 or는 다른 프로시저와 다르게 인자가 되는 모든 논리식 값을 구하지 않기 때문에 특별한 형태로 선언해야 한다. 

만약 x가 5보다 크고, 10보다 작은 것을 판단하려면 `(x > 5) and (x < 10)` 처럼 작성한다. 

어떤 수가 다른 수보다 크거나 같은지 판단하는 조건을 프로시저로 선언하면 다음과 같다.

```swift
func >= (x: Int, y: Int) -> Bool {
    return (x > y) || (x == y)
}
```

다른 논리식으로 고쳐보면 이렇게 선언할 수도 있다. 

```swift
func >= (x: Int, y: Int) -> Bool {
    return !(x < y)
}
```

###### 연습문제 1.1

스위프트 실행기에서 아래 표현식들을 차례대로 계산하면 어떤 값이 나오는지 확인한다. 

```swift
  1> 10
$R0: Int = 10
  2> (5 + 3 + 4)
$R1: (Int) = {
  _value = 12
}
  3> (9 - 1)
$R2: (Int) = {
  _value = 8
}
  4> (6 / 2)
$R3: (Int) = {
  _value = 3
}
  5> ((2 * 4) + (4 - 6))
$R4: (Int) = {
  _value = 6
}

  6> let a = 3
a: Int = 3
  7> let b = a+1
b: Int = 4

  8> a + b + (a * b)
$R5: Int = 19
  9> (a == b)
$R6: (Bool) = {
  _value = 0
}

 10> if (b > a) && (b < (a*b)) { b } else { a }
 11> if (b > a) && (b < (a*b)) { print(b) } else { print(a) }
4

 12> switch (a, b) {
 13.    case (4, _): print(6)
 14.    case (_, 4): print(6+7+a)
 15.    default: print(25)
 16. }
16
```

위에 보이는 것처럼 9번까지는 swift 문법으로도 무난하게 표현 가능하다. 
10번처럼 if 구문에 statement 자리에 값만 넣으면 아무것도 출력되지 않는다. {} 내부에 값만 있으면 해당 값을 대체할 뿐, 새로운 값으로 계산하지 않는다. 그래서 11번처럼 실행기에서 값을 확인하고 싶으면 print()라는 프로시저에 인자값으로 전달해야 한다. 

12번 switch-case 구문에서도 마찬가지다. 조건식 뒤에 변수나 상수에 해당하는 값만 넣으면 아무런 동작을 하지 않는다. 특정한 조건식에 따른 결과를 출력하려면 print() 프로시저를 호출해야 한다.

스위프트에서는 if 구문 결과를 다른 연산자에 인자로 넘기는 표현은 불가능하다. 이렇게 값을 넘겨야 하는 경우는 if 구문과 비슷한 삼항 연산자 Ternary Conditional Operator를 사용해야 한다. `condition ? expression used if true : expression used if false` 

```swift
 17> (2 + if (b > a) { b } else { a })
 error: repl.swift:17:6: error: expected expression after operator
(2 + if (b > a) { b } else { a })
     ^

 17> (2 + ((b > a) ? b : a))
$R7: (Int) = {
  _value = 6
}
```

다음과 같이 switch-case 구문도 if 구문과 마찬가지로 다른 연산자에 인자값으로 표현식을 전달할 수는 없다. 지금 a값이 3이고, b값이 4인 상태에서 19번처럼 a가 switch-case 구문을 대체해서 `a * (a + 1)`로 처리하지 않는다. 다음과 같이 컴파일 에러가 난다.

```swift
 18> switch (a,b) {
 19. case (a,b) where a>b: a
 20. case (a,b) where a<b: b
 21. default: -1
 22. } * (a + 1)
error: repl.swift:22:2: error: consecutive statements on a line must be separated by ';'
} * (a + 1)
 ^
 ;

error: repl.swift:22:3: error: unary operator cannot be separated from its operand
} * (a + 1)
  ^~
```

이렇게 표현식에 일부를 대체해야 하는 복잡한 조건식이 있다면 프로시저를 선언해야만 한다. 프로시저 내에서 원하는 값을 호출한 자리에 대체하고 싶을 때는 `return` 예약어를 사용한다. 만약 조건에 맞아서 실행된 표현식이 `return a` 라면 a값이 되돌아가서 `select(a, b)` 대신에 대체된다. 

```swift
18> func select(_ a: Int,_ b: Int) -> Int {
 19.     switch (a,b) {
 20.     case (a,b) where a>b: return a
 21.     case (a,b) where a<b: return b
 22.     default: return -1
 23.     }
 24. }
 25.
 26. select(a, b) * (a + 1)
```

###### 연습문제 1.2 지나감

###### 연습문제 1.3

세 개 숫자를 인자로 받아서 그 가운데 큰 숫자 두 개를 제곱한 다음, 그 두 값을 덧셈하여 되돌려주는 프로시저를 선언하라.

```swift
func exam1_3(a: Int, b: Int, c:Int) -> Int {
    switch (a,b,c) {
    case (a,b,c) where a > c && b > c:
        return a*a + b*b
    case (a,b,c) where a > b && c > b:
        return a*a + c*c
    case (a,b,c) where b > a && c > a:
        return b*b + c*c
    default:
        return 0
    }
}

exam1_3(a: 10, b: 5, c: 3)
exam1_3(a: 10, b: 7, c: 9)
exam1_3(a: 1, b: 7, c: 9)
```

###### 연습문제 1.4

스위프트에서는 문제처럼 연산자를 대체하는 표현도 불가능하다. 다음과 같이 `값 (if 구문과 연산자) 값` 형태 표현식은 동작하지 않는다.

```swift
func a_plus_abs_b(a: Int, b: Int) -> Int {
    return a (if (b > 0) { + }
    else { - }) b
}
```

다음과 같이 if 구문 아래 값과 연산자를 풀어서 작성하거나 연산자를 다른 방식으로 추상화해야 한다. 다른 방식은 더 복잡한 문법 표현 때문에 여기서 설명하지 않는다.

```swift
func plus(_ a: Int, _ b: Int) -> Int {
    return a + b
}
func minus(_ a: Int, _ b: Int) -> Int {
    return a - b
}
func a_plus_abs_b(a: Int, b: Int) -> Int {
    if (b > 0) {
        return plus(a, b)
    }
    else {
        return minus(a, b)
    }
}
```

###### 연습문제 1.5

```swift
func p() -> Int {
    return p()
}

func test(_ x: Int, _ y: Int) -> Int {
    if (x == 0) {
        return 0
    }
    else {
        return y
    }
}

test(0, p())
```

> 인자 먼저 계산법 

`test(0, p())` 에서 x에는 0을 y에는 p()를 대체하기 전에 0는 값이지만 p()는 프로시저라서 p()를 먼저 계산해야만 한다. p()를 대체하기 전에 p()를 적용해보자. p() 내부에서 다시 p()를 호출하기 때문에 재귀로 반복된다. 모든 인자를 대체하기 전에 p()를 빠져나올 수 없다. 

> 순서대로 계산법

`test(0, p())`에서 순서대로 x부터 0 대체하고 y대신에 p()로 대체한다고 가정하자. 
if 구문을 적용해보니 x값이 0이라서 `return 0`가 실행되고 y값에 포함한 p()는 필요하지 않다. 

#### 1.1.7 연습 뉴튼 계산법으로 제곱근 찾기

위에서 설명했던 프로시저들은 매개변수에 전달하는 인자값에 따라 결과가 달라지기 때문에, 수학의 함수와 매우 비슷하다. 그렇지만 수학의 순수 함수와 컴퓨터 프로시저 사이에는 `효율성`을 고려해야 한다는 중요한 차이점이 있다. 

제곱근을 구하는 수학 문제를 살펴보자. 

`𝑦 ≥ 0 이고 𝑦²=𝑥 일때 √𝑥=𝑦 다.`

이 정의는 수학에서 올바른 함수 정의다. 이 함수로 한 수가 다른 수의 제곱근인지 확인하거나, 제곱근에 대한 일반적인 여러 사실을 추론할 수도 있다. 하지만 이 정의에는 계산을 위한 절차 - 프로시저가 없다. 수학의 함수 정의만 보고 한 수의 제곱근을 어떻게 계산하는 지 알수 없다. 다음과 같이 프로그램 언어로 흉내 내어 함수를 선언해도 마찬가지다. 

```swift
func sqrt(x: Int) -> Int {
    return y where (y >= 0 && square(y) == x)
}
```

역시나 같은 질문이 반복되고 해결되지 않는다. 

함수와 프로시저의 차이는 물체가 어떤 성질을 지니는지 알아내는 것과 그것을 어떻게 만들지 알아내는 정도 차이다. 흔히 문제가 무엇인지 설명하는 지식declarative knowledge과 문제를 해결하기 위한 방법에 대한 지식imperative knowledge의 차이점이라고 한다. 수학은 무엇인지 선언하는 일에 관심을 가지지만, 컴퓨터 과학에서는 어떻게 만드는지 선언하는 데 관심을 둔다. 

그러면 사람은 제곱근을 어떻게 계산할까? 가장 유명한 방식인 뉴튼 계산법으로 가장 가까운 값을 근사값을 반복해서 계산해보자. 계산 방법은 다음과 같다. x 제곱근에 가까운 y 값이 있을 때 y와 x/y의 평균을 구해서 진짜 제곱근에 더 가까운 값을 계산한다. 예를 들어 2의 제곱근은 다음과 같이 계산한다. 처음에는 1을 가까운 값이라고 가정하자.

![제곱근 계산](https://github.com/godrm/SICP-Swift/blob/master/images/1.1.7.png?raw=true)

이런 프로세스를 반복하다보면 점차 2의 제곱근에 가까운 값을 구할 수 있다. 



## <a name="head1.2"></a> 1.2 Procedures and the Processes They Generate



## <a name="head1.3"></a> 1.3 Formulating Abstractions



