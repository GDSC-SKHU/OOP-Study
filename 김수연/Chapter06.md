# 6장

## 목차
- Adapter Pattern
- Proxy Pattern
- Decorator Pattern
- Singlton Pattern
- Template Method Pattern
- Factory Method Pattern
- Strategy Pattern
- Template Callback Pattern


## 디자인 패턴
- 객체 지향 특성 = 도구
  
   설계 원칙 = 도구를 올바르게 사용하는 방법
  
  디자인 패턴 = 레시피

- 디자인 패턴은 상속, 인터페이스, 합성(객체를 속성으로 사용)을 이용한다

# 1. Adapter Pattern

> 호출당하는 쪽의 메서드를 호출하는 쪽의 코드에 대응하도록 중간에 변환기를 통해 호출하는 패턴

- 서로 다른 두 인터페이스 사이에 통신이 가능하게 하는 것
- 개방 폐쇄 원칙을 활용한 설계 패턴
- 객체를 속성으로 만들어 참조하는 디자인 패턴


## 어댑터 패턴을 적용한 코드
```java
// AdapterServiceA 클래스
public class AdapterServiceA {

    ServiceA sa1 = new ServiceA();

    void runService(){
        sa1.runServiceA();
    }
}
```
```java
// AdapterServiceB 클래스
public class AdapterServiceB {

    ServiceB sa1 = new ServiceB();

    void runService() {
        sa1.runServiceB();
    }
}
```
> ServiceA와 ServiceB의 메소드를 runService()라고 하는 같은 이름의 메소드로 호출해서 사용할 수 있게 해주는 변환기이다. 

```java
// 실행클래스
public class ClientWithAdapter {

    public static void main(String[] args) {
        AdapterServiceA asa1 = new AdapterServiceA();
        AdapterServiceB asb1 = new AdapterServiceB();

        asa1.runService();
        asb1.runService();
    }
}

// 결과
ServiceA
ServiceB
```
<img src="./image/i31.png " width=500 height=300 />

-> 클라이언트가 변환기를 통해 runService()라는 동일한 메소드명으로 두 객체의 메소드를 호출하는 것을 볼 수 있다.

# 2. Proxy Pattern

> 제어 흐름을 조정하기 위한 목적으로 중간에 대리자를 두는 패턴

**프록시는 대리자, 대변인**

- 대리자는 실제 서비스와 같은 이름의 메서드를 구현한다. 이 때 인터페이스를 사용한다.

- 대리자는 **실제 서비스에 대한 참조 변수**를 갖는다(합성).

- 대리자는 **실제 서비스의 같은 이름을 가진 메서드를 호출**하고 그 값을 클라이언트에게 돌려준다.

- 대리자는 실제 서비스의 메서드 호출 전후에 별도의 로직을 수행할 수도 있다.

> 프록시 패턴은 실제 서비스 메서드의 반환값에 가감하는 것을 목적으로 하지 않고 제어의 흐름을 변경하거나 다른 로직을 수행하기 위해 사용한다.

📌 "제어 흐름을 조정하기 위한 목적으로 중간에 대리자를 두는 패턴"
개방 폐쇄 원칙과 의존 역전 원칙이 적용된 설계 패턴

## 프록시 패턴의 시퀀스 다이어그램
<img src="./image/i32.png " width=500 height=300 />

## 프록시 패턴을 적용한 코드

```java
// IService 인터페이스 

public interface IService {

    String runSomething();
}
```

```java
// Service 클래스

public class Service implements IService {

    @Override
    public String runSomething() {
        return "Proxy Pattern";
    }
}
```

```java
// Proxy 클래스

public class Proxy implements IService {

    IService service1;

    @Override
    public String runSomething() {
        System.out.println("호출에 대한 흐름 제어가 주목적, 반환 결과를 그대로 전달");

        service1 = new Service();
        return service1.runSomething();
    }

}
```


```java
// 실행클래스

package study.weeok09.pattern;

public class ClientWithProxy {

    public static void main(String[] args) {
        // 프록시를 이용한 호출
        IService proxy = new Proxy();
        System.out.println(proxy.runSomething());
        
    }
}

// 결과
호출에 대한 흐름 제어가 주목적, 반환 결과를 그대로 전달
Proxy Pattern
```

> ClientWithProxy 클래스에서는 IService 가져와 runSomething() 메소드를 호출한다. 실제로는 Proxy의 runSomething() 메소드가 실행되며, 전처리와 후처리가 추가된 결과가 출력된다.

