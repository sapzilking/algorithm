## 코드
```java
class Solution {
    public int solution(int n, int[][] computers) {
        int answer = 0;
        int len = n;
        boolean[] visited = new boolean[n];
        
        for (int i=0; i<len; i++) {
            if (!visited[i]) {
                dfs(i, len, computers, visited);
                answer++;
            }
        }
        return answer;
    }
    
    public void dfs(int i, int len, int[][] computers, boolean[] visited) {
        visited[i] = true;
        
        for (int j=0; j<len; j++) {
            if (i != j && computers[i][j] == 1 && !visited[j]) {
                dfs(j, len, computers, visited);
            }
        }
    }
}
```
<br>

## 풀이
* 해당 문제는 깊이우선탐색으로 해결하기 위해 재귀함수를 사용하였다. 
* dfs를 수행 중 자기자신이 아니면서 값이 1이고, 이미 방문하지 않은 곳이면 다시 dfs를 호출하는 식으로 구현해 주었다.
<br>

## 후기
dfs관련 문제를 몇개 풀었더니 해당 문제는 간단하게 해결할 수 있었다.
