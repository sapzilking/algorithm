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
2022.09.26(월)
```java
import java.util.*;

class Solution {
    public String solution(int[] numbers) {
        // 1.Convert int[] to String[]
        String[] numbersStrArray = Arrays.stream(numbers).mapToObj(String::valueOf).toArray(String[]::new);
        // 2. Sort by comparator
        Arrays.sort(numbersStrArray, (o1, o2) -> {
            StringBuffer sb1 = new StringBuffer(o1);
            StringBuffer sb2 = new StringBuffer(o2);
            sb1.append(o2);
            sb2.append(o1);

            return sb2.compareTo(sb1);
        });
        
        // 3. Check if array is only "0" (e.g ["0", "0", "0"])
        if (numbersStrArray[0].equals("0"))
            return "0";


        return String.join("", numbersStrArray);
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
- 해당 문제는 스트림, 람다, Comparator, join을 이용해서 해결할 수 있었다.
- 문자열을 더하는 부분에서 StringBuffer를 사용했는데 사실 이 부분은 처음 작성한 코드처럼 String을 "+" 연산해도 JVM 컴파일러가 알아서 최적화 작업을 해 주지만 명시적으로 하고 싶어서 heap 메모리 관리를 위해 immutable한 String 클래스 대신 StringBuffer를 사용하였다.
