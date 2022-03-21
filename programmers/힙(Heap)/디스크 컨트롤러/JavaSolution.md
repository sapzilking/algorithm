## 코드
```java
import java.util.*;

class Solution {
    
    public int solution(int[][] jobs) {
        int answer = 0;
        int cnt = 0; //큐에서 작업을 하나 꺼낼 때 마다 1씩 증가
        int idx = 0; //jobs의 index
        int workFinish = 0; //현재 진행중인 작업이 끝나는 시점

        //int sum = 0; //현재까지 경과된 시간

        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(job -> job[1])); //작업 소요시간 기준 오름차순 정렬
        Arrays.sort(jobs, Comparator.comparingInt(job -> job[0])); //jobs를 작업 요청시간 기준 오름차순 정렬

        while (jobs.length > cnt) {
            while (idx < jobs.length && jobs[idx][0] <= workFinish) //작업이 진행되는 동안 요청이 들어온 작업을 큐에 넣는다
                pq.offer(jobs[idx++]);
            if (!pq.isEmpty()) { //큐가 비어있지 않으면 큐에서 소요시간이 가장 짧은 작업을 꺼낸 후 소요시간을 계산한다 
                int[] job = pq.poll();
                answer += job[1] + workFinish - job[0];
                workFinish += job[1];
                /*answer += job[1] + sum - job[0];
                sum += job[1];
                workFinish += job[1];*/
                cnt++;
            } else { //작업을 수행하고 있지 않을 때 들어온 요청에 대해 처리한다
                workFinish = jobs[idx][0];
            }
        }
        return answer / jobs.length; //평균값을 리턴해 준다
    }
}
```

<br>

## 풀이
```
- jobs를 요청시간 기준으로 오름차순 정렬한다.
- jobs에서 가장 먼저 들어온 작업을 진행한다.
- 작업을 진행하는 동안 들어온 작업들을 소요시간 기준 오름차순으로 큐에 넣는다.
- 큐에 있는 값들을 하나씩 꺼내어 소요시간을 계산한다.
- 큐가 비어 있다면(작업을 수행하고 있지 않을 때 들어온 요청) workFinish값을 작업의 요청시간으로 하여 큐에 작업이 들어갈 수 있도록 한다.
```
* 위의 규칙들을 이용해서 코딩을 하여 해결하였다.
* 위의 코드에서 주석처리 한 부분 (sum변수 관련된 부분)이 내가 처음에 코딩한 코드인데, answer값을 계산할때 sum과 workFinish를 사용하는 경우가 같은 것 같은데 왜 sum을 쓰면 안되는지 고민하다 시간을 좀 썼다.  
큐에 작업이 없을 때 새로운 작업을 큐에 넣기 위해 workFinish값을 변경하는 부분을 고려하지 않아서 생긴 문제였다.  
만약 sum을 사용하고 싶다면 workFinish값을 jobs[idx][0]으로 set할 때 sum변수 값도 같이 set해주면 된다. (굳이 그럴필요 없지만...)

