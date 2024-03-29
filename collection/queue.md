# Queue

**Queue** в **Java** - это интерфейс, который представляет собой коллекцию элементов с принципом "первым вошел, первым вышел" (First-In-First-Out, FIFO). Queue предоставляет методы для добавления, удаления и доступа к элементам в определенном порядке.

Основные методы, определенные в интерфейсе **Queue**:
- `boolean add(E e)` - добавляет элемент в очередь. Если очередь заполнена и не может принять больше элементов, то 
генерируется исключение.
- `boolean offer(E e)` - добавляет элемент в очередь. Возвращает **true**, если элемент успешно добавлен, и **false**, если очередь заполнена.
- `E remove()` - удаляет и возвращает элемент из головы очереди. Если очередь пуста, генерируется исключение.
- `E poll()` - удаляет и возвращает элемент из головы очереди. Если очередь пуста, возвращает **null**.
- `E element()` - возвращает элемент из головы очереди, не удаляя его. Если очередь пуста, генерируется исключение.
- `E peek()` - возвращает элемент из головы очереди, не удаляя его. Если очередь пуста, возвращает **null**.

Реализации интерфейса **Queue** в **Java** включают **LinkedList** и **PriorityQueue**.

## LinkedList

**LinkedList** - это двусвязный список, который может использоваться как очередь. Он обеспечивает быстрое добавление и удаление элементов с начала и конца списка.

Пример использования **LinkedList** в качестве очереди:

```java
Queue<String> queue = new LinkedList<>();
queue.add("Serega");
queue.add("Antoha");

System.out.println(queue.peek()); // Serega
System.out.println(queue.size()); // 2

queue.poll();
System.out.println(queue.size()); // 1
```

## PriorityQueue

**PriorityQueue** - это реализация очереди с приоритетом, где элементы добавляются в очередь с учетом их приоритета. Элементы извлекаются в порядке приоритета. Приоритет определяется с использованием сравнения элементов или с помощью компаратора.

Пример использования **PriorityQueue**:
```java
Queue<Integer> queue = new PriorityQueue<>();
queue.add(3);
queue.add(1);
queue.add(2);

System.out.println(queue.peek()); // 1
System.out.println(queue.size()); // 3

queue.poll();
System.out.println(queue.size()); // 2
```

В обоих примерах мы создаем очередь, добавляем элементы, получаем элемент из головы очереди (с помощью `peek()`), и удаляем элемент из головы очереди (с помощью `poll()`).