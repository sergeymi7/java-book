# Map

**Map** в **Java** - это интерфейс, который представляет собой коллекцию пар "ключ-значение". Каждый элемент в **Map**
представлен объектом **Entry**, который содержит ключ и соответствующее ему значение. **Map** не допускает дубликатов
ключей, каждый ключ должен быть уникальным.

Основные методы, определенные в интерфейсе **Map**:

- `V put(K key, V value)` - добавляет пару ключ-значение в **Map**. Если ключ уже существует, то значение будет
  обновлено.
- `V get(Object key)` - возвращает значение, связанное с указанным ключом.
- `boolean containsKey(Object key)` - возвращает **true**, если **Map** содержит указанный ключ.
- `boolean containsValue(Object value)` - возвращает **true**, если **Map** содержит указанное значение.
- `V remove(Object key)` - удаляет пару ключ-значение из **Map** и возвращает значение, связанное с удаленным ключом.
- `int size()` - возвращает количество элементов в **Map**.
- `boolean isEmpty()` - возвращает **true**, если **Map** не содержит ни одной пары ключ-значение.
- `void clear()` - удаляет все пары ключ-значение из **Map**.
- `Set<K> keySet()` - возвращает множество всех ключей в **Map**.
- `Collection<V> values()` - возвращает коллекцию всех значений в **Map**.
- `Set<Map.Entry<K, V>> entrySet()` - возвращает множество всех записей (**Entry**) в **Map**.

Реализации интерфейса **Map** в **Java** включают **HashMap**, **TreeMap** и **LinkedHashMap**.

- **HashMap** - представляет собой хэш-таблицу, которая хранит пары ключ-значение. Он обеспечивает постоянное время
  выполнения для операций добавления, удаления и поиска элементов, но не гарантирует порядок итерации по элементам.
- **TreeMap** - представляет собой отсортированное дерево, которое хранит пары ключ-значение. Он гарантирует
  отсортированный порядок элементов на основе их ключей. Время выполнения операций зависит от высоты дерева и может быть
  O(log n).
- **LinkedHashMap** - подобен **HashMap**, но также поддерживает порядок вставки элементов. Он сохраняет порядок вставки
  элементов и предоставляет доступ к элементам в порядке их добавления.

## Map.Entry

**Map.Entry** - это внутренний интерфейс, представляющий запись (entry) в **Map**, содержащую ключ и соответствующее ему
значение. Интерфейс **Map.Entry** определяет два основных метода:

- `getKey()` - возвращает ключ записи.
- `getValue()` - возвращает значение записи.

Метод `entrySet()` возвращает множество объектов **Map.Entry**, представляющих все записи в **HashMap**. Это позволяет
получить доступ ко всем ключам и значениям в **HashMap** одновременно.

Пример использования entrySet() для итерации по записям в HashMap:

```java
HashMap<String, Integer> map=new HashMap<>();
    map.put("apple",3);
    map.put("banana",5);
    map.put("orange",2);

    Set<Map.Entry<String, Integer>>entries=map.entrySet();
    for(Map.Entry<String, Integer> entry:entries){
    String key=entry.getKey();
    Integer value=entry.getValue();
    System.out.println("Key: "+key+", Value: "+value);
    }
```

В приведенном примере мы получаем множество записей с помощью метода `entrySet()`, а затем выполняем итерацию по этому
множеству, получая ключ и значение каждой записи с помощью методов `getKey()` и `getValue()`.

----

## HashMap

**HashMap** в **Java** - это реализация интерфейса **Map**, которая представляет собой хэш-таблицу, основанную на
принципе "ключ-значение". **HashMap** позволяет хранить пары ключ-значение и обеспечивает быстрое время выполнения
операций добавления, удаления и поиска элементов.

Основные особенности и методы **HashMap**:

- **HashMap** использует хэш-функцию для вычисления индекса, по которому элемент будет храниться. Это позволяет получать
  доступ к элементам по ключу за постоянное время O(1) в среднем случае.
- **HashMap** не гарантирует порядок элементов при итерации. Это означает, что порядок элементов может быть произвольным
  и не зависит от порядка добавления.
- Метод `put(K key, V value)` позволяет добавить пару ключ-значение в HashMap. Если ключ уже существует, то значение
  будет обновлено. Если ключ отсутствует, то новая пара ключ-значение будет добавлена.
- Метод `get(Object key)` позволяет получить значение, связанное с указанным ключом. Если ключ отсутствует, то метод
  вернет значение null.
- Метод `remove(Object key)` позволяет удалить пару ключ-значение по указанному ключу и вернуть удаленное значение. Если
  ключ отсутствует, то метод вернет значение null.
