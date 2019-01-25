+++
draft = false
image = ""
showonlyimage = false
date = "2016-11-05T19:50:47+05:30"
title = "Java 语法"
writer = "子适"
categories = [ "code" ]
weight = 4
+++

## 一、基础语法

### 1.1 约定

- 类名每个单词首字母大写，文件名必须和类名匹配
<!--more-->
- 方法名以小写字母开头
- `public static void main(String args[])` —— java 入口

### 1.2 修饰符

- 可访问
  - 默认
  - 仅对类可见(private)
  - 全部可见(public)
  - 对封装和子类可见(protected)
- 不可访问
  - Java 提供一些不可访问描述符来满足其他功能。
  - Static 描述符是用来创造类方法和变量的。
  - Final 描述符用来最终确定和实施类、方法和变量的。
  - Abstract 描述符用来创造不允许实例化的类和方法。
  - synchronized 和 volatile 描述符用来当做线的。

### 1.3 变量

#### 1.3.1 按来源分类

##### 原始数据类型

- byte
- short、int、long、float、double
- boolean
- char
- 有效声明

```java
int a, b, c; 
int a = 10, b = 10; 
byte B = 22; 
double pi = 3.14159; 
char a = 'a'; 
```



##### 引用数据类型

- 用于访问对象
- 类对象和数组都属于 

#### 1.3.2 按照位置分类

##### 本地变量

- 在方法、构造器或者块内声明

##### 实例变量

- 类中声明，但在方法、构造器或者块外
- 实例创建时被创建

##### 类变量（静态变量）

- 在类中用 `static`关键字声明。在方法、构造器或者块外
- 每个类中只有同一个类变量，不管有多少个对象
- 除了作为常量被声明之外，类变量很少被应用。常量是被作为 public、private, final 和 static 被声明的变量。实例变量的初始值不会被改变。
- 静态变量可以用类的名称访问。ClassName.VariableName

### 1.4 数组

- 声明方法

```java
dataType[] arrayRefVar;   // preferred way.
dataType arrayRefVar[];  //  works but not preferred way.

myList = new int[4]
int[] myList = {1,2}

```

- 数组方法

