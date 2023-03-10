# Observer Pattern
### 정의
주제 객체의 데이터의 변경이 발생한 경우 옵저버 객체가 변경된 상태를 받아오는 패턴
<br>
<br>
### Observerless Case
<b>❗의존성이 강함</b>
<br>
주제의 상태값을 확인하는 객체가 추가될 때 마다
주제의 구현 또한 계속 추가/삭제 되어야함
```java
public class WeatherData {
    public void changed(){
        float humidity = getHumidity();
        
        aDisplay.update(humidity);
        bDisplay.update(humidity);
        // ... 객체 추가마다 변경이 이루어짐
    }
}
```
### Observer Case
주제에서 옵저버 인터페이스를 통해 상태값 통신
<br>
주제 구현체는 옵저버들을 가지며, 주제의 변경 시 옵저버들의 업데이트 함수를 호출하는 형태
<br>
``` java
public class WeatherData implements Subject {
    private List<Observer> observers;
    private float humidity;
    
    public void registerObserver(Observer observer) {
        observers.add(observer);
    }
    
    public void notifyObservers(){
        for(Observer observer:observers){
            observer.update(humidity);
        }
    }
}
```
``` java
public class aDisplay implements Observer {
    private float humidity;
    private WeatherData weatherData;
    
    public aDisplay(WeatherData weatherData){
        this.weatherData = weatherData;
        weatherData.registerObserver(this);
    }
    
    public void update(float humidity) {...}
}
```
### IF
<b>하나의 옵저버가 여러 주제의 상태 값을 요구한다면?</b>
```java
observer : Observer {
    subjects : Subject[];
}
```
observer has subject 구조로 변경
<br>
<br>
단, 주제 구현체가 모두 동일해야함
<br>
대안으로 모든 주제의 결과 값을 Data Class로 wrapping & 사용처에서 topic에 따라 data를 적절히 매핑하여 사용
<br>
e.g.) kafka
<br>
<br>
### 특징
1. 주제는 인터페이스만 알면되고 구현 클래스에 대해 알필요 없다.
2. 그렇기 때문에 옵저버 추가/삭제가 자유롭다
3. 주제에는 변경이 일어나지 않는다

인터페이스간 의존 -> 느슨한 결합 -> 변경의 유연성