- Метод `containsKey(Object key)` позволяет проверить наличие указанного ключа в **HashMap**.
- Метод `containsValue(Object value)` позволяет проверить наличие указанного значения в **HashMap**.
- Метод `size()` возвращает количество элементов в **HashMap**.
- Метод `isEmpty()` возвращает true, если HashMap не содержит ни одной пары ключ-значение.
- Метод `clear()` позволяет удалить все пары ключ-значение из **HashMap**.
- Метод `keySet()` возвращает множество всех ключей в **HashMap**.
- Метод `values()` возвращает коллекцию всех значений в **HashMap**.
- Метод `entrySet()` возвращает множество всех записей (Entry) в **HashMap**, которые представляют собой пары
  ключ-значение.

Пример использования **HashMap**:

```java
HashMap<String, Integer> map=new HashMap<>();
    map.put("Serega",1);
    map.put("Antoha",2);

    System.out.println(map.get("Serega")); // 1
    System.out.println(map.containsKey("Antoha")); // true
    System.out.println(map.size()); // 2

    map.remove("Antoha");
    System.out.println(map.size()); // 1
```

В приведенном примере мы создаем **HashMap**, добавляем в него пары ключ-значение, получаем значение по ключу, проверяем
наличие ключа и удаляем пару ключ-значение по ключу.

### Особенности реализации HashMap в Java:

1. Хэш-таблица: В основе реализации **HashMap** лежит хэш-таблица, которая использует хэш-функцию для вычисления
   индекса, по которому элемент будет храниться. Хэш-функция преобразует ключ в хэш-код, который затем используется для
   определения индекса в массиве.
2. Коллизии: В случае возникновения коллизий, когда различные ключи имеют одинаковый хэш-код и попадают в один и тот же
   индекс хэш-таблицы, **HashMap** использует метод цепочек (separate chaining) для разрешения коллизий. В каждом
   индексе хэш-таблицы может быть связанный список, который содержит элементы с одинаковыми хэш-кодами. При поиске
   элемента происходит последовательный перебор элементов в связанном списке.
3. Динамическое изменение размера: **HashMap** автоматически изменяет размер своей внутренней хэш-таблицы, чтобы
   обеспечить эффективное хранение элементов и уменьшить коллизии. Когда количество элементов в **HashMap** достигает
   определенного порога, размер хэш-таблицы увеличивается, чтобы снизить плотность элементов в каждом индексе.
4. Неупорядоченность: В отличие от некоторых других реализаций **Map**, например, **TreeMap**, **HashMap** не
   гарантирует порядок элементов при итерации. Порядок элементов может быть произвольным и не зависит от порядка
   добавления.
5. Null-ключи и Null-значения: HashMap позволяет использовать null-ключи и null-значения. Это означает, что null может
   быть ключом или значением в **HashMap**.
6. Итерация: При итерации по элементам **HashMap** с помощью итератора или цикла `for-each` порядок элементов может быть
   произвольным и не гарантирует исходный порядок добавления.
7. Потокобезопасность: По умолчанию **HashMap** не является потокобезопасным. Если необходимо использовать **HashMap** в
   многопоточной среде, следует принять меры для обеспечения синхронизации или использовать потокобезопасную реализацию,
   такую как ConcurrentHashMap.
8. Итераторы и модификация: Итератор **HashMap** поддерживает операцию удаления элемента с помощью
   метода `iterator.remove()`.

### Основные моменты внутренней реализации HashMap:

1. **Бакеты**: **HashMap** в **Java** использует массив для хранения данных. Элементы этого массива называются "
   бакетами" (buckets). Каждый **бакет** может содержать одну или несколько пар ключ-значение.
2. **Хеширование**: Для определения **бакета**, в котором будет храниться пара ключ-значение, **HashMap** использует
   хеш-функцию от ключа. Хеш-функция возвращает индекс **бакета**.
3. **Связанные списки и деревья**: Если в одном **бакете** находится несколько пар ключ-значение (это происходит, когда
   хеш-функция возвращает один и тот же индекс для разных ключей, что называется коллизией), они хранятся в виде
   связного списка. С Java 8, если количество элементов в бакете превышает определенный порог (TREEIFY_THRESHOLD,
   который равен 8), связный список преобразуется в балансированное дерево, что улучшает производительность поиска.
4. **Изменение размера**: Когда количество **бакетов** в **HashMap** становится недостаточным (то есть, когда количество
   элементов превышает порог загрузки, определяемый коэффициентом загрузки load factor), происходит операция изменения
   размера (resize). В ходе этой операции создается новый массив с удвоенным размером, и все элементы из старого массива
   переходят в новый.

----

## TreeMap

