## Java

#### Java基础(上)

##### -What is OOPs?

> Object-Oriented Programming is a language that uses objects in programming. In OOP, programmers organize code around "objects," which are data structures that bundle together related data (properties) and functions (methods or behaviors)

Key principles:

- **Encapsulation:** Bundling data and methods together within an object and restricting direct access to some of the object's components, which protects the data.
- **Inheritance:** The ability for a new class to inherit properties and methods from an existing class, which promotes code reuse.
- **Abstraction:** Hiding complex implementation details from the user and only showing the necessary functions. For example, a car stereo has buttons to control it, but you don't need to know the complex internal circuitry to use it.
- **Polymorphism:** The ability for different objects to respond to the same method call in their own unique way.

> [详细阅读](https://www.geeksforgeeks.org/dsa/introduction-of-object-oriented-programming/)



##### -JVM vs. JDK vs. JRE

![image-20251029125336550](Screenshot/image-20251029125336550.png)

<img src="D:\Code\0 myWeb 2023\Note\Screenshot\image-20251029123906202.png" alt="image-20251029123906202" style="zoom:80%;" />

###### **JDK**

(Java Development Kit)

<img src="D:\Code\0 myWeb 2023\Note\Screenshot\image-20251029123819498.png" alt="image-20251029123819498" style="zoom:80%;" />

Java开发工具包：包含 JRE(Java Runtime Environment)，编译器`javac`，`javadoc`

###### JRE

(Java程序运行环境):

1. JVM
2. Java Class Library(基础类库)：提供常用的功能和 API（如 I/O 操作、网络通信、数据结构等）

<img src="D:\Code\0 myWeb 2023\Note\Screenshot\jdk-jre-jvm-jit.png" alt="JDK、JRE、JVM、JIT 这四者的关系" style="zoom: 67%;" />



###### **JVM**

(Java Virtual Machine)

`javac` performs several **translation and compilation steps** to turn your human-readable `.java` source file into a machine-readable `.class` file (bytecode)

1. check errors
2. build a parse tree (AST — Abstract Syntax Tree)
3. constructs internal symbol tables for classes, methods, and fields
4. bytecode generation
5. form `.class` and executed by JVM

利用 JVM 将 `.class` 文件 在不同系统平台(Windows, Mac, Linus) 运行

> **流程图**

```scss
源码 (.java)
   ↓ 编译 (javac)
字节码 (.class)
   ↓ 类加载子系统
方法区(Metaspace) ← 类信息、常量池
   ↓
执行 new 指令
   ↓
堆(Heap) ← 创建对象实例
   ↓
栈(Stack) ← 创建栈帧，调用 <init> 构造方法
   ↓
程序计数器(PC) 指示下一条指令
   ↓
执行引擎解释或JIT编译执行
```

JVM uses both Interpreter && JIT

| Execution mode    | How it runs                                                  | Speed | Who handles it   |
| ----------------- | ------------------------------------------------------------ | ----- | ---------------- |
| **Interpreter**   | Reads bytecode instruction-by-instruction, simulates behavior | Slow  | JVM interpreter  |
| **JIT Compiler ** | Translates frequently executed (“hot”) bytecode into native machine code | Fast  | JVM JIT compiler |

###### JIT

`.class->机器码` 这一步。在这一步 JVM 类加载器首先加载字节码文件，然后通过解释器逐行解释执行，这种方式的执行速度会相对比较慢。而且，有些方法和代码块是经常需要被调用的(也就是所谓的热点代码)，所以后面引进了 **JIT（Just in Time Compilation）** 编译器，而 JIT 属于运行时编译。当 JIT 编译器完成第一次编译后，其会将字节码对应的机器码保存下来，下次可以直接使用。而我们知道，机器码的运行效率肯定是高于 Java 解释器的。这也解释了我们为什么经常会说 **Java 是编译与解释共存的语言** 。

<img src="D:\Code\0 myWeb 2023\Note\Screenshot\jvm-rough-structure-model.png" alt="JVM 的大致结构模型" style="zoom:80%;" />

###### 🌈 拓展阅读

- [基本功 | Java 即时编译器原理解析及实践 - 美团技术团队](https://tech.meituan.com/2020/10/22/java-jit-practice-in-meituan.html)
- [基于静态编译构建微服务应用 - 阿里巴巴中间件](https://mp.weixin.qq.com/s/4haTyXUmh8m-dBQaEzwDJw)

##### **-为什么说 Java 语言“编译与解释并存”？**

这是因为 Java 语言既具有编译型语言的特征，也具有解释型语言的特征。因为 Java 程序要经过先编译，后解释两个步骤，由 Java 编写的程序需要先经过编译步骤，生成字节码（`.class` 文件），这种字节码必须由 Java 解释器来解释执行。

##### -相关问题

1. 面向对象是什么？

   > 支持封装、继承和多态

2. Java和C++ 同为面向对象 有何区别

   > Java 不提供指针来直接访问内存，程序内存更加安全
   >
   > Java 的类是单继承的，C++ 支持多重继承；虽然 Java 的类不可以多继承，但是接口可以多继承。
   >
   > Java 有自动内存管理垃圾回收机制(GC)，不需要程序员手动释放无用内存。
   >
   > C ++同时支持方法重载和操作符重载，但是 Java 只支持方法重载（操作符重载增加了复杂性，这与 Java 最初的设计思想不符）。
   >
   > …

##### -基本语法

###### 注释有哪几种形式？（单行/多行/文档注释）

###### 标识符和关键字区别

> 标识符就是名字；**关键字是被赋予特殊含义的标识符** 
>
> 官方文档：https://docs.oracle.com/javase/tutorial/java/nutsandbolts/_keywords.html
>
> 注意：虽然 `true`, `false`, 和 `null` 看起来像关键字但实际上他们是字面值，同时你也不可以作为标识符来使用。

![image-20251029165305777](D:\Code\0 myWeb 2023\Note\Screenshot\image-20251029165305777.png)

###### `++` \ `--`

> **前缀形式**（例如 `++a` 或 `--a`）：先自增/自减变量的值，然后再使用该变量，例如，`b = ++a` 先将 `a` 增加 1，然后把增加后的值赋给 `b`。
>
> **后缀形式**（例如 `a++` 或 `a--`）：先使用变量的当前值，然后再自增/自减变量的值。例如，`b = a++` 先将 `a` 的当前值赋给 `b`，然后再将 `a` 增加 1。

###### 移位运算符(Shift Operator)

> 首位 0正数；1负数

###### continue/break/return



##### -Project/Package/Class

##### -Class(类) & Object(对象)

`Class` is a template that defines the field and behavior of an `object`

`Object` is an entity of a `class`

```java
class Car {              // Class: defines what a Car is
    String color;
    void drive() {
        System.out.println("The car is driving.");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();   // Object: a specific Car
        myCar.color = "red";
        myCar.drive();
    }
}

```

> Array don't have its own methods; only inherited a few basic `Object` methods (e.g., `hashCode()`, `toString()`)



##### -基本数据类型

- 6 种数字类型：
  - 4 种整数型：`byte`、`short`、`int`、`long`
  - 2 种浮点型：`float`、`double`
- 1 种字符类型：`char`
- 1 种布尔型：`boolean`

> 像 `byte`、`short`、`int`、`long`能表示的最大正数都减 1 了。这是为什么呢？这是因为在二进制补码表示法中，最高位是用来表示符号的（0 表示正数，1 表示负数），其余位表示数值部分。所以，如果我们要表示最大的正数，我们需要把除了最高位之外的所有位都设为 1。如果我们再加 1，就会导致溢出，变成一个负数。

> 注意：
>
> 1. Java 里使用 `long` 类型的数据一定要在数值后面加上 **L**，否则将作为整型解析。
> 2. Java 里使用 `float` 类型的数据一定要在数值后面加上 **f 或 F**，否则将无法通过编译。

这八种基本类型都有对应的包装类分别为：`Byte`、`Short`、`Integer`、`Long`、`Float`、`Double`、`Character`、`Boolean`

###### 基本类型和包装类型区别

> Primitive vs. Wrapper class(Object)
>
> Wrapper classes are a specific type of class designed to "wrap" primitive data types into objects.
>

- Nullability： 基础数据 不可为null；包装(对象类型) 默认为null
- **存储方式**：基本数据类型的局部变量存放在 Java 虚拟机栈中的局部变量表中，基本数据类型的成员变量（未被 `static` 修饰 ）存放在 Java 虚拟机的堆中。包装类型属于对象类型，我们知道几乎所有对象实例都存在于堆中。

> **为什么说是几乎所有对象实例都存在于堆中呢？** 这是因为 HotSpot 虚拟机引入了 JIT 优化之后，会对对象进行逃逸分析，如果发现某一个对象并没有逃逸到方法外部，那么就可能通过标量替换来实现栈上分配，而避免堆上分配内

- AutoBoxing:

  ```java
  Integer i = 10;  //装箱
  int n = i;   //拆箱
  //本质是调用的 包装类方法
  Integer a = Integer.valueOf(10);
  int b = a.intValue();
  
  Integer n = null;
  int x = n; // ❌ NullPointerException
  ```

> 注意：**如果频繁拆装箱的话，也会严重影响系统的性能。我们应该尽量避免不必要的拆装箱操作。**

- **比较方式**：对于基本数据类型来说，`==` 比较的是值。对于包装数据类型来说，`==` 比较的是对象的内存地址。所有整型包装类对象之间值的比较，全部使用 `equals()` 方法。

> ⚠️ 注意：**基本数据类型存放在栈中是一个常见的误区！** 基本数据类型的存储位置取决于它们的作用域和声明方式。如果它们是局部变量，那么它们会存放在栈中；如果它们是成员变量，那么它们会存放在堆/方法区/元空间中。

| Expression                                 | Works?                            | Explanation                   |
| ------------------------------------------ | --------------------------------- | ----------------------------- |
| `int a = 100; Integer b = 100; a == b`     | ✅ true                            | Unboxed automatically         |
| `Integer x = 100; Integer y = 100; x == y` | ✅ true (cached range -128 to 127) |                               |
| `Integer x = 200; Integer y = 200; x == y` | ❌ false                           | Different objects             |
| `x.equals(y)`                              | ✅ true                            | Compares value, not reference |

###### 包装类型缓存机制

`Byte`,`Short`,`Integer`,`Long` 这 4 种包装类默认创建了数值 **[-128，127]** 的相应类型的缓存数据，`Character` 创建了数值在 **[0,127]** 范围的缓存数据，`Boolean` 直接返回 `TRUE` or `FALSE`。

对于 `Integer`，可以通过 JVM 参数 `-XX:AutoBoxCacheMax=<size>` 修改缓存上限，但不能修改下限 -128。`Byte`,`Short`,`Long` ,`Character` 缓存大小固定，无法修改。`Boolean`没有缓存概念。

```java
public class ByteCacheDemo {
    public static void main(String[] args) {
        Byte a = 127;
        Byte b = 127;
        System.out.println(a == b); // true, cached

        Byte x = 128;
        Byte y = 128;
        System.out.println(x == y); // false, new objects

   //valueOf create new object if they are not in [-128,127]
        Byte x = Byte.valueOf((byte)128);
    }
}
```

```java
//Integer 缓存源码
public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}
private static class IntegerCache {
    static final int low = -128;
    static final int high;
    static {
        // high value may be configured by property
        int h = 127;
    }
}
```

两种浮点数类型的包装类 Float,Double 并没有实现缓存机制。

```java
Integer i1 = 33;
Integer i2 = 33;
System.out.println(i1 == i2);// 输出 true

Float i11 = 333f;
Float i22 = 333f;
System.out.println(i11 == i22);// 输出 false

Double i3 = 1.2;
Double i4 = 1.2;
System.out.println(i3 == i4);// 输出 false
```

```java
Integer i1 = 40;
Integer i2 = new Integer(40);
System.out.println(i1==i2);// false
```

<img src="D:\Code\0 myWeb 2023\Note\Screenshot\image-20251030175905691.png" alt="image-20251030175905691" style="zoom: 45%;" />

`Primitive values` won't cache since they are not `Objects`

###### 浮点数精度丢失风险

```java
float a = 2.0f - 1.9f;
float b = 1.8f - 1.7f;
System.out.printf("%.9f",a);// 0.100000024
System.out.println(b);// 0.099999905
System.out.println(a == b);// false
```

> 更多内容，建议看一下[计算机系统基础（四）浮点数](http://kaito-kidd.com/2018/08/08/computer-system-float-point/)这篇文章。

如何解决？ `BigDecimal`

```java
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("1.00");
BigDecimal c = new BigDecimal("0.8");

BigDecimal x = a.subtract(c);
BigDecimal y = b.subtract(c);

System.out.println(x); /* 0.2 */
System.out.println(y); /* 0.20 */
// 比较内容，不是比较值
System.out.println(Objects.equals(x, y)); /* false */
// 比较值相等用相等compareTo，相等返回0
System.out.println(0 == x.compareTo(y)); /* true */
```

###### 超过long整型的数据如何处理

`BigInteger`

##### -JVM储存方式 

> JVM 细节 见前面章节 — JVM vs. JDK vs. JRE

> | Concept             | Description                                                  | Used by                                   |
> | ------------------- | ------------------------------------------------------------ | ----------------------------------------- |
> | **Heap**            | The area where **objects and their instance variables** live. | `new` objects, arrays, instance fields    |
> | **元宇宙Metaspace** | The area where **class-level (static) data**, method bytecode, and metadata live. | `static` variables, class definitions     |
> | **Stack**           | Temporary area for **method calls and local variables**.     | method execution (primitives, references) |

```java
class Demo {
    int x = 10;
    static int y = 20;
}
public class Main {
    public static void main(String[] args) {
        Demo a = new Demo();
        Demo b = new Demo();
        int localVar = 5;
    }
}
```

```kotlin
────────────────────────────────────────────
 Stack (main method):
   	localVar = 5
   a → (reference to Demo object in heap)
────────────────────────────────────────────
 Heap:
   [Demo object #1]
     x = 10
────────────────────────────────────────────
 Metaspace (class area):
   Demo.y = 20
────────────────────────────────────────────

```

```java
class Demo {
    static int staticVar = 100;
    int instantVar = 5;
    //static method can be directly called from class
    static void changeStatic(int newValue) {
        staticVar = newValue; // modifies the same shared variable
        value = 20;   // ❌ ERROR
    }
	//non-static need first to initiate the object
    void changeViaInstance(int newValue) {
        instantVar = 50 //belong to an object
        staticVar = newValue; // also works, same shared variable
    }
}

public class Main {
    public static void main(String[] args) {
        //A static method belongs to the class, so it can exist before any objects are created.
        // method must also be static, because you’re calling it on the class
        Demo.changeStatic(200);  // ✅ changes shared value
        
        Demo a = new Demo();
        Demo b = new Demo();
        //static change every value in all objects
        System.out.println(b.staticVar); // 200

        a.changeViaInstance(300); 
        System.out.println(Demo.staticVar); // 300
        Demo.staticVar = -1;//change accessible using Demo
    }
}

```

```java
class Demo {
    int value = 10;      //堆instance variable (field)成员变量
    static int count = 5;//元static variable (class field)

    void show(int n) {          // n = parameter variable
        int temp = n + value;   //栈temp = local variable
        System.out.println(temp + count);
    }
}
```

##### -变量

###### Member Variable & Local Variable

> Member variable includes Instance var & Class var( `static` )

- **语法形式**：从语法形式上看，成员变量是属于类的，而局部变量是在代码块或方法中定义的变量或是方法的参数；成员变量可以被 `public`,`private`,`static` 等修饰符所修饰，而局部变量不能被访问控制修饰符及 `static` 所修饰；但是，成员变量和局部变量都能被 `final` 所修饰。
- **存储方式**：从变量在内存中的存储方式来看，如果成员变量是使用 `static` 修饰的，那么这个成员变量是属于类的，如果没有使用 `static` 修饰，这个成员变量是属于实例**(instance || object)**的。而对象存在于堆内存，局部变量则存在于栈内存。
- **生存时间**：从变量在内存中的生存时间上看，成员变量是对象的一部分，它随着对象的创建而存在，而局部变量随着方法的调用而自动生成，随着方法的调用结束而消亡。
- **默认值**：从变量是否有默认值来看，成员变量如果没有被赋初始值，则会自动以类型的默认值而赋值（一种情况例外:被 `final` 修饰的成员变量也必须显式地赋值），而局部变量则不会自动赋值。

```java
//final must assign val: at declaration; every constructor
//Otherwise, causing compile error
public class Person {
    final String name;  // no value yet

    public Person(String name) {
        this.name = name;  // assigned here
    }
}
//MUST assigned a value when declared, since final
public class Config {
    static final int MAX_USERS = 100; 
    
    static String VERSION;//default：null;created with class
    int age;         // default：0; created with object
}
```

> `Member variable` contains `instance variable` & `static variable`
>
> `static variable` belongs to `class`
>
> `instance variable` belongs to `object`



###### `static`

静态变量只会被分配一次内存，即使创建多个对象，这样可以节省内存。

static variable 需要通过类名访问，如`class.staticVar`

###### Character & String

- **含义** : 字符常量相当于一个整型值( ASCII 值),可以参加表达式运算; 字符串常量代表一个地址值(该字符串在内存中存放位置)。
- **占内存大小**：字符常量只占 2 个字节; 字符串常量占若干个字节。

##### -方法

###### 静态方法为什么不能调用非静态成员?

- 静态方法是属于类的，在类加载的时候就会分配内存，可以通过类名直接访问。而非静态成员属于实例对象，只有在对象实例化之后才存在，需要通过类的实例对象去访问。
- 在类的非静态成员不存在的时候静态方法就已经存在了，此时调用在内存中还不存在的非静态成员，属于非法操作。

静态方法在访问本类的成员时，只允许访问静态成员（即静态成员变量和静态方法），不允许访问实例成员（即实例成员变量和实例方法），而实例方法不存在这个限制。

###### ⭐️Overloading(重载) & Overriding(重写)

> **Overloading** happens **in the same class**, when multiple methods have the **same name** but **different parameter lists** (different number or types of parameters).

**重载：**

- 发生在**同一个类**中（或者父类和子类之间）
- 方法名必须相同，**参数**列表**必须不同**

**重写：**

- 父类与子类之间（存在继承关系）；
- 方法名、**参数**列表**必须完全相同**。
- 子类方法的**返回类型**必须与父类方法的返回类型**相同**，或者是其**子类**。

```java
class Parent {
    Number getValue() { return 1; }
}
class Child extends Parent {
    Integer getValue() { return 1; } // ✅ allowed (Integer is subclass of Number)
}
```

- 子类方法的访问权限**不能低于**父类方法的访问权限。（public > protected > default > private）

```java
class Parent {
    protected void run() {}
}
class Child extends Parent {
    public void run() {} // ✅ allowed (broader access)
}
```

- 抛出异常范围小于父类

```java
class Parent {
    void read() throws IOException {}
}
class Child extends Parent {
    void read() throws FileNotFoundException {} // ✅ narrower exception
}
```

**注意⚠️**

- 如果父类方法访问修饰符为 **private/final/static** 则子类就不能重写该方法

```java
class Parent {
    static void print() {}
}
class Child extends Parent {
    static void print() {} // ⚠️ hides, not overrides
}
```

- **构造方法无法被重写**

构造方法只属于定义它的那个类，因为无法继承父类构造方法，所以无法重写

> 如果方法的返回值是引用类型，重写时是可以返回该引用类型的子类的。

```java
class Animal {}
class Dog extends Animal {}

class Parent {
    Animal getAnimal() { return new Animal(); }
}
class Child extends Parent {
    @Override
    Dog getAnimal() { return new Dog(); } // ✅ allowed, Dog ⊆ Animal
}

```



#### Java基础(中)

##### -面向对象基础

> 面向过程编程（Procedural-Oriented Programming，POP）和面向对象编程（Object-Oriented Programming，OOP）是两种常见的编程范式，两者的主要区别在于解决问题的方式不同：
>
> - **面向过程编程（POP）**：面向过程把解决问题的过程拆成一个个方法，通过一个个方法的执行解决问题。
> - **面向对象编程（OOP）**：面向对象会先抽象出对象，然后用对象执行方法的方式解决问题。
>
> 相较于 POP
>
> - **易维护**：由于良好的结构和封装性，OOP 程序通常更容易维护。
> - **易复用**：通过继承和多态，OOP 设计使得代码更具复用性，方便扩展功能。
> - **易扩展**：模块化设计使得系统扩展变得更加容易和灵活。

```java
public class Main {
    public static void main(String[] args) {
        // 定义圆的半径
        double radius = 3.0;

        // 计算圆的面积和周长
        double area = Math.PI * radius * radius;
        double perimeter = 2 * Math.PI * radius;

        // 输出圆的面积和周长
        System.out.println("圆的面积为：" + area);
        System.out.println("圆的周长为：" + perimeter);
    }
}
```

###### 创建一个对象用什么运算符?

> new 运算符

###### 对象实体与对象引用有何不同?

> new 创建对象实例（对象实例在堆内存中），对象引用指向对象实例（对象引用存放在栈内存中）。
>
> - 一个对象引用可以指向 0 个或 1 个对象（一根绳子可以不系气球，也可以系一个气球）；
> - 一个对象可以有 n 个引用指向它（可以用 n 条绳子系住一个气球）。

###### ⭐️对象的相等和引用相等的区别

> - 对象的相等一般比较的是内存中存放的内容是否相等。
> - 引用相等一般比较的是他们指向的内存地址是否相等。

```java
String str1 = "hello";
String str2 = new String("hello");
String str3 = "hello";
// 使用 == 比较字符串的引用相等
System.out.println(str1 == str2);
System.out.println(str1 == str3);
// 使用 equals 方法比较字符串的相等
System.out.println(str1.equals(str2));
System.out.println(str1.equals(str3));String str1 = "hello";
String str2 = new String("hello");
String str3 = "hello";
// 使用 == 比较字符串的引用相等
System.out.println(str1 == str2);
System.out.println(str1 == str3);
// 使用 equals 方法比较字符串的相等
System.out.println(str1.equals(str2));
System.out.println(str1.equals(str3));
```

> false
> true
> true
> true

> 此刻  `str1 = "hello"` 存放在 Method Area / Metaspace 中的 String Constant Pool 
>
> 当创建 `String` 类型的对象时，虚拟机会在常量池中查找有没有已经存在的值和要创建的值相同的对象，如果有就把它赋给当前引用。如果没有就在常量池中重新创建一个 `String` 对象。

**⭐️注意**：`Person xiaoZhang = new Person("小张");`

- **堆内存 (heap)** 里创建一个新的 `Person` 对象
- **栈内存 (stack)** 中创建一个变量 `xiaoZhang`
- 把堆中对象的地址（引用值）赋给栈上的变量 `xiaoZhang`。

###### Class constructor

> 构造方法是一种特殊的方法，主要作用是完成对象的初始化工作。
>
> 如果一个类没有声明构造方法，也可以执行！Java会添加默认的不带参数的构造方法。
>
> - **名称与类名相同**：构造方法的名称必须与类名完全一致。
> - **没有返回值**：构造方法没有返回类型，且不能使用 `void` 声明。
> - **自动执行**：在生成类的对象时，构造方法会自动执行，无需显式调用。

```java
class Person {
    String name;
    int age;

    // 编译器自动加上的默认构造方法：
    Person() {
        super(); // 调用父类 Object 的构造方法
    }
}
public class Main {
	public static void main(String[] args) {
		// 这里的 () 实际上是在调用无参构造方法
		Person p = new Person();
	}
}
```

> 如果我们重载了有参的构造方法，记得都要把无参的构造方法也写出来（无论是否用到），因为这可以帮助我们在创建对象的时候少踩坑。
>
> **如果不写无参constructor，会编译报错**，当 `new Person()`

```java
class Person {
    String name;
    int age;
    String location

    Person(String name, int age, String location) {
    	this.name = name;
        this.age = age;
        this.city = city;
	}
    
    Person() {
        this("Unknown", -1, "Earth")
    }
    
    Person(String name) {
        this(name, -1, "Earth"); // 调用三参构造
        //可以不加，java会自动赋默认值；加，考虑业务需要
        //String 默认null，最好加
        //this.age = age;
    }
    
}
public class Main {
	public static void main(String[] args) {
		Person p = new Person();
	}
```

###### 构造方法可否Override

> 构造方法**不能被重写（override）**，但**可以被重载（overload）**。因此，一个类中可以有多个构造方法，这些构造方法可以具有不同的参数列表，以提供不同的对象初始化方式。

###### ⭐️面向对象三大特征

**封装**(Encapsulation)

> 封装是指把一个对象的状态信息（也就是属性）隐藏在对象内部，不允许外部对象直接访问对象的内部信息。但是可以提供一些可以被外界访问的方法来操作属性。

**继承**(Inheritance)

> 继承是使用已存在的类的定义作为基础建立新类的技术，新类的定义可以增加新的数据或新的功能，也可以用父类的功能，但**不能选择性地继承**父类
>
> - 子类拥有父类对象所有的属性和方法（包括私有属性和私有方法），但是父类中的私有属性和方法子类是无法访问，**只是拥有**。
> - 子类可以拥有自己属性和方法，即子类可以对父类进行扩展。
> - 子类可以用自己的方式实现父类的方法。（以后介绍）。

**多态**(Polymorphism)

> - 对象类型（Object type）和引用类型（Reference type）之间具有继承（类）/实现（接口）的关系；
> - 引用类型变量发出的方法调用的到底是哪个类中的方法，必须在程序运行期间才能确定；

```java
Animal a = new Dog();   // 引用类型是 Animal，对象类型是 Dog
```



###### ⭐️Interface(接口) vs. Abstract Class(抽象类)

**共同点：**

- **实例化**：接口和抽象类都不能直接实例化，只能被实现（接口）或继承（抽象类）后才能创建具体的对象。
- **抽象方法**：接口和抽象类都可以包含抽象方法。抽象方法没有方法体，必须在子类或实现类中实现。

**区别**：

- **设计目的**：接口主要用于对类的行为进行约束，你实现了某个接口就具有了对应的行为。抽象类主要用于代码复用，强调的是所属关系。
- **继承和实现**：(`extends` & `implements`)一个类只能继承一个类（包括抽象类），因为 Java 不支持多继承。但一个类可以实现多个接口，一个接口也可以继承多个其他接口。
- **成员变量**：接口中的成员变量只能是 `public static final` 类型的，不能被修改且必须有初始值。抽象类的成员变量可以有任何修饰符（`private`, `protected`, `public`），可以在子类中被重新定义或赋值。
- 方法： 
  - Java 8 之前，接口中的方法默认是 `public abstract` ，也就是只能有方法声明。自 Java 8 起，可以在接口中定义 `default`（默认） 方法和 `static` （静态）方法。 自 Java 9 起，接口可以包含 `private` 方法。
  - 抽象类可以包含抽象方法和非抽象方法。抽象方法没有方法体，必须在子类中实现。非抽象方法有具体实现，可以直接在抽象类中使用或在子类中重写。

**最大区别**：

- 接口不能包含普通变量和实例方法，变量要求`public static final`
- 抽象类能包含普通变量和实例方法

`default`

```java
public interface Animal {
    void makeSound();

    default void eat() {                   // 默认实现
        System.out.println("Eating...");
    }
}

public class Dog implements Animal {
    public void makeSound() {
        System.out.println("Woof!");
    }
}

```

 `static` 

```java
public interface MathHelper {
    static int add(int a, int b) {
        return a + b;
    }
}

int sum = MathHelper.add(3, 5);   // 直接通过接口名调用

```

> 不能被实现类继承或重写。
>
> 通常用来定义与接口相关的“**静态工具逻辑**”。

`private`

```java
public interface Logger {
    default void logInfo(String msg) {
        log("INFO", msg);
    }

    default void logError(String msg) {
        log("ERROR", msg);
    }

    private void log(String level, String msg) {   // 私有方法
        System.out.println(level + ": " + msg);
    }
}
```

###### 浅拷贝 vs 深拷贝

**浅拷贝**：浅拷贝会在堆上创建一个新的对象（区别于引用拷贝`reference copy`的一点），不过，如果原对象内部的属性是引用类型的话，浅拷贝会直接复制内部对象的引用地址，也就是说拷贝对象和原对象共用同一个内部对象。

**深拷贝**：深拷贝会完全复制整个对象，包括这个对象所包含的内部对象。

```java
class Address {
    String city;
    public Address(String city) { this.city = city; }
}

class Person implements Cloneable {
    String name;          // 引用类型（String）
    int age;              // 基本类型
    Address address;      // 引用类型

    public Person(String name, int age, Address address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }

    protected Object clone() throws CloneNotSupportedException {
        return super.clone();   // 浅拷贝
    }
}

public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {
        Address addr = new Address("Tokyo");
        Person p1 = new Person("Frank", 24, addr);
        Person p2 = (Person) p1.clone();

        p2.name = "Mike";
        p2.address.city = "Osaka";

        System.out.println(p1.name + " - " + p1.address.city);
    }
}
// Frank - Osaka
// 因为此处只拷贝了Address地址
// 而String只会影响p2自己
```

![shallow&deep-copy](Screenshot/shallow&deep-copy.png)



##### -⭐️Object

###### Object常见方法

```java
/**
 * native 方法，用于返回当前运行时对象的 Class 对象，使用了 final 关键字修饰，故不允许子类重写。
 */
public final native Class<?> getClass()
/**
 * native 方法，用于返回对象的哈希码，主要使用在哈希表中，比如 JDK 中的HashMap。
 */
public native int hashCode()
/**
 * 用于比较 2 个对象的内存地址是否相等，String 类对该方法进行了重写以用于比较字符串的值是否相等。
 */
public boolean equals(Object obj)
/**
 * native 方法，用于创建并返回当前对象的一份拷贝。
 */
protected native Object clone() throws CloneNotSupportedException
/**
 * 返回类的名字实例的哈希码的 16 进制的字符串。建议 Object 所有的子类都重写这个方法。
 */
public String toString()
/**
 * native 方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。
 */
public final native void notify()
/**
 * native 方法，并且不能重写。跟 notify 一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。
 */
public final native void notifyAll()
/**
 * native方法，并且不能重写。暂停线程的执行。注意：sleep 方法没有释放锁，而 wait 方法释放了锁 ，timeout 是等待时间。
 */
public final native void wait(long timeout) throws InterruptedException
/**
 * 多了 nanos 参数，这个参数表示额外时间（以纳秒为单位，范围是 0-999999）。 所以超时的时间还需要加上 nanos 纳秒。。
 */
public final void wait(long timeout, int nanos) throws InterruptedException
/**
 * 跟之前的2个wait方法一样，只不过该方法一直等待，没有超时时间这个概念
 */
public final void wait() throws InterruptedException
/**
 * 实例被垃圾回收器回收的时候触发的操作
 */
protected void finalize() throws Throwable { }
```

###### `==` vs. `equals()`

`==`

- 对于基本数据类型来说，`==` 比较的是值。
- 对于引用数据类型来说，`==` 比较的是对象的内存地址。

`.equals` 只能用来判断两个**对象**是否相等

```java
// Object类默认方法
public boolean equals(Object obj) {
     return (this == obj);
}
```

###### `hashCode()` & `equals()`

> 如果两个对象的`hashCode` 值相等，那这两个对象不一定相等（哈希碰撞）。
>
> 如果两个对象的`hashCode` 值相等并且`equals()`方法也返回 `true`，我们才认为这两个对象相等。
>
> 如果两个对象的`hashCode` 值不相等，我们就可以直接认为这两个对象不相等

重写 `equals()` 时没有重写 `hashCode()` 方法的话，使用 `HashMap` 可能会出现什么问题？

- 没有重写 `hashCode()` ，导致相同元素内容，存到不同的位置，导致多个`Tom`  key 出现
- 当key为Object时，存在 `equals()`一致，但hashCode不一致，导致查空，这种问题比较隐蔽

```java
Person p1 = new Person("Tom", 18);
Person p2 = new Person("Tom", 18);

map.put(p1, "A");
System.out.println(map.get(p2)); // ❌ null

```

> 扩展：：[Java hashCode() 和 equals()的若干问题解答](https://www.cnblogs.com/skywang12345/p/3324958.html)

##### -String

###### ⭐️String、StringBuffer、StringBuilder 的区别？

`String` 是不可变的	`private final byte[] value;`

`StringBuilder` 与 `StringBuffer` 都继承自 `AbstractStringBuilder` 类。

线程安全

>  `String` 常量，线程安全。`StringBuffer` 对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。`StringBuilder`未加。

性能

> 对 `String` 改变的时候，都会生成一个新的 `String` 对象。     `StringBuffer` 每次都会对 `StringBuffer` 对象本身进行操作。

###### ⭐️字符串拼接用“+” 还是 StringBuilder?

> 通过“+”的字符串拼接方式，实际上是通过 `StringBuilder` 调用 `append()` 方法实现的，拼接完成之后调用 `toString()` 得到一个 `String` 对象 。
>
> **编译器不会创建单个 `StringBuilder` 以复用，会导致创建过多的 `StringBuilder` 对象**。
>
> 而手动创建StringBuilder就不会出现上面问题

```java
String[] arr = {"he", "llo", "world"};
StringBuilder s = new StringBuilder();
for (String value : arr) {
    s.append(value);
}
System.out.println(s);
```

###### `String.intern()`

`intern()` 方法的主要作用是确保字符串引用在常量池中的唯一性。

当调用 `intern()` 时，如果常量池中已经存在相同内容的字符串，则返回常量池中已有对象的引用；否则，将该字符串添加到常量池并返回其引用。

```java
String s1 = new String("ab");  // 堆中对象
String s2 = s1.intern();       // 常量池中没有 "ab"
String s3 = "ab";              // 引用常量池对象

System.out.println(s1 == s2); // ✅ true (JDK 7+)
System.out.println(s2 == s3); // ✅ true
```

[String 类型的变量和常量做“+”运算时发生了什么？](https://javaguide.cn/java/basis/java-basic-questions-02.html#string-类型的变量和常量做-运算时发生了什么)

#### Java基础(下)

##### -异常

**Java 异常类层次结构图概览**：

![Java 异常类层次结构图](Screenshot/types-of-exceptions-in-java.png)

###### Exception 和 Error 有什么区别？

在 Java 中，所有的异常都有一个共同的祖先 `java.lang` 包中的 `Throwable` 类。`Throwable` 类有两个重要的子类:

- **`Exception`** :程序本身可以处理的异常，可以通过 `catch` 来进行捕获。`Exception` 又可以分为 Checked Exception (受检查异常，必须处理) 和 Unchecked Exception (不受检查异常，可以不处理)。
- **`Error`**：`Error` 属于程序无法处理的错误 ，我们没办法通过 `catch` 来进行捕获不建议通过`catch`捕获 。例如 Java 虚拟机运行错误（`Virtual MachineError`）、虚拟机内存不够错误(`OutOfMemoryError`)、类定义错误（`NoClassDefFoundError`）等 。这些异常发生时，Java 虚拟机（JVM）一般会选择线程终止.

> Error              ← serious, unrecoverable (JVM/internal)
>
> Checked Exception: checked at compile time
>
> Unchecked Exception(All inside `RuntimeException`): checked at runtime;

​	

###### Checked Exception

**Checked Exception** 即 受检查异常 ，Java 代码在编译过程中，如果受检查异常没有被 `catch`或者`throws` 关键字处理的话，就没办法通过编译。

###### Unchecked Exception

`RuntimeException` 及其子类都统称为非受检查异常，常见的有（建议记下来，日常开发中会经常用到）：

- `NullPointerException`(空指针错误)
- `IllegalArgumentException`(参数错误比如方法入参类型错误)
- `NumberFormatException`（字符串转换为数字格式错误，`IllegalArgumentException`的子类）
- `ArrayIndexOutOfBoundsException`（数组越界错误）
- `ClassCastException`（类型转换错误）
- `ArithmeticException`（算术错误）
- `SecurityException` （安全错误比如权限不够）
- `UnsupportedOperationException`(不支持的操作错误比如重复创建同一用户)

###### 更倾向于选择哪种？

默认使用 Unchecked Exception，只在必要时才用 Checked Exception。

我们可以把 Unchecked Exception（比如 `NullPointerException`）看作是代码 Bug。对待 Bug，最好的方式是让它暴露出来然后去修复代码，而不是用 `try-catch` 去掩盖它



###### ⭐️异常使用有哪些需要注意的地方？

- 不要把异常定义为静态变量，因为这样会导致异常栈信息错乱。每次手动抛出异常，我们都需要手动 new 一个异常对象抛出。
- 抛出的异常信息一定要有意义。
- 建议抛出更加具体的异常，比如字符串转换为数字格式错误的时候应该抛出`NumberFormatException`而不是其父类`IllegalArgumentException`。
- 避免重复记录日志：如果在捕获异常的地方已经记录了足够的信息（包括异常类型、错误信息和堆栈跟踪等），那么在业务代码中再次抛出这个异常时，就不应该再次记录相同的错误信息。重复记录日志会使得日志文件膨胀，并且可能会掩盖问题的实际原因，使得问题更难以追踪和解决。



