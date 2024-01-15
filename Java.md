# JAVA

1. [내용 정리](#내용-정리)
    - [Collection](#Collection)
    - [Vector](#Vector)
2. [코딩테스트를 위한 문법 정리](#코딩테스트를-위한-문법-정리)
    - [여러가지 정리](#모음)
    - [배열에 요소 추가하기](#Java-배열에-새-요소를-추가하기)
    - [int와 Integer의 차이점](#int-VS-Integer)
    - [String 배열을 int배열로 변환하기](#String-배열을-int배열로-변환하기)
    - [stream.foreach()와 for문의 차이점](#Collection.foreach()과-Collection.stream().foreach())

## 내용 정리

- 인스턴스와 객체는 같은 의미로 사용되고 있지만 엄밀히 따져보면 조금 다른 느낌을 갖고있다.
- 인스턴스는 해당 객체가 “특정 클래스로부터 만들어진” 것임을, 즉 해당 객체가 **특정 클래스에 속해있다는 관계성을** 강조한다.
    - Student s = new Student(”감자”);
    - 이때 s(객체)는 Student class의 인스턴스이다. 라고 많이 표현한다.
 - **OCP 원칙**
     - Open for extension: 확장에는 열려있고
     - Closed for modification: 기존 코드의 변경에는 닫혀있자.  
    새로운 기능을 추가해도 기존 코드에 변경이 없다면, OCP원칙을 지키는 코드라고 이야기할 수 있다.
  
### Collection

[[Java] 자바 - Collection이란? (컬렉션과 제네릭)](https://kadosholy.tistory.com/117#google_vignette)

### Vector

[알기 쉬운 JAVA 벡터 클래스(Vector class)에 대해 알아보자](https://byungmin.tistory.com/9)  



## 코딩테스트를 위한 문법 정리

```java
String[] arr=new String[6]; //선언과 동시에 null로 초기화
String[] arr={"나는","감자"}; //선언과 동시에 초기값 지정
```

### 모음✍🏻
**문자열**

- 인수로 받은 값을 String으로 변환
    - `String.valueOf(5)`
- 쪼개기
    - `String.split()` : 입력받은 정규표식을 기준으로 문자열을 나누어 배열(Array)로 반환
    - `StringTokenizer`클래스 사용
    
    [☕ 자바 split / StringTokenizer - 문자열 자르기 비교](https://inpa.tistory.com/entry/JAVA-☕-Split-StringTokenizer-문자열-자르기-비교하기)
    

    

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
    - `Arrays.copyOfRange(arr,0,3)` : arr의 0~2번째 배열 반환
    - `Arrays.copyOf(arr,3)` : arr의 0~2번째 배열 반환
      
### 📌 Java 배열에 새 요소를 추가하기

1. array → List, List→ array

```java
public static Integer[] addX(Integer myArray[], int x) {
       int i;
       //turn array into ArrayList using asList() method
       List arrList = new ArrayList( Arrays.asList(myArray));

       // adding a new element to the array
       arrList.add(x);

       // Transforming the ArrayList into an array
       myArray = arrList.toArray(myArray);
       return myArray;
   }
```

2. 처음부터 입력 값보다 더 큰 배열 선언하기(제일 쉬움)

```java
class ArrayDemo {
   //Method to add an element x into array myArray
   public static int[] addX(int myArray[], int x) {
       int i;

       // create a new array of a bigger size (+ one element)
       int newArray[] = new int[myArray.length + 1];

       // insert the elements from the old array into the new one
       for (i = 0; i < myArray.length; i++)
           newArray[i] = myArray[i];

       newArray[myArray.length] = x;
       return newArray;
   }

   public static void main(String[] args) {
       int i;

       // initial array of size 10
       int arr[]
               = {0, 1, 2, 45, 7, 5, 17};

       // print the initial array
       System.out.println("Initial Array: " + Arrays.toString(arr));

       // element to be added
       int x = 28;

       // call the addX method to add x in arr
       arr = addX(arr, x);
       // print the updated array
       System.out.println("Array with " + x + " added:" + Arrays.toString(arr));
   }
}
```

3. System.arrayCopy()

```java
class ArrayDemo {
   private static Integer[] addElement(Integer[] myArray, int newElement) {
       //we create a new Object here, an array of bigger capacity
       Integer[] array = new Integer[myArray.length + 1];
       System.arraycopy(myArray, 0, array, 0, myArray.length);
       array[myArray.length] = newElement;
       return array;
   }

   public static void main(String[] args) {
       Integer[] myArray = {20, 21, 3, 4, 5, 88};
       System.out.println("myArray before adding a new element: " + Arrays.toString(myArray));
       myArray = addElement(myArray, 12);
       System.out.println("myArray before adding a new element: " + Arrays.toString(myArray));
   }
}
```

![Untitled (9)](https://github.com/mungsil/TIL/assets/107127451/c5c3be2c-5fa4-487a-9bd7-65bebde59cc3)

4. Arrays.copyOf()

```java
class ArrayDemo {
   private static <X> X[] addElement(X[] myArray, X element) {
       X[] array = Arrays.copyOf(myArray, myArray.length + 1);
       array[myArray.length] = element;
       return array;
   }
   public static void main(String[] args) {
       Integer[] myArray = {20, 21, 3, 4, 5, 88};
       System.out.println("myArray before adding a new element: " + Arrays.toString(myArray));
       myArray = addElement(myArray, 12);
       System.out.println("myArray before adding a new element: " + Arrays.toString(myArray));
   }
}
```

<aside>
💡 **Arrays.copyOf**

Copies the specified array, truncating or padding with nulls (if necessary) so the copy has the specified length. For all indices that are valid in both the original array and the copy, the two arrays will contain identical values. For any indices that are valid in the copy but not the original, the copy will contain null. Such indices will exist if and only if the specified length is greater than that of the original array. The resulting array is of exactly the same class as the original array.
Params:
original – the array to be copied newLength – the length of the copy to be returned
Returns:
a copy of the original array, truncated or padded with nulls to obtain the specified length

Ex) {1,2,3,4}일 때 newLength=2 입력하면 앞에서부터 잘라서 {1,2} return
</aside>

`출처`

[Java에서 배열에 새 요소를 추가하는 방법](https://codegym.cc/ko/groups/posts/ko.417.java-eseo-baeyeol-e-sae-yosoleul-chugahaneun-bangbeob)

### 📌 int VS Integer

자바의 자료형에는 Primitive type과 Reference type이 있다. (기본형과 참조형) 

int는 기본형, Integer는 이를 감싸는 래퍼 클래스이다. 간단하게 말하면 그렇고, 아래 블로그에 잘 정리되어있어서 아래 블로그를 보면 될 것 같다!

[[Java]int 와 Integer 의 차이](https://velog.io/@steadygo247/Javaint-와-Integer-의-차이)

➕ **전체적인 자료형에 대한 정리**

[[Java] 자료형(Data Type) 이해하기 : 기본 / 참조 자료형, 래퍼 클래스](https://adjh54.tistory.com/119)

➕ **int배열과 Integer배열 사이의 변환**

- int[]→ Integer[]
    
    ```java
    int a[] = {1,2,3,4};
    Integer b[] = Arrays.stream(a).boxed().toArray(Integer[]::new);
    ```
    
- Integer[] → int[]
    
    ```java
    int a = Arrays.stream(b).mapToInt(Integer::intValue).toArray();
    ```
    
- Integer클래스의 intValue 메서드_ Integer 객체를 int형 정수로 변환하여 반환한다.
### 📌 String 배열을 int배열로 변환하기

1번 방법

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
String s = br.readLine();
int[] inputs = Arrays.stream(s.split(" ")).mapToInt(Integer::parseInt).toArray();
```
→ 간결하다.

2번 방법

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
int numCount = Integer.parseInt(br.readLine());

int[] arr = new int[numCount];

StringTokenizer st = new StringTokenizer(br.readLine());
for(int i=0 ; i < numCount ; i++) {
    arr[i] = Integer.parseInt(st.nextToken());
}
```
→ StringTokenizer는 공백이 있다면 뒤에 문자열이 공백 자리를 땡겨 채우도록 하므로 1번 방법보다빠르다.


🔎mapToInt

stream 내에 있는 Wrapper class를 primitive type으로 변환하는 언박싱을 수행하는 함수이다.

다른 방법: for문을 사용해주면 된다.


### 📌 Collection.foreach()과 Collection.stream().foreach()

[Java Collections.forEach vs Collections.stream().forEach()](https://wnwngus.tistory.com/59)

결론_ 되도록 Collection.foreach()를 사용하자. 굳이 Collection.stream.().foreach()를 써서 Stream 객체 생성으로 인한 오버헤드를 감수할 필요는 없다. (map(), filter() 등의 가공이 필요한 경우 제외)

➕ **Collection.for메서드와 Collection.foreach메서드 비교.**

for문과 비교하면 Collection.foreach()는 인덱스를 사용하지 않기 때문에 코드가 간결해진다는 장점이 있다. 따라서 당연하게도 인덱스를 사용하지 않기 때문에 요소의 인덱스를 알아내지 못해 불편한 상황이 생길 수 있다. foreach문에서 요소의 인덱스를 알아내려면 인덱스 변수를 따로 선언해야하기 때문이다.
  
