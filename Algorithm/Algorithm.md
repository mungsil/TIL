# 알고리즘

### 시간복잡도와 공간복잡도

`시간 복잡도`는 **입력의 크기**와 *문제를 해결하는데 걸리는 시간*의 상관관계를 의미한다.

`Big-O 표기법`은 주어진 식을 값이 가장 큰 대표항만 남겨서 나타내는 방법이다.
시간 제한이 1초라면, 당신의 프로그램은 ‘3-5억번의 연산안에 답을 내고 종료되어야 한다’ 라는 것을 의미한다.

프로그램을 짤 때마다 연산이 몇 번 이루어지는지 매번 계산해야한다면 이것은 여간 불편한 일이 아닐 것이다.

따라서 입력 N에 따라 적당히 어림잡아 연산이 N번 필요하다. 라고 표현할 것이고, ‘적당히 어림잡아 필요한 연산이 N번이다.’라는 사실을 나타내기 위해 빅오 표기법을 사용한다.

결과적으로 프로그램의 실행 시간은 입력 N에 비례한다(최악의 경우라고 가정). 문제에서 최대 입력값을 알려준다면 해당 값을 토대로 내가 설계한 풀이 방법의 시간복잡도가 허용 시간 복잡도 보다 큰지를 체크하자.

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
