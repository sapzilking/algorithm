## 코드
```java
import java.util.*;
class Solution {
    
    public boolean solution(String[] phone_book) {
        boolean answer = true;
        Arrays.sort(phone_book);
        
        for (int i=0; i<phone_book.length - 1; i++) {
            if (phone_book[i+1].startsWith(phone_book[i])) {
                answer = false;
                break;
            }
        }
        return answer;
    }
}
```

## 풀이
* param으로 받은 phone_book을 정렬 한 뒤 반복, 해당 값과 그 다음 값을 비교하여 그 다음 값이 이전 값으로 시작하는지 판단하였다.