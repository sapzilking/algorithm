## 코드
```java
import java.util.*;

class Solution {
    public int solution(int bridge_length, int weight, int[] truck_weights) {
        Queue<Integer> bridge = new LinkedList<>(); // 트럭을 담을 큐
        int totalTruckWeight = 0; // 현재 다리위에 있는 트럭의 무게의 총 합
        int sec = 0; // 경과된 초

        for (int truckWeight : truck_weights) { // 트럭을 한대씩 꺼낸다
            while(true) { // 트럭을 큐에 넣을때 까지 반복한다
                if (bridge.isEmpty()) { // 큐가 비어있으면 트럭을 큐에 넣는다
                    totalTruckWeight += truckWeight;
                    bridge.offer(truckWeight);
                    sec++;
                    break;
                } else if (bridge.size() == bridge_length) { // 큐가 다리 길이와 같으면 큐의 head에 있는 값을 꺼내고 totalTruckWeight값에서 빼준다
                    totalTruckWeight -= bridge.poll();
                } else if (weight >= totalTruckWeight + truckWeight) { // 현재 다리에 있는 트럭의 무게 + 새로운 트럭의 무게를 다리가 버틸수 있는지 확인한다
                    totalTruckWeight += truckWeight;
                    bridge.offer(truckWeight);
                    sec++;
                    break;
                } else { // 트럭의 진행상황 표현을 위해 큐에 0을 넣어준다
                    bridge.offer(0);
                    sec++;
                }
            }
        }
        return sec + bridge_length; // 현재까지 진행된 초 + 마지막 트럭이 내려와야 하므로 bridge_length를 더한 값을 리턴해준다
    }
}
```

<br>

## 풀이
* 큐를 다리라고 생각하고 한대 씩 현재 다리에 올라갈 수 있는지 조건을 판단한 후 구현해주면 된다. 크게 어렵지 않게 해결할 수 있는 문제였다.

<br>
