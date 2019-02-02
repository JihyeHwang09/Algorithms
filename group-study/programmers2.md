## 2. 가로등

길이가 l인 도로에 가로등이 여러대 놓여 있습니다. 전체 도로를 밝히기 위해 좌/우 각각 d만큼을 밝히는 전구를 사려고합니다. 이때 d 값이 충분히 크다면 전체 도로를 밝게 비출 수 있지만, d 값이 작다면 일부 도로는 빛이 닿지 않습니다.

![](https://user-images.githubusercontent.com/37353837/52056318-450fb680-25a5-11e9-877f-f8be2d5b1fdc.png)

> 도로 길이 l과 가로등의 위치 v가 주어졌을 때, 도로를 모두 밝히는 값 중 최솟값을 구해주세요.

> 시간 복잡도를 고려해 최적값을 찾아낼 수 있는지 물어보는 문제입니다. 시간 복잡도를 고려하지 않고 나이브하게 풀었다면 효율성 테스트케이스를 맞추지 못했을겁니다.

권장 Timecomplexity: O( nlogn )

#### 1) 정답 예시(소팅 & 그리디) - O( nlogn )

```python
def solution(l, v):
    v.sort()
    ans = max(v[0], l - v[-1])
    for i in range(1, len(v)):
        ans = max(ans, (v[i] - v[i-1] + 1)//2)
    return ans
```

#### 2) 정답 예시(이분탐색) - O( nlogn )

- [이진 탐색](https://m.blog.naver.com/1net1/221159842052)

```python
def solution(l, v):
    n = len(v)
    answer = l
    v.sort()

    left, right = 0, l
    while(left <= right) :
        mid = (left + right) // 2

        # 맨 앞 가로등과 맨 뒤 가로등이 도로의 양 끝을 밝히는지 확인
        if v[0] - mid > 0 or v[n-1] + mid < l :
            left = mid + 1
            continue

        # 나머지 가로등으로 이분 탐색
        flag = False
        for i in range(1, n) :
            if v[i-1] + mid < v[i] - mid :
                flag = True
                break
        if flag :
            left = mid + 1
        else :
            answer = mid
            right = mid - 1
    return answer
```

```python
def solution(l, v):
    v.sort()
    ans = max(v[0], l - v[-1])
    for i in range(1, len(v)):
        ans = max(ans, (v[i] - v[i-1] + 1)//2)
    return ans
```

```js
// l은 도로 길이
// v는 가로등의 위치
// v가 0,3,5,7,9,14,15
// sort()의 기본값은 오름차순 정렬
//

const solution(l, v){
v..sort(function(a, b) {
return a - b;}
ans = max in python

}

```

```js
# 해석
## arrayobj.sort(sortFunction)
자바스크립트 배열의 내장 함수에 sort()가 있다.
명칭 그대로 배열 안의 원소를 정렬하는 함수이다.
　
arrayobj는 임의의 Array 개체이다.
 sortFunction는 요소 순서를 결정하는 데 사용되는 함수의 이름이다.
**생략하면 `오름차순`, `ASCII 문자 순서`로 정렬된다.**
// 첫 번째 인수가 두 번째 인수보다 작을 경우 - 값
// 두 인수가 같을 경우 0
// 첫 번째 인수가 두 번째 인수보다 클 경우 + 값


const  score = [4, 11, 2, 10, 3, 1];

/* 오류 */
score.sort(); // 1, 10, 11, 2, 3, 4
              // ASCII 문자 순서로 정렬되어 숫자의 크기대로 나오지 않음

/* 정상 동작 */
score.sort(function(a, b) { // 오름차순
    return a - b;
    // 1, 2, 3, 4, 10, 11
});

score.sort(function(a, b) { // 내림차순
    return b - a;
    // 11, 10, 4, 3, 2, 1
});
```
