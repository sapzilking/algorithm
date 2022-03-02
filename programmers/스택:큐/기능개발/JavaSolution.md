## 코드
```java
import java.util.*;

class Solution {
    
    public int[] solution(int[] progresses, int[] speeds) {
        int day = 1; // 해당 기능이 배포되기 까지의 작업 기간
        int[] deployCnt = new int[100]; // 각 배포마다 몇 개의 기능이 배포되는지 저장할 배열
        
        for (int i = 0; i < progresses.length; i++) {
            while (progresses[i] + (speeds[i] * day) < 100) {
                day++;
            }
            deployCnt[day]++;
        }
        return Arrays.stream(deployCnt).filter(i -> i != 0).toArray();
    }
}
```

<br>

## 풀이
* progresses를 반복하면서 해당 기능이 완료되면 배포까지 걸린 일 수(day)를 deplyCnt배열에 넣는다.
* 다음 반복문에서는 이전 일 수 가 진행되는 동안 기능이 이미 개발이 완료 되었는지 판단한 뒤 완료 되었다면 같은 일 수를 가지는 deplyCnt배열의 기존 값을 1 증가 시킨다.
* 이런식으로 일 수 별 배포되는 기능의 개수를 deployCnt배열에 넣어준 뒤 마지막에 stream.filter를 이용해서 array로 변환한 후 값을 리턴한다.
<br>
