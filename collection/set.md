# Set

**Set** в **Java** - это интерфейс, который расширяет **Collection** и представляет собой неупорядоченную коллекцию
уникальных элементов. В отличие от **List**, **Set** не допускает дубликатов элементов, поэтому каждый элемент в **Set**
должен быть уникальным.

Основные методы, определенные в интерфейсе **Set**:

- `boolean add(E e)` - добавляет элемент в **Set**. Возвращает **true**, если элемент был успешно добавлен, и
  **false**, если элемент уже присутствует в **Set**.
- `boolean addAll(Collection<? extends E> c)` - добавляет все элементы из заданной коллекции в **Set**. Возвращает 
  **true**, если **Set** был изменен после вызова метода.
- `void clear()` - удаляет все элементы из **Set**.
- `boolean contains(Object o)` - возвращает **true**, если **Set** содержит указанный элемент.
- `boolean containsAll(Collection<?> c)` - возвращает **true**, если **Set** содержит все элементы указанной коллекции.
- `boolean equals(Object o)` - возвращает **true**, если указанный объект равен текущему **Set**.
- `int hashCode()` - возвращает хэш-код **Set**.
- `boolean isEmpty()` - возвращает **true**, если **Set** пуст.
- `Iterator<E> iterator()` - возвращает итератор по элементам **Set**.
- `boolean remove(Object o)` - удаляет указанный элемент из **Set**. Возвращает **true**, если элемент был успешно
  удален.
- `boolean removeAll(Collection<?> c)` - удаляет из **Set** все элементы, содержащиеся в указанной коллекции.
  Возвращает **true**, если **Set** был изменен после вызова метода.
- `boolean retainAll(Collection<?> c)` - удаляет из **Set** все элементы, которые не содержатся в указанной коллекции.
  Возвращает **true**, если **Set** был изменен после вызова метода.
- `int size()` - возвращает количество элементов в **Set**.
- `Object[] toArray()` - возвращает массив, содержащий все элементы **Set**.
- `<T> T[] toArray(T[] a)` - возвращает массив, содержащий все элементы **Set**, и приводит его к типу **T**.

Реализации интерфейса **Set** включают **HashSet**, **TreeSet** и **LinkedHashSet**. Каждая из них предоставляет
различные способы хранения и организации элементов в **Set**.

----

## HashSet

**HashSet** в **Java** - это реализация интерфейса **Set**, которая использует хэш-таблицу для хранения элементов и
обеспечивает постоянное время выполнения операций добавления, удаления и поиска элементов (O(1)). **HashSet** не
гарантирует порядок элементов при итерации и не позволяет хранить дубликаты элементов.

Основные особенности и методы **HashSet**:

- **HashSet** основан на хэш-таблице, которая использует хэш-функцию для вычисления индекса, по которому элемент будет
  храниться.
- **HashSet** позволяет добавлять элементы с помощью метода `add(E e)`. Если элемент уже существует в **HashSet**, то
  добавление будет проигнорировано.
- Метод `remove(Object o)` удаляет указанный элемент из **HashSet**.
- Метод `contains(Object o)` позволяет проверить наличие элемента в **HashSet**.
- Метод `size()` возвращает количество элементов в **HashSet**.
- Метод `isEmpty()` возвращает **true**, если **HashSet** не содержит ни одного элемента.
- Метод `clear()` удаляет все элементы из **HashSet**.
- **HashSet** также предоставляет методы для выполнения операций объединения, пересечения и разности множеств, такие
  как `addAll()`, `retainAll()` и `removeAll()`.
- Итерация по элементам **HashSet** может быть выполнена с помощью итератора или цикла **for-each**.

Пример использования **HashSet**:

```java
import java.util.HashSet;

public class Main {

    public static void main(String[] args) {

        HashSet<String> set = new HashSet<>();
        set.add("Serega");
        set.add("Antoha");

        System.out.println(set.contains("Serega")); // true
        System.out.println(set.size()); // 2

        set.remove("Antoha");
        System.out.println(set.size()); // 1

        set.clear();
        System.out.println(set.isEmpty()); // true
    }
}
```

В приведенном примере мы создаем **HashSet**, добавляем в него элементы, проверяем наличие элемента, удаляем элемент и
очищаем **HashSet**.

----

## TreeSet

