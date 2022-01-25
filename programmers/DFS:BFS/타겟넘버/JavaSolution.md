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

## 풀이
* 의상의 종류를 key로, 의상의 가짓 수를 value로 clothesMap에 담아줍니다.
* **곱의법칙**을 이용해서 경우의 수를 계산해 줍니다.
  예를 들어 상의가 2벌, 하의가 1벌이라면 나올 수 있는 경우의 수는

  |num|case| 
  |:---:|:---:|
  |1|1번상의를 입었을 때|
  |2|2번상의를 입었을때|
  |3|상의를 입지 않았을 때|
  |4|1번하의를 입었을 때|
  |5|하의를 입지 않았을 때|

   이렇게 5가지 경우의 수가 있습니다.  
   <br>
   위의 조건을 코드로 구현한 부분이 ```result = result * (v+1)``` 이 부분이구요. +1은 해당 종류의 옷을 입지 않았을 때를 나타냅니다.  
   <br>
   그리고 마지막으로 제한조건에 명시되어 있듯이 아무옷도 입지 않을수는 없으므로 -1을 해준 후 답을 리턴해 줍니다.
