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
