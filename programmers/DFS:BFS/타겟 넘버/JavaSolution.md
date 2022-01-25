## 코드
```java
class Solution {
    
    public int solution(int[] numbers, int target) {
        return recursive(numbers, target, 0,0);
    }
    
    int recursive(int[] numbers, int target, int idx, int sum) {
        if (numbers.length == idx) {
            if (target == sum) {
                return 1;
            }
            return 0;
        }
        return recursive(numbers, target, idx+1, sum+numbers[idx]) + recursive(numbers, target, idx+1, sum-numbers[idx]);
    }
}
```
<br>

## 풀이
* 해당 문제는 깊이우선탐색으로 해결하기 위해 재귀함수를 사용하였다. 
* 재귀함수를 잘 이해하고 있으면 어렵지 않게 풀 수 있는문제이다.
<br>

## 후기
해당 문제가 재귀함수로 해결해야 한다는 건 알았지만, 머릿속으로 어떤 식으로 해야할지 바로 떠오르지 않아서, 하나하나 디버깅을 하며 구현하였다.  
앞으로 재귀함수에 더 익숙해질 수 있도록 연습해야겠다.
