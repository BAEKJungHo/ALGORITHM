# 배열

## 🔑 기본 문제

### [점수 계산](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/array/score/Main.java)

```
* 예시 입력 1
* 10
* 1 0 1 1 1 0 0 1 1 0
*
* 예시 출력 1
* 10
```

```java
public int solution(int[] numbers) {
    int score = 0;
    int sequence = 1;
    for(int i=0; i<numbers.length; i++) {
        if(numbers[i] > 0) {
            score += sequence;
            sequence++;
        } else {
            sequence = 1;
        }
    }
    return score;
}
```

### [등수 구하기](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/array/rank/Main.java)

```
N명의 학생의 국어점수가 입력되면 각 학생의 등수를 입력된 순서대로 출력하는 프로그램을 작성하세요.
같은 점수가 입력될 경우 높은 등수로 동일 처리한다.
즉, 가장 높은 점수가 92점인데 92점이 3명 존재하면 1등이 3명이고 그 다음 학생은 4등이 된다.

* 예시 입력 1
* 5
* 87 89 92 100 76
*
* 예시 출력 1
* 4 3 2 1 5
```

```java
// 같거나 자기가 점수가 크면 순위 1 유지
// 자기 점수가 더 낮으면 순위 + 1
public List<Integer> solution(int[] scores) {
    List<Integer> answer = new ArrayList<>();
    int rank = 1;
    for(int i=0; i<scores.length; i++) {
        for(int k=0; k<scores.length; k++) {
            if(scores[i] < scores[k]) {
               rank++;
            }
        }
        answer.add(rank);
        rank = 1;
    }
    return answer;
}
```

## 🔑 피보나치 수열

- 피보나치 수열이란 앞의 2개의 수를 합하여 다음 숫자가 되는 수열이다.
- Ex. 1 1 2 3 5 8 13 21 34 55

### [피보나치 수열](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/array/fibonaccisequence/Main.java)

```
* 예시 입력 1
* 10
*
* 예시 출력 1
* 1 1 2 3 5 8 13 21 34 55
```

```java
public int[] solution(int count) {
    int start = 1;
    int[] answer = new int[count];
    answer[0] = 1;
    answer[1] = 1;
    for(int i=2; i<count; i++) {
        answer[i] = answer[i-2] + answer[i-1];
    }
    return answer;
}

// 손 코딩 문제 
public void solution2(int n) {
    int a=1, b=1, c;
    System.out.println(a+" "+b+" ");
    for(int i=2; i<n; i++) {
        c=a+b;
        System.out.println(c+ " ");
        a = b;
        b = c;
    }
}
```

## 🔑 소수(에라토스테네스 체)

- 소수란 1과 자기 자신만으로 나누어 떨어지는 1보다 큰 양의 정수를 의미한다.
- Ex. 2, 3, 5, 7, 11, 13, 17, 19

### [소수](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/array/eratosthenes/Main.java)

```
자연수 N이 입력되면 1부터 N까지의 소수의 개수를 출력하는 프로그램을 작성하세요.
```

- Point
  - N+1 만큼의 0으로 초기화된 배열 생성
  - 이중 포문 BUT if 문으로 제어 필요 -> 무작정 이중 포문 돌릴 시 시간 초과에 걸릴 수 있음.
  - 자기 배수에 해당하는 배열 부분들을 1 로 업데이트(즉, 소수가 아닌 부분은 1로 업데이트)

```java
public int solution(int number) {
    int cnt = 0;
    int[] ch = new int[number+1];
    for(int i=2; i<=number; i++) {
        if(ch[i] == 0) {
            cnt++;
            for(int k=i; k<=number; k=k+i) { // 자기 배수에 해당하는 배열 부분들을 1 로 업데이트(즉, 소수가 아닌 부분은 1로 업데이트)
                ch[k] = 1;
            }
        }
    }
    return cnt;
}
```

### [뒤집은 소수](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/array/reverseprimenumber/Main.java)

```
* 예시 입력 1
* 9
* 32 55 62 20 250 370 200 30 100
*
* 예시 출력 1
* 23 2 73 2 3
```

- Point
  - N+1 만큼의 0으로 초기화된 배열 생성
  - 이중 포문 BUT if 문으로 제어 필요 -> 무작정 이중 포문 돌릴 시 시간 초과에 걸릴 수 있음.
  - 자기 배수에 해당하는 배열 부분들을 1 로 업데이트(즉, 소수가 아닌 부분은 1로 업데이트)

```java
public List<Integer> solution(String[] numbers) {
    List<Integer> result = new ArrayList<>();
    for (String number : numbers) {
        int reversedNumber = Integer.parseInt(new StringBuilder(number).reverse().toString()); // StringBuilder 를 이용한 뒤집기
        if(isPrime(reversedNumber)) {
            result.add(reversedNumber);
        }
    }
    return result;
}

private boolean isPrime(int number) {
    if(number == 1) {
        return false;
    }
    if(isNotWellKnownPrime(number)) {
        for(int i = 2; i < number; i++) { // 소수 구하는 로직 이 부분이 핵심 Point
            if (number % i == 0) {
                return false;
            }
        }
    }
    return true;
}

private boolean isNotWellKnownPrime(int number) {
    return number != 2;
}
```

