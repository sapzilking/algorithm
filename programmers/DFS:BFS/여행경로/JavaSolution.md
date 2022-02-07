## 코드
```java
import java.util.*;

class Word {
        String word;
        int cnt;

        Word(String word, int cnt) {
            this.word = word;
            this.cnt = cnt;
        }
    }

class Solution {
    public int solution(String begin, String target, String[] words) {
        Queue<Word> queue = new LinkedList<>();
        boolean[] checked = new boolean[words.length]; //방문한 문자에 대해 재방문 하지 않기 위해 사용

        queue.offer(new Word(begin, 0));

        while (!queue.isEmpty()) { // 큐가 빌 때 까지 반복
            Word word = queue.poll();
            if (word.word.equals(target)) { //단어와 target이 같으면 탐색횟수를 리턴한다.
                return word.cnt;
            }
            for (int i = 0; i < words.length; i++) {
                if (checked[i]) // 방문한 문자인지 확인
                    continue;
                if (addQueue(word.word, words[i])) { //글자수가 1개 다르면 해당 단어를 큐에 삽입
                    queue.offer(new Word(words[i], word.cnt + 1));
                    checked[i] = true;
                }
            }
        }
        return 0;
    }
    
    // 단어를 비교해서 다른 글자 수가 1개이면 true, 아니면 false를 리턴한다.
    public boolean addQueue(String begin, String word) {
        int diffCnt = 0;

        for (int i = 0; i < word.length(); i++) {
            if (begin.charAt(i) != word.charAt(i)) {
                diffCnt++;
            }
        }
        if (diffCnt == 1) 
            return true;
        return false;
    }
}
```
<br>

## 풀이
* 해당 문제는 넓이 우선 탐색을 활용해 어렵지 않게 해결 하였다.
