# State Pattern
### 정의
미리 정해진 상태 전환 규칙에 따라 알아서 상태를 바꾸는 패턴
<br>
상태가 변경됨에 따라 행동을 바꿀 수 있는 패턴
<br>
<br>
### Stateless Case
<b>❗확장이 어려움</b>
<br>
새로운 상태가 발생할 때 마다
상태와 상태를 확인하는 조건문을 추가해야함
```java
public class Machine {
  // 4가지 상태
  final static int SOLD_OUT = 0;
  final static int NO_COIN = 1;
  final static int HAS_COIN = 2;
  final static int SOLD = 3;
  
  // 초기 상태
  int state = SOLD_OUT;
  
  public void 동전투입() {
    if (state == NO_COIN) {
      state = HAS_COIN;
    } else if (state == SOLD_OUT) {
      ...
    } else {
      ...
    }
  }
  
  public void 동전반환() {
    if (state == HAS_COIN) {
      state = NO_COIN;
    } else if (state == NO_COIN){
      ...
    } else {
      ...
    }
  }
  
  public void 손잡이돌리기() {
    if (state == HAS_COIN) {
      state = SOLD;
    } else if (state == SOLD) {
      ...
    } else {
      ...
    }
  }
  
  ...
  
}
```
### State Case
상태 인터페이스를 정의하여 모든 상태를 대상으로 상태 클래스 구현
<br>
조건문 대신 상태 클래스에 작업 위임
<br>
``` java
public class Machine {
  State soldOutState;
  State noCoinState;
  State hasCoinState;
  State soldState;
  
  State state = soldOutState;
  
  public void 동전투입() {
    state.동전투입();
  }
  
  public void 동전반환() {
    state.동전반환();
  }
  
  public void 손잡이돌리기() {
    state.손잡이돌리기();
  }
}
```
``` java
public class NoCoinState implements State {
  Machine machine;
  
  public NoCoinState(Machine machine) {
    this.machine = machine;
  }
  
  public void 동전투입() {
    machine.setState(machine.getHasCoinState());
  }
  
  public void 동전반환() {
    ...
  }
  
  public void 손잡이돌리기() {
    ...
  }
}
```
### 특징
1. 각 상태의 행동을 캡슐화 가능하다
2. 새로운 상태가 추가되더라도 변경에는 닫혀있고 확장에는 열려있다 (OCP)
