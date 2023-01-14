# Reflection

### Что такое Рефлексия?

**Рефлексия** — это **API**, который позволяет:
* получать информацию о переменных, методах внутри класса, о самом классе, его конструкторах, реализованных 
интерфейсах и т.д.;
* получать новый экземпляр класса;
* получать доступ ко всем переменным и методам, в том числе приватным;
* преобразовывать классы одного типа в другой (**cast**);
* делать все это во время исполнения программы.

### Недостатки Рефлексии

* Производительность хуже в сравнении с классической работой с классами, методами и переменными;
* Ограничения безопасности. Если мы захотим использовать рефлексию на классе, который защищен с помощью специального 
  класса **SecurityManager**, то ничего не выйдет т.к. этот класс будет выбрасывать исключения каждый раз, как мы 
  попытаемся получить доступ к закрытым членам класса. Такая защита может применяться, например, в Апплетах 
  (**Applets**);
* Получение доступа к внутренним членам класса, что нарушает принцип **инкапсуляции**.

## Класс Class

Класс `Class` является входной точкой в мир рефлексии

`Class` есть у всех объектов в **Java**:
* классов, интерфейсов, перечислений;
* примитивов и обёрток над ними;
* массивов;
* `void` также имеет `Class`.

Для примера будем использовать класс `Cat` из пакета `cattery`

