## 코드
```java
import java.util.*;

class Solution {
    
    static class Answer {
	int idx;
	int cnt;
        
        public Answer(int idx, int cnt) {
		this.idx = idx;
		this.cnt = cnt;
	}
        public int getIdx() { return idx; }
    }
    
    public int[] solution(int[] answers) {
        int[] first = {1, 2, 3, 4, 5};
	int[] second = {2, 1, 2, 3, 2, 4, 2, 5};
	int[] third = {3, 3, 1, 1, 2, 2, 4, 4, 5, 5};
        
        List<Answer> answerList = new ArrayList<>();
        
	for (int i = 0; i < 3; i++)
		answerList.add(new Answer(i+1, 0));
	for (int i = 0; i < answers.length; i++) {
		if (answers[i] == first[i % first.length]) { answerList.get(0).cnt++; }
		if (answers[i] == second[i % second.length]) { answerList.get(1).cnt++; }
		if (answers[i] == third[i % third.length]) { answerList.get(2).cnt++; }
	}
	int maxCnt = Math.max(answerList.get(0).cnt, Math.max(answerList.get(1).cnt, answerList.get(2).cnt));

        return answerList.stream().filter(a -> a.cnt == maxCnt).mapToInt(Answer::getIdx).sorted().toArray();
    }
}
```

<br>

## 풀이
* 정답을 반복문을 돌면서 수포자 각각의 배열을 완전탐색으로 탐색하여 해결하였다.
<br>

## 후기
* 수포자 각각의 배열에 인덱스를 어떻게 할지만 구하면 쉽게 해결할 수 있는 문제였다.
