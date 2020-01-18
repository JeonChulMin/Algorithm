# Queue 인터페이스

```java
public void offer(Element data);
//순차적으로 보관
public Element poll();
//가장 먼저 보관한 값을 꺼내고 반환
public Element peek();
//가장 먼저 보관한 값을 단순 참조
public boolean isEmpty();
//비어있는지 확인
```



## ※ 예제

```java
import java.util.Queue;
import java.util.LinkedList;
public class Program
{
	public static void main(String[] args)
	{
		Queue<String> q = new LinkedList<String>();
		q.offer("Kim");
		q.offer("Park");
		System.out.println(q.peek()); // 제일 먼저들어간 Kim을 참조
        q.poll(); // Kim을 꺼냄
        while(q.isEmpty() == false)
        {
            System.out.println(q.poll());
		}
	}
}
```

