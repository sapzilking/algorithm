## 이중 For문을 이용한 풀이
```java
import java.util.*;

class Solution {
    public int[] solution(int[] prices) {
        List<Integer> list = new ArrayList<>();

        for (int i = 0; i < prices.length; i++) {
            for (int j = i + 1; j < prices.length; j++) {
                if (prices[i] > prices[j]) {
                    int time = j - i;
                    list.add(time);
                    break;
                } else if (j == prices.length - 1) {
                    list.add(j - i);
                }
            }
        }
        list.add(0);

        return list.stream().mapToInt(Integer::intValue).toArray();
    }
}
```

## Stack을 이용한 풀이
```
import java.util.*;

class Solution {

    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < prices.length; i++) {
            while (!stack.isEmpty() && prices[i] < prices[stack.peek()])
                answer[stack.peek()] = i - stack.pop();
            stack.push(i);
        }

        while (!stack.isEmpty())
            answer[stack.peek()] = prices.length - stack.pop() - 1;

        return answer;
    }
}
```
<br>

## 풀이
* 이중 for문을 이용하는 방법과 스택을 이용하는 방법 2가지로 문제를 풀어 보았다.

<br>
