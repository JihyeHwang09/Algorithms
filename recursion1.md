#### `순환 함수`란 무엇이며, `무한 루프에 빠지지 않으려면` 어떤 경우가 존재해야 하는지 <br>그리고 `수학적 귀납법`에 대해 알아봅시다.

> **본 포스팅은**
> <[인프런 - 권오흠 강사님의 영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/) > **자료를 인용하였음을 알려드립니다.**

---

## 순환이란?

![](https://user-images.githubusercontent.com/37353837/50761057-c331b380-12ac-11e9-9511-2b121de54791.png)

## recursion은 항상 무한루프에 빠질까?

![](https://user-images.githubusercontent.com/37353837/50761063-c6c53a80-12ac-11e9-8a68-71643ba8b228.png)

```java
// 1 ~ n까지의 합을 구한다.
int main() {
    int result = func(4);
}

int func(int n) {
    if (n == 0) {
        return 0;
    }
    else {
        return n + func(n-1);
    }
}
```

## 무한루프에 빠지지 않으려면? & recursion의 해석

```java
// 이 함수의 mission은 0 ~ n까지의 합을 구하는 것이다.
int func(int n) {
    // Base case: 적어도 하나의 recursion에 빠지지 않는 경우가 존재해야 한다.
    // n = 0이라면, 합은 0이다.
    if (n == 0)
    return 0;
    else
    // Recursive case: recursion을 반복하다보면 결국 base case로 수렴해야 한다.
    // n이 0보다 크다면,
    //  0에서 n까지의 합은 0에서 n-1까지의 합에 n을 더한 것이다.
    return n + func(n-1);
}
```

## 순환함수와 수학적 귀납법

### 정리: `func(int n)`은 `음이 아닌 정수 n`에 대해서 `0에서 n까지의 합`을 올바르게 계산한다.

### 증명:

1.  `n=0`인 경우: **n=0인 경우 `0`을 반환**한다. 올바르다.
2.  임의의 양의 정수 k에 대해서 `n < k`인 경우, 0에서 n까지의 합을 올바르게 계산하여 반환한다고 가정하자.
3.  `n = k인 경우`를 고려해보자. `func`은 **먼저 `func(k-1)` 호출**하는데 2번의 가정에 의해서
    `0에서 k-1까지의 합`을 **올바르게 계산하여 반환**한다.
    `메서드 func`은 **그 값에 `n`을 더해서 반환**한다.
    따라서 **`메서드 func`는 `0에서 k까지의 합`을 올바로 계산하여 반환**한다.

```java
package lec00.algorithm;

public class Alg02 {
	public static void main(String[] args) {
		int n = 4;
		func(n);
	}
	public static void func(int k) {
		if (k <= 0)
			return;
// Base case: 적어도 하나의 recursion에 빠지지 않는 경우가 존재해야 한다.
		else {
			System.out.println("Hello...");
			func(k-1);
// Recursive case: recursion을 반복하다보면 결국 base case로 수렴해야 한다.
		}
	}
}
// recursion이 항상 무한루프에 빠지는 것은 아니다.
```

```java
package lec00.algorithm;

// 1 ~ n까지의 합을 구한다.
public class Alg03 {
	public static void main(String[] args) {
		int result = func(4);
		System.out.println(result);
	}

	public static int func(int n) {
		if(n <= 0)
			return 0;
		else {
			return n + func(n-1);
		}
		/*
	public static int func(int n) {
//	이 함수의 mission은 0~n까지의 합을 구하는 것이다.
	if (n == 0)
		return 0;
//		n=0이라면 합은 0이다.
	else
		return n + func(n-1);
//		n이 0보다 크다면 0에서 n까지의 합은
//		0에서 n-1까지의 합에 n을 더한 것이다.
}
*/
	}

}

```

---

## Factorial: n!

![](https://user-images.githubusercontent.com/37353837/50761066-c88efe00-12ac-11e9-961a-4850e55da65e.png)

![](https://user-images.githubusercontent.com/37353837/50761576-10faeb80-12ae-11e9-8a40-f6f4c1c01c86.png)

```java
int factorial(int n)
{
    if (n == 0) {
        return 1;
    } else {
        return n* factorial(n-1);
    }
}
```

## 정리: `factorial(int n)`은 `음이 아닌 정수 n`에 대해서 `n!`을 올바르게 계산한다.

## 증명:

1. `n = 0`인 경우: **n=0인 경우 `1`을 반환**한다. 올바르다.
2. 임의의 양의 정수 k에 대해서 `n < k`인 경우 `n!`을 올바르게 계산한다고 가정하자.
3. `n = k`인 경우를 고려해보자. `factorial`은 **먼저 `factorial(k-1)` 호출**하는데 <br>
   2번의 가정에 의해서 `(k-1)!`을 **올바르게 계산하여 반환**한다. <br>
   따라서 **`메서드 factorial`은 `k \* (k-1)! = k!`을 반환**한다.

```java
public static int factorial(int n)
{
	if (n == 0)
	return 1;
	else
	return n * factorial(n-1);
```