📌 **프록시 패턴을 사용하여 AOP를 구현하면 핵심 로직에 대한 수정 없이 공통 기능을 추가할 수 있으며, 코드의 재사용성과 유지보수성을 향상시킬 수 있습니다.**

->  코드를 잘 보면 인터페이스를 중간에 두어 구체클래스들에게 영향을 받지 않게 설계되어 있다. 또한, 직접 접근하지 않고 Proxy를 통해서 한번 더 우회해서 접근하도록 되어있다. (제어 흐름을 조정하기 위함)

# 3. Decorator Pattern
> 메서드 호출의 반환값에 변화를 주기 위해 중간에 장식자를 두는 패턴

**📌 데코레이터 패턴은 프록시 패턴과 구현 방법이 같다. 다만 프록시 패턴은 클라이언트가 최종적으로 돌려 받는 반환값을 조작하지 않고 그대로 전달하는 반면 데코레이터 패턴은 클라이언트가 받는 반환값에 장식을 덧입힌다.**

1. 프록시 패턴
- 제어의 흐름을 변경하거나 별도의 로직 처리를 목적으로 한다.
- 클라이언트가 받는 반환값을 특별한 경우가 아니면 변경하지 않는다.

2. 데코레이터 패턴
- 클라이언트가 받는 반환값에 장식을 더한다.

- 장식자는 **실제 서비스와 같은 이름의 메서드**를 구현한다. 이때 인터페이스를 사용한다.

- 장식자는 **실제 서비스에 대한 참조 변수를 갖는다(합성)**.

- 장식자는 **실제 서비스의 같은 이름을 가진 메서드를 호출하고, 그 반환값에 장식을 더해 클라이언트에게 돌려**준다.

- 장식자는 실제 서비스의 메서드 호출 전후에 별도의 로직을 수행할 수도 있다.

## 데코레이션 패턴을 적용한 코드

```java
// IService 인터페이스
public interface IService {

    public abstract String runSomething();
}

```


```java
// Service 클래스
public class Service implements IService{

    @Override
    public String runSomething() {
        return "서비스 짱!";
    }
}

```


```java
// Decoreator 클래스
public class Decoreator implements IService{

    IService service;

    @Override
    public String runSomething() {
        System.out.println("호출에 대한 장식 주목적, 클라이언트에게 반환 결과에 장식을 더하여 전달");
        service = new Service();
        return "정말" + service.runSomething(); // "정말"이라는 장식을 더함
    }
}
```
 

 ```java
// 실행클래스
public class ClientWithDecolator {

    public static void main(String[] args) {
        IService decoreator = new Decoreator();
        System.out.println(decoreator.runSomething());
    }
}

// 결과
호출에 대한 장식 주목적, 클라이언트에게 반환 결과에 장식을 더하여 전달
정말서비스 짱!
 ```

-> 반환값에 장식을 더한다는 것을 빼면 프록시 패턴과 동일하다. 

-> 실제 서비스의 반환 값을 이쁘게 장식하는 패턴이 데코레이터 패턴

# 4. Singlton Pattern

> 클래스의 인스턴스, 즉 객체를 하나만 만들어 사용하는 패턴 

> 싱글톤 패턴은 오직 인스턴스를 하나만 만들고 그것을 계속해서 재사용한다.

- new를 실행할 수 없도록 생성자에 private 접근 제어자를 지정한다.
- 유일한 단일 객체를 반환할 수 있는 정적 메서드가 필요하다.
- 유일한 단일 객체를 참조할 정적 참조 변수가 필요하다.

```java
public class Singleton {
  static Singleton singletonObject;// 정적 참조 변수
  
  private Singleton() {};// private 생성자
  // private 생성자로 외부에서의 인스턴스 생성 방지

  //객체 반환 정적 메서드
  public static Singleton getInstance() {
    if (singletonObject == null) {
      singletonObject = new Singleton();
    }
    
    return singletonObject;
  }
}
```

⭐️ 싱글턴 패턴의 특징
1. private 생성자를 갖는다.
2. 단일 객체 참조 변수를 정적 속성으로 갖는다.
3. 단일 객체 참조 변수가 참조하는 단일 객체를 반환하는 getInstance()정적 메서드를 갖는다.
4. 단일 객체는 쓰기 가능한 속성을 갖지 않는 것이 정석이다.


💡 커넥션 풀, 스레드 풀, 디바이스 설정 객체 등과 같은 경우 인스턴스를 여러 개 만들게 되면 불필요한 자원을 사용하게 되고, 또 프로그램이 예상치 못한 결과를 낳을 수 있다. 
- 이때 싱클톤 패턴을 사용해서 애플리케이션 전역에서 단 하나의 인스턴스만을 생성하고 사용하자 ! 