**TreeSet** в **Java** - это реализация интерфейса **Set**, которая хранит элементы в отсортированном порядке. Каждый
элемент в **TreeSet** автоматически располагается в соответствии с их значением. **TreeSet** использует структуру
красно-черного дерева для хранения элементов, что обеспечивает эффективный поиск, вставку и удаление элементов (O(log
n)).

Основные особенности и методы **TreeSet**:
**TreeSet** хранит уникальные элементы и автоматически сортирует их в естественном порядке или с использованием
заданного компаратора при создании TreeSet.

- Метод `add(E e)` позволяет добавлять элементы в **TreeSet**. При добавлении **TreeSet** автоматически сортируется и
  перестраивается, чтобы элементы оставались в отсортированном порядке.
- Метод `remove(Object o)` удаляет указанный элемент из **TreeSet**.
- Метод `contains(Object o)` позволяет проверить наличие элемента в **TreeSet**.
- Метод `size()` возвращает количество элементов в **TreeSet**.
- Метод `isEmpty()` возвращает true, если **TreeSet** не содержит ни одного элемента.
- Метод `clear()` удаляет все элементы из **TreeSet**.
- **TreeSet** также предоставляет методы для получения первого и последнего элемента в отсортированном порядке, такие
  как `first()` и `last()`.
- Итерация по элементам **TreeSet** может быть выполнена с помощью итератора или цикла **for-each**.

Пример использования **TreeSet**:

```java
import java.util.TreeSet;

public class Main {

    public static void main(String[] args) {

        TreeSet<String> set = new TreeSet<>();
        set.add("Serega");
        set.add("Antoha");

        System.out.println(set.contains("Serega")); // true
        System.out.println(set.size()); // 2

        set.remove("Antoha");
        System.out.println(set.size()); // 1

        set.clear();
        System.out.println(set.isEmpty()); // true
    }
}
```

В приведенном примере мы создаем **TreeSet**, добавляем в него элементы, проверяем наличие элемента, удаляем элемент и
очищаем **TreeSet**. Элементы **TreeSet** автоматически сортируются в естественном порядке (алфавитном порядке для
строк).

----

## LinkedHashSet

**LinkedHashSet** в **Java** - это реализация интерфейса **Set**, которая объединяет особенности **HashSet** и 
**LinkedHashSet**. Он сохраняет порядок добавления элементов, что позволяет обеспечить итерацию в порядке добавления. 
Как и **HashSet**, **LinkedHashSet** обеспечивает постоянное время выполнения операций добавления, удаления и поиска
элементов (O(1)).

Основные особенности и методы **LinkedHashSet**:

- **LinkedHashSet** хранит уникальные элементы и сохраняет порядок добавления элементов. При итерации по элементам
  **LinkedHashSet** элементы будут возвращаться в том порядке, в котором они были добавлены.
- Метод `add(E e)` позволяет добавлять элементы в **LinkedHashSet**. Если элемент уже существует в **LinkedHashSet**, то
  добавление будет проигнорировано.
- Метод `remove(Object o)` удаляет указанный элемент из **LinkedHashSet**.
- Метод `contains(Object o)` позволяет проверить наличие элемента в **LinkedHashSet**.
- Метод `size()` возвращает количество элементов в **LinkedHashSet**.
- Метод `isEmpty()` возвращает **true**, если **LinkedHashSet** не содержит ни одного элемента.
- Метод `clear()` удаляет все элементы из **LinkedHashSet**.
- **LinkedHashSet** также предоставляет методы для выполнения операций объединения, пересечения и разности множеств,
  такие как `addAll()`, `retainAll()` и `removeAll()`.
- Итерация по элементам **LinkedHashSet** может быть выполнена с помощью итератора или цикла **for-each**.

Пример использования **LinkedHashSet**:

```java
import java.util.LinkedHashSet;

public class Main {

    public static void main(String[] args) {

        LinkedHashSet<String> set = new LinkedHashSet<>();
        set.add("Serega");
        set.add("Antoha");

        System.out.println(set.contains("Serega")); // true
        System.out.println(set.size()); // 2

        set.remove("Antoha");
        System.out.println(set.size()); // 1

        set.clear();
        System.out.println(set.isEmpty()); // true
    }
}
```

В приведенном примере мы создаем **LinkedHashSet**, добавляем в него элементы, проверяем наличие элемента, удаляем
элемент и очищаем **LinkedHashSet**. Порядок элементов будет сохраняться в соответствии с порядком их добавления.