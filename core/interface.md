# Интерфейсы

Механизм наследования очень удобен, но он имеет свои ограничения. В частности мы можем наследовать только от одного
класса, в отличии, например, от языка С++, где имеется множественное наследование. В языке **Java** подобную проблему
частично позволяют решить интерфейсы. Интерфейсы определяют некоторый функционал, не имеющий конкретной реализации,
который затем реализуют классы, применяющие эти интерфейсы. И один класс может применить множество интерфейсов. Чтобы
определить интерфейс, используется ключевое слово **interface**. Например:

```java
interface Printable {

    void print();
}
```

Данный интерфейс называется **Printable**. Интерфейс может определять константы и методы, которые могут иметь, а могут и
не иметь реализации. Методы без реализации похожи на абстрактные методы абстрактных классов. Так, в данном случае
объявлен один метод, который не имеет реализации. Все методы интерфейса не имеют модификаторов доступа, но фактически по
умолчанию доступ **public**, так как цель интерфейса - определение функционала для реализации его классом. Поэтому весь
функционал должен быть открыт для реализации. Чтобы класс применил интерфейс, надо использовать ключевое слово
**implements**:

```java
public class Program {

    public static void main(String[] args) {

        Book b1 = new Book("Java. Complete Referense.", "H. Shildt");
        b1.print();
    }
}

interface Printable {

    void print();
}

class Book implements Printable {

    String name;
    String author;

    Book(String name, String author) {
        this.name = name;
        this.author = author;
    }

    public void print() {
        System.out.printf("%s (%s) \n", name, author);
    }
}
```

В данном случае класс **Book** реализует интерфейс **Printable**. При этом надо учитывать, что если класс применяет
интерфейс, то он должен реализовать все методы интерфейса, как в случае выше реализован метод **print**. Потом в
методе **main**
мы можем создать объект класса **Book** и вызвать его метод **print**. Если класс не реализует какие-то методы
интерфейса, то такой класс должен быть определен как абстрактный, а его неабстрактные классы-наследники затем должны
будут реализовать эти методы. В то же время мы не можем напрямую создавать объекты интерфейсов, поэтому следующий код не
будет работать:

```java
Printable pr=new Printable();
    pr.print();
```

Одним из преимуществ использования интерфейсов является то, что они позволяют добавить в приложение гибкости. Например,
в дополнение к классу **Book** определим еще один класс, который будет реализовывать интерфейс **Printable**:

```java
class Journal implements Printable {

    private String name;

    String getName() {
        return name;
    }

    Journal(String name) {
        this.name = name;
    }

    public void print() {
        System.out.println(name);
    }
}
```

Класс **Book** и класс **Journal** связаны тем, что они реализуют интерфейс **Printable**. Поэтому мы динамически в
программе можем создавать объекты **Printable** как экземпляры обоих классов:

```java
public class Program {

    public static void main(String[] args) {
        Printable printable = new Book("Java. Complete Reference", "H. Shildt");
        printable.print();      //  Java. Complete Reference (H. Shildt)
        printable = new Journal("Foreign Policy");
        printable.print();      // Foreign Policy
    }
}

interface Printable {

    void print();
}

class Book implements Printable {

    String name;
    String author;

    Book(String name, String author) {
        this.name = name;
        this.author = author;
    }

    public void print() {
        System.out.printf("%s (%s) \n", name, author);
    }
}

class Journal implements Printable {

    private String name;

    String getName() {
        return name;
    }

    Journal(String name) {
        this.name = name;
    }

    public void print() {
        System.out.println(name);
    }
}
```

### Интерфейсы в преобразованиях типов

Все сказанное в отношении преобразования типов характерно и для интерфейсов. Например, так как класс **Journal**
реализует интерфейс **Printable**, то переменная типа **Printable** может хранить ссылку на объект типа **Journal**:

```java
    Printable p=new Journal("Foreign Affairs");
    p.print();
    // Интерфейс не имеет метода getName, необходимо явное приведение
    String name=((Journal)p).getName();
    System.out.println(name);
```

И если мы хотим обратиться к методам класса **Journal**, которые определены не в интерфейсе **Printable**, а в самом
классе **Journal**, то нам надо явным образом выполнить преобразование типов:

```java
((Journal)p).getName();
```

### Методы по умолчанию

Ранее до **JDK 8** при реализации интерфейса мы должны были обязательно реализовать все его методы в классе. А сам
интерфейс мог содержать только определения методов без конкретной реализации. В **JDK 8** была добавлена такая
функциональность как методы по умолчанию. И теперь интерфейсы кроме определения методов могут иметь их реализацию по
умолчанию, которая используется, если класс, реализующий данный интерфейс, не реализует метод. Например, создадим метод
по умолчанию в интерфейсе **Printable**:

