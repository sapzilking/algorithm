## 코드
```java
import java.util.Arrays;
import java.util.PriorityQueue;
import java.util.stream.Collectors;

class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
        PriorityQueue<Integer> pq = Arrays.stream(scoville).boxed().collect(Collectors.toCollection(PriorityQueue::new)); //scoville를 우선순위 큐에 넣어준다.
            
        while (pq.size() > 1 && pq.peek() < K) { //큐의 사이즈가 1보다 작거나 같으면 새로운 음식을 만들 수 없으므로 큐의 사이즈가 1보다 크고 가장 작은 값이 K보다 작을동안 반복한다
            pq.offer(pq.poll() + (pq.poll() * 2)); //새로운 음식을 큐에 넣어준다.
            answer++;
        }
        if (pq.peek() < K) //큐에서 가장 작은값이 K보다 작으면 K이상으로 만들 수 없는 것이므로 answer에 -1을 대입한다.
            answer = -1;
        
        return answer;
    }
}
```

<br>

## 풀이
* 우선순위 큐를 이용해 간단하게 해결할 수 있으므로 풀이 생략

