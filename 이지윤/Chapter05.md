# Chapter 05 . 객체 지향 설계 5원칙 - SOLID

---

## 📍 [SRP (Single Responsibility Principle)]((https://steady-coding.tistory.com/370)) : 단일 책임 원칙

> SRP : 몰빵이 아닌 역할을 분담하는 것. ( 객체 지향 4대 특성 中 추상화 )

## 📍 [OCP (Open Closed Principle)](https://steady-coding.tistory.com/378) : 개방 페쇄 원칙

> <center>확장에는 열려있고 변경에 대해서는 닫혀 있어야 함.</center>
> <center>⬇</center>
> <center>기능을 변경하거나 확장할 수 있으나 그 기능을 사용하는 코드는 수정하지 않음.</center>

## 📍 [LSP (Liskov Substitution Principle)](https://steady-coding.tistory.com/383) : 리스코프 치환 원칙

> <center>서브 타입은 언제나 자신의 기반 타입으로 교체할 수 있어야 함. ( 객체 지향 4대 특성 中 상속 ) </center>
> <center>⬇</center>
> <center>하위 클래스의 인스턴스는 상위형 객체 참조 변수에 대입해 상위 클래스의 인스턴스 역할을 하는 데 문제가 없어야 함.</center>

## 📍 [ISP (Interface Segregation Principle)](https://steady-coding.tistory.com/385) : 인터페이스 분리 원칙

> SRP _ 클래스 분할 / ISP _ 인터페이스 분할 </br>\
> 클라이언트는 자신이 사용하지 않는 메서드에 의존 관계를 맺으면 안됨. </br>\
> 인터페이스 최소주의 원칙 : 인터페이스를 통해 외부에 제공할 때에는 최소한의 메서드만 제공 / **사용 불가능한 경우나 불필요한 형변환을 줄일 수 있음.**

## 📍 [DIP (Dependency Inversion Principle)](https://steady-coding.tistory.com/388) : 의존 역전 원칙 

> 자신보다 변하기 쉬운 것에 의존하던 것을 추상화된 인터페이스나 상위 클래스를 두어 변하기 쉬운 것의 변화에 영향 받지 않게 하는 것.</br>\
> **즉, 자신보다 변하기 쉬운 것에 의존하지 마라.**

### ⭐️ 추가
> SoC (Separation Of Concents) : 관심이 같은 것끼리는 모으고, 관심이 다른 것은 가능한 서로 영향을 주지 않도록 분리하는 것. 