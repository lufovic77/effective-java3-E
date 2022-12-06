## 생성자 대신 정적 팩터리 메서드를 고려하라

---
### 요약
`정적 팩터리 메서드와 public 생성자는 각자의 쓰임새가 있으니 상대적인
장단점을 이해하고 사용하는 것이 좋다. 그렇다 하더라도 정적 팩터리를 사용하는게
유리한 경우가 더 많으므로 무작정 public 생성자를 제공하던 습관이 있다면 고치자.
`
---

### 흔히 사용되는 정적 팩토리 메서드 명명 방식.
```java
public class Main{
    public void main(){
        //from: 매개변수가 1개일 경우,
        Dog dog = Dog.from(name);
        
        //of: 여러 매개변수를 사용할 경우,
        Dog dog = Dog.of(name, age);
        
        //valueOf: from, of 보다 자세한 버전.
        Dog dog = Dog.valueOf(name, age);
        
        //getInstance: 인스턴스를 반환하지만, 같은 인스턴스임을 보장하지 않음.
        Dog dog = getInstance(age);
        
        //newInstance: 매번 새로운 인스턴스를 반환.
        Dog dog = Dog.newIncetance(name, age);
        
        //getType: 다른 클래스의 팩터리 메서드를 사용할 경우.
        Dog dog = Animal.getDog(name);
        
        //newType: 다른 클래스의 팩터리 메서드를 사용, 매번 새로운 인스턴스를 반환.
        Dog dog = Animal.newDog(name);
        
        //getType, newType의 간결한 버전.
        Dog dog = Animal.dog(age);
    }
}

```
`*참고: 위의 명명방식은 반드시 그렇다는 것은 아니다. 또한, 라이브러리나
 다른사람의 코드를 쉽게 이해할 수 있기도 하지만, 생성방식에 대한 확인은 필요하다.
 `
 
### 장점
 - 이름을 가질 수 있다.
    - 생성자는 시그니처가 겹치면 여러 개를 만들 수 없는데, 이름을 다르게 하면 시그니처가 겹쳐도 상황에 맞는걸 여러 개 만들 수 있어서 자유도가 높음.
 - 호출될 때마다 인스턴스를 새로 생성하지 않을 수도 있다.
    - 이미 만들어둔 객체를 캐싱해서 재활용. 요건 싱글턴을 만족시킬때도 좋을것 같다. 
 - 반환 타입의 하위 타입 객체를 반환할 수도 있다.
    - 인터페이스의 구현체나 클래스의 하위 클래스들을 반환할 수 있는 자유도가 있다.
 - 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수도 있다.
 - 정적 팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.
    - JDBC를 사용하면 내가 MySQL을 붙일지, PostgreSQL을 붙일지 모른다.
 
### 단점
 - 상속을 하려면 public이나 protected 생성자가 필요하니 정적 팩터리 메서드만 제공하면 하위 클래스를 만들수 없다.
   (불변 타입으로 만들경우 오히려 장점이 될수 있다)
 - 정적 팩터리 메서드는 프로그래머가 확인작업이 필요하다.(주석을 달자)
    - javadoc 문서화에 관한 이야기다. 
    
## 완벽 공략
### EnumMap과 EnumSet
enum을 key, set으로 쓰는 map, set은 hashMap/hashSet 대신 이걸 쓰는게 좋다.
#### EnumMap
Javadoc에 따르면

"when the map is created. Enum maps are represented internally as arrays. This representation is extremely compact and efficient."

-> hashmap은 key를 bucket에 저장하고 각 bucket이 linked list를 참조 하고 있음. (linkedlist에는 hash(key)가 같은 element가 들어감) 그런데 enummap의 경우 key로 사용할 값이 제한되어 있으므로, 그 갯수만큼 길이를 가진 array를 선언하고. 해당 index에 값을 넣으면 됨.
#### EnumSet
Javadoc에 따르면

"when the set is created. Enum sets are represented internally as bit vectors."

-> hashset은 hashmap과 같은데 map의 value가 있다 없다를 표현하는 지시자 같은 값이 들어감. enumset은 값이 있다 없다만 표시하면 되니까 enummap 처럼 array로 구현하지 않고 10101011 같은 bitvector로 구현이 가능.

출처: 인프런 강의 게시판

## 열거 타입 (enumeration)

- 싱글톤 패턴을 구현할때 사용하기도 함
    - 요거는 뒤에 아이템 3에서 나오는데, 원소가 하나뿐인 enum을 선언하면 항상 같은 객체를 반환하므로 싱글톤을 보장하는 가장 확실한 방법이다.
- enum은 당연히 자바의 클래스처럼 생성자, 메소드, 필드를 가질 수 있다.
    
    ```java
    public enum Country{
    		
        int number;
    	
        KOREA(0), JAPAN(1), CHINA(2);
    
        Country(int number){
            this.number = number;
        }
    }
    ```
    
