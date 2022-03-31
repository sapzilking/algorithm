## 코드
```java
class Solution {
    public int solution(String name) {
        int answer = 0;
        int nameLen = name.length();
        int min = nameLen - 1; //정방향 역방향 판단용

        for (int i = 0; i < nameLen; i++) {
            //상하 최소 조작 횟수 판단
            answer += Math.min(name.charAt(i) - 'A', 'Z' - name.charAt(i) + 1);

            int nextIdx = i + 1;
            //다음 문자가 A인지 확인
            while (nextIdx < nameLen && name.charAt(nextIdx) == 'A')
                nextIdx++;
            min = Math.min(min, i * 2 + nameLen - nextIdx); //기존의 min과 역방향 이동 중 최소 조작 회숫 판단
            min = Math.min(min, (nameLen - nextIdx) * 2 + i); //기존의 min과 역방향 먼저 이동 후 정방향으로 이동 했을 때 중 최소 조작 횟수 판단
        }
        return answer + min;
    }
}
```

<br>

## 풀이
1. 각각의 배열을 오름차순 정렬한다.
2. 여벌의 체육복이 있는 학생이 체육복을 도난당했다면 lost,reserve에서 해당하는 배열의 값을 -1로 해준다.
3. 체육복을 도난당한 학생들의 배열과 여벌의 체육복이 있는 학생들의 배열을 돌며 조건에 해당되면 reserve배열에 해당하는 값을 -1로 바꿔주고, answer값을 1 늘려준다.

* lost와 reserve배열에서 조건에 해당했을 때 값을 -1로 해주는 이유는 -1로 해야 -1혹은+1 했을 때 각각 -2와 0 이기 때문이다.


