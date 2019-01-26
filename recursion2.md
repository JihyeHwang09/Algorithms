#### 이번에는 지난 포스트에 이어서, `순환적으로 사고하기`와 `문자열의 길이 계산`, `배열의 합` 등의 예제에 대해 알아봅시다.

> **본 포스팅은**
> <[인프런 - 권오흠 강사님의 영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/) > **자료를 인용하였음을 알려드립니다.**

---

# 순환적으로 사고하기(Recursive Thinking)

## `Recursion`은 수학함수 계산에만 유용한가?

> **수학함수 뿐 아니라 다른 많은 문제들을 `recursion`으로 해결할 수 있다.**

---

## 문자열의 길이 계산

![](https://user-images.githubusercontent.com/37353837/50836374-6b727580-139c-11e9-8240-0c69a49a35cc.png)

`문자열의 길이를 계산`하고 싶다면,

1. **첫 번째 문자열을 뺀** 나머지 문자열의 길이를 계산
2. `1`을 **더하면** 된다.

```java
// base case: 문자열의 길이가 0인 경우
// -> 첫 번째 문자열이 존재하지 X
if the string is empty
    return 0;
// 첫 번째 문자열을 제거한 그 문자열의 길이를 계산한 다음, 1을 더한다.
else
    return  1 plus the length of the string
     that excludes the first character;
```

![](https://user-images.githubusercontent.com/37353837/50836558-d0c66680-139c-11e9-9f55-3a9c5f43701e.png)

```java
int length(char *str) {
    if (*str == '\0') {
        return 0;
    } else {
        return 1 + length(str + 1);
    }
}
```

```java
// 문자열 str을 입력받아 길이를 계산하는 메서드 length
public static int length(String str) {
    // base case: 문자열의 길이가 0인 문자열과 동일하다면
    // -> 즉, 문자열의 길이가 0라면
    if (str.equals("")) {
        return 0;
    } else {
        // Java에서 substring(n)은
        //  index값이 n보다 작은(앞에 있는) 문자열을 제거한 문자열을 반환한다.
        // str.substring(1)은
        //  str에서 index값이 1인 위치 이후부터의 문자열을 가져온다.
        // -> 즉, 입력받은 str에서
        //  index값이 0인 첫 글자를 제외한 문자열을 반환한다.

        // 1 + length(str.substring(1))는 그것의 길이를 계산한 다음,
        //  1을 더해서 반환한다.
        return 1 + length(str.substring(1));
    }
}
```

## 문자열의 프린트

```java
// 입력한 하나의 문자열을 출력하는 메서드 printChars
public static void printChars(String str) {
    if (str.length() == 0) {
        return;
    } else {
        // 문자열의 첫 글자를 화면에 출력한다.
        // Java에서 str.charAt(n)은 인덱스 n의 위치에 해당되는 문자를 추출해준다.
        System.out.print(str.charAt(0));
        // 첫 글자를 제외한 나머지 문자열을 화면에 출력한다.
        printChars(str.substring(1));
    }
}
```

## 문자열을 뒤집어 프린트

![](https://user-images.githubusercontent.com/37353837/50836588-eb004480-139c-11e9-8472-efa2db29ebd9.png)

이 문자열을 뒤집어 프린트하려면,

1. 먼저 **`첫 글자`를 제외한 문자열**을 **뒤집어 프린트** 한다.
2. **마지막으로, `첫 글자`를 프린트** 한다.

```java
public static void printCharsReverse(String str) {
    // base case: 입력된 문자열 str의 길이가 0라면, 아무 일도 일어나지 X
    if (str.length() == 0)
    return;
    // 문자열의 길이가 1 이상이라면,
    else {
        // 1. 먼저 첫 글자를 제거한 문자열을 화면에 뒤집어서 출력한다.
        printCharsReverse(str.substring(1));
        // 2. 마지막으로, 원래 문자열의 첫 글자를 화면에 출력한다.
        System.out.print(str.charAt(0));
    }
}
```

## 2진수로 변환하여 출력

```java
// 음이 아닌 정수 n을 이진수로 변환하여 출력한다.
public void printInBinary(int n) {
    if (n < 2) {
        System.out.print(n);
    } else {
        // n을 2로 나눈 몫을 먼저 2진수로 변환하여 출력한다.
        // 마지막 비트를 제외한 나머지 비트가 표현하는 숫자이다.
        printInBinary(n/2);
        // n을 2로 나눈 나머지를 출력한다.
        // 마지막 비트를 표현하는 숫자이다.
        System.out.print(n%2);
    }
}
```

## 배열의 합 구하기

```java
// n개인 data의 합 구하기
// data[0]에서 data[n-1]까지의 합을 구하여 반환한다.
public static int sum(int n, int[] data) {
    if (n <= 0)
        return 0;
    else
    //sum(n-1, data) 을 호출하면,
    //  data[0]에서 data[n-2]까지 데이터의 합을 구한다.
    // 그 후, 마지막 데이터인 data[n-1]을 더해준다.
    // recursion이 1씩 줄어들다가 0이 될 때, 빠져나온다.
    // -> 무한루프에 빠질 일이 X
        return sum(n-1, data) + data[n-1];

}

```

## 데이터 파일로부터 n개의 정수 읽어오기

실제로 자주 쓰는 코드 형태는 X
**recursion 예제**로만 참고

```java
// Scanner in이 참조하는 파일로부터 n개의 정수를 입력받아
//  배열 data의 data[0], ..., data[n-1]에 저장한다.
public void readFrom(int n, int [] data, Scanner in) {
    // base case: n이 0일 때는 아무것도 하지 X
    if (n == 0) {
        return;
    } else {
        // 1. n-1개의 데이터를 읽어온다.
        // ->  data[0], ..., data[n-2]에 저장한다.
        readFrom(n-1, data, in);
        // 2. 마지막 한 개의 데이터를 읽어온다.
        // -> 읽어온 데이터를 data[n-1]에 저장한다.
        data[n-1] = in.nextInt();
    }
}
```

---

## `Recursion` vs `Interation`

- **모든 `순환함수`는 `반복문(interation)`으로 변경 가능**
- 그 역도 성립함. 즉, **모든 `반복문`은 `순환함수(recursion)`으로 표현 가능함**
- `순환함수`는 **복잡한 알고리즘을 단순하고 알기쉽게 표현**하는 것을 가능하게 함
- 하지만, **함수 호출에 따른 오버헤드**가 있음(매개변수 전달, 액티베이션 프레임 생성 등)