- enum의 값 비교 시 == 연산자를 이용하는게 낫다.
    - `.equals`를 이용하면 NPE가 발생할 수 있기 때문에 이런 예외 자체를 피하자.

## 인터페이스에 정적 메소드

- 자바 8과 9에서 인터페이스에 대한 변화가 있었다.
    - default method를 가질 수 있다.
        - default 메소드란?
        
        ```java
        public interface InterfaceTest {
            default void hi() {
                System.out.println("HI");
            }
        }
        ```
        
        - default 키워드가 붙은 메소드.
        - 인터페이슨데 로직이 담긴 메소드가 있다!
            - 원래는 기능에 대한 선언만 했지만, 이제는 로직을담은 메소드를 가질 수 있다.
        - 왜 필요할까?
            - 만약 내가 인터페이스를 하나 만들어서 사람들이 잘 쓰고 있는데, 여기다 기능을 하나 추가하고 싶다.
            - 추가한 순간 그걸 다시 오버라이드 해야하니까 오류가 발생할 수 있다.
            - 요때 그냥 default 메소드를 선언해서 넣어주면 인터페이스의 구현체들에서도 수정없이 그냥 사용할 수 있게된다.
    - 정적 메소드를 가질 수 있다.
        - 기본적으로 인터페이스에서 static이 붙고 따로 접근 제어자가 없으면 public이라고 보면 된다.
            - 얘는 default 처럼 안에 로직 구현이 됨. 인스턴스화를 통해 호출하는걸 원하는지(default 메소드), 아니면 그냥 호출하는걸(static) 원하는지에 따라 다르게 사용하면 된다.
        - 자바 9부터 private static 메소드를 가질 수 있다.
            - 인터페이스 내부의 정적 메소드에서 public으로 오픈하지 않고 공통적으로 사용하고 싶은 메소드가 있을 수 있다. 그럴때 private으로 공개 안하고 사용하는 느낌.
        - 다만, private인 필드는 가질 수 없다. (자바 11부턴 가능)
- 요런것들이 도입되면서 인터페이스들의 기능이 풍부해질 수 있게 되었다.

## 서비스 제공자 프레임워크

- 확장 가능한 애플리케이션이란?
    - 코드를 고치지 않아도 외적인 요소를 고쳤을때 다른 동작을 할 수 있는 애플리케이션
    - ex) 콘솔로 출력하던걸 이메일로 보내도록 바꾸기
- 서비스 제공자 등록 API
    - 스프링에서 bean에 등록하던 것을 생각하면 된다.
- 서비스 접근 API
    - 서비스를 가져옴
    - 스프링에서 applicationContext.getBean(HelloService.class) 처럼 빈 가져오는 경우

## 브릿지 패턴

- 구현체와 추상을 분리하고 그 사이에 다리를 놓는 것을 브릿지 패턴이라고 한다.
- 예를 들어 게임에서 챔피온과 스킨이 있다고 생각.
    - 만약 챔피온 내에 스킨의 구현 내용이 직접적으로 들어있다면, 스킨이 추가될때마다 챔피온을 위한 클래스를 계속 만들어줘야한다.
        - KDA 스킨이 적용된 아리
        
        ```java
        class KDA아리{
        	void skillQ { System.out.println("KDA아리의 Q!!")};
        }
        ```
        
        - 만약 PoolParty 스킨이 새롭게 만들어지면
        
        ```java
        class PoolParty아리{
        	void skillQ { System.out.println("PoolParty아리의 Q!!")};
        }
        ```
        
        - 요렇게 새로운 클래스를 또 만들어줘야함.
        - 근데, 아래처럼 내부 필드에 명시해두면
        
        ```java
        class Champion{
        	Skin skin;
        }
        ```
        
        - Skin은 스킨대로 구현체를 추가해두면 그만!
- 요게 스프링 의존 주입같은 개념이랑 거의 비슷한거같다.

## 리플렉션

- 우리가 작성한 모든 클래스들은 jvm의 ClassLoader가 불러와서 메모리 어딘가에 저장한다.
    - 요런 정보들을 reflection이라고 할 수 있음
        - 애노테이션에 사용자가 넘긴 값들을 읽어올수도 있고,
        - 이름에 맞는 메소드를 가져올수도 있고.
    - 요런 정보에 접근하는건 접근 지시자를 무시함 (private 메소드를 가져올수도 있다는 뜻)
    
    ```java
    Class<?> aClass = Class.forName("com.kakao.ade.job.TestService");
    
    Constructor<?> constructor = aClass.getConstructor();
    constructor.newInstance();
    ```
    
    요렇게 문자열로 클래스 정보를 꺼내오면, 이 다음부터는 생성자를 가지고 인스턴스화를 할수도 있고, 정의된 메소드를 가져올 수도 있다.


 
