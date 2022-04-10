## 코드
```java
class Solution {
    public static String solution(String number, int k)  {
        StringBuilder sb = new StringBuilder();
        int nextIdx = 0;

        //만들어야 하는 수의 자릿수를 맞출 수 있는 최대 범위 까지 반복
        for (int i = 0; i < number.length() - k; i++) {
            char max = '0';
            for (int j = nextIdx; j <= i + k; j++) { //현재 index 부터 만들어야 하는 수의 자릿수를 맞출 수 있는 최대 범위까지 반복
                if (number.charAt(j) == '9') { //9가 가장 큰 수 이므로 현재 숫자가 9이면 max값으로 set하고 반복문을 빠져나간다.
                    max = number.charAt(j);
                    nextIdx = j + 1;
                    break;
                } else if (number.charAt(j) > max) { //현재 숫자가 기존의 max보다 클 때
                    max = number.charAt(j);
                    nextIdx = j + 1;
                }
            }
            sb.append(max);
        }
        return sb.toString();
    }
}
```

<br>

## 풀이
1. 첫번째 for문 : 만들어야 하는 정답 자릿수의 수를 만들 수 있는 범위 내의 최대 index (number: "1231234", k: 3이면 4자리수를 만들어야 하므로 index 3까지만 반복. 그 이상 가면 4자리수를 못만든다.)
2. 이전에 찾은 max값의 index부터 정답 자릿수의 수를 만들 수 있는 범위 까지 반복한다.  
2-1. 기존의 max값과 꺼내온 숫자를 비교하여 더 크다면 max값을 변경한다.  
2-2. 반복이 끝나면 현재 max값을 stringBuilder에 추가한다. (StringBuilder를 사용한 이유는 String을 사용하면 문자열 덧셈 연산 시 매번 새로운 객체를 생성하기 때문에 메모리 및 시간을 낭비할 수 있기 때문이다.)



