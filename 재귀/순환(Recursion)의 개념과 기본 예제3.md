# 순환(Recursion)의 개념과 기본 예제3

## Designing Recursion 순환 알고리즘의 설계

- 재귀 함수를 설계, 요령에 대해 생각해본다.



## 순환적 알고리즘 설계

- 적어도 하나의 base case, 즉 순환되지 않고 종료되는 case가 있어야 함
- 모든 case는 결국 base case로 수렴해야 함
- base case가 여러 가지가 있을 수도 있다.

- 여기서는 일반적 함수와 재귀 함수를 구현할 경우 가장 큰 차이점 중 하나인 **암시적(implicit) 매개변수를 명시적(explicit) 매개변수로 바꾸어라**라는 점을 살펴본다.



## 순차 탐색

- 이 함수의 미션은 data[0]에서 data[n-1] 사이에서 target을 검색하는 것이다.
- 하지만 검색 구간의 시작 인덱스 0은 보통 생략한다, 즉 암시적 매개변수이다.

```java
int search(int [] data, int n, int target) {
	for(int i=0; i<n; i++) {
		if(data[i]==target) {
			return i;
		}
	}
	return -1;
}
```

- 0은 배열의 시작이 0으로 시작하니까 생략하여 암시적 매개변수로 사용하는 경우가 많다. 하지만 재귀 함수의 경우에는 저렇게 하지 않는 것을 추천한다.

#### 매개 변수의 명시화

```java
int search(int [] data, int begin, int end, int target) {
	if(begin > end) {
		return -1;
	}
	else if(target == items[begin]) {
		return begin;
	}
	else {
		return search(data, begin+1, end, target);
	}
}
```

- 검색 구간의 시작점을 명시적으로 지정한다.



#### 첫번째 알고리즘은 끝 지점은 명시적으로 되어 있지만 시작 위치는 암시적이다.

#### 두번째 알고리즘은 두 지점다 명시적으로 해줬다, 그 이유는 맨 처음 이 search를 호출할 때는 

#### search(data, 0, n-1, target) 함수로 들어와서 1에서부터 n-1 사이로 수정된다. 

#### 이처럼 재귀 함수의 매개변수들은 맨 처음 함수만을 생각해서 설계하면 안되고 좀 더 일반적인 형태를 가져야 한다.

#### 따라서 검색할 위치를 시작 위치를 명시적으로 해줘야 한다. 나중에 재귀함수에서 명시할 수 없기 때문에

#### 하지만 생략할 수 있는 경우 생략하면 된다. 예를 들어 end는 고정일 경우 사용하지 않고 data.length를 사용해서 하면 된다.

