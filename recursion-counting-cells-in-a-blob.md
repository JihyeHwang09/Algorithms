#### 이번에는 `Recursion의 응용 - Counting Cells in a Blob`에 대해 알아봅시다.

> **본 포스팅은**
> <[인프런 - 권오흠 강사님의 영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/) > **자료를 인용하였음을 알려드립니다.**

---

## Counting Cells in a Blob

![](https://user-images.githubusercontent.com/37353837/51452195-50c8d500-1d7c-11e9-9f27-d2b8fe9f3f9b.png)

- `Binary` 이미지
- 각 픽셀은 `background pixel`(white)이거나
  혹은 `image pixel`(blue)
- **서로 연결된 `image pixel`들의 집합**을 `blob`이라고 부름
- **상하좌우** 및 **대각방향**으로도 연결된 것으로 간주

![](https://user-images.githubusercontent.com/37353837/51456369-c6d73700-1d90-11e9-8ec1-19683ffb7e58.png)

- 입력:

  - `N * N` 크기의 2차원 그리드(grid)
  - 하나의 좌표 `(x, y)`

- 출력:

  - 픽셀 `(x, y)`가 포함된 blob의 크기,
  - `(x, y)`가 **어떤 blob에도 속하지 않는 경우에는** `0`

---

## Recursive Thinking

바로 코드부터 작성하지 않고
먼저, **`순환적인 사고`를 `글`로 적어보자.**

```
현재 픽셀이 이 속한 blob의 크기를 카운트하려면
    현재 픽셀이 image color가 아니라면
        0을 반환한다
    현재 픽셀이 image color라면
        먼저 현재 픽셀을 카운트한다 (count=1).
        현재 픽셀이 중복 카운트되는 것을 방지하기 위해 다른 색으로 칠한다.
        현재 픽셀에 이웃한 모든 픽셀들에 대해서
            그 픽셀이 속한 blob의 크기를 카운트하여 카운터에 더해준다.
        카운터를 반환한다.
```

## 순환적 알고리즘

`N * N` 크기의 2차원 그리드(grid)를 보고, **blob의 크기를 계산**해보자.
blob의 크기는 **count값에 누적하여 계산**하자.

### 1.

![](https://user-images.githubusercontent.com/37353837/51456413-eec69a80-1d90-11e9-8039-225bf34518e8.png)

> count = 0

### 2.

![](https://user-images.githubusercontent.com/37353837/51456433-fdad4d00-1d90-11e9-9552-16b92be434c3.png)
현재 cell을 칠했기 때문에 **count에 1 증가**시킨다.

> count = **1**

> **인접한 8개의 픽셀 각각에 대해서** > **순서대로 그 픽셀이 포함된 blob의 크기를 count한다.** > `북`, `북동`, `동`, `동남`, ... 이런 순서로 고려한다.

### 3. `북`쪽 픽셀을 검사

> ![](https://user-images.githubusercontent.com/37353837/51456490-2f261880-1d91-11e9-8c5f-f7cb7ac4a04c.png)
> count = **1**

### 4-1) `북동`쪽 픽셀을 검사

> ![](https://user-images.githubusercontent.com/37353837/51456595-a8257000-1d91-11e9-93b8-f17cc43cdf48.png)
> count = **1**

### 4-2)

> ![](https://user-images.githubusercontent.com/37353837/51456662-e589fd80-1d91-11e9-908e-cafe4f8101b2.png)
> count = 1 + 3 = **4**

#### 5. `동`쪽과 `남동`쪽 픽셀을 검사

> ![](https://user-images.githubusercontent.com/37353837/51456697-0a7e7080-1d92-11e9-8cdd-31a20941584a.png)
> count = **4**

### 6-1) `남`쪽 픽셀을 검사

> ![](https://user-images.githubusercontent.com/37353837/51456777-46b1d100-1d92-11e9-804d-176999fb00e8.png)
> count = **4**

#### 6-2)

> ![](https://user-images.githubusercontent.com/37353837/51456857-7f51aa80-1d92-11e9-8f78-15268b94c25e.png)
> count = 4 + 9 = **13**

#### 7. `남서`, `서`, `북서` 방향으로 픽셀을 검사

> ![](https://user-images.githubusercontent.com/37353837/51456921-c2ac1900-1d92-11e9-8003-e8efdd5f53bf.png)
> count = **13**

---

## Counting Cells in a Blob

```java
Algorithm for countCells (x, y) {
    // 예외 처리: pixel (x, y)가 유효한 좌표가 아닐 때(grid의 범위를 벗어날 때)
    // -> (x < 0 || y < 0 || x > N || y > N)
    if the pixel (x, y) is outside the grid
        // 0을 return하고 함수를 종료한다.
        the result is 0;
    // Base Case: 1) pixel (x, y)가 0이 아니거나
    // (-> 즉, 이 함수에서는 image pixel이 아니면-> background pixel을 의미)
    // 2) 이미 카운트된 (빨간색으로 칠해진)셀일 경우
    else if pixel (x, y) is not an image pixel or already counted
        // 0을 return하고 함수를 종료한다.
        the result is 0;
    // 이미 카운트된 pixel도 아니고 image pixel일 경우
    else
        // 이미 카운트했다는 걸 표시하기 위해서
        // 그 pixel (x, y)를 빨간색으로 칠한다;
        set the colour of the pixel (x, y) to a red colour;
        // 1) 그 pixel에 1(자기 자신)을 더한 후,
        // 2) 이 pixel에 인접한 8개의 인접 pixel 각각에 대해서 recursion을 호출한다.
        // 3) recursion을 8번 호출한 그 결과들을 다 더해준다.
        the result is 1 plus the number of cells in each piece of
            the blob that includes a nearest neighbour;
}
```

### Java 코드로 구현해보기

위의 알고리즘을 `Java` 코드로 구현해 봅시다.

```java
private static int BACKGROUND_COLOR = 0;
private static int IMAGE_COLOR = 1;
private static int ALREADY_COUNTED = 2;

public int countCells (int x, int y) {
    int result;
    // N * N 그리드는 0 ~ N-1까지가 유효한 좌표이므로
    if (x < 0 || x >= N || y < 0 || y >= N)
        return 0;
    // grid[x][y]가 IMAGE_COLOR이 아니라는 건,
    // grid[x][y]이
    // 1) 0 (BACKGROUND_COLOR)이거나
    // 2) 0 (ALREADY_COUNTED)일 경우라는 뜻이다.
    else if (grid[x][y] != IMAGE_COLOR)
        return 0;
        // 그렇지 않다면, 카운트할 셀이기 때문에 ALREADY_COUNTED를 표시하기 위해
        // 해당 셀을 빨간색으로 칠해준다.
    else {
        grid[x][y] = ALREADY_COUNTED;
        // grid[x][y]의 값인 1과
        // (여기에서 더하는 1은 자기자신을 의미한다.)
        // 이 셀에 인접한 8개의 셀 각각의 recursion을 호출해서
        // 그 결과를 다 더해준 값이 답이 된다.
        return 1 + countCells(x - 1, y + 1)
        + countCells(x, y + 1)
        + countCells(x + 1, y + 1) + countCells(x - 1, y)
        + countCells(x + 1, y) + countCells(x - 1, y - 1)
        + countCells(x, y - 1) + countCells(x + 1, y - 1)
    }
}
```