```java
interface Printable {

    default void print() {
        System.out.println("Undefined printable");
    }
}
```

Метод по умолчанию — это обычный метод без модификаторов, который помечается ключевым словом **default**. Затем в классе
**Journal** нам необязательно этот метод реализовать, хотя мы можем его и переопределить:

```java
class Journal implements Printable {

    private String name;

    String getName() {
        return name;
    }

    Journal(String name) {
        this.name = name;
    }
}
```

### Статические методы

Начиная с **JDK 8** в интерфейсах доступны статические методы - они аналогичны методам класса:

```java
interface Printable {

    void print();

    static void read() {
        System.out.println("Read printable");
    }
}
```

Чтобы обратиться к статическому методу интерфейса также, как и в случае с классами, пишут название интерфейса и метод:

```java
class Programm {

    public static void main(String[] args) {
        Printable.read();
    }
}
```

### Приватные методы

По умолчанию все методы в интерфейсе фактически имеют модификатор **public**. Однако начиная с **Java 9** мы также можем
определять в интерфейсе методы с модификатором private. Они могут быть статическими и нестатическими, но они не могут
иметь реализации по умолчанию.

Подобные методы могут использоваться только внутри самого интерфейса, в котором они определены. То есть к примеру нам
надо выполнять в интерфейсе некоторые повторяющиеся действия, и в этом случае такие действия можно выделить в приватные
методы:

```java
public class Program {

    public static void main(String[] args) {
        Calculatable c = new Calculation();
        System.out.println(c.sum(1, 2));
        System.out.println(c.sum(1, 2, 4));
    }
}

class Calculation implements Calculatable {
}

interface Calculatable {

    default int sum(int a, int b) {
        return sumAll(a, b);
    }

    default int sum(int a, int b, int c) {
        return sumAll(a, b, c);
    }

    private int sumAll(int... values) {
        int result = 0;
        for (int n : values) {
            result += n;
        }
        return result;
    }
}
```

### Константы в интерфейсах

Кроме методов в интерфейсах могут быть определены статические константы:

```java
interface Stateable {

    int OPEN = 1;
    int CLOSED = 0;

    void printState(int n);
}
```

Хотя такие константы также не имеют модификаторов, но по умолчанию они имеют модификатор доступа **public static final**
, и поэтому их значение доступно из любого места программы. Применение констант:

```java
public class Program {

    public static void main(String[] args) {
        WaterPipe pipe = new WaterPipe();
        pipe.printState(1);
    }
}

class WaterPipe implements Stateable {

    public void printState(int n) {
        if (n == OPEN)
            System.out.println("Water is opened");
        else if (n == CLOSED)
            System.out.println("Water is closed");
        else
            System.out.println("State is invalid");
    }
}

interface Stateable {

    int OPEN = 1;
    int CLOSED = 0;

    void printState(int n);
}
```

## Множественная реализация интерфейсов

Если нам надо применить в классе несколько интерфейсов, то они все перечисляются через запятую после слова 
**implements**:

```java
interface Printable {
    // методы интерфейса
}

interface Searchable {
    // методы интерфейса
}

class Book implements Printable, Searchable {
    // реализация класса
}
```

Наследование интерфейсов Интерфейсы, как и классы, могут наследоваться:

```java
interface BookPrintable extends Printable {

    void paint();
} 
```

При применении этого интерфейса класс **Book** должен будет реализовать как методы интерфейса **BookPrintable**, так и
методы базового интерфейса **Printable**.

### Имплементация двух интерфейсов с одинаковыми методами

При множественном наследовании, если мы наследуем интерфейсы с одинаковыми методами, у которых одинаковые входные и 
выходные аргументы, достаточно добавить реализацию один раз, она будет общей для всех интерфейсов:

```java
class Program {

    public static void main(String[] args) {
        WaterPipe pipe = new WaterPipe();
        pipe.printState(1);
    }
}

class WaterPipe implements Stateable1, Stateable2 {

    public void printState(int n) {
        if (n == OPEN)
            System.out.println("Water is opened");
        else if (n == CLOSED)
            System.out.println("Water is closed");
        else
            System.out.println("State is invalid");
    }
}

interface Stateable1 {

    int OPEN = 1;
    int CLOSED = 0;

    void printState(int n);
}

interface Stateable2 {
    
    void printState(int n);
}
```