```java
package cattery;

class Cat {

    private String name;
    public String color;

    public Cat() {
        this.name = "";
    }

    public Cat(String name, String color) {
        this.name = name;
        this.color = color;
    }

    private sayMeow() {
        System.out.println("Meooow!");
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

### Получение класса

1. `Class<?> catClass = Сlass.forName(“cattery.Cat”);`
   - вызов метода `forName()` необходимо обернуть в блок `try-catch` т.к. метод может бросить 
   `ClassNotFoundException`, в случае если он не найдет класс с таким именем.
2. `Cat cat = new Cat(); 
   Class<? extends Cat> catClass = cat.getClass();`
    - В этом случае оборачивать метод `getClass()` в блок `try-catch` нет необходимости т.к. мы вызываем этот метод у 
      существующего класса, который видит компилятор. Компилятор не может точно знать тип переменной, поэтому мы и 
      имеем `? extends Cat`, как дженерик тип.
3. `Class<Cat> catClass =
   Cat.class;`
   - соответственно в этом примере тоже не требуется блок `try-catch`

Чем больше мы знаем о классе, тем точнее будет тип этого класса при получении `Класса` класса.

### Получение информации о полях класса

`getDeclaredFields()` - метод возвращает все объявленные переменные в классе.
Пример:
```java
Class<Cat> catClass = Cat.class;
Field[] declaredFields = catClass.getDeclaredFields();
```
____
`getDeclaredField()` - Метод возвращает переменную по её имени. Если переменной с таким именем нет, то метод 
выбросит **checked** `NoSuchFieldException`. Пример:
```java
Class<Cat> catClass = Cat.class;
Field catNameField = catClass.getDeclaredField("name");
```
----
`getFields()` - в отличие от `getDeclaredFields()` возвращает только **public** поля. Пример:
```java
Class<Cat> catClass = Cat.class;
Field[] fields = catClass.getFields();
```
----
`getField()` - возвращает только **public** переменные. Даже если поле с таким именем есть, но оно не публичное, 
метод `getField()` бросит `NoSuchFieldException`. Пример:
```java
Class<? extends Cat> catClass = new Cat().getClass();
Field catColorField = catClass.getField("color");
```

### Получение информации о методах класса

`getDeclaredMethods()` - возвращает все объявленные методы в классе. Пример:
```java
Class<Cat> catClass = Cat.class;
Method[] declaredMethods = catClass.getDeclaredMethods();
```
----
`getDeclaredMethod()` - принимает имя и **var-args** с типами параметров метода. Если такого метода в классе нет, мы 
получим **checked** `NoSuchMethodException`. Пример:
```java
Class<Cat> catClass = Cat.class;
Method sayMeowMethods = catClass.getDeclaredMethod("sayMeow");
Method setCatNameMethods = catClass.getDeclaredMethod("setName", String.class);
```
----
`getMethods()` - возвращает все **public** методы класса и **public** методы его родительского класса/интерфейсов. 
Пример:
```java
Class<Cat> catClass = Cat.class;
Method[] methods = catClass.Methods();
```
----
`getMethod()` - возвращает все **public** методы класса и **public** методы его родительского класса/интерфейсов. 
Пример:
```java
Class<Cat> catClass = Cat.class;
Method notifyAllMethod = catClass.Method("notifyAll");
```
----
`getEnclosingMethod()` - если класс является локальным или анонимным, метод `getEnclosingMethod()` возвращает тот 
метод в котором этот класс был создан, иначе метод возвращает **null**. Пример:
```java
Class<Cat> catClass = Cat.class;
Method enclosingMethod = catClass.getEnclosingMethod();
```

## Класс Field

Класс `Field` предоставляет возможность:
* получить значение поля, его тип, имя, а также модификаторы поля
* получить список аннотаций, класс, в котором объявлено поле и другую информацию
* установить новое значение в поле, даже если оно объявлено как **private**

### Получение значения переменной

Для того, чтобы получить значение из класса `Field` существуют методы **getByte(), getShort(), getInt(), getLong(), 
getFloat(), getDouble(), getChar(), getBoolean()** и **get()**. 

#### Пример получения **public** переменной:
```java
Class<? extends Cat> catClass = new Cat().getClass();
Field catColorField = catClass.getField("color");
String catColor = (String) catColorField.get();
```

#### Пример получения **private** переменной:
```java
Class<? extends Cat> catClass = new Cat().getClass();
Field catNameField = catClass.getField("name");
catNameField.setAccessible(true);
String catName = (String) catNameField.get();
```
Нельзя просто так взять и получить значение приватной переменной. Для этого, перед вызовом метода `get()`, 
необходимо вызвать метод `setAccessible(true)`.

### Получение имени, типа и модификаторов переменной
####Пример получения имени и типа переменной getName(), getType():
```java
Class<? extends Cat> catClass = new Cat().getClass();
Field catColorField = catClass.getField("color");
String catColorFieldName = catColorField.getName(); //color
Class<?> catColorFieldType = catColorField.getType(); //String
```
####Пример получения модификаторов переменной getModifiers():
```java
Class<? extends Cat> catClass = new Cat().getClass();
Field catColorField = catClass.getField("color");
int modifiers = catColorField.getModifiers(); // 1
Modifier.isPrivate(modifiers); // false
Modifier.isFinal(modifiers);  // false
```
### Получение аннотаций переменной
Для получения аннотаций переменной существуют методы : **getAnnotations()** и **getDeclaredAnnotations()**, 
**getAnnotationsByType()** и **getDeclaredAnnotationsByType()**, **getAnnotation()** и **getDeclaredAnnotation()**.
Но, пары методов **getAnnotations() и getDeclaredAnnotations(), getAnnotationsByType() и getDeclaredAnnotationsByType
(), getAnnotation()** и **getDeclaredAnnotation()** делают одно и то же. 

* **getAnnotations()** возвращает массив аннотаций метода
* **getAnnotation()** возвращает аннотацию по типу
* **getAnnotationsByType()** возвращает массив аннотаций по типу. 

### Изменение переменных
Для изменения переменных используются следующие методы:
**setByte(), setShort(), setInt(), setLong(), setFloat(), setDouble(), setChar(), setBoolean()** и **set()**.

#### Изменение public переменной
```java
Cat cat = new Cat();
Class<? extends Cat> catClass = cat.getClass();
Field catColorField = catClass.getField("color");
catColorField.set(cat, "black");
```

#### Изменение private и/или final переменной
```java
Cat cat = new Cat();
Class<? extends Cat> catClass = cat.getClass();
Field catColorField = catClass.getField("color");
catColorField.setAccessible(true);
catColorField.set(cat, "black");
```