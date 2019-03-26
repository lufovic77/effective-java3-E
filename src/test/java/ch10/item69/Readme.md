
## 예외는 진짜 예외 상황에만 사용하라.

---

#### 예외는 오직 예외 상황에서만 써야한다. 

##### 아래와 같이 절대로 일상적인 제어 흐름용으로 쓰여선 안된다.
```java

try{
    int i = 0;
    while(true)
        range[i++].climb();
} catch (ArrayIndexOutOfBoundsException e) {
    
}
```

##### 일상적인 제어 흐름으로 변경한 코드
```java

for(Mountain m : range)
    m.climb();

```


#### 잘 설계된 API라면 클라이언트가 정상적인 제어 흐름에서 예외를 사용할 일이 없게 해야 한다.

##### Iterator 인터페이스의 next, hasNext가 각각 상태 의존적 메서드와 상태 검사 메서드에 해당한다.
```java
for(Iterator<Foo> i = collection.iterator(); i.hasNext();){
    Foo foo = i.next();
}
```

##### Iterator에 hasNext가 없을 경우, 클라이언트가 대신 해야한다.
```java
try{
    Iterator<Foo> i = collection.iterator();
    while(true)
        Foo foo = i.next();
        ...
    
} catch (NoSuchElementException e){}
```
---


#### hasNext와 같은 상태 검사 메서드를 사용하거나 옵셔널이나 null을 반환할 수도 있다.

##### 상태검사 메서드, 옵셔널, 특정 값 중 하나를 선택하는 지침

1. 외부 동기화 없이 여러 스레드가 동시에 접근할 수 있거나 외부 요인으로 상태가 변할 수 있다면 옵셔널이나 특정
값을 사용한다. 상태 검사 메서드와 상태 의존적 메서드 호출사이에 객체의 상태가 변할 수 있기 때문이다.

2. 성능이 중요한 상황에서 상태 검사 메서드가 상태 의존적 메서드의 작업 일부를 중복 수행한다면 옵셔널이나 특정
값을 사용한다.

```
상태 검사 메서드: hasNext와 같은 상태를 검사하는 메서드
상태 의존적 메서드: next와 같이 상태검사 메서드에 의존적인 메서드

상태 검사 메서드가 상태 의존적 메서드의 작업 일부를 중복 수행할 경우를 말하는거 같다.
```

3. 다른 모든 경우엔 상태 검사 메서드 방식이 조금 더 낫다고 할 수 있다. 가독성이 살짝 더 좋고,
잘못 사용했을 때 발견하기가 쉽다. 상태 검사 메서드 호출을 깜빡 잊었다면 상태 의존적 메서드가 예외를 던져
버그를 확실히 드러낼것이다. 반면 특정 값을 넘기는 방식은 지나쳐도 발견하기가 어렵다.
(옵셔널은 해당하지 않는다.isPresent와 같은 상태를 검사하는 메서드가 있다.) 


### 요약

`
예외는 예외 상황에서 쓸 의도로 설계 되었다. 정상적인 제어 흐름에서 사용해서는 안되며, 이를 프로그래머에게
강요하는 API를 만들어서도 안 된다.
`