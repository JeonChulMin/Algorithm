# K번째 수



## 문제 설명

배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
3. 2에서 나온 배열의 3번째 숫자는 5입니다.

배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

## 제한사항

- array의 길이는 1 이상 100 이하입니다.
- array의 각 원소는 1 이상 100 이하입니다.
- commands의 길이는 1 이상 50 이하입니다.
- commands의 각 원소는 길이가 3입니다.

### 입출력 예

| array                 | commands                          | return    |
| --------------------- | --------------------------------- | --------- |
| [1, 5, 2, 6, 3, 7, 4] | [[2, 5, 3], [4, 4, 1], [1, 7, 3]] | [5, 6, 3] |

### 입출력 예 설명

[1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다.
[1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다. [6]의 첫 번째 숫자는 6입니다.
[1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다. [1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.



### 내 풀이

> 1. 함수를 하나 만들어서 숫자 하나(해당 번째의 숫자)를 리턴 받게 한다.
>
> 2. 다음 그 함수에서 배열을 잘라주기, 근데 배열 자르는 방법이 어떤 것들이 있나 생각해보기
>   2-1. copyofRange(배열, 시작 인덱스, 끝 인덱스) 함수로 자를 수 있음
>   위 방법 말고도 좋은 방법이 있을까?
>
> 3. 배열을 정렬해주는 함수를 하나 만들어서 정렬된 배열을 반환하도록 한다.
>
>   3-1. Arrays.sort() 말고도 다른 정렬 생각해보기



```Java
import java.util.Arrays;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] result = new int[commands.length];
		for(int i = 0; i < commands.length; i++) {
			result[i] = sliceArray(array, commands[i]);
		}
        return result;
    }
    
    public int sliceArray(int[] array, int[] command) {
		int[] temp = Arrays.copyOfRange(array, command[0]-1, command[1]);
		temp = sort(temp);
		return temp[command[2]-1];
    }
    public int[] sort(int[] arr) {
		Arrays.sort(arr);
		return arr;
	}
}
```



- 전부 라이브러리를 사용해서 무언가 성능 측면에서 좋아보이지 않는다.
- 다음에는 merge, quick, heap 등 여러 가지 중에서 어떤 것을 적용하는 것이 좋을 지 생각해보고 적용하도록 하자