| SN   | 方法和描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | public static int binarySearch (Object[] a, Object key) 使用二进制搜索算法搜索对象的指定数组（字节，整数，双精度等）来指定值。该数组必须在进行此调用之前进行分类。如果它被包含在列表 (-(insertion point + 1)， 将返回索引搜索关键字。 |
| 2    | public static boolean equals (long[] a, long[] a2) 如果多头的两个指定数组彼此相等返回true。两个数组认为是相等判定方法：如果两个数组包含相同的元素数目，并在两个数组元素的所有相应对相等。如果两个数组相等，返回true。同样的方法可以用于所有其它的原始数据类型 (Byte, short, Int, etc.) |
| 3    | public static void fill(int[] a, int val) 将指定的int值到指定的int型数组中的每个元素。同样的方法可以用于所有其它的原始数据类型(Byte, short, Int etc.) |
| 4    | public static void sort(Object[] a) 将对象指定的数组升序排列，根据其元素的自然顺序。同样的方法可以用于所有其它的原始数据类型( Byte, short, Int, etc.) |

### 1.5 枚举

### 1.6 语句

- 增强 for 循环

```java
int [] numbers = {1,2,3}
for(int x : numbers){
    
}
```

- if

```java
if....
else if
else
```

- switch

```java
switch(expression){
    case value :
        //
       break; //optional
    default : //Optional
}
```

### 1.7 包装类

#### 1.7.1 Number 类

![number_classes](/Users/cshi/Desktop/学习笔记/assets/number_classes.jpg)

- 编译器处理将数据包装进包装类的过程——装箱

```java
public class Test{

   public static void main(String args[]){
      Integer x = 5; // boxes int to an Integer object
      x =  x + 10;   // unboxes the Integer to a int
      System.out.println(x); 	//15
   }
}
```

- Number 方法——常用

| SN   | 方法描述                                                     |
| ---- | ------------------------------------------------------------ |
| 1    | xxxValue()  这个Number对象的值转换为XXX的数据类型并返回      |
| 2    | compareTo()  把这个Number对象与参数做比较                    |
| 3    | equals()  确定这个数字对象是否等于参数                       |
| 4    | valueOf()  返回一个Integer对象持有指定的原始值               |
| 5    | toString()  返回表示指定的int或整数的值的String对象          |
| 6    | parseInt()  此方法用于获取某个字符串的原始数据类型           |
| 7    | abs()  返回参数的绝对值                                      |
| 8    | ceil()  返回的最小整数大于或等于该参数。返回为double         |
| 9    | floor()  返回的最大整数小于或等于该参数。返回为double        |
| 10   | rint()  返回的整数，它是最接近值该参数值。返回为double       |
| 11   | round()  返回最接近的long或者int，通过该方法的返回类型所指参数 |
| 12   | min()   max() 返回两个参数中较小/大的                        |
| 13   | sqrt()  返回参数的平方根                                     |
| 14   | exp()  返回自然对数的底数e，该参数的幂值                     |
| 15   | log()  返回参数的自然对数                                    |
| 16   | pow()  返回第一个参数的提高至第二个参数的幂值                |

#### 1.7.2 Character 类

```java
Character ch = new Character('a');
```

- Character 方法

| SN   | 方法描述                                                     |
| ---- | ------------------------------------------------------------ |
| 1    | isLetter()  确定具体的char值是一个字母                       |
| 2    | isDigit()  确定具体的char值是一个数字                        |
| 3    | isWhitespace() 确定具体的char值是一个空格                    |
| 4    | isUpperCase() 确定具体的char值是一个大写字母                 |
| 5    | isLowerCase() 确定具体的char值是一个小写字母                 |
| 6    | toUpperCase() 返回指定字符值的大写形式                       |
| 7    | toLowerCase() 返回指定字符值的小写写形式                     |
| 8    | toString() 返回代表指定的字符值的一个String对象,即一个字符的字符串 |

### 1.8 字符串 String

- 构造

```java
String greeting = "Hello";
char [] helloArray = {'h','e','l','l','o'};
String helloString = new String(helloArray)
```

- String 类是不可变的。修改的字符串，应用 StringBuffer 和 StringBuilder 类

- 长度—— `helloStirng.length()`

- 连接字符串——

  ```java
  string1.concat(string2)
  ```

  - ```java
    "Hello," + " world" + "!"
    ```

- 字符串方法

- 太多了 ，见  ( String 类方法 )[http://wiki.jikexueyuan.com/project/java/strings.html]

  常用——`char charAt(int index) ` 返回指定索引处的字符。

### 1.9 日期和时间

- Date 类
- 构造函数
  - `Date()`——初始化对象的当前日期时间
  - Date(long millisec)—— 接收一个参数等于自 1970 年 1 月 1 日午夜起已经过的毫秒数
- 常用方法—— `.toString()`
- 格式化日期—— SimpleDateFormat 类

```java
Date dNow = new Date( );
SimpleDateFormat ft = 
      new SimpleDateFormat ("E yyyy.MM.dd 'at' hh:mm:ss a zzz");
```

- 休眠10秒 —— `Thread.sleep(5*60*10); `

## 二、面向对象

### 2.1 继承

- `extends` —— 继承类，Java 只能单继承，即只能继承一个类
- `implements`——继承接口，可以继承多个接口

### 2.2 重写方法

- 前提：父类中的方法没有加 final 
- 规则：
  - 参数列表完全相同
  - 重写函数访问级别不能大于原函数
  - `static` 方法不能被重写
  - 构造函数不能重写
- `super`关键字——指向继承的父类

```java
class Animal{
   public void move(){
      System.out.println("Animals can move");
   }
}

class Dog extends Animal{
   public void move(){
      super.move(); // invokes the super class method
      System.out.println("Dogs can walk and run");
   }
}
```

### 2.3 多态

- 对象可以有多种形态。
- 最常用的，一个实例因为继承了类或多个接口，故可以用不同的父类来引用它。

### 2.4 抽象类和抽象方法

- 抽象类

  - 不能被实例话，必须继承使用

  - ```java
    public abstract class Employee{
        
    }
    
    public class Salary extends Employee{
        
    }
    ```

- 抽象方法

  - 只声明，不实现，实现交给继承类去做/

  - ```java
    public abstract class Employee
    {
       public abstract double computePay();
       //Remainder of class definition
    }
    ```

  - 如果一个类中含有一个抽象方法，类必须也是抽象的。

  - 任何一个子类必须覆盖这个抽象方法，或者继续将它声明为抽象方法。

  ```java
  public class Salary extends Employee
  {
     private double salary; // Annual salary
     public double computePay()
     {
        System.out.println("Computing salary pay for " + getName());
        return salary/52;
     }
  
  }
  ```

  ### 2.5 接口

  ```java
  public interface NameOfInterface	// 默认是 public 的
  {
      void NameOfAction();	// 默认是 public 的
     //Any number of final, static fields
     //Any number of abstract method declarations\
  }
  ```

  

  - 接口是抽象方法的集合。实现了接口的类必须继承所有抽象方法
  - 接口不能包含实例变量。接口中唯一能出现的变量必须被同时声明为 static 和 final 。
  - 一个接口可以继承多个接口—— `extends`

  ### 2.6 包

  - 两个位于同一个包内的类，直接引用
  - 不再同一个包内

  ```java
  import payroll.*;
  import payroll.Employee;
  ```

  ### 2.7 嵌套类

  - java 支持嵌套类，在类内定义一个类

  ```java
  class OuterClass{
      ...
      class NestedClass{
          ...
      }
  }
  ```

  - 嵌套类分为静态和非静态

    - 有 `static` 修饰符修饰的——静态嵌套类，不能直接引用外部类定义的实例变量和方法。

    ```java
    OuterClass.StaticNestedClass	// 访问方法
    
    ```

    - 没有 `static` 修饰——内部类，可以访问外部类的成员(即使`private`修饰的)，实例化内部类，必须先实例化外部类。

    ```java
    OuterClass.InnerClass innerObject = outerObject.new InnerClass();
    ```

  - 内部类还有两种类型——局部类和匿名类，在方法体内声明

    - 局部类再块中（大部分时候是方法中）声明。可以访问方法的参数。

    - 匿名类——只使用一次的局部类，推荐使用匿名类。代码简洁，可同时声明和实例化。

      ```java
      interface HelloWorld{
          public void greet();
          public void greetSomeone(String someone);
      }
      
      public void sayHello(){
          // 局部类的声明和实例化
          class EnglishGreeting implements HelloWorld{
              ...
          }
          
          HelloWorld englishGreeting = new EnglishGreeting();
       // 匿名类 声明+实例化
          HelloWorld frenchGreeting = new HelloWorld(){	// new 运算符， 接口没有构造器，加一对空括号
              String name = "tout le monde";
              public void greet(){
                  ...
              }
              ...
          };	// 分号结尾说明这是一条语句
          
      }
      ```

  - Lambda 表达式

  ## 三、 java 进阶

  ### 3.1 集合

  - 一个集合框架是一个统一的体系结构表示和操作的集合
  - 集合框架= 集合接口 + 集合类 + 算法
  - Collection 接口

  | SN   | 接口描述                                                     |
  | ---- | ------------------------------------------------------------ |
  | 1    | **Collection 接口** 这让你可以使用对象组；它是集合层次阶段的顶端 |
  | 2    | **List 接口** 它继承了 Collection 并且 List 的一个实例存储了元素的一个有序集合 |
  | 3    | **Set** 它继承了 Collection 来处理集，它必须含有特殊的元素   |
  | 4    | **SortedSet** 它继承了 Set 来处理 排序的 set                 |
  | 5    | **Map** 它将独特的键和值匹配                                 |
  | 6    | **Map Entry** 这描述了映射中的一个元素(一个键值对)。它是 Map 的一个内部类。 |
  | 7    | **SortedMap** 它继承了 Map 因此键按升序保持                  |
  | 8    | **Enumeration** 它是旧有的接口并定义了你可以在对象的集合中列举(一次获得一个)元素的方法。这个旧有的接口被迭代器取代了。 |

  - Collection 类

  | SN   | 类描述                                                       |
  | ---- | ------------------------------------------------------------ |
  | 1    | **AbstractCollection** 实现大部分的 Collection 接口          |
  | 2    | **AbstractList** 继承 AbstractCollection 并且实现大部分 List 接口 |
  | 3    | **AbstractSequentialList** 通过一个使用有序的而不是随机访问它的元素的集合继承 AbstractList |
  | 4    | **LinkedList** 通过继承 AbstractSequentialList 实现一个链表  |
  | 5    | **ArrayList**  通过继承 AbstractList 实现一个动态数组        |
  | 6    | **AbstractSet** 继承 AbstractCollection 并实现大部分的 Set 接口 |
  | 7    | **HashSet** 用一个哈希表继承 AbstractSet                     |
  | 8    | **LinkedHashSet** 继承 HashSet 来允许插入顺序迭代            |
  | 9    | **TreeSet** 实现在树中存储的一个集。继承 AbstractSet         |
  | 10   | **AbstractMap** 实现大部分的 Map 接口                        |
  | 11   | **HashMap** 用一个哈希表继承 AbstractMap                     |
  | 12   | **TreeMap** 用一棵树继承 AbstractMap                         |
  | 13   | **WeakHashMap** 用一个使用弱键的哈希表来继承 AbstractMap     |
  | 14   | **LinkedHashMap** 继承 AbstractMap 来允许插入顺序迭代        |
  | 15   | **IdentityHashMap** 继承 AbstractMap 类并且当比较文档时平等使用参考 |

  - 算法

  [集合算法](https://www.tutorialspoint.com/java/java_collection_algorithms.htm)

  - #### 遍历集合——Iterator

    - 每个集合都提供了 `.iterator()`方法，该方法返回一个指向集合开头的迭代器。
    - 使用步骤：

    ```java
     Iterator itr = al.iterator();
          
          while(itr.hasNext()) {
             Object element = itr.next();
             System.out.print(element + " ");
          }
    
    ```

    - Iterator 迭代器声明的方法

    | Sr.No. | 方法和描述                                                   |
    | ------ | ------------------------------------------------------------ |
    | 1      | **boolean hasNext（）**如果有更多元素，则返回true。否则，返回false。 |
    | 2      | **对象下一个（）**返回下一个元素。如果没有下一个元素，则抛出NoSuchElementException。 |
    | 3      | **void remove（）**删除当前元素。如果尝试调用remove（）之前没有调用next（），则抛出IllegalStateException。 |

    - `ListIterator` 声明的方法

    | Sr.No. | 方法和描述                                                   |
    | ------ | ------------------------------------------------------------ |
    | 1      | **void add（Object obj）**将obj插入元素前面的列表中，该元素将在下一次调用next（）时返回。 |
    | 2      | **boolean hasNext（）**如果有下一个元素，则返回true。否则，返回false。 |
    | 3      | **boolean hasPrevious（）**如果有前一个元素，则返回true。否则，返回false。 |
    | 4      | **对象下一个（）**返回下一个元素。如果没有下一个元素，则抛出NoSuchElementException。 |
    | 5      | **int nextIndex（）**返回下一个元素的索引。如果没有下一个元素，则返回列表的大小。 |
    | 6      | **对象上一个（）**返回前一个元素。如果没有前一个元素，则抛出NoSuchElementException。 |
    | 7      | **int previousIndex（）**返回前一个元素的索引。如果没有前一个元素，则返回-1。 |
    | 8      | **void remove（）**从列表中删除当前元素。如果在调用next（）或previous（）之前调用remove（），则抛出IllegalStateException。 |
    | 9      | **void set（Object obj）**将obj分配给当前元素。这是调用next（）或previous（）最后返回的元素。 |

### 3.2 泛型 Generic

#### 基础

- 核心意义——参数化的类型

```java
class Gen<T>{
    T ob;
    Gen(T o){
        ob = 0;
    }
}

Gen<Integer> iOb;
iOb = new Gen<Integer> (88)	// 此处 88 自动装箱为 Integer 对象

```

- 不能引用基本类型（int , double 等），但装箱后可以。
- 受限的泛型——有限的类型参数

```java
<T extends superclass>

```

- 返回三个`Comparable`对象中最大的泛型

```java
public class MaximumTest
{
   // determines the largest of three Comparable objects
   public static <T extends Comparable<T>> T maximum(T x, T y, T z)
   {                      
      T max = x; // assume x is initially the largest       
      if ( y.compareTo( max ) > 0 ){ max = y; }
      if ( z.compareTo( max ) > 0 ){ max = z; }
      return max; // returns the largest object   
   }
    
   public static void main( String args[] )
   {
      System.out.printf( "Max of %d, %d and %d is %d\n\n", 
                   3, 4, 5, maximum( 3, 4, 5 ) );

      System.out.printf( "Max of %s, %s and %s is %s\n","pear",
         "apple", "orange", maximum( "pear", "apple", "orange" ) );
   }
}

```

#### 泛型类

```java
public class Box<T> {
  private T t;
  public void add(T t) {
    this.t = t;
  }
  public T get() {
    return t;
  }
 
    public static void main(String[] args) {
         Box<Integer> integerBox = new Box<Integer>();
         Box<String> stringBox = new Box<String>();

         integerBox.add(new Integer(10));
         stringBox.add(new String("Hello World"));

         System.out.printf("Integer Value :%d\n\n", integerBox.get());
         System.out.printf("String Value :%s\n", stringBox.get());
      }
}

```

### 3.3 匿名函数 Lamdba

### 3.4 流 Stream

### 3.5 并发编程

### 3.6 注解 annotation

- 不会直接影响所注解的代码的行为。
- 作用——为编译器提供信息，编译时和部署时处理，运行时处理。
- 格式

```java
@Entity	//普通

@Author(name = "shi",
       date = "2019")	// 带参数的注解
class MyClass(){...}

@SuppressWarnings("unchecked")	// 如果只有一个参数，且元素名为 value ,可以省略名

```

- 定义注解

```java
@interface ClassPreamble{
    String author();
    String date();
    int currentRevision() default 1;	// 默认值
    ...
}

//使用
@ClassPreamble(
	author = "shi",
...
)
public class ...

```

- Java.lang 中预定义的注解常用
  - `@Deprecated`——元素已被弃用
  - `@Override`——该元素覆盖了超类中声明的元素
  - `@SuppressWarning`——通知编译器忽略指定类型的警告
- 用来注解注解的注解——元注解 `java.lang.annotation`
  - `@Retation`
  - `@Documented`
  - `@Target`
  - `@Inherited`

## static

在JVM加载类的时候，若该类存在static修饰的成员变量和成员方法，则会为这些成员变量和成员方法在固定的位置开辟一个固定大小的内存区域，

被static修饰的成员变量和成员方法独立于该类，**不依赖于某个特定的实例变量，也就是说它被该类的所有实例共享。所有实例的引用都指向同一个地方，任何一个实例对其的修改都会导致其他实例的变化。**

static 修饰的变量和方法可以直接通过类名访问。

## Optional类

Optional 类是一个可以为null的容器对象。如果值存在则isPresent()方法会返回true，调用get()方法会返回该对象。

Optional 是个容器：它可以保存类型T的值，或者仅仅保存null。Optional提供很多有用的方法，这样我们就不用显式进行空值检测。

```
public MyClass findById(int id){
        Optional<MyClass> myClass=myClasses.stream().filter(m->m.getId()==id).findFirst();
        if(myClass.isPresent()){
            return myClass.get();
        }
        else{
            return null;
        }
    }

```
