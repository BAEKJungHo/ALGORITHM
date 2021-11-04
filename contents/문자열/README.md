# 문자열

## 🔑 기본 문제

### [문장 속 가장 긴 단어 찾기](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/string/wordinsentence/Main.java)

```
한 개의 문장이 주어지면 그 문장 속에서 가장 긴 단어를 출력하는 프로그램을 작성하세요.
* 예시 입력
* it is time to study
*
* 예시 출력
* study
```

```java
public String solution(String sentence) {
    String answer = "";
    int m = Integer.MIN_VALUE;
    String[] words = sentence.split(" ");
    for (String word : words) {
        int len = word.length();
        if(len > m) {
            m = len;
            answer = word;
        }
    }
    return answer;
}
```

### [문자 찾기](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/string/findstring/Main.java)

- Point
  - char 비교는 `==` 사용


```java
public int solution(String str, char c) {
    int result = 0;
    c = Character.toUpperCase(c);
    char[] words = str.toUpperCase().toCharArray();
    for (char word : words) {
        if(word == c) {
            result++;
        }
    }
    return result;
}
```

### [문자열 압축](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/string/compactstring/Main.java)

```
* 예시 입력 1
* KKHSSSSSSSE
*
* 예시 출력 1
* K2HS7E
*
* 예시 입력 2
* KSTTTSEEKFKKKDJJGG
*
* 예시 출력 2
* KST3SE2KFK3DJ2G2
```

- Point
  - charAt() 을 이용한 비교


```java
// i 번째랑 i+1 번째의 문자를 비교한다.
public String solution2(String s){
    String answer="";
    s=s+" ";
    int cnt=1;
    for(int i=0; i<s.length()-1; i++){
        if(s.charAt(i)==s.charAt(i+1)) cnt++;
        else{
            answer+=s.charAt(i);
            if(cnt>1) answer+=String.valueOf(cnt);
            cnt=1;
        }
    }
    return answer;
}
```

### [최단 거리 계산](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/string/shortdistance/Main.java)

링크 참고

## 🔑 indexOf() 를 사용한 문제

### [중복 문자열 제거](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/string/duplicatedwordsremove/Main.java)

- 입력 : ksekkset
- 출력 : kset

- String class 의 indexOf()
  - 처음 발견되는 문자열 위치를 반환한다.
  - 중복된 문자열이 존재해도 무조건 처음 발견되는 문자열 위치를 반환한다.
  - `핵심 코드 : str.indexOf(str.charAt(i)) == i`
    - 반복문 i 변수의 값과 i 번째 문자가 발견되는 값이 같으면 StringBuilder 에 추가

```java
// indexOf : 처음 발견되는 문자열 위치를 반환
public String solution2(String str) {
    StringBuilder stringBuilder = new StringBuilder();
    for(int i=0; i<str.length(); i++) {
        if(str.indexOf(str.charAt(i)) == i) {
            stringBuilder.append(str.charAt(i));
        }
    }
    return stringBuilder.toString();
}
```

## 🔑 replaceAll() 을 사용한 문제 : 정규식 문제

### [숫자만 추출하기](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/string/extractnumbers/Main.java)

- 입력 : g0en2T0s8eSoft
- 출력 : 208

```java
// Solv1. replaceAll 이용
public int solution(String str) {
    str = str.replaceAll("[^0-9]", "");
    return Integer.parseInt(str);
}

// Solv2. 문자열을 문자로 쪼갠 다음, Character 클래스의 isDigit 이용
public int solution2(String str) {
    String answer = "";
    for(char x : str.toCharArray()) {
        if(Character.isDigit(x)) {
            answer += x;
        }
    }
    return Integer.parseInt(answer);
}
```

### [유효한 팰린드롬](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/string/palindrome/valid/Main.java)

- Point
  - replaceAll() 이용
  - StringBuilder 의 reverse() 

```
앞에서 읽을 때나 뒤에서 읽을 때나 같은 문자열을 팰린드롬이라고 한다.
문자열이 입력되면 해당 문자열이 팰린드롬이면 "YES", 아니면 “NO"를 출력하는 프로그램을 작성하세요.
 * 단 회문을 검사할 때 알파벳만 가지고 회문을 검사하며, 대소문자를 구분하지 않습니다.
 * 예시 입력 1
 * found7, time: study; Yduts; emit, 7Dnuof
 *
 * 예시 출력 1
 * YES
```

```java
// Tip. 알파벳 이외의 문자들의 무시합니다. -> 특정 문자를 제외한 문자를 무시한다 -> 정규식 replaceAll 이용 가능성이 큼.
// replaceAll 정규식 이용
public String solution(String str) {
    str = str.toUpperCase().replaceAll("[^A-Z]", "");
    String reversedStr = new StringBuilder(str).reverse().toString();
    if(str.equals(reversedStr)) {
        return "YES";
    }
    return "NO";
}
```

## 🔑 replace() 를 사용한 문제

### [암호](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/string/password/Main.java)

- 문제 내용 링크 참고

```java
// replace 이용
public String solution2(int n, String s){
    String answer = "";
    for(int i=0; i<n; i++) {
        String tmp = s.substring(0, 7).replace("#", "1").replace("*", "0");
        int num = Integer.parseInt(tmp, 2);
        answer += (char) num;
        s = s.substring(7);
    }
    return answer;
}
```

## 🔑 lt, rt, 교환코드를 사용하는 문제

### [단어 뒤집기](https://github.com/BAEKJungHo/algorithms/blob/master/src/src/main/java/inflearn/string/reversewords/Main.java)

```
N개의 단어가 주어지면 각 단어를 뒤집어 출력하는 프로그램을 작성하세요.
* 예시 입력 1
* 3
* good
* Time
* Big
*
* 예시 출력 1
* doog
* emiT
* giB
```

- Point
  - lt(left), rt(right) 인덱스 활용
  - 교환코드 활용

```java
public List<String> solution(String[] words) {
    List<String> answer = new ArrayList<>();
    /**
     * 아래의 문제는 손 코딩으로도 낼 만한 문제임.
     *
     * study -> 가운데(u)를 기준으로 lt(s,t) rt(d,y) 끼리 변경하기
     * lt == rt 이면 다 바뀐 것
     * good -> 무조건 lt < rt 밖에 없음
     */
    for(String word : words) {
        char[] s = word.toCharArray();
        int lt = 0;
        int rt = word.length()-1;
        while(lt < rt) {
            // 교환 코드
            char tmp = s[lt];
            s[lt] = s[rt];
            s[rt] = tmp;
            lt++;
            rt--;
        }
        String tmp = String.valueOf(s);
        answer.add(tmp);
    }

    return answer;
}
```
