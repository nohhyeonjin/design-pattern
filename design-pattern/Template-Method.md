# Template Method Pattern
### 정의
알고리즘이 구조적으로 비슷하여 일반화가 가능한 경우 일반화하되, 일부 단계는 서브클래스에서 의존하도록 하는 패턴
<br>
<br>
### 예시
Coffee 클래스와 Tea 클래스의 알고리즘이 구조적으로 비슷한 상황
```java
public class Coffee {
  void prepare(){
    boilWater();    // 공통함수
    brewCoffeeGrinds();
    pourInCup();    // 공통함수
    addSugar();
  }
}

public class Tea {
  void prepare(){
    boilWater();
    steepTeaBag();
    pourInCup();
    addLemon();
  }
}
```
#### 방법1. 일반 상속
```java
public abstract class Beverage {
  abstract prepare();
  boilWater();
  pourInCup();
}

public class Coffee extends Beverage {
  @Override
  prepare();
  
  brewCoffeeGrinds();
  addSugar();
}

public class Tea extends Beverage {
  @Override
  prepare();
  
  steepTeaBag();
  addLemon();
}
```
- prepare 함수에 대해 각 클래스마다 구현 필요
#### 방법2. 템플릿 메소드
```java
public abstract class Beverage {
  final void prepare{   // 템플릿 메소드
    boilWater();
    brew();
    pourInCup();
    addCondiments();
  }
  
  abstract void brew();
  abstract void addCondiments();
  
  void boilWater() { ... }
  void pourInCup() { ... }
}
```
- 중복 코드를 줄일 수 있음
