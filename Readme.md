## Effective Java 3/E(JAVA 8 기준) 스터디

### 2장 객체 생성과 파괴

1. [**생성자 대신 정적 팩터리 메서드를 고려하라.**](./src/test/java/ch02/item01)

2. [**생성자에 매개변수가 많다면 빌더를 고려하라.**](./src/test/java/ch02/item02)

3. [**private 생성자나 열거 타입으로 싱글턴임을 보증하라.**](./src/test/java/ch02/item03)

4. [**인스턴스화를 막으려거든 private 생성자를 사용하라.**](./src/test/java/ch02/item04)

5. [**자원을 직접 명시하지 말고 의존 객체 주입을 사용하라.**](./src/test/java/ch02/item05)

6. [**불필요한 객체 생성을 피하라.**](./src/test/java/ch02/item06)

7. [**다 쓴 객체 참조를 해제하라.**](./src/test/java/ch02/item06)

8. [**finalizer와 cleeaner 사용을 피하라.**](./src/test/java/ch02/item07)

9. [**try-finally보다는 try-with-resources를 사용하라.**](./src/test/java/ch02/item08)

### 3장 모든 객체의 공통 메서드

10. [**equals는 일반 규약을 지켜 재정의하라.**](./src/test/java/ch03/item10)

11. [**equals를 재정의하려거든 hashCode도 재정의하라.**](./src/test/java/ch03/item11)

12. [**toString을 항상 재정의하라.**](./src/test/java/ch03/item12)

13. [**clone 재정의는 주의해서 진행하라.**](./src/test/java/ch03/item13)

14. [**Comparable을 구현할지 고려하라.**](./src/test/java/ch03/item14)

### 4장 클래스와 인터페이스

15. [**클래스와 멤버의 접근 권한을 최소화하라.**](./src/test/java/ch04/item15)

16. [**public 클래스에서는 public 필드가 아닌 접근자 메서드를 사용하라.**](./src/test/java/ch04/item16)

17. [**변경 가능성을 최소화하라.**](./src/test/java/ch04/item17)

18. [**상속보다는 컴포지션을 사용하라.**](./src/test/java/ch04/item18)

19. [**상속을 고려해 설계하고 문서화하라. 그러지 않았다면 상속을 금지하라.**](./src/test/java/ch04/item19)

20. [**추상 클래스보다는 인터페이스를 우선하라.**](./src/test/java/ch04/item20) 

21. [**인터페이스는 구현하는 쪽을 생각해 설계하라.**](./src/test/java/ch04/item21) 

22. [**인터페이스는 타입을 정의하는 용도로만 사용하라.**](./src/test/java/ch04/item22) 

23. [**태그 달린 클래스보다는 클래스 계층구조를 활용하라**](./src/test/java/ch04/item23) 

24. [**맴버 클래스(중첩클래스)는 되도록 static으로 만들라**](./src/test/java/ch04/item24) 

25. [**톱 레벨 클래스는 한 파일에 하나만 담으라.**](./src/test/java/ch04/item25) 

### 5장 제네릭

26. [**로 타입??(로 = raw)은 사용하지 말라.**](./src/test/java/ch05/item26)

27. [**비검사 경고를 제거하라.**](./src/test/java/ch05/item27)

28. [**배열보다는 리스트를 사용하라.**](./src/test/java/ch05/item28)

29. [**이왕이면 제네릭 타입으로 만들라.**](./src/test/java/ch05/item29)

30. [**이왕이면 제네릭 메서드로 만들라.**](./src/test/java/ch05/item30)

31. [**한정적 와일드카드를 사용해 API 유연성을 높이라.**](./src/test/java/ch05/item31)

32. [**제네릭과 가변인수를 함께 쓸 때는 신중하라.**](./src/test/java/ch05/item32)

33. [**타입 안전 이종 컨테이너를 고려하라.**](./src/test/java/ch05/item33)

### 6장 열거타입과 애너테이션

34. [**int 상수 대신 열거 타입을 사용하라.**](./src/test/java/ch06/item34) 

35. [**ordinal 메서드 대신 인스턴스 필드를 사용하라.**](./src/test/java/ch06/item35)

36. [**비트 필드 대신 EnumSet을 사용하라.**](./src/test/java/ch06/item36)

37. [**ordinal 인덱싱 대신 EnumMap을 사용하라**](./src/test/java/ch06/item37)