## 🔑 2차원 배열

### [격자판 최대 합](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/array/gridsum/Main.java)

```
 N*N의 격자판이 주어지면 각 행의 합, 각 열의 합, 두 대각선의 합 중 가 장 큰 합을 출력합니다.
 
* 예시 입력 1
* 5
* 10 13 10 12 15
* 12 39 30 23 11
* 11 25 50 53 15
* 19 27 29 37 27
* 19 13 30 13 19
*
* 예시 출력 1
* 155
```

- Point
    - Math.max(a, b) 이용하여 최대값을 비교

```java
// 행, 열에 대한 합을 구한다.
// 1. Math.max 로 answer 와 행을 비교한 후 answer 에 대입
// 2. Math.max 로 answer 와 열을 비교
    // 이 과정이 끝나면 answer 에는 각 행과 열의 합에 대한 max 값이 있음
// 대각선 반복문을 돌린다.
    // Math.max 로 answer 와 왼쪽 대각선, 오른쪽 대각선 합을 비교
public int solution(int n, int[][] grid) {
    int answer=-2147000000;
    int sum1=0, sum2=0;
    for(int i=0; i<n; i++){
        sum1=sum2=0;
        for(int j=0; j<n; j++){
            sum1+=grid[i][j];
            sum2+=grid[j][i];
        }
        answer=Math.max(answer, sum1);
        answer=Math.max(answer, sum2);
    }
    sum1=sum2=0;
    for(int i=0; i<n; i++){
        sum1+=grid[i][i];
        sum2+=grid[i][n-i-1];
    }
    answer=Math.max(answer, sum1);
    answer=Math.max(answer, sum2);

    return answer;
}
```

## 🔑 다중 포문

### [봉우리](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/array/peak/Main.java)

```java
int[] dx={-1, 0, 1, 0};
int[] dy={0, 1, 0, -1};

/*
   방향이 들어가는 문제는 아래 처럼 사용
   int[] dx = {-1, 0, 1, 0};
   int[] dy = {0, 1, 0, -1};
   3중 포문 필요 : 격자판 i,k 에 대한 2중 포문 + 좌표 p 에 대한 포문
 */
public int solution(int n, int[][] grid) {
    int answer=0;
    for(int i=0; i<n; i++){ // 격자판 행 반복
        for(int k=0; k<n; k++){ // 격자판 열 반복
            boolean isPeak=true;
            for(int p=0; p<4; p++){ // 봉우리를 구하기 위해 비교해야 하는 좌표 반복
                int nx=i+dx[p];
                int ny=k+dy[p];
                if(nx>=0 && nx<n && ny>=0 && ny<n && grid[nx][ny]>=grid[i][k]){
                    isPeak=false;
                    break;
                }
            }
            if(isPeak) answer++;
        }
    }
    return answer;
}
```

### [임시반장 정하기](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/array/classpresident/Main.java)

```java
/*
    핵심 : 3중 포문
    첫 번째 for : i 번째 학생
    두 번째 for : j 번째 학생
    세 번째 for : k 학년
    즉, i 번째 학생의 k 학년 == j 번째 학생의 k 학년을 비교
 */
public int solution(int n, int[][] arr) {
    int answer=0, max=0;
    for(int i=1; i<=n; i++){ // 학생 i
        int cnt=0;
        for(int j=1; j<=n; j++){ // 학생 j
            for(int k=1; k<=5; k++){ // 학년
                if(arr[i][k]==arr[j][k]){ // i 번 학생의 k 학년과, j 번 학생의 k 학년이 같은지
                    cnt++;
                    break;
                }
            }
        }
        if(cnt>max){
            max=cnt;
            answer=i;
        }
    }
    return answer;
}
```

### [멘토링](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/array/mentoring/Main.java)

```java
/*
     0 1 2 3  --> 등수
   0 3 4 1 2
   1 4 3 1 2
   2 3 1 4 2
   세로 0,1,2 는 테스트 번호
   m 은 테스트 번호
 */
public int solution(int n, int m, int[][] arr){
    int answer=0;
    for(int i=1; i<=n; i++){
        for(int j=1; j<=n; j++){
            int cnt=0;
            for(int k=0; k<m; k++){ // k 는 테스트 번호
                int pi=0, pj=0;
                for(int s=0; s<n; s++){ // s 는 등수
                    if(arr[k][s]==i) pi=s; // pi 는 i 번째 학생의 등수
                    if(arr[k][s]==j) pj=s; // pj 는 j 번째 학생의 등수수
               }
                if(pi<pj) cnt++;
            }
            if(cnt==m){ // Ex. (3, 1) -> m 번의 테스트가 다 통과되면 cnt 는 m 과 같아야 함함
               answer++;
                //System.out.println(i+" "+j);
            }
        }
    }
    return answer;
}
```