## Вложенные интерфейсы

Как и классы, интерфейсы могут быть вложенными, то есть могут быть определены в классах или других интерфейсах.
Например:

```java
class Printer {

    interface Printable {

        void print();
    }
}
```

При применении такого интерфейса нам надо указывать его полное имя вместе с именем класса:

```java
public class Journal implements Printer.Printable {

    String name;

    Journal(String name) {
        this.name = name;
    }

    public void print() {
        System.out.println(name);
    }
}
```

Использование интерфейса будет аналогично предыдущим случаям:

```java
    Printer.Printable p=new Journal("Foreign Affairs");
    p.print();
```

Интерфейсы как параметры и результаты методов И так же, как и в случае с классами, интерфейсы могут использоваться в
качестве типа параметров метода или в качестве возвращаемого типа:

```java
public class Program {

    public static void main(String[] args) {
        Printable printable = createPrintable("Foreign Affairs", false);
        printable.print();
        read(new Book("Java for impatients", "Cay Horstmann"));
        read(new Journal("Java Dayly News"));
    }

    static void read(Printable p) {
        p.print();
    }

    static Printable createPrintable(String name, boolean option) {
        if (option)
            return new Book(name, "Undefined");
        else
            return new Journal(name);
    }
}

interface Printable {

    void print();
}

class Book implements Printable {

    String name;
    String author;

    Book(String name, String author) {
        this.name = name;
        this.author = author;
    }

    public void print() {
        System.out.printf("%s (%s) \n", name, author);
    }
}

class Journal implements Printable {

    private String name;

    String getName() {
        return name;
    }

    Journal(String name) {
        this.name = name;
    }

    public void print() {
        System.out.println(name);
    }
}
```

Метод **read()** в качестве параметра принимает объект интерфейса **Printable**, поэтому в этот метод мы можем передать
как объект **Book**, так и объект Journal. Метод **createPrintable()** возвращает объект **Printable**, поэтому также мы
можем возвратить как объект **Book**, так и **Journal**. Консольный вывод:

```java
    Foreign Affairs
    Java for impatients(Cay Horstmann)
    Java Dayly News
```

## Механизм обратного вызова

Одним из распространенных способов использования интерфейсов в **Java** является создание обратного вызова. Суть
обратного вызова состоит в том, что мы создаем действия, которые вызываются при других действиях. То есть одни действия
вызываются другими действиями. Стандартный пример - нажатие на кнопку. Когда мы нажимаем на кнопку, мы производим
действие, но в ответ на это нажатие запускаются другие действия. Например, нажатие на значок принтера запускает печать
документа на принтере и т.д. Рассмотрим следующий пример:

```java
public class EventsApp {

    public static void main(String[] args) {
        Button button = new Button(new ButtonClickHandler());
        button.click();
        button.click();
        button.click();
    }
}

class ButtonClickHandler implements EventHandler {

    public void execute() {
        System.out.println("Кнопка нажата!");
    }
}

interface EventHandler {

    void execute();
}

class Button {

    EventHandler handler;

    Button(EventHandler action) {
        this.handler = action;
    }

    public void click() {
        handler.execute();
    }
}
```

Итак, здесь у нас определен класс **Button**, который в конструкторе принимает объект интерфейса **EventHandler** и в
методе
**click** (имитация нажатия) вызывает метод **execute** этого объекта. Далее определяется реализация **EventHandler** в
виде класса
**ButtonClickHandler**. И в основной программе объект этого класса передается в конструктор **Button**. Таким образом,
через конструктор мы устанавливаем обработчик нажатия кнопки. И при каждом вызове метода **button.click()** будет
вызываться этот обработчик. В итоге программа выведет на консоль следующий результат:

```java
    Кнопка нажата!
    Кнопка нажата!
    Кнопка нажата!
```

Но, казалось бы, зачем нам выносить все действия в интерфейс, его реализовать, почему бы не написать проще сразу в
классе **Button**:

```java
class Button {

    public void click() {
        System.out.println("Кнопка нажата!");
    }
}
```

Дело в том, что на момент определения класса нам не всегда бывают точно известны те действия, которые должны
производиться. Особенно если класс **Button** и класс основной программы находятся в разных пакетах, библиотеках и могут
проектироваться разными разработчиками. К тому же у нас может быть несколько кнопок - объектов Button и для каждого
объекта надо определить свое действие. Например, изменим главный класс программы:

