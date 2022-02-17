## 코드
```java
import java.util.*;

class Solution {
    
    public int solution(int[] citations) {
        int answer = 0;
	Arrays.sort(citations);

	for (int i = 0; i < citations.length ; i++) {
	    int h = citations.length - i;
	    if (citations[i] >= h) {
	        answer = h;
		break;
	    }
	}
	return answer;
    }
}
```
<br>

## 풀이
* citations를 오름차순 정렬한 뒤 반복하면서 citations의 원소값이 h보다 크거나 같으면 h를 answer에 담은 뒤 반복문을 빠져나온다.

## 후기
* 해당 문제는 예제를 한 3개정도 적어보니 규칙이 보여서 어렵지 않게 해결할 수 있었다.