**TreeMap** в **Java** - это реализация интерфейса **SortedMap**, которая представляет собой отсортированное дерево,
основанное на структуре красно-черного дерева. **TreeMap** хранит пары "ключ-значение", где элементы автоматически
сортируются по ключу в естественном порядке или с использованием заданного компаратора.

Основные особенности и методы **TreeMap**:

- Сортировка: **TreeMap** автоматически сортирует элементы по ключу. При вставке нового элемента или при изменении ключа
  существующего элемента, TreeMap перестраивает структуру дерева для поддержания отсортированности.

- **Ключи**: Ключи в **TreeMap** должны быть сравнимыми или должны быть заданы в компараторе. Если ключи реализуют
  интерфейс **Comparable**, то **TreeMap** будет использовать их естественный порядок. Если необходимо использовать
  пользовательский порядок, можно передать компаратор при создании **TreeMap**.
- **Доступ к элементам**: **TreeMap** предоставляет методы для доступа к элементам по ключу. Некоторые из них
  включают `put(K key, V value)` для добавления пары ключ-значение, `get(Object key)` для получения значения по
  ключу, `remove(Object key)` для удаления элемента по ключу.
- **Итерация**: **TreeMap** поддерживает итерацию по элементам в отсортированном порядке. Методы `keySet()`, `values()`
  и `entrySet()` возвращают представления ключей, значений и пар "ключ-значение" соответственно.
- **Навигация**: **TreeMap** предоставляет методы для навигации по элементам. Например, `firstKey()` возвращает
  наименьший ключ, `lastKey()` возвращает наибольший ключ, `lowerKey(K key)` возвращает наибольший ключ, меньший
  заданного ключа, и так далее.
- **Допустимость null-ключей**: В **TreeMap** не допускаются null-ключи. Попытка вставить null-ключ вызовет
  исключение **NullPointerException**.
- **Время выполнения операций**: Большинство операций в **TreeMap** выполняются за время O(log n), где n - количество
  элементов в дереве. Однако в худшем случае некоторые операции могут потребовать время O(n).

Пример использования **TreeMap**:

```java
TreeMap<String, Integer> treeMap=new TreeMap<>();
    treeMap.put("Serega",1);
    treeMap.put("Antoha",2);

    System.out.println(treeMap.get("Serega")); // 1
    System.out.println(treeMap.containsKey("Antoha")); // true
    System.out.println(treeMap.size()); // 2

    treeMap.remove("Antoha");
    System.out.println(treeMap.size()); // 1
```

----

## LinkedHashMap

**LinkedHashMap** в **Java** - это реализация интерфейса **Map**, которая расширяет класс **HashMap**. Он представляет
собой хэш-таблицу, которая дополнительно поддерживает связанный список элементов, который сохраняет порядок вставки
элементов. То есть, порядок элементов в **LinkedHashMap** соответствует порядку их добавления.

Основные особенности и методы **LinkedHashMap**:

- **Сохранение порядка вставки**: **LinkedHashMap** поддерживает порядок элементов в соответствии с порядком их
  добавления. Это означает, что при итерации по элементам **LinkedHashMap** они будут возвращаться в порядке, в котором
  они были вставлены.
- **Хэш-таблица и связанный список**: **LinkedHashMap** использует хэш-таблицу для быстрого доступа к элементам по ключу
  и связанный список для хранения элементов в порядке вставки. Каждый элемент в хэш-таблице также содержит ссылки на
  предыдущий и следующий элементы в связанном списке.
- **Доступ к элементам**: **LinkedHashMap** предоставляет методы для доступа к элементам по ключу, аналогично HashMap.
  Некоторые из них включают `put(K key, V value)` для добавления пары ключ-значение, `get(Object key)` для получения
  значения по ключу, `remove(Object key)` для удаления элемента по ключу.
- **Итерация**: LinkedHashMap поддерживает итерацию по элементам в порядке их добавления. Методы `keySet()`, `values()`
  и `entrySet()` возвращают представления ключей, значений и пар "ключ-значение" соответственно в порядке их добавления.
- **Допустимость null-ключей и null-значений**: **LinkedHashMap** допускает как null-ключи, так и null-значения.
- **Время выполнения операций**: Время выполнения операций в **LinkedHashMap** аналогично времени выполнения операций в
  HashMap.

Пример использования **LinkedHashMap**:

```java
LinkedHashMap<String, Integer> linkedHashMap = new LinkedHashMap<>(); 
linkedHashMap.put("Serega", 1);
linkedHashMap.put("Antoha", 2);

System.out.println(linkedHashMap.get("Serega")); // 1 
System.out.println(linkedHashMap.containsKey("Antoha")); // true
System.out.println(linkedHashMap.size()); // 2

linkedHashMap.remove("Antoha"); 
System.out.println(linkedHashMap.size()); // 1
```