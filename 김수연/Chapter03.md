# 3장 자바와 객체 지향

## 목차
- 클래스와 객체
- 캡슐화
- 상속
- 다형성
- 추상화
- 추상클래스

# 1. 클래스와 객체
- 클래스: 객체를 만들기 위한 틀 또는 설계도. 멤버 변수와 메서드를 정의함.
  - 같은 속성과 기능을 가진 객체를 총칭하는 개념
- 객체: 클래스를 기반으로 생성된 실체. 각자 독립적인 상태를 가지며, 멤버 변수에 저장된 값을 조작할 수 있는 메서드를 가지고 있음.
  - 세상에 존재하는 유일무이한 사물

## **클래스와 객체의 구분 방법**
> 클래스는 분류에 대한 개념이고
객체는 실체화한 것이다.

**ex) 사람 -> 클래스, 김연아 -> 객체**


# 2. 캡슐화
- 객체의 내부 상태를 외부에서 직접 접근하지 못하게 하여, 객체의 무결성을 보호하는 것을 말함.
- 정보 은닉(information hiding)과도 비슷한 개념. 객체의 내부 구조를 숨기고, 외부에서는 객체가 노출하는 인터페이스만을 사용할 수 있게 함.

접근 제어자

	ㆍpublic : 클래스 외부에서도 접근이 가능함
    ㆍprivate : 클래스 내부에서만 접근이 가능함
    ㆍprotected : 상속받은 자식 클래스에서만 접근 가능함
    ㆍdefault : 같은 패키지 내 클래스에서 접근이 가능함

<img src="./image/i16.png " width=550 height=300 />

> 상속을 받지 않았다면 객체 멤버는 객체를 생성한 후 참조 변수를 통해 접근할 것

> 정적 멤버는 클래스명.정적멤버 형식으로만 접근하는 것을 권장.

### ** 클래스 멤버 : 객체 멤버 - static 멤버 : 인스턴스 멤버
클래스의 속성을 static으로 지정할 시
- 스태틱 영역에 할당
- 객체 생성시 힙 영역에 할당 안 됨
- 클래스명.속성명으로 접근 가능

static 키워드 O
- 클래스 멤버 = static 멤버 = 정적 멤버 -> 모든 객체들이 같은 값을 가질 때 사용

static 키워드 X
- 객체 멤버 = 인스턴스 멤버

## ex
- 사람 클래스의 인구
- 고양이의 다리 개수 
> 사람.인구, 고양이.다리개수 형식으로 접근하는 것이 홍길동.인구수, 키티.다리개수 형식으로 접근하는 것보다 권장됨.


<img src="./image/i17.png " width=550 height=300 />

# 3. 상속
- 이미 정의된 클래스를 기반으로 새로운 클래스를 정의하는 것을 말함.
- 상위 클래스에서 정의한 필드와 메서드를 하위 클래스에서 그대로 사용할 수 있게 됨.

## 하위 클래스는 상위 클래스다
- 상속 관계에서 반드시 만족해야 함
  - 포유류는 동물이다.
  - 고래는 포유류다.
  - 고래는 동물이다.

최상위 클래스
```java
public class 동물 {
	String myClass;
    
    동물() {
    	myClass = "동물";
    }
    
    void showMe() {
    	System.out.println(MyClass);
    }
}
```
동물 클래스를 상속받은 동물의 종류 클래스
```java
public class 포유류 extends 동물 {
	포유류() {
    	myClass = "포유류";
    }
}
```
```java
public class 조류 extends 동물 {
	조류() {
    	myClass = "조류";
    }
}
```
동물 종류 클래스를 상속받은 동물 클래스들
```java
public class 고래 extends 포유류 {
	고래() {
    	myClass = "고래";
    }
}
```
```java
public class 박쥐 extends 포유류 {
	박쥐() {
    	myClass = "박쥐";
    }
}
```
```java
public class 참새 extends 조류 {
	참새() {
    	myClass = "참새";
    }
}
```
```java
public class 펭귄 extends 조류 {
	펭귄() {
    	myClass = "펭귄";
    }
}
```
클래스로 객체 생성
```java
public class Main {
	public static void main(String[] args) {
    	동물 animal = new 동물();
    	포유류 mammalia = new 포유류();
    	조류 bird = new 조류();
    	고래 whale = new 고래();
    	박쥐 bat = new 박쥐();
    	참새 sparrow = new 참새();
    	펭귄 penguin = new 펭귄();
        
        animal.showMe();
        mammalia.showMe();
        bird.showMe();
        whale.showMe();
        bat.showMe();
        sparrow.showMe();
        penguin.showMe();
    }
}
```
```java
public class Main {
	public static void main(String[] args) {
    	동물 animal = new 동물();
    	동물 mammalia = new 포유류();
    	동물 bird = new 조류();
    	동물 whale = new 고래();
    	동물 bat = new 박쥐();
    	동물 sparrow = new 참새();
    	동물 penguin = new 펭귄();
        
        animal.showMe();
        mammalia.showMe();
        bird.showMe();
        whale.showMe();
        bat.showMe();
        sparrow.showMe();
        penguin.showMe();
    }
}
```
```java
public class Main {
	public static void main(String[] args) {
    	동물[] animals = new 동물[7];
    	animals[0] = new 동물();
    	animals[1] = new 포유류();
    	animals[2] = new 조류();
    	animals[3] = new 고래();
    	animals[4] = new 박쥐();
    	animals[5] = new 참새();
    	animals[6] = new 펭귄();
        
        for (int i=0; i<animals.length; i++) {
        	animals[i].showMe();
        }
    }
}
```
> 결과 모두 같음!

