## 코드
```java
import java.util.*;

class Solution {
    
    int answer = 0;
    Queue<Print> queue = new LinkedList<>();
    
    public int solution(int[] priorities, int location) {
        for (int i = 0; i < priorities.length; i++) { queue.offer(new Print(i, priorities[i])); }
        
        while (!queue.isEmpty()) {
            final Print print = queue.stream().max(Comparator.comparingInt(p -> p.priority)).orElseThrow();
            final int maxPriority = print.priority;
            if (maxPriority > queue.peek().priority) {
                queue.offer(queue.poll());
            } else {
                Print poll = queue.poll();
                answer++;
                if (poll.location == location) break;
            }
        }
        return answer;
    }
    
    class Print {
        int location;
        int priority;

        public Print(int location, int priority) {
            this.location = location;
            this.priority = priority;
        }
    }
}```

<br>

## 풀이

<br>
