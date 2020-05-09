# H-Index



## 문제 설명

H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.



## 제한사항

- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.



### 입출력 예

| citations       | return |
| --------------- | ------ |
| [3, 0, 6, 1, 5] | 3      |



### 입출력 예 설명

이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.







```
class Solution {
    public int solution(int[] citations) {
        int answer = 0;
        
        return answer;
    }
}
```

어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index입니다.

[3,0,6,1,5] > 3

이게 왜 정렬 문제일까를 생각해보자

0,1,3,5,6 정렬하면 이렇게 됨

length = n편

112345

로직을 어떻게 자야할 까

h index가 여러 개 일 수 있음  그 중 max 값을 구해야함

1, 1, 4, 4, 4, 5

h index : 1, 2, 3, 4


$$
H-Index = max(min(f(i), i))
$$

- f(i)는 i 번째 논문의 인용 횟수



1. max 변수 만들어서 항상 최대 값 유지하기
2. 로직은 어떻게 짤까
   1. 우선 정렬하기
   2. for문 사용해서 인덱스 0부터 조사해서 count 변수를 사용해 해당 인용수 까지 도달하면 max랑 비교해서 선정하기

30615

[6, 5, 3, 1, 0]



10, 8, 5, 4, 3    / 4

25, 8, 5, 3, 3    / 3

ㄴㅇ

| 25   | 8    | 5    | 3    | 3    |
| ---- | ---- | ---- | ---- | ---- |
| 0    | 1    | 2    | 3    | 4    |



| 10   | 8    | 5    | 4    | 3    |
| ---- | ---- | ---- | ---- | ---- |
| 0    | 1    | 2    | 3    | 4    |

Formally, if *f* is the function that corresponds to the number of citations for each publication, we compute the *h*-index as follows. 

1. First we order the values of *f*  from the largest to the lowest value. 
2. Then, we look for the last position in which *f*  is greater than or equal to the position (we call *h* this position). For example, if we have a researcher with 5 publications A, B, C, D, and E with 10, 8, 5, 4, and 3 citations, respectively, the *h*-index is equal to 4 because the 4th publication has 4 citations and the 5th has only 3. 
3. In contrast, if the same publications have 25, 8, 5, 3, and 3 citations, then the index is 3 because the fourth paper has only 3 citations.



If we have the function *f* ordered in decreasing order from the largest value to the lowest one, we can compute the *h*-index as follows:







https://en.wikipedia.org/wiki/H-index

위키백과에 계산 방법이 나와있음





6 5 3 1 0

0 1 2 3 4



로직이 내림 차순으로 정렬 후에 해당 인덱스 값과 크거나 같은 마지막 위치를 찾으면 답...

Arrays.sort(arrays, Collections.reverseOrder());

// arrays 자리에는 primitive type은 안됨

예를 들어 int arr[] = {1,2,3,4}는 안되고 Integer arr[] = {1,2,3,4}는 됨





[22, 42]  / 2



42 22 

1 2

[20,19,18,1] / 3

[20,19,18,17] /  4





```java
import java.util.*;


class Solution {
    public int solution(int[] citations) {
        int max = 0;
        int count = 0;
        Integer cita[] = new Integer[citations.length];
        for(int i = 0; i < citations.length; i++){
            cita[i] = citations[i];
        }
        Arrays.sort(cita, Comparator.reverseOrder());
        for(int i=0; i<cita.length; i++) {
            
			if((i+1) <= cita[i]) {
				max = i+1;
			} 
		}
      
        return max;
        
    }
}
```







# Integer 와 int 차이