<img src="./image/i14.png " width=550 height=300 />

> 상위 클래스로 갈수록 추상화/일반화가 되고 하위 클래스로 갈수록 구체화/특수화가 진행된다.

## 상속관계에서 만족해야만 하는 문장
- 상속 관계: 하위 클래스 is a kind of 상위 클래스 (해석: 하위 클래스는 상위 클래스의 한 분류다.)
- 다중 상속을 허용하지 않는다.
- 예제: 고래는 동물의 한 분류다.
- 영희는 아빠가 될 수 없다. (일반화 불가)
- 펭귄은 동물의 역할을 수행할 수 있다. (일반화 가능)

> 'is a' 보단 'a kind of'
펭귄은 한마리의 조류이다 보단 펭귄은 조류의 한 종류이다.

## 상속의 강력함
- 상속을 통해 최상위 클래스 Object의 특성을 물려받아 toString() 메서드를 모든 서브클래스에서 사용가능하다.
- 구체화된 객체들을 하나의 일반화된 개념으로 사용할 수 있다.

### 상속과 인터페이스
<img src="./image/i15.png " width=550 height=300 />

> 인터페이스는 'be able to'와 같이 "무엇을 할 수 있는" 형태로 만드는 것이 좋다.

자바 API 예시
- Comparable 인터페이스 : 비교할 수 있는
- Runnable 인터페이스 : 실행할 수 있는
- 인터페이스는 클래스가 '무엇을 할 수 있다'라는 기능을 구현하도록 강제 하게 된다.
# 4. 다형성
- 하나의 타입에 대해 여러 가지의 기능을 제공할 수 있는 것을 말함.
- 상속 관계에서 상위 클래스의 참조 변수를 하위 클래스의 객체로 참조할 수 있는 것을 말함.
- 메서드 오버로딩과 오버라이딩을 통해 다형성을 구현할 수 있음.

## 오버라이딩(overriding)과 오버로딩 예제
 하위 클래스에서는 상위 클래스의 메서드를 그대로 사용하거나 필요한 부분만 수정하여 사용가능 
```java
public class Animal {
    //오버라이딩 - 재정의: 상위클래스의 메서드와 같은 메서드 이름, 같은 인자 리스트
    public void makeSound() {
        System.out.println("동물이 소리를 냅니다.");
    }
    // 오버로딩 - 중복정의: 같은 메서드 이름, 다른 인자 리스트
    public void makeSound(String sound) {
        System.out.println("동물이 " + sound + " 소리를 냅니다.");
    }
}

public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("개가 짖습니다.");
    }

    public void makeSound(String sound) {
        System.out.println("개가 " + sound + " 소리를 냅니다.");
    }
}

public class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("고양이가 야옹합니다.");
    }

    public void makeSound(String sound) {
        System.out.println("고양이가 " + sound + " 소리를 냅니다.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal1 = new Dog();
        Animal animal2 = new Cat();
        animal1.makeSound();// 오버라이딩
        animal1.makeSound("멍멍");//오버로딩
        animal2.makeSound();// 오버라이딩
        animal2.makeSound("냥냥");//오버로딩
    }
}

```
→ **상위 클래스 타입의 객체 참조 변수를 사용하더라도 하위 클래스에서 오버라이딩(재정의)한 메서드가 호출된다.**

- 하위 클래스가 재정의한 메서드를 알아서 호출해 줌으로써 형변환이나 instanceof 연산자를 써서 하위 클래스가 무엇인지 신경 쓰지 않아도 된다.

- 오버라이딩을 통한 메서드 재정의, 오버로딩을 통한 메서드 중복 정의를 통해 다형성을 제공함으로써 사용편의성을 준다.

- Animal animal1 = new Dog();
위 코드에서 animal1의 makeSound() 메서드를 실행하면 Animal 객체에 의해 정의된 메서드가 아니라 Dog 객체에 의해 재정의된 makeSound()메서드가 실행된다!


