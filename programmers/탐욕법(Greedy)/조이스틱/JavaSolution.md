## 코드
```java
class Solution {
    public int solution(String name) {
        int answer = 0;
        int nameLen = name.length();
        int min = nameLen - 1;

        for (int i = 0; i < nameLen; i++) {
            //상하 최소 조작 횟수 판단
            answer += Math.min(name.charAt(i) - 'A', 'Z' - name.charAt(i) + 1);

            int nextIdx = i + 1;
            //다음 문자가 A인지 확인
            while (nextIdx < nameLen && name.charAt(nextIdx) == 'A')
                nextIdx++;
            min = Math.min(min, i * 2 + nameLen - nextIdx); //각 자릿수 마다 역방향으로 이동 시 조작 횟수 판단
            min = Math.min(min, (nameLen - nextIdx) * 2 + i); //역방향으로 먼저 이동 후 정방향으로 이동 했을 때가 더 빠른 경우 판단
        }
        return answer + min;
    }
}
```

<br>

## 풀이
1. 조이스틱 상•하 이동 최소값 판단  
  * 아스키 코드값을 비교하여 더 작은 값으로 판단한다. ( ```Math.min(name.charAt(i) - 'A', 'Z' - name.charAt(i) + 1)``` )
2. 조이스틱 좌•우 이동 최소값 판단  
  * 최초의 최소 이동값은 정방향으로 쭉 갔을 때의 값인 nameLen - 1로 설정해 둔다. ( ```int min = nameLen - 1``` )  
  * 각 자릿수에서 역방향으로 이동했을 때의 값을 구해서 현재 최소값과 비교하여 더 작은 이동횟수를 최소값으로 정한다. ( ```i * 2 + nameLen - nextIdx``` -> 역방향 이동 시 조작 횟수)
  * ```BBBBAAB``` 처럼 처음부터 역방향으로 갔다가 정방향을 가는게 최소 이동횟수가 더 작은 경우도 있으므로 해당 조건도 최소값 비교를 해준다. ( ```(nameLen - nextIdx) * 2 + i``` )


