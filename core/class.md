# Классы

## Классы и объекты

**Java** является объектно-ориентированным языком, поэтому такие понятия как "класс" и "объект" играют в нем ключевую
роль. Любую программу на **Java** можно представить как набор взаимодействующих между собой объектов.

Шаблоном или описанием объекта является класс, а объект представляет экземпляр этого класса. Можно еще провести
следующую аналогию. У нас у всех есть некоторое представление о человеке - наличие двух рук, двух ног, головы, туловища
и т.д. Есть некоторый шаблон - этот шаблон можно назвать классом. Реально же существующий человек (фактически экземпляр
данного класса)
является объектом этого класса.

Класс определяется с помощью ключевого слова **сlass**:

```java
class Cat {}
```

В данном случае класс называется **Cat**. После названия класса идут фигурные скобки, между которыми помещается тело
класса - то есть его поля и методы.

Любой объект может обладать двумя основными характеристиками: **состояние** - некоторые данные, которые хранит объект,
и **поведение** - действия, которые может совершать объект. Для хранения состояния объекта в классе применяются поля или
переменные класса.

Для определения поведения объекта в классе применяются методы. Например, класс **Cat** мог бы иметь следующее
определение:

```java
class Cat {

    String name;        // имя
    int age;            // возраст

    void displayInfo() {
        System.out.printf("Name: %s \tAge: %d\n", name, age);
    }
}
```

Как правило, классы определяются в разных файлах. Файл кода должен называться по имени этого класса, то есть в данном
случае файл должен называться **Cat.java**.

### Конструкторы

Кроме обычных методов классы могут определять специальные методы, которые называются конструкторами. Конструкторы
вызываются при создании нового объекта данного класса. Конструкторы выполняют инициализацию объекта.

Если в классе не определено ни одного конструктора, то для этого класса автоматически создается конструктор без
параметров.

Выше определенный класс **Cat** не имеет никаких конструкторов. Поэтому для него автоматически создается конструктор по
умолчанию, который мы можем использовать для создания объекта **Cat**. В частности, создадим один объект:

```java
public class Program {

    public static void main(String[] args) {
        Cat tom = new Cat(); // создание объекта
        tom.displayInfo();
        // изменяем имя и возраст
        tom.name = "Tom";
        tom.age = 5;
        tom.displayInfo();
    }
}

class Cat {

    String name;    // имя
    int age;        // возраст

    void displayInfo() {
        System.out.printf("Name: %s \tAge: %d\n", name, age);
    }
}
```

Для создания объекта **Cat** используется выражение **new Cat()**. Оператор **new** выделяет память для объекта **Cat**.
И затем вызывается конструктор по умолчанию, который не принимает никаких параметров. В итоге после выполнения данного
выражения в памяти будет выделен участок, где будут храниться все данные объекта **Cat**. А переменная **tom** получит
ссылку на созданный объект.

Если конструктор не инициализирует значения переменных объекта, то они получают значения по умолчанию. Для переменных
числовых типов это число 0, а для типа string и классов — это значение null (то есть фактически отсутствие значения).

После создания объекта мы можем обратиться к переменным объекта **Cat** через переменную **tom** и установить или
получить их значения, например, **tom.name = "Tom"**.

В итоге мы увидим на консоли:

```java
    Name:null Age:0
    Name:Tom Age:5
```

Если необходимо, чтобы при создании объекта производилась какая-то логика, например, чтобы поля класса получали какие-то
определенные значения, то можно определить в классе свои конструкторы. Например:

```java
public class Program {

    public static void main(String[] args) {
        Cat bob = new Cat();      // вызов первого конструктора без параметров
        bob.displayInfo();
        Cat tom = new Cat("Tom"); // вызов второго конструктора с одним параметром
        tom.displayInfo();
        Cat sam = new Cat("Sam", 7); // вызов третьего конструктора с двумя параметрами
        sam.displayInfo();
    }
}

class Cat {

    String name;    // имя
    int age;        // возраст

    Cat() {
        name = "Undefined";
        age = 5;
    }

    Cat(String n) {
        name = n;
        age = 5;
    }

    Cat(String n, int a) {
        name = n;
        age = a;
    }

    void displayInfo() {
        System.out.printf("Name: %s \tAge: %d\n", name, age);
    }
}
```

