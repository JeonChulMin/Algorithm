# Hash 개요

자바에서 배열은 내부 인덱스를 이용하여 자료의 검색이 한번에 이루어지기 때문에 빠른 검색 속도를 보이지만 데이터의 삽입, 삭제시 많은 데이터가 밀리거나 빈자리를 채우기 위해 해당 인덱스로 이동해야 하기 때문에 많은 시간이 소요된다.

반면 연결 리스트는 삽입, 삭제시 인근 노드들의 참조값만 수정해 줌으로써 빠른 처리가 가능하다. 단 처음 노드와 마지막 노드 이외의 위치에서 데이터를 삽입, 삭제할 경우나 데이터를 검색할 경우에는 해당 노드를 찾기 위하여 처음부터 순회검색을 해야하기 때문에 데이터의 수가 많아질수록 효율이 떨어질 수 밖에 없는 구조이다.

이러한 한계를 극복하기 위해서 제시된 방법이 Hash이다.



# Hash 개념

Hash는 내부적으로 배열을 사용하여 데이터를 저장하기 때문에 빠른 검색 속도를 가진다. 그리고 데이터의 삽입과 삭제시 기존 데이터를 밀어내거나 채우는 작업이 필요없도록 특별한 알고리즘을 이용하여 데이터와 연관된 고유한 숫자를 만들어낸 뒤 이를 인덱스로 사용한다. 

특정 데이터가 저장되는 인덱스를 그 데이터만의 고유한 위치이기 때문에 삽입시 다른 데이터의 사이에 끼어들거나 삭제시 다른 데이터로 채울 필요가 없으므로 삽입과 삭제시 데이터의 이동이 없도록 만들어진 구조이다.

Hash가 내부적으로 사용하는 배열을 Hash Table이라고 하며 그 크기에 따라 성능 차이가 많이 날 수 있다.



# Hash method

Hash는 Hash Table을 이용하여 데이터를 저장한다. 이때 특별한 알고리즘을 이용하여 데이터의 고유한 숫자값을 만들어 인덱스로 사용하는데 이 알고리즘을 구현한 메소드를 Hash method라고 하며 Hash method에 의해 반환된 데이터 고유의 숫자 값을 Hash Code라고 한다.

자바에서는 Object 클래스의 hashCode()라는 메소드를 이용하여 모든 객체의 Hash Code를 구할 수 있다.

Hash Method를 구현하는 방법은 여러 가지가 있지만 가장 간단한 방법으로는 나머지 연산자를 이용하는 것이다.

데이터의 고유한 hashCode를 구한 뒤 hashCode를 테이블의 크기로 나머지 연산을 한 결과를 해당 데이터의 인덱스로 사용하는 것이다.

예를 들어 "a", "b", "c"의 hashCode가 각각 97, 98, 99 라고 하고 Hash Table의 크기가 10이라고 했을 때 테이블에 저장될 인덱스는 다음과 같다.

97 % 10 = 7

98 % 10 = 8

99 % 10 = 9

정리하면 Table의 7번 인덱스에는 "a"를 저장, 8번 인덱스에는 "b"를 저장, 9번 인덱스에는 "c"를 저장하는 방식이다.

이후 검색 시 hashCode를 가지고 나머지 연산한 결과를 가지고 인덱스를 참조하여 데이터를 꺼낸다.



하지만 hashCode가 다르더라도 나머지 연산을 한 결과가 같을 수 있으므로 Hash Table에 동일한 인덱스에 저장을 하게되므로 충돌이 발생한다. 이런 충돌을 최소화하기 위한 방법으로는 나머지 연산의 값이 최대한 중복되지 않도록 테이블의 크기를 소수(prime number)로 만드는 것이다. 하지만 테이블의 크기를 소수로 만드는 것은 충돌을 줄이는 방법일 뿐 해결하기 위한 방법은 아니다. 충돌 해결 방법으로 **개방주소법**과 **분리연결법** 2가지가 있다.

개방주소법은 배열만을 사용하며 저장 인덱스가 겹칠 경우 해당 인덱스의 옆 인덱스에 저장하는 방식이다. 이때 또 옆 인덱스와의 충돌이 일어나면 또 다시 옆 인덱스로 저장되기 때문에 충돌이 많이 일어날 경우 심각한 성능 저하가 발생할 수 있기 때문에 분리연결법에 대해서만 알아본다.

