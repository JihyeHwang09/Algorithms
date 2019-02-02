# 2019 상반기 공채 대비 코딩테스트 실전 모의고사 2회

- 참고 사이트
- [빅오표기법](https://www.youtube.com/watch?v=6Iq5iMCVsXA)

## 1. 배열 회전

배열의 회전이란 모든 원소를 오른쪽으로 한 칸씩 이동시키고,마지막 원소는 배열의 맨 앞에 넣는 것을 말합니다.
두 배열 arrA와 arrB가 매개변수로 주어질 때,
arrA를 회전해 arrB로 만들 수 있으면 true를,그렇지 않으면 false를 return 하는 solution 함수를 작성해주세요.

> 반복문을 사용할 수 있는지 물어보는 문제

> 아주 기초적인 문제이니 어렵지 않게 풀 수 있었을거에요.

## `Python` 코드

```python
# def는 함수 정의
# rotate는 함수 이름
def rotate(arr):
    return arr[-1:] + arr[:-1]
# python array modules
# slice notation(:)


# solution이라는 이름을 가진 함수를 정의
def solution(arrA, arrB):
    arrA_len = len(arrA)
    arrB_len = len(arrB)

    # 길이가 다른 배열은 회전해도 같아질 수 없으므로, early return
    if(arrA_len!=arrB_len):
        return False

    # arrA를 한칸씩 회전하며, arrB와 같은지 확인
    for _ in range(arrA_len):
        if arrA == arrB:
            return True
        arrA = rotate(arrA)
    return False
```

---

## Python 관련 내 해석

```python
# def는 함수 정의
# rotate는 함수 이름
def rotate(arr):
    return arr[-1:] + arr[:-1]
# python array modules
# slice notation(:)
# arr[-1:]배열의 끝부터 첫번째까지의 item
# arr[-1:]배열의 처음부터 끝까지의 item

```

```python
def 함수이름():   # 1. 첫 행
    본문          # 2. 함수를 호출했을 때 실행할 코드 블록
```

파이썬에서는
끝에서부터 index를 매길때는 `음수`를 사용한다.
![](https://user-images.githubusercontent.com/37353837/52057862-82764300-25a9-11e9-8203-171f68a3ad06.png)

```python
ex)
 word = 'Python'

word[-1]
# last chracter
# 출력값 'n'
word[-6]
# sixth-last character
# 출력값 'P'
```

### Pytoh에서의 slice

#### step을 명시하지 않을 경우

**start:stop[:step]**

> 여기서 [:step]은 써도 되고 안써도 된다.

1. a[start:end] # start부터 end-1까지의 item
2. a[start:] # start부터 리스트 끝까지 item
3. a[:end] # 처음부터 end-1까지의 item
4. a[:] # 리스트의 모든 item

#### step을 명시하는 경우

1. a[start:end:step]# start부터 end-1까지 step만큼 인덱스 증가시키면서
   step을 지정할 때 :end에 유의하세요 end는 end부터 포함시키지 않겠다는 의미이지 end가 꼭 포함된다는 의미는 아닙니다.

또 start나 end가 음수가 음수인 경우에는 리스트의 끝에서부터 카운트하겠다는 의미입니다.

1. a[-1] # 맨 뒤의 item
2. a[-2:] # 맨 뒤에서부터 item2개
3. a[:-n] # 맨 뒤의 item n개 빼고 전부

예제를 보여드릴게요

```python
a = [10,11,12,13,14,15,16,17,18,19]

print "a =", a
print "a[0:1]:", a[0:1]
print "a[0:1]:", a[0:10]
print "a[0:1]:", a[0:20]
print "a[0:1]:", a[0:10:2]
print "a[0:1]:", a[:-2]
print "a[0:1]:", a[:-30]
```

의 결과는

```python
a = [10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
a[0:1]: [10]
a[0:1]: [10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
a[0:1]: [10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
a[0:1]: [10, 12, 14, 16, 18]
a[0:1]: [10, 11, 12, 13, 14, 15, 16, 17]
a[0:1]: []
입니다.
```

---

```python
a[start:end] # start부터 end-1까지의 item
a[start:] # start부터 리스트 끝까지 item
a[:end] # 처음부터 end-1까지의 item
a[:] # 리스트의 모든 item
```

즉, rotate라는 함수는 arr를 받아서 배열의 끝부터 맨앞까지 검사하는 함수이다.

---

## Python -> JavaScript로 바꾸기

참고

- [김승하 선생님 교재 JAVASCRIPT로 만나는 세상- 배열](https://helloworldjavascript.net/pages/190-array.html)
- [MDN Array.prototype.slice()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

```js
const rotate(arr) {
 // 배열로부터 새로운 값 생성

// * slice 메소드
// 배열의 일부분에 해당하는 새로운 배열을 반환한다.
// 원본 배열에 아무런 영향을 미치지 않는다.
//  얕은 복사(shallow copy)를 하므로, 배열 안에 배열 또는 객체가 들어있을 때는 주의해서 사용해야 한다.

// 1. 인덱스 arr의 마지막 번째부터 arr의 맨 앞까지의 요소들을 가지고 새로운 배열을 생성한다.
// 2.
    return arr.slice(-1, 0);

}




// # solution이라는 이름을 가진 함수를 정의
def solution(arrA, arrB):
    arrA_len = len(arrA)
    arrB_len = len(arrB)

    // # 길이가 다른 배열은 회전해도 같아질 수 없으므로, early return
    if(arrA_len!=arrB_len):
        return False

    // # arrA를 한칸씩 회전하며, arrB와 같은지 확인
    for _ in range(arrA_len):
        if arrA == arrB:
            return True
        arrA = rotate(arrA)
    return False
```

def rotate(arr):
return arr[-1:] + arr[:-1]

def solution(arrA, arrB):
// len()은 리스트에 들어있는 원소 개수
// -> 즉, 리스트의 크기를 알려주는 함수
arrA_len = len(arrA)
arrB_len = len(arrB)

```js
const rotate(arr){
return arr.slice(-1, 0) +arr(0, -1);
}
const solution(arrA, arrB){
let arrA_len = arrA.length;
let arrB_len = arrB.length;
// 첫 번째 base case
// 배열의 길이가 다르면, 회전해도 같아질 수 없으므로
// return하고 함수를 종료한다.
if (arrA_len !== arrB_len) {
return false;
}
// 두 번째 base case
// arrA를 한칸씩 회전하면서, arrB와 같은지를 확인한다.

}
```