Теперь в классе определено три конструктора, каждый из которых принимает различное количество параметров и устанавливает
значения полей класса. Консольный вывод программы:

```java
    Name:Undefined Age:5
    Name:Tom Age:5
    Name:Sam Age:7
```

#### Ключевое слово this

Ключевое слово **this** представляет ссылку на текущий экземпляр класса. Через это ключевое слово мы можем обращаться к
переменным, методам объекта, а также вызывать его конструкторы.

### Инициализаторы

Кроме конструктора начальную инициализацию объекта вполне можно было проводить с помощью инициализатора объекта.
Инициализатор выполняется до любого конструктора. То есть в инициализатор мы можем поместить код, общий для всех
конструкторов:

```java
public class Program {

    public static void main(String[] args) {
        Cat undef = new Cat();
        undef.displayInfo();
        Cat tom = new Cat("Tom");
        tom.displayInfo();
    }
}

class Cat {

    String name;    // имя
    int age;        // возраст

    /*начало блока инициализатора*/ {
        name = "Undefined";
        age = 5;
    }
    /*конец блока инициализатора*/

    Cat() {
    }

    Cat(String name) {
        this.name = name;
    }

    Cat(String name, int age) {
        this.name = name;
        this.age = age;
    }

    void displayInfo() {
        System.out.printf("Name: %s \tAge: %d\n", name, age);
    }
}
```

Консольный вывод:

```java
    Name:Undefined Age:5
    Name:Tom Age:5
```

## Абстрактный класс

Кроме обычных классов в **Java** есть абстрактные классы. Абстрактный класс похож на обычный класс. В абстрактном классе
также можно определить поля и методы, но в то же время нельзя создать объект или экземпляр абстрактного класса.
Абстрактные классы призваны предоставлять базовый функционал для классов-наследников. А производные классы уже реализуют
этот функционал.

При определении абстрактных классов используется ключевое слово **abstract**:

```java
public abstract class Human {

    private String name;

    public String getName() {
        return name;
    }
}
```

Но главное отличие состоит в том, что мы не можем использовать конструктор абстрактного класса для создания его объекта.
Например, следующим образом:

```java
Human h=new Human();
```

Кроме обычных методов абстрактный класс может содержать абстрактные методы. Такие методы определяются с помощью
ключевого слова **abstract** и не имеют никакой реализации:

```java
public abstract void display();
```

Производный класс обязан переопределить и реализовать все абстрактные методы, которые имеются в базовом абстрактном
классе. Также следует учитывать, что если класс имеет хотя бы один абстрактный метод, то данный класс должен быть
определен как абстрактный.

Зачем нужны абстрактные классы? Допустим, мы делаем программу для обслуживания банковских операций и определяем в ней
три класса: **Person**, который описывает человека; класс **Employee**, который описывает банковского служащего;
класс **Client**, который представляет клиента банка. Очевидно, что классы **Employee** и **Client** будут производными
от класса **Person**, так как оба класса имеют некоторые общие поля и методы. И так как все объекты будут представлять
либо сотрудника, либо клиента банка, то напрямую мы от класса **Person** создавать объекты не будем. Поэтому имеет смысл
сделать его абстрактным.

```java
public class Program {

    public static void main(String[] args) {
        Employee sam = new Employee("Sam", "Leman Brothers");
        sam.display();
        Client bob = new Client("Bob", "Leman Brothers");
        bob.display();
    }
}

abstract class Person {

    private String name;

    public String getName() {
        return name;
    }

    public Person(String name) {
        this.name = name;
    }

    public abstract void display();
}

class Employee extends Person {

    private String bank;

    public Employee(String name, String company) {
        super(name);
        this.bank = company;
    }

    public void display() {
        System.out.printf("Employee Name: %s \t Bank: %s \n", super.getName(), bank);
    }
}

class Client extends Person {

    private String bank;

    public Client(String name, String company) {
        super(name);
        this.bank = company;
    }

    public void display() {
        System.out.printf("Client Name: %s \t Bank: %s \n", super.getName(), bank);
    }
}
```

Другим хрестоматийным примером является система геометрических фигур. В реальности не существует геометрической фигуры
как таковой. Есть круг, прямоугольник, квадрат, но просто фигуры нет. Однако же и круг, и прямоугольник имеют что-то
общее и являются фигурами:

