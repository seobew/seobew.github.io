## 다형성(Polymorphism)이란?

### 개요

보통 다형성하면 생각하는 것은 객체지향 프로그래밍일 것이다. 객체지향 프로그래밍에서는 중요한 3가지 요소가 있는데, 바로 캡슐화, 상속, 그리고 **다형성**이다. 

> 객체지향 프로그래밍 : 프로그램을 단순히 데이터와 처리 방법으로 나누는 것이 아니라, 프로그램을 수많은 '객체'라는 기본 단위로 나누고 이 객체들의 상호작용으로 서술하는 방식
>
> 캡슐화 : 데이터(속성)과 데이터를 처리하는 함수를 하나로 묶는 것
>
> 상속 : 상위(부모) 객체의 필드(속성)와 메소드를 하위(자식) 객체에게 물려주는 행위이며, 하위 객체는 상위 객체를 확장해서 추가적인 필드(속성)와 메소드를 가질 수 있음

### 다형성

다형성은 간단히 설명하면, 서로 다른 객체**(서로 다른 클래스)**가 동일한 메세지에 대하여 서로 다른 방법으로 응답할 수 있는 기능을 의미한다. __(같은 모양의 코드가 다른 행위를 하는 것)__ 상속을 통해 기능을 확장 및 변경하는 것을 가능하게 해주고, 같은 클래스 내에 코드의 길이까지 줄여주는 좋은 개념이다.

다형성에서 예로 가장 많이 드는 것은 도형과 그 도형을 상속하는 삼각형, 사각형, 원이다. 도형에 존재하는 Draw라는 메서드를 삼각형, 사각형, 원은 똑같이 호출해도 다르게 작동을 해야하는 것이다.

<img src="http://cfile2.uf.tistory.com/image/1920A7124C8F866B55FE54" width=500>

```{.java}
class Figure
{
public:
	virtual string draw() = 0;	
};

class Triangle : public Figure
{
public:
	virtual string draw() { return "Draw Triangle"; }
};

class Square : public Figure
{
public:
	virtual string draw() { return "Draw Square"; }
};

class Circle : public Figure
{
public:
	virtual string draw() { return "Draw Circle"; }
};
```

_위 예시는 가상함수를 이용해서 추상클래스를 만들어 사용하는 예시입니다._ 



이런 다형성을 녹여내는 방법에는 여러가지가 있는데, 그 중 대표적인 것이 **오버로딩**과 **오버라이딩**이다. 

* 오버로딩

  * **같은 이름의 메소드를 여러 개 가지면서 매개변수의 유형과 개수가 다르도록 하는 기술**

  * 오버로딩은 가장 이해하기 쉬운 다형성의 예이다.

  * ```{.java}
    class O{
        public void a(int param){
            System.out.println("숫자출력");
            System.out.println(param);
        }
        public void a(String param){
            System.out.println("문자출력");
            System.out.println(param);
        }
    }
    ```

* 오버라이딩

  * **상위 클래스가 가지고 있는 메소드를 하위 클래스가 재정의 해서 사용할 수 있게 하는 기술**

  * 위에서 든 도형, 삼각형, 사각형, 원의 예시가 바로 오버라이딩이다.

  * ```{.java}
    class A{
        public String x(){return "A.x";}
    }
    class B extends A{
        public String x(){return "B.x";}
        public String y(){return "y";}
    }
    class B2 extends A{
        public String x(){return "B2.x";}
    }
    ```



#### 추가로 같이 알면 좋을 것 

추상 클래스, 인터페이스!

> * 추상클래스 : '추상적인 형태'만 제안하고, 실제 구현은 자식 클래스로 미룸
>   * 가상함수(virtual) 를 포함하고 있다면 추상클래스
>   * 추상클래스는 인스턴스를 만들 수 없음
> * 인터페이스 : 모든 멤버함수가 가상함수인 클래스를 인터페이스라고 부르기도 함



##### 참고한, 참고할만한사이트

객체지향 개념 다시 잡기 : https://www.slideshare.net/plusjune/ss-46109239

생활코딩 다형성 : https://opentutorials.org/module/516/6127

다형성, 오버로딩 오버라이딩 : https://brunch.co.kr/@kd4/4

상속, 다형성 : http://pacs.tistory.com/entry/C-%EC%83%81%EC%86%8D%EA%B3%BC-%EB%8B%A4%ED%98%95%EC%84%B1-Inheritance-Polymorphism