---
description: Kotlin
---

# <같은 숫자는 싫어> 코틀린 풀이

{% embed url="https://school.programmers.co.kr/learn/courses/30/lessons/12906" %}
문제
{% endembed %}

풀이 :

```kotlin
import java.util.*;

public class Solution {
    public int[] solution(int[] arr) {
        ArrayList<Integer> list = new ArrayList<>();
        
        for (int i = 0; i < arr.length - 1; i++) {
            if (arr[i] == arr[i + 1]) {
                continue;
            }
            list.add(arr[i]);
        }
        
        // 마지막 원소는 비교에서 제외되므로 항상 추가해야 합니다.
        list.add(arr[arr.length - 1]);

        // ArrayList를 배열로 변환
        int[] answer = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {
            answer[i] = list.get(i);
        }

        return answer;
    }
}
```
