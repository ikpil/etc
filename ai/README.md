# 서론
# 본문

## 다음 미로의 입구(●, (0, 0) 위치)에서 출발하여 출구(▲, (4, 4) 위치)로 나오는 가장 짧은 경로를 탐색하려고 한다. 이동은 상, 하, 좌, 우의 방 향으로 1칸씩 할 수 있다고 가정한다.

사진 추가 하면 좋을것 같음

### (가) 상태공간 탐색으로 이 문제를 풀이하기 위한 문제표현에 대해 설명 하라. 

풀이하기 위한 표현하기 위해선 3가지 정의가 필요하다고 배웠습니다.

- 상태 묘사 정의
- 초기 상태, 목표 상태 정의
- 연산자 정의

### 상태 묘사 정의
이 문제의 경우, 미로의 상태와 커서 위치 상태로 분리 할 수 있으며, 미로의 상태는 상수이고, 커서의 위치 상태만 변수입니다. 다음과 강티 묘사가 가능 합니다.

표현한 상수인 미로의 묘사 
```cpp
// 의사 코드 형태로 이해하면 됩니다.
struct Block
{
    // up, right, down, left 방향순으로 false는 막힘 true는 열림을 표현
    bool dir[4] = { false, false, false, false };
};

class Maze
{
public:
    Block xy2d[4][4];
}
```

미로의 커서 상태 묘사
```cpp
// 의사 코드 형태로 이해하면 됩니다.
class MazeCursor
{
public:
    int x = 0, y = 0;
};
```

### 초기 상태, 목표 상태 정의
미로와 미로의 커서로 분리 했으므로, 미로는 상수이고, 커서만 변수로서의 상태 공간을 갖습니다. 그러므로 다음과 같이 표현 하여, MMazeCursor 만 관리하면 됩니다.

다음과 같습니다.

```cpp
// 의사 코드 형태로 이해하면 됩니다.
// 미로의 각 공간마다 방향에 따른 이동 가능 유무를 저정합니다.
Maze maze;
maze.xy2d[0][0].dir = { true, true, false, false };
maze.xy2d[0][1].dir = { false, false, false, true };
...
maze.xy2d[4][4].dir = { false, true, true, false };

// 입구, 초기 상태를 의미 합니다.
MazeCursor cursor;
cursor.x = 0;
cursor.y = 0;

// 출구, 목표 상태를 의미 합니다.
MazeCursor goal;
goal.x = 4;
goal.y = 4;
```

### 연산자 정의
미로 커서의 상태가 묘사 되었으므로, 미로 커서의 상태 변경을 위한 연산자를 정의 합니다. 

다음과 같습니다.

```cpp
// 의사 코드 형태로 이해하면 됩니다.
// maze : 상수인 미로 판 
// cursor : 미로 커서 상태
// dir : 움직이려는 방향

bool move(const Maze& maze, MazeCursor& cursor, int dirV)
{    
    // 현재 커서로 부터 이동 방향으로 이한 이동이 가능한지 체크
    if (false == maze.xy2d[cursor.x][cursor.y].dir[dirV])
    {
        return false;
    }

    // 커서 이동값 상수
    // dirV이 0 일 때, 위쪽
    // dirV이 1 일 때, 오른쪽
    // dirV이 2 일 때, 아래쪽
    // dirV이 3 일 때, 왼쪽
    MazeCursor moveVector[4];

    // 위쪽 이동에 대한 값 묘사
    moveVector[0].x = 0;
    moveVector[0].y = 1;

    // ...

    // 왼쪽 이동에 대한 값 묘사
    moveVector[3].x = -1;
    moveVector[3].y = 0;

    // 커서 이동 
    cursor.x = cursor.x + moveVector[dirV].x;
    cursor.y = cursor.Y + moveVector[dirV].y;

    return true;
}
```


### (나) 균일비용 탐색을 적용하여 문제의 해를 구하려고 한다. 비용을 정 의하고, 이에 따른 탐색 트리를 구하라.

### (다) A* 알고리즘을 적용하여 문제의 해를 구하려고 한다. 평가함수를 정의하고, 이에 따른 탐색 트리를 구하라.

# 결론