-> 이를 통해 여러 곳에서 동일한 인스턴스에 접근하여 데이터를 공유하거나 중복 생성을 방지

# 5. Template Method Pattern

>상위 클래스의 견본 메서드에서 하위 클래스가 오버라이딩한 메서드를 호출하는 패턴


- 상위 클래스에 공통 로직을 수행하는 템플릿 메서드와 하위 클래스에 오버라이딩을 강제하는 추상 메서드 또는 선택적으로 오버라이딩할 수 있는 훅 메서드를 두는 패턴
- 구성 요소
  - 템플릿 메서드 : 공통 로직 수행, 로직 중에 하위 클래스에서 오버라이딩한 추상 메서드/훅 메서드를 호출
  - 템플릿 메서드에서 호출하는 추상 메서드 : 하위 클래스가 반드시 오버라이딩해야 한다.
  - 템플릿 메서드에서 호출하는 훅 메서드 : 하위 클래스가 선택적으로 오버라이딩한다.



# 6. Factory Method Pattern

  > 오버라이드된 메서드가 객체를 반환하는 패턴 (객체 생성을 캡슐화)


- 하위 클래스에서 팩터리 메서드를 오버라이딩해서 객체를 반환하게 하는 것


## 팩터리 매서드 패턴를 적용한 코드

```java
// 추상클래스 Animal
public abstract class Animal {
    // 추상 팩터리 메서드
    abstract AnimalToy getToy();
}
```


```java
// 추상클래스 AnimalToy = 팩터리 메서드가 생성할 객체의 상위 클래스
public abstract class AnimalToy {

    abstract void identify();
}
```


```java
/ Dog 클래스
public class Dog extends Animal{

    // 추상 팩터리 메서드 오버라이딩
    @Override
    AnimalToy getToy() {
        return new DogToy();
    }
}
```


```java
// Cat 클래스
public class Cat extends Animal {

    // 추상 팩터리 메서드 오버라이딩
    @Override
    AnimalToy getToy() {
        return new CatToy();
    }

}
```


```java
// Dog의 장난감 클래스
public class DogToy extends AnimalToy{

    @Override
    void identify() {
        System.out.println("나는 테니스 공! 강아지의 친구");
    }
}
```

```java
// Cat 의 장난감 클래스
public class CatToy extends AnimalToy{

    @Override
    void identify() {
        System.out.println("난 고양이니까 캣타워 갖고싶어.");
    }
}
```


```java
/ 실행클래스
public class Driver {

    public static void main(String[] args) {
        // 팩터리 메서드를 보유한 객체들 생성
        Animal boli = new Dog();
        Animal kitty = new Cat();

        // 팩터리 메서드가 반환하는 객체들
        AnimalToy  boltBall = new DogToy();
        AnimalToy  kittyTower = new CatToy();

        // 팩터리 메서드가 반환한 객체들을 사용
        boltBall.identify();
        kittyTower.identify();
    }
}

// 결과
나는 테니스 공! 강아지의 친구
난 고양이니까 캣타워 갖고싶어.
```

## 시퀀스 다이어그램

<img src="./image/i33.png " width=450 height=300 />

-> 오버라이드된 메서드가 객체를 반환하는 패턴

# 7. Strategy Pattern
## 디자인 패턴의 꽃인 전략 패턴
> 클라이언트가 전략을 생성해 전략을 실행할 컨텍스트에 주입하는 패턴

- ⭐️ 구성 요소
  - 전략 메서드를 가진 전략 객체
  - 전략 객체를 사용하는 컨텍스트 (전략 객체의 사용자/소비자)
  - 전략 객체를 생성해 컨텍스트에 주입하는 클라이언트 (제3자, 전략 객체의 공급자)

<img src="./image/i34.png " width=400 height=300 />

- 템플릿 메서드 패턴과 유사한데, 같은 문제의 해결책으로 상속을 이용할 땐 템플릿 메서드 패턴, 객체 주입을 이용할 땐 전략 패턴을 사용한다.

## 전략패턴을 적용한 코드 

```java 
/ 전략 인터페이스
public interface Strategy {
    public abstract void runStrategy();
}
```


```java 
// 총
public class StrategyGun implements Strategy{

    @Override
    public void runStrategy() {
        System.out.println("탕! 탕!");
    }
}
```

```java 
// 검
public class StrategySword implements Strategy{

    @Override
    public void runStrategy() {
        System.out.println("챙 챙챙");
    }
}
```

