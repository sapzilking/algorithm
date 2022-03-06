## 코드
### Queue 사용
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
                answer++;
                if (queue.poll().location == location) break;
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
}
```

### PriorityQueue 사용
```java
import java.util.*;

class Solution {
    
    public int solution(int[] priorities, int location) {
        int answer = 1;
        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
    
        Arrays.stream(priorities).forEach(p -> pq.offer(p));
        
        while (!pq.isEmpty()) {
            for (int i = 0; i < priorities.length; i++) {
                if (pq.peek() == priorities[i]) {
                    if (i == location) return answer;
                    pq.poll();
                    answer++;
                }
            }
        }
        return answer;
    }
}
```

<br>

## 풀이
1. Queue를 사용한 문제 풀이
* location과 priority를 멤버변수로 갖는 Print라는 내부 클래스를 만든다.
* 큐가 빌 때 까지 반복하며 현재 큐의 max priority를 구한 뒤 해당 max값보다 작은 값은 큐에서 뺀 후 다시 큐에 넣는다.
* 큐의 head에서 꺼낸 값이 max값 보다 크거나 같다면 answer값을 1 증가 시킨 후 큐에서 제거 해준다. 이 때 location을 비교해서 parameter로 받은 location과 같다면 반복문을  빠져나온 후 answer값을 리턴해 준다.
2. PriorityQueue를 사용한 문제 풀이
* param으로 받은 priorities의 값들을 우선순위 큐에 넣은 후 내림차순으로 정렬을 한 값을 pq에 넣는다.
* 큐가 빌 때 까지 반복하며 priorities의 길이만큼 반복문을 수행한다.
* priorities에서 꺼낸 값과 pq의 head에서 꺼낸 값이 같다면 location과 i값을 비교하여 찾고자 하는 값인지 확인한다.
* 찾고자 하는 값이라면 answer를 그대로 리턴하고, 아니라면 answer값을 1 증가시킨 후 pq의 head에 있는 값을 제거한 뒤 이어서 반복문을 수행한다.

<br>