-> 상위 클래스 타입의 객체 참조 변수를 사용하더라도 하위 클래스에서 오버라이딩한 메서드가 호출된다!!

->  상위 클래스 참조 변수로 하위 클래스가 오버라이딩한 메서드를 사용할 수 있다.

 
# 5. 추상화
> 구체적인 것을 분해해 관심 영역에 대한 특성만을 가지고 재조합하는 것

- 객체에서 공통적인 부분을 뽑아내어 추상적인 개념으로 다루는 것을 말함
- 객체 지향에서 추상화의 결과는 클래스
- OOP의 추상화는 모델링
- 클래스 설계에서 추상화 사용됨
- 클래스 설계를 위해 애플리케이션 경계부터 정해야함
## Ex
병원 애플리케이션 -> 시력, 몸무게 정보나 접수하다. 등의 기능이 필요

은행 애플리케이션 - > 시력, 몸무게 정보는 필요없고 나이, 연봉이나 이체하다. 대출하다. 등의 기능이 필요

> 구체적인 것을 분해해서 관심 영역(애플리케이션 경계)에 있는 특성만 가지고 재조합함. (모델링)

-> 자바는 이러한 객체 지향의 추상화를 "class 키워드"를 통해 지원
### 추상화의 개념
  - 상속을 통한 추상화, 구체화
  -  인터페이스를 통한 추상화
  - 다형성을 통한 추상화
## 예시를 통해 추상화 과정과 그에따른 T 메모리 변화

<img src="./image/i18.png " width=450 height=300 />

->자바 코드로 변환

```java
Mouse.java
public class Mouse {
 public int age;
 public int countOfTail;


 public void sing(){
 	System.out.println(name + "찍찍!!!");
 }
 }
```

```java
MouseDriver.java
public class MouseDriver {
	public static void main(String[] args){
    		Mouse mickey = new Mouse();
            	 mickey.name = "미키";
                mickey.age = 85;
                mickey.countOfTail = 1;
                
                mickey.sing();
                
              mickey = null;
                
               Mouse jerry = new Mouse();
                
              jerry.name = "제리";
               jerry.age = 73;
              jerry.countOfTail = 1;
                
               jerry.sing();
	}
 }

```
① Mouse mickey = new Mouse(); 여기까지 T 메모리 스냅샷
<img src="./image/i19.png " width=450 height=300 />
- java.lang 패키지와 모든 클래스(Mouse,MouseDriver)이 T메모리 스태틱 영역에 배치된다.
- Mouse의 name, age, countOfTail의 변수 저장 공간이 없다.

② Mouse mickey = new Mouse();

<img src="./image/i20.png " width=450 height=300 />


1) Mouse mickey 

    Mouse 객체에 대한 참조 변수 mickey를 만든다.

2) new Mouse() : 객체 생성자를 호출하는 구문

     생성된 객채는 T 메모리의 힙 영역에 배치된다.


3)  대입문

     Mouse 객체에 대한 주소(포인터)를 참조 변수 mickey에 할당한다.


③ mickey.name = "미키";
  mickey.age = 85;
  mickey.countOfTail = 1;
  코드 실행 시 힙 영역 Mouse 객체 공간의 name, age, countOfTail에 각각 값을 대입

<img src="./image/i21.png " width=450 height=300 />

- 객체 참조 변수 mickey와 참조 연산자(.)를 이용해 실제 힙 상의 객체에 접근해 name 속성에 "미키" 라는 문자열 할당한다. 
  - 같은 방법으로 mickey.age = 85;
  mickey.countOfTail = 1; 실행

④ mickey.sing(); 실행시 "미키 찍찍" 출력

⑤ 10번째줄 mickey = null;을 실행하면 객체 참조 변수인 mickey가 더이상 힙 영역의 Mouse 객체(:Mouse)를 참조하지 않는다.

<img src="./image/i22.png " width=450 height=300 />

⑥ jerry 변수도 mickey와 동일한 방식으로 생성

<img src="./image/i23.png " width=450 height=300 />

- 💡 힙 영역에 보이는 Mouse 객체는 이전의 그 Mouse 객체가 아니다!!

⑦ "제리 찍찍"을 출력한 뒤 mai() 메서드 스택 프레임을 종료하는 닫는 중괄호를 만나 프로그램 종료!


# 6. 추상 클래스
- 인스턴스를 생성할 수 없는 클래스를 말함.
하위 클래스에서 구현해야 하는 메서드를 추상 메서드로 정의할 수 있음.
- 추상 클래스를 상속한 하위 클래스는 추상 클래스의 추상 메서드를 모두 구현해야 함.

### Reference
[추상클래스와 인터페이스의 차이점](https://devlog-wjdrbs96.tistory.com/370)