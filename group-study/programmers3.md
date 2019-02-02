## 3. 빙고

> 빙고 게임 보드에 적힌 숫자가 담겨있는 배열 board, 게임 보드에서 순서대로 지운 숫자가 들어있는 배열 nums가 매개변수로 주어질 때, board에서 nums에 들어있는 숫자를 모두 지우면 몇 개의 빙고가 만들어지는지 return하도록 solution함수를 완성해주세요.

![](https://user-images.githubusercontent.com/37353837/52056346-548eff80-25a5-11e9-9ac0-fafb3fded9de.png)

수학적 사고력을 해야 풀 수 있는 문제입니다. 이 문제를 풀려면 다음 두가지 일을 해야합니다.

step 1. board에 있는 nums의 원소 찾아 마크
step 2. board에 가로 / 세로 / 대각선을 확인해 빙고 체크

이때, step1에서 hash/set을 이용해 O( n3 )이 아닌 O( n2 ) 코드를 짜는 것이 관건입니다.

권장 Time complexity: O( n2 )

- 참고

* [자료구조- map과 set(출처: MDN)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Keyed_collections)

```python
def solution(board, nums):
    n = len(board)
    vertical = [0 for _ in range(n)]
    horizontal = [0 for _ in range(n)]
    lu_diag = 0
    ru_diag = 0

    # 탐색을 O(1)로 하기 위해 nums를 set 자료구조로 변환
    # set: 집합
    # 순서가 없다.
    # 집합이므로 중복된 데이터가 들어갈 수 없다.
    # 중복되지 않는 숫자(데이터)를 구할 때 사용하면 유요앟다.

    # 확인 필요: hashset이나 hashmap의 key값은 hashcode 비교에 의해서 중복여부가 확인된다.
    # hashCode()를 가지고 비교를 하고 ===로 비교해서 true를 리턴하거나
    # equals()로 비교해서 true를 리턴하는지 체크해서
    # 기존 element를 덮어 쓸 것인지를 결정한다.

    nums = set(nums)
    for p in range(n):
        for q in range(n):
            if board[p][q] in nums:
                horizontal[q]+=1
                vertical[p]+=1
                if p == q:
                    lu_diag+=1
                if p + q == n - 1:
                    ru_diag += 1

    cnt = 0
    cnt += vertical.count(n)
    cnt += horizontal.count(n)
    if lu_diag == n:
        cnt += 1
    if ru_diag == n:
        cnt += 1
    return cnt
```
