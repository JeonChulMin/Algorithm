

# Level 1 모의고사

# 문제 설명

수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

# 제한 조건

- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

# 입출력 예

| answers     | return  |
| ----------- | ------- |
| [1,2,3,4,5] | [1]     |
| [1,3,2,4,2] | [1,2,3] |

# 입출력 예 설명

## 입출력 예 #1

- 수포자 1은 모든 문제를 맞혔습니다.
- 수포자 2는 모든 문제를 틀렸습니다.
- 수포자 3은 모든 문제를 틀렸습니다.

따라서 가장 문제를 많이 맞힌 사람은 수포자 1입니다.

## 입출력 예 #2

- 모든 사람이 2문제씩을 맞췄습니다.



```java
class Solution {
    public int[] solution(int[] answers) {
        int p1[] = {1,2,3,4,5};
		int p2[] = {2,1,2,3,2,4,2,5};
		int p3[] = {3,3,1,1,2,2,4,4,5,5};
        int count[] = {0,0,0};
        
        count[0] = check(answers, p1);
		count[1] = check(answers, p2);
		count[2] = check(answers, p3);
        
        return max(count);
    }
    
    public int check(int answers[], int arr[]) {
		int count = 0;
		int i = 0;
		for(int idx=0; idx<answers.length; idx++) {
			if(i == arr.length) {
				i = 0;
			}
			if(answers[idx] == arr[i]) {
				count++;
				i++;
			}else {
				i++;
			}
		}	
		return count;
	}
    
    
    public int[] max(int count[]) {
		int max = count[0];
		int cnt = 0;
		int idx =0;
		boolean ch[] = {false, false, false};
		for(int i = 1; i < count.length; i++) {
			max = Math.max(max, count[i]);
		}
		
		for(int z = 0; z < count.length; z++) {
			if(max == count[z]) {
				ch[z] = true;
				cnt++;
			}
		}
		int result[] = new int[cnt];
		for(int x =0; x<count.length; x++) {
			if(ch[x] == true) {
				result[idx] = x+1;
				if((idx+1) == cnt) {
					break;
				}
				idx++;
			}
		}
		
		return result;
		
	}
}
```



# 다른 사람 코드 참고

- 다른 사람의 코드에서는 비교를 %로 해주었다.

```java
for(int i = 0; i < answers.length; i++) {
	if(answers[i] == p1[i%5])
		count[0]++;
	if(answers[i] == p2[i%8])
		count[1]++;
	if(answers[i] == p3[i%10])
		count[2]++;
}
```

- 그리고 내 코드에서는 최댓값을 구하고 그와 같은 값이 있을 경우를 찾느라 반복문을 많이 사용했는데 arrayList를 사용하면 코드 양을 줄일 수 있다.
- ArrayList를 토대로 길이, 그 안의 값을 사용해서 배열을 만들고 값을 넣고 리턴해주면 된다.

```java
List <Integer> maxP = new ArrayList<>();

for(int i = 0; i < count.length; i++) {
	if(max == count[i]) {
		maxP.add(i);
	}
}
```



# Reference

- https://eunsamar.tistory.com/89

