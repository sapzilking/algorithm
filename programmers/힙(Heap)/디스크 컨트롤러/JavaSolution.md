## 코드
```java
import java.util.PriorityQueue;
import java.util.stream.IntStream;
import java.util.Collections;

class Solution {
    public int[] solution(String[] operations) {
        PriorityQueue<Integer> minPq = new PriorityQueue<>();
        PriorityQueue<Integer> maxPq = new PriorityQueue<>(Collections.reverseOrder());

        for (String op : operations) {
            if (op.startsWith("I")) {
                minPq.offer(Integer.parseInt(op.split(" ")[1]));
                maxPq.offer(Integer.parseInt(op.split(" ")[1]));
            } else if (op.startsWith("D")) {
                if (op.split(" ")[1].startsWith("-")) {
                    maxPq.remove(minPq.poll());
                } else {
                    minPq.remove(maxPq.poll());
                }
            }
        }
        if (minPq.isEmpty() && maxPq.isEmpty())
            return IntStream.of(0, 0).toArray();
        return IntStream.of(maxPq.poll(), minPq.poll()).toArray();
    }
}
```

<br>

## 풀이
* 우선순위 큐를 하나만 사용해서 풀려고 했으나, 우선순위큐의 rear의 값을 삭제하는 메서드가 지원되지 않아서 우선순위큐를 2개 써서 해결하였다.

