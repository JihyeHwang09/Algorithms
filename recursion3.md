#### 이번에는 지난 포스트에 이어서, `순환적 알고리즘 설계 방법`에 대해 알아봅시다.

> **본 포스팅은**
> <[인프런 - 권오흠 강사님의 영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/) > **자료를 인용하였음을 알려드립니다.**

---

# 순환적 알고리즘 설계

**적어도 하나의 `base case`, 즉 `순환되지 않고 종료되는 case`가 있어야 함**

**모든 case는 결국 base case로 수렴해야 함**

> **암시적(implicit) 매개변수**를 `명시적(explicit) 매개변수`로 바꾸어라.

## 순차 탐색

- 이 함수의 미션은 **data[0]에서 data[n-1] 사이에서 target을 검색하는 것**이다.
- 하지만, **검색 구간의 시작 인덱스 `0`은 보통 생략**한다.
- -> 즉, `암시적 매개변수`이다.
  > 이 함수는 시작 위치는 `0`으로 `암시`, 끝 위치는 `명시`되어 있다.

```java
// "배열의 데이터가 n개이니까 당연히 인덱스 0부터 시작하겠지."라고
//  암묵적으로 동의한 것이므로 생략됨
// 배열의 시작지점이 명시적으로 0이라고 표현되어 있지 X
int search(int [] data, int n, int target) {
  for (int i = 0; i < n; i++) {
    if (data[i] == target)
    return i;
  }
  return -1;
}
```

## 매개변수의 `명시화`: 순차 탐색

- 이 함수의 미션은 **data[begin]에서 data[end] 사이에서 target을 검색**한다.
- 즉, **검색구간의 시작점을 `명시적(explicit)`으로 지정**한다.

- **시작 위치가 begin으로 `명시`, 끝 위치는 end로 `명시`되어 있다.**

> 이 함수를 `search(data, 0, n-1, target)`으로 호출한다면, <br>위의 순차 탐색에서 예시로 든 search함수와 **완전히 동일한 일**을 한다.

```java
int search(int [] data, int begin, int end, int target) {
  // begin > end이면, 데이터가 0개이다.
  if (begin > end) {
  return -1;
  // begin = end는 데이터가 1개라는 뜻
} else if (target == data[begin]) {
  // end를 찾을 필요 없이 begin을 return한다.
  return begin;
} else if {
  return search(data, begin + 1, end, target);
}
```

## 순차 탐색: 다른 버전

- 이 함수의 미션은 **data[begin]에서 data[end] 사이에서 target을 검색**한다.
- 즉, **검색구간의 시작점을 `명시적(explicit)`으로 지정**한다.

### 예제1

```java
int search(int [] data, int begin, int end, int target) {
  if (begin > end) {
    return -1;
  } else if (target == items[end]) {
    return end;
  } else {
    return search(data, begin, end-1, target);
  }
}

```

### 예제2

```java
int search(int [] data, int begin, int end, int target) {
  if (begin > end) {
    return -1;
  } else {
    int middel = (begin + end) / 2;
    if (data[middle] == target) {
      return middle;
    }
    int index = search(data, begin, middle - 1, target);
    if (index != -1) {
      return index;
    } else {
      return search(data, middle + 1, end, target);
    }
  }
}

```

---

## 매개변수의 명시화: `최대값 찾기`

- 이 함수의 미션은 **data[begin]에서 data[end] 사이에서 최대값을 찾아 반환**한다.
- **`begin <= end`라고 가정**한다.

```java
int findMax(int [] data, int begin, int end) {
  // base case: 데이터가 0개 일 경우가 X. 1개일 경우이다.
  // 데이터가 0개일 경우, 최대값이 정의되지 X 때문이다.
  // begin = end일 경우, 데이터가 1개이다.
  if (begin == end) {
    return data[begin];
  } else {
    return Math.max(data[begin], findMax(data, begin + 1, end));
  }
}

```

## 최대값 찾기: 다른 버전

```java
int findMax(int [] data, int begin, int end) {
  if (begin == end) {
    return data[begin];
  } else {
    int middle = (begin + end) / 2;
    int max1 = findMax(data, begin, middle);
    int max2 = findMax(data, middle + 1, end);
    return Math.max(max1, max2);
  }
}
```

---

## `이진 탐색(Binary Search)`

- **`items[begin]부터 items[end] 사이`에서 target을 검색한다.**

```java
public static int binarySearch(String[] items,
String target, int begin, int end) {
  // base case: 데이터의 개수가 0일 경우
  if (begin > end) {
    return -1;
  } else {
    int middle = (begin + end) / 2;
    // Java에서 문자열끼리의 비교는 compareTo() 메서드를 이용한다.
    // cf) s1.compareTo(s2) 메서드는 문자열의 사전적 값을 비교
    //     s1 < s2일 경우, 음의 정수를 반환
    //     s1 == s2일 경우, 0을 반환
    //      s1 > s2일 경우, 양의 정수를 반환
    int compResult = target.compareTo(items[middle]);
    if (comResult == 0) {
      return middle;
    } else if (compResult < 0) {
      return binarySearch(items, target, begin, middle -1);
    } else {
      return binarySearch(items, target, middle + 1, end);
    }
  }
}
```