```java 
// 활
public class StrategyBow implements Strategy{

    @Override
    public void runStrategy() {
        System.out.println("피슝~ , 활");
    }

}
```

```java 
// 무기를 사용할 군인 (전략을 사용할 컨텍스트)
public class Soldier {

    void runContext(Strategy strategy) {
        System.out.println("전투 시작");
        strategy.runStrategy();
        System.out.println("전투 종료");
    }
}
```

```java 
// 무기를 조달해서 군인에게 지급해 줄 보급 장교
// = 전략을 생성해 컨텍스트에 주입할 클라이언트
public class Client {

    public static void main(String[] args) {
        Strategy strategy = null;
        Soldier rambo = new Soldier();

        // 총을 람보에게 전달해서 전투를 수행하게 한다.
        strategy = new StrategyGun();
        rambo.runContext(strategy);

        System.out.println();

        // 검을 람보에게 전달해서 전투를 수행하게 한다.
        strategy = new StrategySword();
        rambo.runContext(strategy);

        System.out.println();

        // 활을 람보에게 전달해서 전투를 수행하게 한다.
        strategy = new StrategyBow();
        rambo.runContext(strategy);
    }
}

// 결과
전투 시작
탕! 탕!
전투 종료

전투 시작
챙 챙챙
전투 종료

전투 시작
피슝~ , 활
전투 종료
```

- 전략 - 무기(총, 칼, 활)
- 컨텍스트 - 군인
- 클라이언트 - 보급장교

> 보급 장교가 무기를 군인에게 지급해 주면 군인은 주어진 무기에 따라 전투를 수행하게 된다.


-> 전략을 다양하게 변경해가면서 컨텍스트를 실행할 수 있다. 

-> 전략 패턴은 다양한 곳에서 다양한 문제 상황의 해결책으로 사용된다. 

-> 템플릿 메서드 패턴과 유사하며 같은 문제의 해결책으로 상속을 이용하는 템플릿 메서드 패턴과 객체 주입을 통한 전략 패턴 중에서 선택/적용할 수 있다. 

-> 단일 상속만이 가능한 자바 언어에서는 상속이라는 제한이 있는 템플릿 메서드 패턴보다는 전략 패턴이 더 많이 활용된다.


# 8. Template Callback Pattern

> 전략을 익명 내부 클래스로 구현한 전략 패턴

- 전략 패턴의 변형으로, DI에서 사용하는 특별한 형태의 전략 패턴
- 전략 패턴과 모든 것이 동일한데 전략을 익명 내부 클래스로 정의해서 사용한다.

## 전략패턴의 코드를 템플릿 콜백 패턴의 코드로 변경


```java
// 전략 인터페이스
public interface Strategy {
    public abstract void runStrategy();
}
```


```java
// Soldier 코드
public class Soldier {

    void runContext(String weaponSound) {
        System.out.println("전투 시작");
        executeWeapon(weaponSound).runStrategy();
        System.out.println("전투 종료");
    }
    
    // 전략을 생성하는 코드가 Soldier 클래스 내부로 옮겨짐
    private Strategy executeWeapon(final String weaponSound) {
        return new Strategy() {
            @Override
            public void runStrategy() {
                System.out.println(weaponSound);
            }
        };
    }
}
```

> 익명 내부 클래스를 사용하기 때문에 StrategyGun, StrategySword, StrategyBow 클래스는 필요없다. (전략을 생성하는 코드를 Soldier 클래스 내부로 구현)

```java
public class Client {

    public static void main(String[] args) {
        Soldier rambo = new Soldier();

        rambo.runContext("총 탕탕 총총");

        System.out.println();

        rambo.runContext("칼! 칼 스윽");

        System.out.println();

        rambo.runContext("도끼 도독 퍽");
    }
}


//결과
전투 시작
총 탕탕 총총
전투 종료

전투 시작
칼! 칼 스윽
전투 종료

전투 시작
도끼 도독 퍽
전투 종료
```


-> 클라이언트에서 구현했으면 중복됐을 전략을 생성하는 코드를 컨텍스트로 이관했기 때문에 클라이언트 클래스의 코드에서는 총을 쏘는 효과음인지, 칼을 쓰는 효과음인지, 도끼를 쓰는 효과음인지만 넣어주면 된다. 

-> 스프링은 이런 형식으로 리팩터링된 템플릿 콜백 패턴을 DI에 적극 활용하고 있다. 따라서 스프링을 이해하고 활용하기 위해서는 전략 패턴과 템플릭 콜백 패턴, 리팩터링된 템플릿 콜백 패턴을 잘 기억해두어야 한다!