```java
// абстрактный класс фигуры
abstract class Figure {

    float x; // x-координата точки
    float y; // y-координата точки

    Figure(float x, float y) {
        this.x = x;
        this.y = y;
    }

    // абстрактный метод для получения периметра
    public abstract float getPerimeter();

    // абстрактный метод для получения площади
    public abstract float getArea();
}

// производный класс прямоугольника
class Rectangle extends Figure {

    private float width;
    private float height;

    // конструктор с обращением к конструктору класса Figure
    Rectangle(float x, float y, float width, float height) {
        super(x, y);
        this.width = width;
        this.height = height;
    }

    public float getPerimeter() {
        return width * 2 + height * 2;
    }

    public float getArea() {
        return width * height;
    }
}
```

## Внутренние и вложенные классы

Классы могут быть вложенными (**nested**), то есть могут быть определены внутри других классов. Частным случаем
вложенных классов являются внутренние классы (**inner class**). Например, имеется класс **Person**, внутри которого
определен класс **Account**:

```java
public class Program {

    public static void main(String[] args) {
        Person tom = new Person("Tom", "qwerty");
        tom.displayPerson();
        tom.account.displayAccount();
    }
}

class Person {

    private String name;
    Account account;

    Person(String name, String password) {
        this.name = name;
        account = new Account(password);
    }

    public void displayPerson() {
        System.out.printf("Person \t Name: %s \t Password: %s \n", name, account.password);
    }

    public class Account {

        private String password;

        Account(String pass) {
            this.password = pass;
        }

        void displayAccount() {
            System.out.printf("Account Login: %s \t Password: %s \n", Person.this.name, password);
        }
    }
}
```

Внутренний класс ведет себя как обычный класс за тем исключением, что его объекты могут быть созданы только внутри
внешнего класса.

Внутренний класс имеет доступ ко всем полям внешнего класса, в том числе закрытым с помощью модификатора **private**.
Аналогично внешний класс имеет доступ ко всем членам внутреннего класса, в том числе к полям и методам с
модификатором **private**.

Ссылку на объект внешнего класса из внутреннего класса можно получить с помощью выражения **Внешний_класс.this**,
например, **Person.this**.

Объекты внутренних классов могут быть созданы только в том классе, в котором внутренние классы определены. В других
внешних классах объекты внутреннего класса создать нельзя.

Еще одной особенностью внутренних классов является то, что их можно объявить внутри любого контекста, в том числе внутри
метода и даже в цикле:

```java
public class Program {

    public static void main(String[] args) {
        Person tom = new Person("Tom");
        tom.setAccount("qwerty");
    }
}

class Person {

    private String name;

    Person(String name) {
        this.name = name;
    }

    public void setAccount(String password) {
        class Account {

            void display() {
                System.out.printf("Account Login: %s \t Password: %s \n", name, password);
            }
        }
        Account account = new Account();
        account.display();
    }
}
```

### Статические вложенные классы

Кроме внутренних классов также могут быть статические вложенные классы. Статические вложенные классы позволяют скрыть
некоторую комплексную информацию внутри внешнего класса:

```java
class Math {

    public static class Factorial {

        private int result;
        private int key;

        public Factorial(int number, int x) {
            result = number;
            key = x;
        }

        public int getResult() {
            return result;
        }

        public int getKey() {
            return key;
        }
    }

    public static Factorial getFactorial(int x) {
        int result = 1;
        for (int i = 1; i <= x; i++) {
            result *= i;
        }
        return new Factorial(result, x);
    }
}
```

Здесь определен вложенный класс для хранения данных о вычислении факториала. Основные действия выполняет метод 
**getFactorial**, который возвращает объект вложенного класса. И теперь используем классы в методе **main**:

```java
public static void main(String[]args){
    Math.Factorial fact=Math.getFactorial(6);
    System.out.printf("Факториал числа %d равен %d \n",fact.getKey(),fact.getResult());
    }
```

## Анонимные классы

Анонимные классы объявляются без указания в коде имени класса. Анонимные классы могут быть созданы:

#### 1) как реализация интерфейса:

```java
public class Foo {

    // Анонимный класс, который реализует интерфейс SayHello
    static SayHello h = new SayHello() {
        @Override
        public void say() {
            System.out.println("Метод внутреннего анонимного класса");
        }
    };

    public static void main(String[] args) {
        h.say();
    }
}

// somewhere
interface SayHello {

    void say();
}
```

На практике, чаще, реализуют функциональные интерфейсы, с помощью анонимных классов, не смотря на наличие лямбд. Вот
перечень функциональных интерфейсов из пакета **java.util.function**. Это не магия, а просто набор готовых заготовок для
ваших будущих реализаций.

#### 2) как наследник определённого класса:

```java
public class External {

    // Анонимный класс наследуется от класса Foo
    static Foo foo = new Foo() {
        @Override
        public void show() {
            super.show();
            System.out.println("Метод внутреннего анонимного класса");
        }
    };

    public static void main(String[] args) {
        foo.show();
    }
}

class Foo {

    public void show() {
        System.out.println("Метод суперкласса");
    }
}
```

Анонимный класс может быть как статическим, так и нестатическим. Это напрямую зависит от того, статическим или
нестатическим является блок, в котором анонимный класс был объявлен. Если анонимный класс объявлен в статическом блоке:

```java
import java.util.function.Consumer;

public class Anonymous {

    public static void main(String[] args) {
        Consumer<String> foo = new Consumer() {
            @Override
            public void accept(Object o) {
                System.out.println(o + " TODO something useful!");
            }
        };
        foo.accept("Работа анонимного класса в статическом методе.");
    }
}
```

То его второй экземпляр можно создать так: **Consumer otherInstance = foo.getClass().newInstance()**; (эту строку нужно
завернуть в try-catch или пробросить исключения выше). И переиспользуем ту же логику, но уже в другом инстансе:
otherInstance.accept("Работа второго экземпляра анонимного класса в статическом методе.");. Если же анонимный класс был
объявлен внутри нестатического блока, то для создания второго экземпляра анонимного класса нужно передать в его
конструктор ссылку на обрамляющий класс. В противном случае получим **InstantiationException**. Вот как это выглядит в
коде:

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.util.function.Consumer;

public class Anonymous {

    public void nonStaticMethod() {
        // собственно наш анонимный класс
        Consumer<String> foo = new Consumer() {
            @Override
            public void accept(Object o) {
                System.out.println(o + " TODO something useful!");
            }
        };
        foo.accept("Работа анонимного класса в НЕстатическом методе.");
        // достаем конструктор у анонимного класса
        Constructor[] constructors = foo.getClass().getDeclaredConstructors();
        // Записываем ссылку на объект Anonymous в массив параметров, для конструктора.
        Object[] params = new Object[1];
        params[0] = this;
        // Создаем новую ссылку типа Consumer
        Consumer otherInstance = null;
        try {
            // создаем новый экземпляр анонимного класса, передав в его конструктор массив параметров, ссылку на текущий
            // класс, в котором мы и осуществляем все манипуляции с анонимным классом.
            otherInstance = (Consumer) constructors[0].newInstance(params);
        } catch (InstantiationException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        }
        otherInstance.accept("Работа второго экземпляра анонимного класса в НЕстатическом методе.");
    }

    public static void main(String[] args) {
        Anonymous anon = new Anonymous();
        anon.nonStaticMethod();
    }
}
```

Любой анонимный внутренний класс может за один раз реализовать только один интерфейс. Так же, за один раз можно либо
расширить класс, либо реализовать интерфейс, но не одновременно. Анонимные классы полезны в некоторых "узких" участках
кода, когда нет необходимости их потом переиспользовать где-то еще. Чаще всего на практике используют лишь один
экземпляр анонимного класса. Если же реализацию интерфейса придется использовать много раз в коде — то лучше
использовать лямбда-выражения (лямбды), которые стали доступны начиная с **JAVA 8**. Например, реализацию интерфейса 
**Consumer**, в текущем уроке, можно переписать с помощью лямбд:

```java
import java.util.function.Consumer;

public class Anonymous {

    public static void main(String[] args) {
        Consumer<String> foo = o -> System.out.println(o + " TODO something useful!");
        foo.accept(" Using lambda :)");
    }
}
```
