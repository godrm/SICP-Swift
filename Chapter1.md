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

[1.1 The Elements of Programming](https://github.com/godrm/SICP-Swift/blob/master/1.1.md)

[1.2 Procedures and the Processes They Generate](https://github.com/godrm/SICP-Swift/blob/master/1.2.md)

[1.3 Formulating Abstractions](https://github.com/godrm/SICP-Swift/blob/master/1.3.md)




