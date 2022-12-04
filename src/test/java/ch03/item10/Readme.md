## equals는 일반 규약을 지켜 재정의하라

---

### 요약
`꼭 필요한 경우가 아니면 equals를 재정의 하지말자. 재정의시 클래스의 핵심
필드 모두를 빠짐없이 아래 5가시 규약을 지키며 재정의 해야한다.`

---

### equals 메서는 논리적 동치 관계를 구현하며, 다음을 만족한다.
 - 반사성
 - 대칭성
 - 추이성
 - 일관성  
   - 한번 같으면 영원히 같고, 한번 다르면 영원히 다르다. 불변 클래스를 예로 들을 수 있음 (https://limkydev.tistory.com/68)
 - null-아님
 
 ---
 
## 몰랐던 개념
- 오토박싱
  - 기본 타입 : int, long, float, double, boolean 등
  - Wrapper 클래스 : Integer, Long, Float, Double, Boolean 등
  - 박싱: 기본타입 -> Wrapper 클래스
    - int i = 10; Integer wrapperI = 10;
    - 자동으로 바꿔주는게 오토박싱
- 불변 객체
  - 대표적으로 String, Boolean, Integer, Float, Long 등등
  - String a = "aa"; 에서 a = "bb" 로 재할당을 한다해도, a가 참조하고 있는 heap영역의 객체가 바뀌는 것이지 heap영역에 있는 값이 바뀌는 것이 아니다.
    - 아예 새로운 객체를 만들고 a가 그 새로운 객체를 포인팅 하도록 설정. 기존 "aa"는 GC의 대상이 된다. 
    
  