분리연결법은 Hash Table에 연결 리스트에서 사용하는 Node 객체를 저장하는 것이다. 즉, Hash Table의 셀마다 연결 리스트를 하나씩 저장하도록 하고 충돌이 발생하는 데이터는 연결 리스트의 다음 노드로 계속 추가해 가는 것이다. 검색시에는 Hash Table의 인덱스를 찾은 후 연결된 리스트를 순차적으로 탐색하며 찾으려는 hashCode와 저장된 노드의 hashCode를 비교해서 찾는다.





# HashMap

- 저장은 느리지만 많은 양의 데이터를 검색하는데 뛰어난 성능을 보인다.
- TreeMap은 HashMap 비해 저장이 빠르지만 데이터를 가져올 때 약간 느리다.

Map 인터페이스는 Key, Value를 하나의 세트로 묶어서 저장하는 컬렉션 클래스를 구현하는데 사용한다. 여기서 key는 중복될 수 없고 value는 중복될 수 있다. 중복된 키와 값을 저장하면 기존 값이 없어지고 새로 저장된 값이 저장된다.



### method

| method                                       | 설명                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| HashMap()                                    | HashMap 객체 생성 ex) HashMap <String, Integer> hm = new HashMap <String, Integer>(); |
| HashMap(int initCapacity)                    | 지정된 값을 초기 용량으로 하는 HashMap 객체 생성             |
| HashMap(int initCapacity, float loadFactory) | 지정된 값을 초기 용량과 load factory의 HashMap 객체 생성     |
| HashMap(Map m)                               | 주어진 Map에 저장된 모든 요소를 저장한 HashMap 객체 생성     |
| Object clone()                               | 현재 HashMap을 복제하여 반환 ex) newMap = (HashMap)map.clone(); |
| void clear()                                 | Map의 모든 객체를 삭제                                       |
| boolean containsKey(Object key)              | 지정된 key 객체와 일치하는 Map의 key 객체가 있는 지 확인     |
| boolean containsValue(Object value)          | 지정된 value 객체와 일치하는 Map의 value 객체가 있는 지 확인 |
| Set entrySet()                               | Map에 저장되어 있는 key-value 쌍을 Map.Entry 타입의 객체로 저장한 "Set"으로 반환 |
| boolean equals(Object o)                     | 동일한 Map인지 비교                                          |
| Object get(Object key)                       | 지정한 key 객체에 대응하는 value 객체를 찾아서 반환          |
| int hashCode()                               | hash code 반환                                               |
| boolean isEmpty()                            | Map이 비어있는지 확인                                        |
| Set keySet()                                 | Map에 저장된 모든 key 객체를 반환한다.                       |
| Object put(Object key, Object Value)         | Map에 value 객체를 key 객체에 연결하여 저장                  |
| void putAll(Map t)                           | 지정된 Map의 모든 key-value 쌍을 추가                        |
| Object remove(Object key)                    | 지정한 key 객체와 일치하는 key-value 객체를 삭제             |
| int size()                                   | Map에 저장된 key-value 쌍의 개수를 반환                      |
| Collection values()                          | Map에 저장된 모든 value 객체를 반환                          |



### Map.Entry 인터페이스

Map 인터페이스의 내부 인터페이스로 Map에 저장되는 key와 value를 다루기 위한 인터페이스

따라서 Map 인터페이스를 구현하는 클래스는 Map.Entry 인터페이스도 함께 구현해야 한다.



### method

| method                        | 설명                                    |
| ----------------------------- | --------------------------------------- |
| boolean equals(Object o)      | 동일한 Entry인지 비교                   |
| Object getKey()               | Entry의 key 객체를 반환                 |
| Object getValue()             | Entry의 value 객체를 반환               |
| int hashCode()                | Entry의 해시코드를 반환                 |
| Object setValue(Object value) | Entry의 value 객체를 지정된 객체로 바꿈 |



Hashmap은 Map을 구현했으므로 key와 value를 묶어서 하나의 데이터(entry)로 저장한다.



### http://tech.javacafe.io/2018/12/03/HashMap/ 내용 추가하기



### 추가 정보

멀티쓰레드에서 동시에 HashMap을 건드려 key-value 값을 사용하면 문제가 될 수 있기 때문에 멀티쓰레드에서는 HashTable을 쓴다.



#### 참고 사이트

https://whatisthenext.tistory.com/81

https://hyeonstorage.tistory.com/265

https://vaert.tistory.com/107