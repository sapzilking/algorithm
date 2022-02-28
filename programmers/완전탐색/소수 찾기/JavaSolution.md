## 코드
```java
import java.util.*;

class Solution {
    
    static int answer = 0;
    List<Integer> numberList = new ArrayList<>(); // 조합한 수들을 저장하는 리스트
    boolean[] visited = new boolean[7];
    
    public int solution(String numbers) {
        String tmp = "";
        for (int i = 0; i < numbers.length(); i++)
            dfs(numbers, tmp, i + 1);
        numberList.stream().forEach(Solution::addPrimeCnt);
        return answer;
    }
    
    // 가능한 모든 경우의 수를 만들어 numberList에 넣는 재귀함수
    void dfs(String number, String tmp, int size) {
        if (tmp.length() == size) {
            int tmpNum = Integer.parseInt(tmp);
            if (!numberList.contains(tmpNum))
                numberList.add(tmpNum);
        } else {
            for (int i = 0; i < number.length(); i++) {
                if (!visited[i]) {
                    visited[i] = true;
                    tmp += number.charAt(i);
                    dfs(number, tmp, size);
                    visited[i] = false;
                    tmp = tmp.substring(0, tmp.length() - 1);
                }
            }
        }
    }
    
    // param으로 들어온 number가 소수인지 판별한 후 소수이면 answer값을 1 증가시키는 메서드
    static void addPrimeCnt(int number) {
        if(number < 2) return;
        for(int i = 2; i <= (int)Math.sqrt(number); i++)
            if(number % i == 0) return;
        answer++;
    }
}
```

<br>

## 풀이
* 주어진 문자열(numbers)의 수로 만들 수 있는 모든 수의 조합을 구한 뒤 (dfs)
* 해당 수들(numberList)을 반복하며 소수를 판별 한 뒤 소수이면 answer값을 1 증가(addPrimeCnt)하였다.
* 그리고 answer값을 리턴해 주었다.
<br>

## 후기
* 재귀함수의 원리와 소수판별 알고리즘을 이용해서 문제를 해결하였다.
* 만약 주어진 숫자까지 소수가 몇개있는지 판별하는 문제였다면 `에라스토테네스의 체` 방식을 이용하였을 것이다.
