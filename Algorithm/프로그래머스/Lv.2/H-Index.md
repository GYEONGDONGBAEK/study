# [프로그래머스] H-Index

## 문제 링크:

[문제 바로가기](https://school.programmers.co.kr/learn/courses/30/lessons/42747)

## 문제 설명:

H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과[1](https://school.programmers.co.kr/learn/courses/30/lessons/42747#fn1)에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 `n`편 중, `h`번 이상 인용된 논문이 `h`편 이상이고 나머지 논문이 h번 이하 인용되었다면 `h`의 최댓값이 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

### 제한사항

- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

### 입출력 예

| citations | return |
| --- | --- |
| [3, 0, 6, 1, 5] | 3 |

### 입출력 예 설명

이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.

## 문제 풀이:

```java
import java.util.*;
class Solution {
    public int solution(int[] citations) {
        Arrays.sort(citations);
        int len = citations.length;
        for(int i=0;i<len;i++){
            if(citations[i]>=len-i){
                return len-i;
            }
        }
        return 0;
    }
}
----------------------------------------------------------
정확성  테스트
테스트 1 〉	통과 (0.69ms, 84.8MB)
테스트 2 〉	통과 (0.71ms, 78.6MB)
테스트 3 〉	통과 (0.88ms, 84.8MB)
테스트 4 〉	통과 (0.53ms, 76.6MB)
테스트 5 〉	통과 (0.90ms, 77.2MB)
테스트 6 〉	통과 (0.59ms, 78.8MB)
테스트 7 〉	통과 (0.63ms, 72.1MB)
테스트 8 〉	통과 (0.44ms, 81.4MB)
테스트 9 〉	통과 (0.34ms, 77.1MB)
테스트 10 〉	통과 (0.48ms, 77.3MB)
테스트 11 〉	통과 (0.62ms, 73.3MB)
테스트 12 〉	통과 (0.39ms, 77.2MB)
테스트 13 〉	통과 (0.58ms, 76.3MB)
테스트 14 〉	통과 (0.91ms, 83.2MB)
테스트 15 〉	통과 (0.60ms, 76.9MB)
테스트 16 〉	통과 (0.35ms, 77.3MB)
채점 결과
정확성: 100.0
합계: 100.0 / 100.0
```

### **문제 풀이 해석:**

어떤 과학자가 발표한 논문 `n`편 중, `h`번 이상 인용된 논문이 `h`편 이상이고 나머지 논문이 h번 이하 인용되었다면 `h`의 최댓값이 이 과학자의 H-Index 란 설명이 있었기 때문에, 일단 오름차순으로 정렬한 후 배열을 순회하면서 citations[i]>=len-i 이 설명과 동일한 역할을 한다. 이 후 그때의 인덱스를 리턴하는 문제였다.