# JAVA

1. [내용 정리](#내용-정리)

2. [코딩테스트를 위한 문법 정리](#코딩테스트를-위한-문법-정리)

## 내용 정리

- 인스턴스와 객체는 같은 의미로 사용되고 있지만 엄밀히 따져보면 조금 다른 느낌을 갖고있다.
- 인스턴스는 해당 객체가 “특정 클래스로부터 만들어진” 것임을, 즉 해당 객체가 **특정 클래스에 속해있다는 관계성을** 강조한다.
    - Student s = new Student(”감자”);
    - 이때 s(객체)는 Student class의 인스턴스이다. 라고 많이 표현한다.

## 코딩테스트를 위한 문법 정리

```java
String[] arr=new String[6]; //선언과 동시에 null로 초기화
String[] arr={"나는","감자"}; //선언과 동시에 초기값 지정
```

**문자열**

- 인수로 받은 값을 String으로 변환
    - `String.valueOf(5)`
- 쪼개기
    - `String.split()` : 입력받은 정규표식을 기준으로 문자열을 나누어 배열(Array)로 반환
    - `StringTokenizer`클래스 사용
    
    [☕ 자바 split / StringTokenizer - 문자열 자르기 비교](https://inpa.tistory.com/entry/JAVA-☕-Split-StringTokenizer-문자열-자르기-비교하기)
    

- 인수 , 인자, 매개변수, Parameter, Argument ?
    
    **Parameter** = 인자, 매개변수 (함수를 정의할 때 사용)
    
    **Argument** = 인수 (함수에 실제로 값을 넘겨줄 때 사용)
    
    **`reference`**
    
    [매개변수(Parameter)와 인수(Argument)의 차이점은 무엇일까?](https://7942yongdae.tistory.com/155)
    

**배열 정렬하기** 

```java
int[] arr = {4,2,6,3,9}
```

- 오름차순 정렬
    - `Arrays.sort(arr)`
- 내림차순 정렬
    - `Arrays.sort(arr,Collections.reverseOrder())`
- 특정 구간 정렬
    - `Arrays.sort(arr, 0, 2)`
- 요소의 인덱스 찾기
    - Arrays.*sort*(arr); //오름차순 정렬 후
    - `Arrays.*binarySearch*(arr, 4)` // 4의 index 반환(결과: 2)

🍬 

- 배열 → List
    - `List<int[]> list =Arrays.asList(arr)`
- 배열의 특정 범위 가져오기
    - `Arrays.copyOfRange(arr,0,3)`
