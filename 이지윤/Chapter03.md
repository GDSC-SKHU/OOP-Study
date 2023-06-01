## Chapter 03. 자바와 객체 지향

---


### 📍 객체 지향은 인간 지향이다
> 함수 : 코드를 논리적인 단위로 구분하고 분할해서 정복하자는 것. </br>
> D & C : Divide and Conquer / 분할 정복

| 클래스명 (class) |        사람        |    객체명 (object)    |                이지윤:사람                 |
|:------------:|:----------------:|:------------------:|:-------------------------------------:|
|   **속성들**    | 나이</br>몸무게<br/>키 | **속성들 (property)** |  나이: 23</br>몸무게: 40 kg<br/>키 : 200cm  |
|   **행위들**    | 먹다</br>자다</br>울다 |  **행위들 (method)**  |           먹다</br>자다</br>울다            |


 > **따라서, 객체 지향은 직관적이다. 이유가 뭘까❓**
 

### 💡 객체 지향의 4대 특성
  - **캡슐화 (Encapsulaion)** : 정보 은닉
  - **상속 (extends)** : 재사용
  - **추상화 (Abstraction)** : 모델링
  - **다형성 (Polymorphism)** : 사용 편의

### 💡 객체 vs 클래스

> **객체** : 실존함. / 세상에 존재하는 유일무이한 사물 / 클래스의 인스턴스 </br>
> **클래스** : 실존하지 않음. / 분류, 집합, 같은 속성과 기능을 가진 객체를 총칭하는 개념 </br>
>  **⭐️ 즉, 같은 특성을 가진 객체의 집합 = 클래스**

### 📍 추상화는 모델링이다.
> 추상화 : 구체적인 것을 분해해서 context에 있는 특성만 가지고 재조합하는 것 = 모델링 </br>
> context : '이 어플리케이션은 어디에 사용될 것인가?'라는 질문에 해당함. 

### 💡 추상화와 T 메모리
```java
public class MouseDriver {
	public static void main(String[] args) {
        // Mouse(클래스) mickey(객체 참조변수) = new Mouse(객체)
		Mouse mickey = new Mouse();
        
		mickey.name = "미키";
		mickey.age = 85;
		mickey.countOfTail = 1;

		mickey.sing();

		mickey = null; // Garbage Collector 등장! (힙 영역의 메모리 공간 사라짐.)

      //새로운 객체 생성 jerry 
		Mouse jerry = new Mouse();

		jerry.name = "제리";
		jerry.age = 73;
		jerry.countOfTail = 1;
        
        // 메소드
		jerry.sing();
	}
}
```

> **❗ 추상화를 통해 모델링을 하게 되면 ❗**️</br>
> 클래스 멤버 (static_정적) -> 클래스 멤버 속성 / 메소드 </br>
> 객체 멤버 (인스턴스 멤버)-> 객체 멤버 속성 / 메소드 </br>

> **❗ 정적 속성 vs 객체 속성 ❗</br>**
> 정적 속성 = 모든 객체가 같은 값을 가질 때 사용하는 것이 기본 </br>
> 정적 메서드 = 객체의 존재 여부와 관계 x / 객체가 아닌 클래스에 속함. </br>
> </br>
> 정적 속성은 클래스 배치 시 메모리 공간이 확보되지만 객체 속성일 경우 실제 메모리 공간 x , 힙 영역에 객체가 생성되면 그 때 메모리 할당.


### 📍 상속 : 재사용 + 확장 
> 상위 클래스의 특성을 하위 클래스에서 상속(**특성** 상속)하고 필요한 특성을 추가 및 확장, 재사용해서 사용할 수 있다는 의미

<img width="700" alt="Screenshot 2023-05-31 at 10 50 56 PM" src="https://github.com/GDSC-SKHU/OOP-Study/assets/84395062/57c28f7d-2511-4bea-b3ad-241a843d82a8"/>

> 하위 클래스 is a kind of 상위 클래스 </br>
> ex) 조류는 동물의 한 분류이다. -> 조류 is a kind of 동물


- 인터페이스 (be able to) : 클래스가 '무엇을 할 수 있다'라고 하는 기능을 구현하도록 강제

