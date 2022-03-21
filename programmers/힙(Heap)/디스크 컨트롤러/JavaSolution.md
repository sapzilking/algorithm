## 코드
```java
import java.util.*;

class Solution {
    
    public int solution(int[][] jobs) {
        int cnt = 0;
        int idx = 0;
        int workFinish = 0; //작업이 끝나는 시점
        int answer = 0;
        //int sum = 0; //현재까지 경과된 시간

        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(job -> job[1])); //작업 소요시간 기준 오름차순 정렬
        Arrays.sort(jobs, Comparator.comparingInt(job -> job[0])); //jobs를 작업 요청시간 기준 오름차순 정렬

        while (jobs.length > cnt) {
            while (idx < jobs.length && jobs[idx][0] <= workFinish) //작업이 진행되는 동안 요청이 들어온 작업을 큐에 넣는다
                pq.offer(jobs[idx++]);
            if (!pq.isEmpty()) { //큐가 비어있지 않으면 큐에서 소요시간이 가장 작은 작업을 꺼내서 계산한다 
                int[] job = pq.poll();
                answer += job[1] + workFinish - job[0];
                workFinish += job[1];
                /*answer += job[1] + sum - job[0];
                sum += job[1];
                workFinish += job[1];*/
                cnt++;
            } else { //작업을 수행하고 있지 않을 때 들어온 요청에 대해 처리하기 위해 workFinish값을 조정한다
                workFinish = jobs[idx][0];
            }
        }
        return answer / jobs.length;
    }
}
```

<br>

## 풀이
* 우선순위 큐를 하나만 사용해서 풀려고 했으나, 우선순위큐의 rear의 값을 삭제하는 메서드가 지원되지 않아서 우선순위큐를 2개 써서 해결하였다.

