# Factory Pattern
### 정의
객체 생성을 캡슐화하여 서브클래스가 어떤 클래스를 생성할지 결정하는 패턴
<br>
<br>
### Factoryless Case
<b>❗저수준 구성요소에 의존</b>
```java
public class PizzaStore {
  public Pizza order(String type) {
    Pizza pizza = null;
    if (type.equals("cheese") {
      pizza = new CheesePizza();
    } else if (type.equals("pepperoni") {
      pizza = new PepperoniPizza();
    } else if (type.equlas("clam") {
      pizza = new ClamPizza();
    }
    
    pizza.prepare();
    pizza.bake();
    pizza.cut();
    
    return pizza;
  }
}
```
Pizza 구상 클래스 변경 시 PizzaStore 클래스까지 변경이 필요할 수 있으니 PizzaStore는 Pizza 구상 클래스에 의존한다
<br>
➡ 고수준 구성요소가 저수준 구성요소에 의존
### Factory Case
<b> ⭕ 추상화에 의존</b>
```java
public abstract class PizzaStore {
  public Pizza order(String type) {
    Pizza pizza = createPizza(type);
    
    pizza.prepare();
    pizza.bake();
    pizza.cut();
    
    return pizza;
  }
  
  abstract Pizza createPizza(String type);   // 팩토리 메서드
}
```
PizzaStore는 Pizza 추상 클래스에 의존, Pizza 구상 클래스는 인터페이스를 구현하며 추상 클래스에 의존
<br>
➡ 고수준 구성요소와 저수준 구성요소가 모두 추상 클래스에 의존
### 특징
- 객체 생성 코드를 메소드로 만들며 코드 중복 제거 가능
- 추상 클래스나 인터페이스를 바탕으로 DIP 성립 가능
