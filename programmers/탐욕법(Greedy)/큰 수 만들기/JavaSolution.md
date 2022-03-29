## 코드
```java
import java.util.stream.Collectors;
import java.util.*;

class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        Arrays.sort(lost);
        Arrays.sort(reserve);
        int answer = n - lost.length;

        //여벌 체육복이 있는 학생이 체육복을 도난 당한 경우
        for (int i = 0; i < lost.length; i++) {
            for (int j = 0; j < reserve.length; j++) {
                if (lost[i] == reserve[j]) {
                    answer++;
                    lost[i] = -1;
                    reserve[j] = -1;
                    break;
                }
            }
        }
        

        for (int i = 0; i < lost.length; i++) {
            for (int j = 0; j < reserve.length; j++) {
                if (lost[i] - 1 == reserve[j] || lost[i] + 1 == reserve[j]) {
                    answer++;
                    reserve[j] = -1;
                    break;
                }
            }
        }
        
        return answer;
    }
}
```

<br>

## 풀이
1. 각각의 배열을 오름차순 정렬한다.
2. 여벌의 체육복이 있는 학생이 체육복을 도난당했다면 lost,reserve에서 해당하는 배열의 값을 -1로 해준다.
3. 체육복을 도난당한 학생들의 배열과 여벌의 체육복이 있는 학생들의 배열을 돌며 조건에 해당되면 reserve배열에 해당하는 값을 -1로 바꿔주고, answer값을 1 늘려준다.

* lost와 reserve배열에서 조건에 해당했을 때 값을 -1로 해주는 이유는 -1로 해야 -1혹은+1 했을 때 각각 -2와 0 이기 때문이다.