38. [**확장할 수 있는 열거 타입이 필요하면 인터페이스를 사용하라.**](./src/test/java/ch06/item38)

39. [**명명 패턴보다 애너테이션을 사용하라.**](./src/test/java/ch06/item39)

40. [**@Override 애너테이션을 일관되게 사용하라.**](./src/test/java/ch06/item40)

41. [**정의하려는 것이 타입이라면 마커인터페이스를 사용하라.**](./src/test/java/ch06/item41)

### 7장 람다와 스트림

42. [**익명 클래스보다는 람다를 사용하라.**](./src/test/java/ch07/item42)

43. [**람다보다는 메서드 참조를 사용하라.**](./src/test/java/ch07/item43)

44. [**표준 함수형 인터페이스를 사용하라.**](./src/test/java/ch07/item44)

45. [**(함수형 인터페이스를 만들기 보다) 표준 함수형 인터페이스를 사용하라.**](./src/test/java/ch07/item45)

46. [**스트림에서는 부작용 없는 함수를 사용하라.**](./src/test/java/ch07/item46)

47. [**반환 타입으로는 스트림보다 컬렉션이 낫다.**](./src/test/java/ch07/item47)

48. [**스트림 병렬화는 주의해서 적용하라.**](./src/test/java/ch07/item48)

### 8장 메서드

49. [**매개변수가 유효한지 검사하라.**](./src/test/java/ch08/item49)

50. [**적시에 방어적 복사본을 만들라.**](./src/test/java/ch08/item50)

51. [**메시지 시그니처를 신중히 설계하라.**](./src/test/java/ch08/item51)

52. [**메서드, 생성자의 다중정의는 신중하게 해야 한다.**](./src/test/java/ch08/item52)

53. [**가변인수는 신중히 사용하라.**](./src/test/java/ch08/item53)

54. [**null이 아닌, 빈 컬렉션이나 배열을 반환하라.**](./src/test/java/ch08/item54)

55. [**옵셔널 반환은 신중히 하라.**](./src/test/java/ch08/item55)

56. [**공개된 API 요소에는 항상 문서화 주석을 작성하라.**](./src/test/java/ch08/item56)

### 9장 일반적인 프로그래밍 원칙

57. [**지역변수의 범위를 최소화하라.**](./src/test/java/ch09/item57)

58. [**전통적인 for 문보다는 for-each 문을 사용하라.**](./src/test/java/ch09/item58)

59. [**(직접 만들어서 사용하기 보다) 라이브러리를 익히고 사용하라.**](./src/test/java/ch09/item59)

60. [**정확한 답이 필요하다면 float과 double은 피하라.**](./src/test/java/ch09/item60)

61. [**박싱된 기본 타입보다는 기본 타입을 사용하라.**](./src/test/java/ch09/item61)

62. [**다른 타입이 적절하다면 문자열 사용을 피하라.**](./src/test/java/ch09/item62)

63. [**문자열 연결은 느리니 주의하라.**](./src/test/java/ch09/item63)

64. [**박싱된 기본 타입보다는 기본 타입을 사용하라.**](./src/test/java/ch09/item64)

65. [**객체는 인터페이스를 사용해 참조하라.**](./src/test/java/ch09/item65)

66. [**네이티브 메서드는 신중히 사용하라.**](./src/test/java/ch09/item66)

67. [**최적화는 신중히 하라.**](./src/test/java/ch09/item67)

68. [**일반적으로 통용되는 명명 규칙을 따르라.**](./src/test/java/ch09/item68)

### 10장 예외

69. [**예외는 진짜 예외 상황에만 사용하라.**](./src/test/java/ch10/item69)

70. [**복구할 수 있는 상황에는 검사 예외를, 프로그래밍 오류에는 런타임 예외를 사용하라.**](./src/test/java/ch10/item70)

71. [**필요 없는 검사 예외 사용은 피하라.**](./src/test/java/ch10/item71)

72. [**표준 예외를 사용하라.**](./src/test/java/ch10/item72)

73. [**추상화 수준에 맞는 예외를 던져라.**](./src/test/java/ch10/item73)

74. [**메서드가 던지는 모든 예외를 문서화하라.**](./src/test/java/ch10/item74)

75. [**예외의 상세 메시지에 실패 관련 정보를 담으라.**](./src/test/java/ch10/item75)

76. [**가능한 한 실패 원자적으로 만들라.**](./src/test/java/ch10/item76)

77. [**예외를 무시하지 말라.**](./src/test/java/ch10/item77)
