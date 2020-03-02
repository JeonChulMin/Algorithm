# Java 에서의 정렬

# 기본 타입 데이터의 정렬

- Arrays 클래스가 primitive 타입 데이터를 위한 정렬 메서드를 제공

```java
int [] data = new int [capacity];
// data 배열 안에 데이터가 꽉 차있다고 가정
Arrays.sort(data);
//  자동 정렬
Arrays.sort(data, 0, size);
// 만일 배열 안에 데이터가 꽉 차있지 않고 size -1 까지 차있다면 위와 같이 정렬
// size는 데이터의 갯수
```

- int 이외의 다른 primitive 타입 데이터 double, char 등 에 대해서도 제공

# 객체의 정렬 : 문자열

- 이제 primitive 타입이 아닌 객체 타입의 정렬에 대해 알아본다.

```java
String [] fruits = new String[] {"Pineapple", "Apple", "Orange", "Banana"};
Arrays.sort(fruits);
for(String name : fruits) {
	System.out.println(name);
}
```

- 데이터의 일부분만 정렬하고 싶다면 아까와 같이 시작 인덱스와 데이터의 갯수를 매개변수로 주면 된다.
- 문자열은 String 클래스 자체가 사전식 순서로 크기를 구분하기 때문에 알파벳 순으로 정렬된다.

# ArrayList 정렬 : 문자열

```java
List<String> fruits = new ArrayList<String>();
fruits.add("Pineapple");
fruits.add("Apple");
fruits.add("Orange");
fruits.add("Banana");
Collections.sort(fruits);
for(String name : fruits) {
	System.out.println(name);
}
```

- 배열이 아니니 Arrays 사용 못하고 Collections.sort 사용

# 객체의 정렬 : 사용자 정의 객체

```java
public class Fruit {
	public String name;
	public int quantity;
	public Fruit(String name, int quantity) {
		this.name = name;
		this.quantity = quantity;
	};
}
//
Fruit [] fruits = new Fruit[4];
fruits[0] = new Fruit("Pineapple", 70);
fruits[1] = new Fruit("Apple", 100);
fruits[2] = new Fruit("Orange", 80);
fruits[3] = new Fruit("Banana", 90);

Arrays.sort(fruits);
```

- 객체를 정렬한다는 것인데, 정렬은 크기 순으로 정렬한다는 것인데 어떤 것이 누가 더 큰 건지 알 수 없다. 누가 더 큰 지 정의되어 있지 않기 때문에 비교할 수 없다.
- 위 코드는 돌아가지 않는다.
- 사용자 정의 객체를 정렬하고 싶다면 객체 간 크기 비교를 정의해줘야 한다.
- 2가지 방법이 있다.

# 객체의 정렬 : Comparable Interface

```java
public class Fruit implements Comparable<Fruit> {
	public String name;
	public int quantity;
	public Fruit(String name, int quantity) {
		this.name = name;
		this.quantity = quantity;
	}
	public int compareTo(Fruit other) {
		return name.compareTo(other.name);
		// 객체가 들어왔을 때 이름 기준으로 비교해서 정렬
		// 규칙 정의!
	}
}
// 이름 순으로 정렬
Fruit [] fruits = new Fruit[4];
fruits[0] = new Fruit("Pineapple", 70);
fruits[1] = new Fruit("Apple", 100);
fruits[2] = new Fruit("Orange", 80);
fruits[3] = new Fruit("Banana", 90);

Arrays.sort(fruits);
```

- Comparable Interface은 제네릭스
- 클래스는 아니고 인터페이스, compareTo 메소드 사용
- 결과로 Apple, Banana, Orange, Pineapple 순으로 정렬됨



# 만약 이름이 아니라 재고수량으로 정렬하고 싶다면?

```java
public class Fruit implements Comparable<Fruit> {
	public String name;
	public int quantity;
	public Fruit(String name, int quantity) {
		this.name = name;
		this.quantity = quantity;
	}
	public int compareTo(Fruit other) {
		return quantity - other.quantity;
	} // compareTo 함수는 음수(작을 경우) / 0(같을 경우) / 양수(클 경우)로 리턴한다. 
}
// 재고 수량 순으로 정렬
Fruit [] fruits = new Fruit[4];
fruits[0] = new Fruit("Pineapple", 70);
fruits[1] = new Fruit("Apple", 100);
fruits[2] = new Fruit("Orange", 80);
fruits[3] = new Fruit("Banana", 90);

Arrays.sort(fruits);
```

- 이번에는 파인애플, 오렌지, 바나나, 사과 순으로 정렬된다.



# 두 가지 기준을 동시에 지원하려면?

- 하나의 객체 타입에 대해서 2가지 이상의 기준으로 정렬을 지원하려면 Comparator를 사용

```java
Comparator<Fruit> nameComparator = new Comparator<Fruit>() {
	public int compare(Fruit, fruit1, Fruit fruit2) {
		return fruit1.name.compareTo(fruit2.name);
	}
};
Comparator<Fruit> quantComparator = new Comparator<Fruit>() {
	public int compare(Fruit, fruit1, Fruit fruit2) {
		return fruit1.quantity - fruit2.quantity;
	}
};
Arrays.sort(fruits, nameComparator);
// or
Arrays.sort(fruits, quantComparator);
```

- Comparator 인터페이스를 이용, 필수적인 멤버 메소드인 compare 메소드를 이용해서 비교, compare 함수는 음수 / 0 / 양수를 반환
- 객체 배열과 Comparator를 같이 넘겨줌
- nameComparator은 Comparator interface를 implement 하는 어떤 class의 객체
- 위 코드는 잘못됨, 인터페이스를 가지고 새로운 객체를 만들어내는게 잘못됨, 하나의 클래스를 만들어서 그 클래스에 인터페이스를 적용해서 사용,  그 다음 그 클래스 객체 생성해서 사용

