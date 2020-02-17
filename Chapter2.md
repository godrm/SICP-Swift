## 2장. 데이터로 요약하는 방식 (Building Abstractions with Data)

```
We now come to the decisive step of mathematical abstraction: we forget about what the symbols stand for.... [The mathematician] need not be idle; there are many operations which he may carry out with these symbols, without ever having to look at the things they stand for.
—Hermann Weyl, The Mathematical Way of Thinking
```

1장에서는 프로그램을 설계하는 데 계산 프로세스와 프로시저가 어떤 역할을 하는지 살펴봤다. 
프로그램을 작성한다는 것은 기본 데이터 값과 연산을 어떻게 사용하는지부터 시작한다. 프로시저는 매개 변수와 조건식을 가지고 복잡한 프로시저를 어떻게 정의하느냐가 중요하다. 프로시저는 프로세스가 자라나는 규칙을 정의하는 것이라서 계산 과정이 비슷하게 움직이는 알고리즘을 분석도 했다. 

이 장에서는 복잡한 데이터를 어떻게 요약하는지 공부한다. 앞으로는 단순한 데이터만 가지고 풀기 어려운 문제를 살펴본다. 프로그램은 복잡한 현상들을 비슷하게 흉내내서 부품처럼 프로세스로 만들 수 있다. 이런 계산 물체를 만들기 위해서, 여러 데이터 물체를 묶어서 묶음 데이터로 요약하는 방법을 살펴본다. 

데이터 묶음은 묶음 프로시처럼 더 높은 수준에서 프로그램 설계를 생각할 수 있고, 모듈을 조립해서 프로그램을 작성하는 데 꼭 필요하다. 복잡한 데이터를 만들려면 기본 데이터만으로 부족하다. 언어 표현력을 넓혀서 문제 풀이에 좀 더 적합한 방식으로 데이터를 다뤄야 한다. 

유리수를 다루는 시스템을 기본 데이터로 다룬다고 생각해보자. 분모와 분자를 각각 정수로 나타낼 수 밖에 없다. 그리고 계산을 한다고 해도 분모와 분자를 각각 계산하는 프로시저를 두 개 만들어야만 한다. 이렇게 하면 어떤 분모와 어떤 분자가 쌍을 이루는지도 기억해야 하고 불편하다. 그래서 유리수 프로그램에서는 유리수 하나를 분모와 분자 한 쌍 데이터를 묶어서 만들어 사용해야 한다. 

예를 들어 ax + by 형태 `일차 결합 linear combination` 식을 표현해보자. 이름이 a,b,x,y가 모두 숫자를 나타낼 때 다음과 같이 만들 수 있다. 

```swift
func liner_combination(a: Int, b: Int, x: Int, y: Int) -> Int {
    return a * x + b * y
}
```

이 상태에서 정수 뿐만 아니라 유리수나 복소수, 다항식 등 어떤 것이든지 덧셈과 곱셈을 하는 표현식으로 프로시저를 고쳐야 한다면 어떻게 해야할까. 어떤 데이터가 들어오더라도 덧셈add과 곱셈mul 계산할 수 있는 더 똑똑한 표현이 필요하다. 

```swift
func add<T>(_ a: T, _ b: T) -> T where T : Numeric {
    return a + b
}

func mul<T>(_ a: T, _ b: T) -> T where T : Numeric {
    return a * b
}

func linear_combination<T>(a: T, b: T, x: T, y: T) -> T where T : Numeric {
    return add(mul(a, x), mul(b, y))
}
```

스위프트는 명확하지 않은 모든 데이터 타입에 대해 미리 계산 방식을 결정할 수 없다. 적어도 어떤 역할을 해야 하는지 숫자 형태라는 것을 <T>와 where 조건으로 명시해야 한다. 자세한 문법은 나중에 확인해보자.

데이터 요약을 통해 프로그램을 구성할 때, 여러 부품 사이에 알맞은 요약 경계 abstraction barrier를 구분해야 한다. 이런 경계를 구분해서 묶음 데이터를 만들 때 가장 중요한 것은 프로그래밍 언어로 묶는 표현이다. 여러 데이터를 묶는 방법도 여러 가지가 있고, 프로시저만으로도 복잡한 데이터를 표현할 수 있다는 것을 알았다. 묶음 데이터 가운데 가장 많이 사용하는 것은 차례열sequence과 나무tree 구조 표현도 살펴본다. 

묶음 데이터를 설명할 때 중요한 것은 닫힘 성질closure property이다. 묶음 데이터를 묶으면 다시 묶음 데이터가 된다는 것이다. 묶음 데이터는 기본 데이터를 묶어서 만들어지고, 묶음 데이터를 다시 묶어도 묶음 데이터가 된다. 

여러 프로그램 부품을 조립하다보면 서로 부품이 맞지 않는 경우가 생기기도 하는데, 묶음 데이터를 활용해서 여러 부품 사이에서 공통 인터페이스conventional interface 역할을 한다. 이를 설명하기 위해서 닫힘 성질을 만족하는 그래픽 언어를 만든다. 

이 장부터는 숫자 말고도 데이터로 표현하는 글자 표현 symbolic expression을 배워서 언어의 표현력을 끌어올린다. 집합을 나타내는 방법들도 확인한다. 숫자를 다룰 때도 여러 계산 프로세스로 구현할 수 있었듯이, 복잡한 데이터도 여러 방법으로 있고 알고리즘에 따라 시간과 공간이 달라진다는 것을 알게 된다. 

그 이후에는 프로그램에서 한 가지 데이터를 여러 방법으로 나타낼 수 있어야 할 때 프로그램 구조에 대해 공부한다. 이 문제는 서로 다른 타입 데이터를 다룰 수 있도록 일반화된 연산generic operation을 만든다. 앞서 설명한 것처럼 요약의 경계를 확실하게 구분하기 위해서 `데이터 중심으로 프로그램 작성하는 방법`을 알아본다. 여러 데이터를 처리하는 다항식 산술 연산 꾸러미를 만들어본다. 


### 목차

[2.1 Introduction to Data Abstraction](https://github.com/godrm/SICP-Swift/blob/master/2.1.md)

[2.2 Hierarchical Data and the Closure Property](https://github.com/godrm/SICP-Swift/blob/master/2.2.md)

[2.3 Symbolic Data](https://github.com/godrm/SICP-Swift/blob/master/2.3.md)

[2.4 Multiple Representations for Abstract Data](https://github.com/godrm/SICP-Swift/blob/master/2.4.md)

[2.5 Systems with Generic Operations](https://github.com/godrm/SICP-Swift/blob/master/2.5.md)

