## 코드
```java
import java.util.*;

class Solution {
    
    static boolean[] visited;
    static List<String> answerList;
    
    public String[] solution(String[][] tickets) {
        visited = new boolean[tickets.length]; //방문 확인용
        answerList = new ArrayList<>(); //정답을 담을 리스트
        Arrays.sort(tickets, Comparator.comparing(t -> t[1]));
        dfs(0,"ICN", "ICN", tickets);

        return answerList.get(0).split(" ");
    }
    
    public static void dfs(int count, String start, String dest, String[][] tickets) {
            if (count == tickets.length) { //모든공항 다돌았을때
                answerList.add(dest);
                return;
            }
            for (int i = 0; i < tickets.length; i++) {
                if (!visited[i] && tickets[i][0].equals(start)) {
                    visited[i] = true;
                    dfs(count+1, tickets[i][1], dest + " " + tickets[i][1], tickets);
                    visited[i] = false;
                }
            }
        }
}
```
<br>

## 풀이
* TODO
