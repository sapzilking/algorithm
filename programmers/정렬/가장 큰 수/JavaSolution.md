## 코드
```java
import java.util.*;

class Solution {
    
    public String solution(int[] numbers) {
        // numbers를 String배열로 변환
        String[] numbersToStrArr = Arrays.stream(numbers) 
                .mapToObj(String::valueOf)
                .toArray(String[]::new);
        Arrays.sort(numbersToStrArr, (n1, n2) -> (n2+n1).compareTo(n1+n2)); //정렬
        
        if (numbersToStrArr[0].equals("0")) //numbers가 모두 0일때
			return "0";
        
        return String.join("", numbersToStrArr); //String으로 리턴
    }
}
```
<br>

## 풀이
* ASCII코드 값에 따라 정렬하기 위해 int배열을 String 배열로 변환한다.
* 그 다음 두 수를 합쳤을 때 더 큰수를 판별하기 위해 Comparator를 구현해서 numbersToStrArr를 정렬한다.
* numbers가 모두 0일때는 0만 리턴하는 조건을 추가한 뒤, numbersToStrArr를 String으로 변환 후 리턴한다.
<br>

## 후기
해당 문제는 스트림, 람다, Comparator, join을 이용해서 해결할 수 있었다.
