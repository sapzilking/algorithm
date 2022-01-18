## 코드
```java
import java.util.*;

class Solution {
    
    public String solution(String[] participant, String[] completion) {
        String answer = null;
        Map<String, Integer> participantMap = new HashMap<>();
        
        for (String p : participant) {
            participantMap.put(p, Optional.ofNullable(participantMap.get(p)).orElse(0) + 1);
        }
        
        for (String c : completion) {
            participantMap.replace(c, participantMap.get(c) - 1);
        }
        
        Set<String> keys = participantMap.keySet();
        
        for (String key : keys) {
            if (participantMap.get(key) == 1) {
                answer = key;
                break;
            }
        }
        return answer;
    }
}
```

## 풀이
participant의 값을 participantMap의 key로 하고 해당 이름을 가진 선수의 수를 value로 담는다. (이렇게 한 이유는 동명이인이 있다는 제한사항 때문에)
그다음 completion을 반복하면서 participantMap에서 해당하는 이름을 가진 선수의 수를 하나씩 빼준다.
제한사항으로 completion의 길이는 participant의 길이보다 1 작다는 조건이 있으므로, 결국 participantMap의 value가 1인 사람이 완주하지 못한 사람이다.


