#### 이번에는 `Recursion의 응용 - 미로 찾기`에 대해 알아봅시다.

> **본 포스팅은**
> <[인프런 - 권오흠 강사님의 영리한 프로그래밍을 위한 알고리즘 강좌](https://www.inflearn.com/course/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B0%95%EC%A2%8C/) > **자료를 인용하였음을 알려드립니다.**

---

## 미로 찾기

![](https://user-images.githubusercontent.com/37353837/51436914-1f4afd80-1cd9-11e9-8664-8568bc7317b2.png)

## Recursive Thinking

현재 위치에서 출구까지 가는 경로가 있으려면

1. **현재 위치가 출구**이거나 혹은
2. 이웃한 셀들 중 하나에서 **현재 위치를 지나지 않고** 출구까지 가는 경로가 있거나

---

## 미로 찾기(Decision Problem)

> 답이 `yes` or `no`인 문제
> ![](https://user-images.githubusercontent.com/37353837/51436907-f3c81300-1cd8-11e9-947c-1698556fff1c.png)

1. **어떤 위치를 나타내는 x, y값**이 주어졌을 때
2. **(x, y)로부터 출구로까지 가는 경로**가 있는지 없는지를 판단
3. 경로가 **있으면** `true`를, **없으면** `flase`를 반환한다.

```java
boolean findPath(x, y)  {
    // Base Case: 현재 위치 자체가 출구인지를 검사
    if (x, y) is the exit
        // 현재 위치 = 출구라면, true를 return하고 종료
        return true;
    // 현재 위치가 출구가 X라면,
    else
        // 현재 위치와 인접한 셀들(이 경우에는 4개) 중에(현재 위치를 지나지 않고!!)
        // 출구까지 가는 경우가 만약에 있다면
        // 현재 위치로부터 해당 셀로 가서 경로를 따라가면
        // 출구까지 가는 경로가 있는 것이다.

        // (x', y')가 (x, y)의 인접한 셀들 4개
        //for each니까 각각에 대해서!
        for (each neighbouring cell (x', y') of (x, y) do){
            // (x', y')가 통로에 속한 셀이라면(지나다닐 수 있는 셀이라면)
            //  (x', y')가 통로에 속한 셀이 X(벽에 위치한 셀)라면,
            // 무시하고 넘어가면 된다.
            if (x', y') is on the pathway
                // 한 칸 이동한 위치에서  recursion으로 다시 검사
                if findPath(x', y')
                    return true;
        }
        // for문을 빠져나와서 여기까지 왔다는 것은
        // 위에 있는 코드의 if findPaht(x', y'){return true;}에서
        // return true하지 않았다는 뜻이다.

        // -> 따라서, 출발하는 현재 위치가 출구가 X고,
        // 인접한 셀들도 통로가 아니라면(벽이라면)
        // 미로를 빠져나갈 수 있는 경로가 X므로
        // false를 return한다.
        return false;
}
```

> Recursion 코드를 작성할 때는 **항상 이것이 `무한루프`에 빠지지는 않는가? **생각해야 한다.
> 따라서 `Base Case`(무한 루프에서 빠져나올 수 있는 조건)이 반드시 필요
> Recursion을 반복하다보면, 반드시 `Base Case`로 수렴한다는 게 보장되어야 한다!

---

## 미로 찾기 1

자신이 미로에 갇혔다고 생각해보자.

> **가장 중요한 일** 중에 하나가 무엇인가?

> `내가 가 본 위치`와 `아직 가보지 않은 위치`를 **구분하는 것**이다.
> **이를 구분하지 않으면, `무한루프`를 돌 수 있겠죠?**

미로 찾기 문제를 푸는 것도 마찬가지이다.

> **`이미 방문해 본 위치`와 `방문하지 않은 위치`를 적절하게 표시해서 구분할 필요가 있다.**

```java
boolean findPath(x, y) {
     // 현재 위치가 출구라면
    if (x, y) is the exit
    // true를 return하고 함수를 종료한다.
    reutrn true;
    else
    // (x, y)가 방문한 위치라면, 방문한 위치라고 표시를 해둔다.
    // recursion이 1번 반복될 때마다
    // 새로운 셀이 visited로 표시가 되고, 셀의 개수는 유한하기 때문에
    // -> 어떤 경우에도 무한 루프에 빠지지 않게 된다.
    mark (x, y) as a visited cell;
    // (x, y_)와 인접한 4개의 위치 각각(x', y')에 대해서
    for (each neigthbouring cell (x', y') of (x, y) do) {
        // 1. (x', y')의 셀이 pathway가 아니거나(벽의 일부거나)
        // 2. 이미 방문한 셀이라면, 그 셀을 검사해볼 필요가 X
        // -> (x', y')가 통로이면서 방문한 적이 없는 셀일 경우만 검사하면 된다!
        // (그 셀에서 출구로 가는 경로가 있는지를 검사하면 됨)
        if (x', y') is on the pathway and not visited
            if findPath(x', y')
                return true;
    }
    return false;
}
```

### point 1

```java
    mark (x, y) as a visited cell;
```

recursion이 1번 반복될 때마다
새로운 셀이 visited로 표시가 되고, 셀의 개수는 유한하기 때문에
-> 무한 루프에 빠지지 않게 된다.

### point 2

```java
       if (x', y') is on the pathway and not visited
           if findPath(x', y')
               return true;
```

- recursion에 들어가기 전에 먼저,
  그 지점(x', y')이 **벽이 아닌지** 혹은 **이미 방문한 지점이 아닌지**를 **체크** 한다.
- 둘 다에 해당되지 않으면, recursion에 들어가게 설계한다.

---

## 미로 찾기 2

- 무조건 **`(x, y)`에 인접한 각각의 셀`(x', y')`**이 `벽`인지, `이미 방문한 셀`인지
  **체크하지 X**고,
- 그냥 findPath(x', y')로 **recursion을 호출**한다.
- **대신, 이 함수의 맨 앞에 `조건`을 준다.**
- 만약에 `호출된 (x, y)`가 1. `벽`이나 2. `방문한 위치`라면 즉시 `false`를 return한다.

* 이 경우에는 미로 찾기 1번 방식보다 **recursion이 호출되는 횟수는 많아진다.**
  대신 **코드는 간결해진다**는 장점이 있다.
* cf) 미로 찾기 1번, 2번 코드는 **어느 코드가 더 낫다고 결론지을 수 없고, 보통 취향에 따라 선택**해서 작성한다.

```java
boolean findPath(x, y) {
    // First Base Case: (x, y)가 벽이거나 이미 방문한 셀이라면,
    if (x, y) is either on the wall or visited cell
    // 즉시 false를 return하고 함수를 종료한다.
        return false;
    // 그렇지 않으면서 (x, y)가 출구라면
    else if (x, y) is the exit
        // (x, y)부터 출구까지가는 경로가 존재하는 것이므로
        // true를 return하고 함수를 종료한다.
        return true;
    // 그렇지 않다면((x, y)가 출구가 아니라면)
    else
        // 이 셀(x, y)를 visited라고 표시를 해서
        // 이 위치를 중복 방문하는 일을 방지한 다음에
        mark (x, y) as a visited cell;
        // 그 위치(x, y)에 인접한 각각의 셀(x', y')에 대해서
        for (each neighbouring cell (x', y') of (x, y) do) {
            // (x', y')가 벽인지, 방문했는지 여부를 검사하지 않고
            // 그냥 recursion을 호출한다.
            // 왜냐하면, recursion을 호출하면 함수가 실행되고
            // 즉시(맨 처음 코드) if절에 걸려서 false가 return될 것이기 때문에
            // 여기에서 굳이 검사해 주지 않는다!
            if findPath(x', y')
            // 인접한 셀이 최대 4개이므로 4번 호출하고,
            // 그 중 하나라도 true라면 true를 반환하고 함수를 종료한다.
                return true;
        }
        // 아래 코드까지 왔다는 것은 전부 false라는 뜻이다.
        // -> 따라서, false를 return 한다.
        return false;
        }
}
```

---

## class Maze

Maze의 출구를 찾는 함수를 `Java`로 구현해보자.

```java
public class Maze {
    private static int N = 8;
    private static int[][] maze = {
        {0, 0, 0, 0, 0, 0, 0, 1},
        {0, 1, 1, 0, 1, 0, 0, 1},
        {0, 0, 0, 1, 0, 0, 0, 1},
        {0, 1, 0, 0, 1, 1, 0, 0},
        {0, 1, 1, 1, 0, 0, 1, 1},
        {0, 1, 0, 0, 0, 1, 0, 1},
        {0, 0, 0, 1, 0, 0, 0, 1},
        {0, 1, 1, 1, 0, 1, 0, 0},

    };

    private static final int PATHWAY_COLOUR = 0; // white
    private static final int WALL_COLOUR = 1; // blue
    private static final int BLOCKED_COLOUR = 2; // red
    private static final int PATH_COLOUR = 3; // green

```

- `PATHWAY_COLOUR`: **아직 가본 적 없는** cell (지나다닐 수 있는 통로)
- `WALL_COLOUR`: `벽`이어서 사람들이 **지나다닐 수 없는** cell

> 방문했던 셀을 표시하기 위해 2가지 색깔이 필요함
>
> 1. 출구까지의 경로가 막힌 셀
> 2. 출구까지 가는 경로가 될 가능성이 있는 셀

- `BLOCKED_COLOR`: `visited`이며, 출구까지의 경로상에 **있지 않음이 밝혀진** cell
  (가본 셀인데 꽝인 경로)
- `PATH_COLOR`: `visited`이며, 아직 출구로 가는 **경로가 될 가능성이 있는** cell

```java
    // recursion으로 미로의 출구를 찾는 함수인 findMazePath
    public static boolean findMazePath(int x, int y) {
        if (x < 0 || y < 0 || x >= N || y >= N)
            return false;
        else if (maze[x][y] != PATHWAY_COLOUR)
            return false;
        else if (x == N-1 && y == N-1) {
            maze[x][y] = PATH_COLOUR;
            return true;
        }
        else {
            maze[x][y] = PATH_COLOUR;
            if (findMazePath(x-1, y) || findMazePath(x, y + 1)
            || findMazePath(x+1, y) || findMazePath(x, y - 1)) {
                return true;
            }
            maze[x][y] = BLOCKED_COLOR; // dead end
            return false;
        }
    }

    public static void main(String [] args) {
        printMaze();
        // (0, 0)로부터 출발해서 미로를 탈출할 수 있는 경로가 있는지 알고 싶다.
        // -> 매개변수를 (0, 0)로 준다.
        // -> (0, 0)인 입구로부터 미로의 출구가 있는지를 검사하게 된다.
        findMazePath(0, 0);
        printMaze();
    }
// 아래 중괄호는 public class Maze를 닫아주는 중괄호임
}
```

### point 1

```java
        else {
            maze[x][y] = PATH_COLOUR;
            if (findMazePath(x-1, y) || findMazePath(x, y + 1)
            || findMazePath(x+1, y) || findMazePath(x, y - 1)) {
                return true;
            }
```

- **recursion으로 호출할 때**
  findMazePath의 매개변수인 (x, y)가
  `음수`인지, `양수`인지 또는 `0`인지를 검사하지 않고 무작정 호출하기 한다.
- 이렇게 recursion이 호출되면, **가장 먼저**
  `[x][y]`가 유효한 범위에 있는가를 검사해야 한다.

### point 2

```java
// x < 0 || y < 0 || x >= N || y >= N라는 것은
// 미로의 범위 바깥에 있다는 것을 의미한다.
// -> 현재 위치(x, y)가 미로의 범위 바깥에 위치한다면,
        if (x < 0 || y < 0 || x >= N || y >= N)
            // 즉시 false를 return 한다.
            return false;
```

`N X N` 그리드이므로 **유효한 좌표는 `0` ~ `N -1`**이다.

### point 3

```java
        else if (maze[x][y] != PATHWAY_COLOUR)
            return false;
```

> `[x][y]`가 **벽의 일부**이거나 **이미 방문한 셀**이라면 false를 retrun 한다.
> 이걸 뒤집어 말하면
> `[x][y]`의 color가 PATHWAY_COLOUR가 아니라면,
> 즉, visited(green, red)나 wall(blue)라면 false를 return하면 된다.

### point 4

```java
        else if (x == N-1 && y == N-1) {
            maze[x][y] = PATH_COLOUR;
            return true;
        }
```

`x == N-1 && y == N-1`라는 것은 이 `[x][y]`가 `출구`라는 뜻이다.
따라서, 이 경우에는 `true`를 return 한다.
그리고 이 위치를 `PATH_COLOUR`인 `초록색`으로 칠한다.

### point 5

```java
        else {
            maze[x][y] = PATH_COLOUR;
            if (findMazePath(x-1, y) || findMazePath(x, y + 1)
            || findMazePath(x+1, y) || findMazePath(x, y - 1)) {
                return true;
            }
```

- `북 -> 동 -> 남 -> 서` 순으로 검사한다.
- 이 4가지 방향을 시도해 봐서 그 중 하나라도 출구로 가는 경로가 있다면,
  `true`를 return하고 함수를 종료한다.

### point 6

```java
            maze[x][y] = BLOCKED_COLOR; // dead end
            return false;
```

- 코드의 실행흐름이 여기까지 도달했다는 것은
  이 위치에서 어느 방향으로 가더라도
  이미 가본 셀을 거치지 않고서는 출구까지 가는 경로가 없다.
  -> **즉, 이 maze[x][y]는 꽝이다!**
- 이 자리를 `BLOCKED_COLOR`인 `빨간색`으로 칠한다.
- 그 후 false를 return하고 함수를 종료한다.

---

## 움직인 경로

- 아래 그림은 방금 위에서 살펴본 알고리즘을 호출했을 때
  **실제로 미로상에서 어떻게 움직이는지**를 그림으로 그린 것이다.
  ![](https://user-images.githubusercontent.com/37353837/51438044-41994700-1cea-11e9-946e-989b8443499e.png)

- 물론, 실제로 움직이는 경로는 각각의 위치에서 어느 쪽(동, 서, 남, 북)을
  먼저 시도해보느냐에 따라 달라질 수 있다.

- 이 그림의 예는 항상 어떤 위치에서 `북 -> 동 -> 남 -> 서` 순으로
  검사한다는 가정하에 그린 것이다.