```java
public class EventsApp {

    public static void main(String[] args) {
        Button tvButton = new Button(new EventHandler() {
            private boolean on = false;

            public void execute() {
                if (on) {
                    System.out.println("Телевизор выключен..");
                    on = false;
                } else {
                    System.out.println("Телевизор включен!");
                    on = true;
                }
            }
        });
        Button printButton = new Button(new EventHandler() {
            public void execute() {
                System.out.println("Запущена печать на принтере...");
            }
        });
        tvButton.click();
        printButton.click();
        tvButton.click();
    }
}
```

Здесь у нас две кнопки - одна для включения-выключения телевизора, а другая для печати на принтере. Вместо того, чтобы
создавать отдельные классы, реализующие интерфейс **EventHandler**, здесь обработчики задаются в виде анонимных
объектов, которые реализуют интерфейс **EventHandler**. Причем обработчик кнопки телевизора хранит дополнительное
состояние в виде логической переменной on. В итоге консоль выведет нам следующий результат:

```java
    Телевизор включен!
    Запущена печать на принтере...
    Телевизор выключен..
```

## Функциональный интерфейс

Функциональный интерфейс в **Java** – это интерфейс, который содержит только один абстрактный метод. Основное 
назначение – использование в лямбда выражениях и **method reference**.

Наличие одного абстрактного метода — это единственное условие, таким образом функциональный интерфейс может содержать
так же **default** и **static** методы.

К функциональному интерфейсу можно добавить аннотацию **@FunctionalInterface**. Это не обязательно, но при наличии
данной аннотации код не скомпилируется, если будет больше или меньше, чем один абстрактный метод.

Рекомендуется добавлять **@FunctionalInterface**. Это позволит использовать интерфейс в лямбда выражениях, не
остерегаясь того, что кто-то добавит в интерфейс новый абстрактный метод и он перестанет быть функциональным.

В **Java** есть встроенные функциональные интерфейсы, размещенные в пакете **java.util.function**. Наиболее часто
используются: **Consumer<T>, Function<T,R>, Predicate<T>, Supplier<T>, UnaryOperator<T>**.

```java
import java.util.function.Predicate;

//Определяем свой функциональный интерфейс
@FunctionalInterface
interface MyPredicate {

    boolean test(Integer value);
}

public class Tester {

    public static void main(String[] args) throws Exception {
        MyPredicate myPredicate = x -> x > 0;
        System.out.println(myPredicate.test(10));   //true
        //Аналогично, но используется встроенный функциональный интерфейс java.util.function.Predicate
        Predicate<Integer> predicate = x -> x > 0;
        System.out.println(predicate.test(-10));    //false
    }
}
```

Но оказывается есть один тонкий момент, описанный в **Java Language Specification**: _“interfaces do not inherit from Object,
but rather implicitly declare many of the same methods as Object.”_ Это означает, что функциональные интерфейсы могут
содержать дополнительно абстрактные методы, определенные в классе **Object**. Код ниже валиден, ошибок компиляции и времени
выполнения не будет:

```java

@FunctionalInterface
public interface Comparator<T> {

    int compare(T o1, T o2);

    boolean equals(Object obj);
    // другие default или static методы
}
```

Интерфейс может наследоваться от другого интерфейса, в случае если интерфейс наследуется от функционального интерфейса и
не содержит в себе новых абстрактных методов, тогда этот интерфейс также является функциональным. Но интерфейс может
содержать только один абстрактный метод и множество дефолтных методов, и он до сих пор будет считаться функциональным.

```java

@FunctionalInterface
public interface ComplexFunctionalInterface extends SimpleFuncInterface {

    default public void doSomeWork() {
        System.out.println("Doing some work in interface impl...");
    }

    default public void doSomeWork() {
        System.out.println("Doing some other work in interface impl...");
    }
}
```

Верхний пример до сих пор является функциональным интерфейсом. Теперь давайте рассмотрим, как мы можем использовать
лямбда-выражения для замены анонимного внутреннего класса для реализации функциональных интерфейсов:

```java
/*
 *Implementation the interface by creating an
 *anonymoous inner class versus using
 *lambda expression.
 */
public class SimpleFunInterfaceTest {

    public static void main(String[] args) {
        carryOutWork(new SimpleFunInterface() {
            @Override
            public void doWork() {
                System.out.println("Do work in SimpleFun impl...");
            }
        });
        carryOutWork(() -> System.out.println("Do work in lambda exp impl..."));
    }

    public static void carryOutWork(SimpleFuncInterface sfi) {
        sfi.work();
    }
}
```

Результат программы будет следующим:

```java
    Do work in SimpleFun impl...
    Do work in lambda exp impl...
```







