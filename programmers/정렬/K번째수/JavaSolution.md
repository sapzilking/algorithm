## 코드
```java
import java.util.*;

class Solution {
    
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        for (int i = 0; i < commands.length; i++) {
            int[] copyAndSortArray = Arrays.stream(Arrays.copyOfRange(array, commands[i][0] - 1, commands[i][1])).sorted().toArray();
            answer[i] = copyAndSortArray[commands[i][2] - 1];
        }
        return answer;
    }
}
```
<br>

## 풀이
* array 배열 특정 위치 값 복사 및 정렬 후 특정 인덱스의 값을 answer배열에 넣은 후 리턴한다.
<br>

## 후기
* 이 문제는 간단하기에 따로 설명할 내용이 없다.
