## 코드
```java
import java.util.*;
import java.util.stream.Collectors;

class Solution {
    
    class Song implements Comparable<Song> {
        int idx;
        String genre;
        int play;

        public Song(int idx, String genre, int play) {
            this.idx = idx;
            this.genre = genre;
            this.play = play;
        }

        @Override
        public int compareTo(Song o) {
            if (!this.genre.equalsIgnoreCase(o.genre))
                return this.genre.compareTo(o.genre);
            return o.play - this.play;
        }
    }
    
    public int[] solution(String[] genres, int[] plays) {
        List<Song> songList = new ArrayList<>();
        Map<String, Integer> hm = new HashMap<>();
        List<Integer> resultList = new ArrayList<>();
        int cnt = genres.length;

        //모든 노래에 대해 Song클래스 생성 후 List에 저장
        for (int i = 0; i < cnt; i++) {
            Song song = new Song(i, genres[i], plays[i]);
            songList.add(song);
        }
        Collections.sort(songList); //해당 리스트를 노래 장르 기준으로 정렬한 뒤 동일 장르내에서는 재생횟수 기준으로 정렬

        //key: 장르, value: 장르의 재생횟수
        for (int i = 0; i < cnt; i++) {
            hm.put(genres[i], hm.getOrDefault(genres[i], 0) + plays[i]);
        }

        //재생횟수를 기준으로 desc정렬 후 sortedMap에 저장
        HashMap<String, Integer> sortedMap = hm.entrySet()
          .stream()
          .sorted((o1, o2) -> o2.getValue().compareTo(o1.getValue()))
          .collect(Collectors.toMap(
            Map.Entry::getKey,
            Map.Entry::getValue,
            (a1, a2) -> a1, LinkedHashMap::new) //순서보장을 위해 LinkedHashMap사용
           );

        for (String key : sortedMap.keySet()) {
            int maxCnt = 0; //장르별 최대 2곡제한 판별을 위한 flag
            for (Song song : songList) {
                if (key.equals(song.genre) && maxCnt < 2) {
                    resultList.add(song.idx);
                    maxCnt++;
                } else if (maxCnt == 2) {
                    break;
                }
            }
        }

        //list -> array 변환 후 return
        return resultList.stream().mapToInt(Integer::intValue).toArray();
    }
}
```

## 풀이
* return해야 하는 값이 배열의 index이므로, 정렬 후에 index가 꼬이지 않도록 하기 위해 '배열의 인덱스', '장르', '재생횟수'로 Song이라는 클래스를 만들었다.  
  Song은 클래스 이므로 정렬 방식을 custom 하기 위해 Comparable인터페이스를 구현한뒤 compartTo를 override해주었다.  
  이 때 정렬 조건은 장르를 기준으로 동일한 장르이면 재생횟수의 desc로 정렬하였다.
<br><br>
* 그 다음 재생횟수가 가장 많은 장르를 구하기 위해 'hm'에 장르를 key로, 재생횟수를 value로 하여 map을 만든 후
  해당 map을 value(재생횟수) 기준 desc로 정렬한 뒤 'sortedMap'에 넣어주었다.
<br><br>
* 그 다음 'sortedMap의 key(장르)로 반복문을 돌면서, songList에서 장르별 최대 2곡씩 꺼내온뒤, 해당 index를 'resultList'에 넣어주었다.
<br><br>
* 마지막으로 list -> array로 변환해 준뒤 return 하였다.
<br>

## 후기
해당 문제를 통해 Comparable, Comparator인터페이스에 대해 알게되었고, lambda, stream등의 사용법에 좀 더 익숙해 질 수 있었다.
