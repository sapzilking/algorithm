## 코드
```java
import java.util.*;

class Solution {
    public int solution(int[] people, int limit) {
        int answer = 0;
        int minIdx = 0;
        Arrays.sort(people);

        for (int maxIdx = people.length - 1; maxIdx >= minIdx; maxIdx--) {
            if (people[maxIdx] >= limit) { //people[maxIdx]의 값이 limit보다 크거나 같으면 바로 answer의 값을 1 증가시키고 continue
                answer++;
                continue;
            }
            if (people[maxIdx] + people[minIdx] <= limit) { minIdx++; } //가장 무거운 사람과 가장 가벼운 사람을 더한 값이 limit값 보다 작거나 같으면 minIdx를 증가 1 증가 시켜준다.
            answer++; //answer(구명보트의 개수)를 1 증가 시켜준다.
        }
        return answer;
    }
}
```

<br>

## 풀이
* 구명보트 개수의 최솟값을 구해야 하므로, people를 오름차순 정렬 해준 뒤 가장 큰 값과 가장 작은 값을 더하면서 비교해 주면 된다.  
  사람의 무게가 limit보다 크거나 같으면 더이상 태울 수 없으므로 그대로 answer를 1 증가시켜주고 continue를 해주고, 
  아니라면 가장 무거운 사람과 가장 가벼운 사람을 더해준뒤 limit값과 비교한뒤 적절한 처리를 해 준다.



