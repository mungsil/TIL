# 알고리즘

### 시간복잡도와 공간복잡도

`시간 복잡도`는 **입력의 크기**와 *문제를 해결하는데 걸리는 시간*의 상관관계를 의미한다.

`Big-O 표기법`은 주어진 식을 값이 가장 큰 대표항만 남겨서 나타내는 방법이다.

O(1) < O(lgN) < O(N) < O(NlgN) < O( $N^2$) < O( $2^N$) < O(N!)

![Untitled](https://github.com/mungsil/TIL/assets/107127451/aa0b67ed-0ec3-416b-a0f3-5d7d0667a72f)


주어진 문제를 보고 떠올린 풀이를 바로 적용하지 말고 내 풀이가 이 문제를 제한 시간 내에 해결할 수 있는 지를 점검하자. 예를 들어, N이 500인데 O( $2^N$)풀이를 생각했다면 잘못된 풀이이다.

    
- 문제 1 (정답 풀이)
    
    ```java
    /*
    3의 배수이거나 5의 배수인 수를 모두 합한 값을 반환하는 함수
     */
    public class Main {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            int input = scanner.nextInt();
            Main main = new Main();
    
            System.out.println(main.answer(input));
        }
    
        public int answer(int input) {
            int sum=0;
            for (int i = 1; i <= input; i++) {
                if (i % 3 == 0 | i % 5 == 0) {
                    sum =sum+ i;
                }
            }
            return sum;
        }
    
    }
    ```
    

### 공간 복잡도

입력의 크기와 문제를 해결하는데 필요한 공간의 상관관계

- 512MB = 1.2억개의 int를 선언할 수 있다.

`reference`

[[바킹독의 실전 알고리즘] 0x01강 - 기초 코드 작성 요령 I](https://www.youtube.com/watch?v=9MMKsrvRiw4&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY&index=2)