> Q1 . 상위 클래스는 하위 클래스에게 **물려줄 특성**이 많은게 좋음? 적은게 좋음?</br>
> Q2 . 인터페이스는 구현을 **강제할 메서드**가 많은게 좋음? 적은게 좋음? </br>
> A1_hint . **LSP (리스코프 치환 원칙)** </br>
> A2_hint . **ISP (인터페이스 분할 원칙)** 

### 💡 상속과 T 메모리
> ❗️ 하위 클래스의 인스턴스가 생성될 때 상위 클래스의 인스턴스도 함께 생성 ❗️


```java
public class Driver {
    public static void main(String[] args) {

        // 펭귄 한 마리가 태어나니 펭귄 역할을 하는 pproro라 이름 지음.
        Penguin pororo = new Penguin();

        //name은 뽀로로 , habitat은 남극
        pororo.name = "뽀로로";
        pororo.habitat = "남극";

        //pororo 이름 보여줘 
        pororo.showName(); // 결과 : 뽀로로
        //pororo 서식지 알려줘 
        pororo.showHabitat(); // 결과 : 남극

        // 펭귄 한 마리가 태어나니 동물 역할을 하는 pingu라고 이름을 지음.
        Animal pingu = new Penguin(); 

        //name : 핑구 
        pingu.name = "핑구";
        // pingu.habitat = "EBS";

        //pingu 이름 보여줘.
        pingu.showName(); // 결과 : 핑구
        //pingu는 Animal의 특성만 가져오는데 showHabitat은 존재하지 않음.
        // pingu.showHabitat();

        // 이게 왜 안될까?
        // 동물 한 마리가 태어나니 펭귄 역할을 하는 happyfeet라고 이름을 지음.
        // 이미 펭귄 클래스가 동물 클래스를 상속받고 있어서..? 
        // Penguin happyfeet = new Animal();
    }
}
```
- **형변환 연산**
  - 명시적 형변환 연산(Casting)
    - 좁은 <-> 넓은 데이터 타입으로 직접 형변환을 해주는 것. 대신 값 손실 위험 o
  - 암묵적 형변환 연산(Promotion)
    - 좁은 데이터 타입에서 넓은 데이터 타입으로 자동으로 형변환이 이루어지는 것.

### 📍 다형성 : 사용편의성
> **overriding (올라타기)** : 맨 위에 올라탄 존재만 보임. / **재정의**: 상위클래스의 메서드와 **같은 메서드** 이름, **같은 인자** 리스트 </br>
> **overloading (적재하기)** : 옆으로 적재된 모든 존재가 보임. / **중복정의**: **같은 메서드** 이름, **다른 인자** 리스트


```java
public class Driver {
  public static void main(String[] args) {
    //한 마리의 펭귄이 태어나니 펭귄 역할을 하는 pororo 라고 이름을 지음.
    Penguin pororo = new Penguin();

    // name : 뽀로로 / habitat : 남극
    pororo.name = "뽀로로";
    pororo.habitat = "남극";


    pororo.showName(); //결과 : 어머 내 이름은 알아서 뭐하게요?
    pororo.showName("초보람보"); // *오버로딩 / 결과 : 초보람보 안녕, 나는 뽀로로라고 해
    pororo.showHabitat(); // 결과 : 뽀로로는 남극에 살아

    //펭귄 한 마리가 태어나니 동물 역할을 하는 pingu 라고 이름을 지음.
    Animal pingu = new Penguin();

    //name: 핑구
    pingu.name = "핑구";
    //Animal을 참조했지만 Penguin에 의해서 재정의되어 가려졌기 때문에 Penguin의 showName()이 실행됨.
    pingu.showName(); // 결과 : 어머 내 이름은 알아서 뭐하게요?
  }
}
```

> ⭐️ 다형성을 **사용 편의성**이라고 정의한 이유 </br>
> **오버로딩**은 함수명 하나만 가지고 인자 목록만 달리하면 되니 편리하다.</br>
> 특히 **제네릭**을 이용하면 하나의 함수만 구현해도 다수의 함수를 구현한 효과를 낼 수 있음. </br>
> 오버라이딩은 하위 클래스가 재정의한 메서드를 알아서 호출해주기 때문에 하위 클래스를 신경쓰지 않아도 돼서 깔끔한 코드를 유지할 수 있음. </br>


###  📍 캡슐화 : 정보 은닉

---

###  이해가 잘 안돼서 이해 다 되면 올릴 예정 😅
