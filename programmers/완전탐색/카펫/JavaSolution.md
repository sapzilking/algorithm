## 코드
```java
import java.util.*;

class Solution {
    public int[] solution(int brown, int yellow) {
        int[] answer = new int[2];
        int size = brown + yellow; // 카펫 사이즈

        for (int i = 1; i <= size; i++) {
            int row = i;
            int column = size / i;

            if (row < column) // column이 row보다 더 크면 안되니 continue처리
                continue;
            if (row * column == size && (row - 2) * (column - 2) == yellow) { // 사이즈가 row * column과 같고 yellow의 크기가 param이 맞을 때
                answer[0] = row;
                answer[1] = column;
                break;
            }
        }
        return answer;
    }   
}

```

<br>

## 풀이
* param으로 주어지는 brown과 yellow를 더해서 전체 카펫의 사이즈를 구한다.
* 1부터 카펫의 사이즈까지 반복하며, row가 column보다 크거나 같다는 조건이 있으므로 해당 조건일 때는 continue로 다음 조건으로 간다.
* row가 column보다 크거나 같아지면 row * column이 카펫의 사이즈와 같은지, 현재 row와 column으로 yellow의 개수를 구해서 param으로 받은 yellow와 같은지 두개의 조건을 확인 한 후 둘 다 맞다면 answer에 값을 채워준 후 break문을 통해 반복문을 빠져나간다.


## 후기
* 그림으로 카펫을 그려본 후 brown과 yellow의 규칙을 찾아서 해결하면 간단하게 풀 수 있는 문제였다.
