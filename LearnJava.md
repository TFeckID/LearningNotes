# Java：从入门到问灵

## Java SE

### Eclipse使用

- 常用快捷键

```java
CTRL+ALT+↓ //向下复制一行
CTRL+ALT+↑ //向上复制一行
```

- 如何生成jar包并导入项目

  - jar的概念：jar是多个class文件的压缩包

  - jar的作用：可以利用别人写好的东西

  - 生成jar包：选中项目-->右键-->Export-->Java-->Jar-->指定保存路径和名    

    ​                    称-->Finish

  - 导入jar包：复制到项目路径下并添加至构建路径(BuildPath)

### 注释与API文档生成

- 注释标记
  - //   单行注释     将单行注释符后的一整行声明为注释，只能声明一行
  - /* ...... */  多行注释  将多行注释符中间的内容声明为注释，可以声明多行
  - /** ...... */  文档注释  一般用于变量，方法，接口以及类本身前面。作用一是解释注释后的语句块的作用；而是便于生成Java API文档。

    - 文档注释的使用为：在要添加文档注释的代码块的上一行敲下/**接着按回车，这样就能生成对应代码块的文档注释
- 生成Java API文档
  - 通过Eclipse生成文档：
    - 

### 数据类型



### 数组

各类型数组初始化值

|  byte   |   0    |
| :-----: | :----: |
|  short  |   0    |
|   int   |   0    |
|  long   |   0    |
|  float  |  0.0   |
| double  |  0.0   |
| boolean | false  |
|  char   | 空字符 |
| String  |  null  |

### switch...case

> JDK1.7之前只能由int，byte，short，char作为判断条件。
>
> JDK1.8之后可以由String作为判断条件，不能由long作为条件。

### 面向对象概述

- 成员变量和局部变量的区别

  - 在类中位置不同，成员变量在类中方法外，局部变量在方法中定义
  - 内存中位置不同，成员变量在堆内存，局部变量在栈内存
  - 生命周期不同，成员变量随对象的创建（消失）而创建（消失），局部变量随方法的调用而存在，随方法执行完毕而消失
  - 初始化值不同，成员变量有默认初始化值，局部变量没有初始化值，必须赋值后才能使用

- 注意事项

  - 局部变量可以和成员变量同名，在方法中使用时采用就近原则
  - 基本数据类型

  | 数据类型 | 占用字节 | 默认值 | 数据类型 | 占用字节 | 默认值 |
  | :------: | :------: | :----: | :------: | :------: | :----: |
  |   byte   |          |   0    |  short   |          |   0    |
  |   int    |          |   0    |   long   |          |   0    |
  |  float   |          |  0.0   |  double  |          |  0.0   |
  |   char   |          | \u0000 | boolean  |          | false  |

  - 引用数据类型包括：数组，类，接口，枚举

### 代码块的概述分类

- 代码块概述：
  + 使用{}括起来的代码称为代码块
- 代码块分类
  * 根据位置及声明不同，分为局部、构造、静态和同步代码块
- 代码块应用：
  * 局部代码块：
    + 在方法中出现，限定变量生命周期，及早释放，提高内存利用率
  * 构造代码块：
    + 类中方法外出现，多个构造方法中相同的代码存放在一起，每次构造都执行，并在构造前执行
  * 静态代码块：
    + 在类中方法外出现，加了static修饰符
    + 在类中方法外执行，加了static修饰符，用于给类初始化，只执行一次
    + 随着类加载而加载并同时运行
    + 一般用于加载驱动
    + 优先于主方法执行
    + 加载顺序：静态代码块>构造代码块(>构造方法)>局部代码块

### 类的继承

- 继承(extends)
  - super()默认走父类的空参构造，若没有空参构造，需在super()中指定参数
  - this()访问本类的有参或无参构造
- 继承中成员方法关系

  - 子类可使用同名方法重写父类方法，并可用super()访问父类方法

  - final关键字

    - 修饰类，类不能被继承
    - 修饰变量，变量变成常量,并且常与public static配合使用，目的方便访问常量。例 public static final int MAX_VALUE；
    - 修饰方法，方法不能被重写
    - final修饰变量初始化时机

    ​    ① 声明时显式初始化

    ​    ② 构造函数内初始化

### 类的多态

- 当方法形参时用多态，可以适配不同的子类对象，保证代码扩展性

  - instanceof关键字，用于判断对象是否属于某类，

    用法：  <对象名>  instanceof  <类名>
  
- 静态多态与动态多态

  - 静态多态：方法重载
  - 动态多态：方法重写；动态绑定。

### 抽象类

+ 抽象类的特点
  - 类名和方法名前必须用abstract关键字修饰
    * abstract class <name>
    * asbtract void method(){ }
  - 抽象类不能被实例化
    * 按照多态的方法，由具体子类实例化
  - 抽象类不一定有抽象方法，有抽象方法的一定是抽象类或接口
  - 抽象类的子类要么是抽象类，要么重写所有抽象方法
+ 抽象类的成员特点
  - 成员变量：可以是变量或常量，abstract不能修饰成员变量
  - 有构造方法，用于子类初始化父类成员
  - 成员方法可以是抽象或非抽象
  - 抽象类的成员方法特性
    * 抽象方法：子类继承后必须重写才能执行
    * 非抽象方法：子类继承可直接调用，也可重写，提高代码复用性
    * 当无法描述一个方法时，就定义为抽象方法
+ 抽象类总结：拥有抽象方法的类一定是抽象类，抽象类一旦被继承，必须对里面的抽象方法进行重写

### 接口定义及特点

* 接口特点

  - 接口用关键字interface声明

       ```java
  interface <interfaceName> {}
       ```

  - 类实现接口用implements关键字

    ```java
    class <className> implements <interfaceName>
    ```

  - 接口不能直接实例化

  - 接口的子类可以是抽象类，也可以是具体类，具体类要重写接口中的所有方法

* 成员特点

  + 成员变量只能是常量，并且是静态且公共的

    - 默认修饰符：public static final
    - 变量默认为公共静态常量，但建议手动指定修饰符

  + 成员方法：只能是抽象方法

    + 接口中没有构造方法

    + 默认修饰符：public abstract
    + 方法默认为公共抽象方法，但建议手动指明修饰符

* 类与类，接口与接口，接口与类的关系

  + 类与类：

    - 继承关系，只能单继承，可以多层继承

      ```java
      class A{}
      class B extend A{}
      class C extend B{}
      ```

  + 类与接口：

    + 实现关系，类实现接口，可以单实现，也可以多实现

      ```java
      interface InterA{}
      interface InterB{}
      class A implements InterA,InterB{}
      ```

    + 可以在继承一个类的同时实现多个接口

      ```java
      class B extend A implements InterA,InterB{}
      ```

  + 接口与接口

    + 继承关系，可以单继承，也可以多继承

### 抽象类与接口的区别

+ 成员区别
  - 抽象类：
    - 成员变量：可以是变量，也可以是常量
    - 有构造方法
    - 成员方法：可以是抽象，也可以是非抽象
  - 接口：
    - 成员变量：只可以是常量
    - 成员方法：只可以是抽象方法
+ 关系区别
  - 类与类：
    - 继承关系，且只能单继承
  - 类与接口
    - 实现关系，可以单实现，也可多实现
  - 接口与接口
    - 继承关系，可以单继承，也可多继承
+ 设计理念区别
  - 抽象类   被继承体现的是"is a "的关系，抽象类中定义的是该继体系的共性功能
  - 接口       被实现的是"like a"的关系，接口中定义的是该继承体系的扩展功能

### 四种权限修饰符的作用

|                    | 本类 | 同一个包下子类与无关类 | 不同包下子类 | 不同包下无关类 |
| :----------------: | :--: | :--------------------: | :----------: | :------------: |
|      private       |  Y   |                        |              |                |
| 默认不写任何修饰符 |  Y   |           Y            |              |                |
|     protected      |  Y   |           Y            |      Y       |                |
|       public       |  Y   |           Y            |      Y       |       Y        |

- 常见修饰符组合
  - 权限修饰符：private，默认，protected，public
  - 状态修饰符：static，final
  - 抽象修饰符：abstract

### 内部类的概述和特点

- 在类内定义的类称为内部类
- 定义内部类对象的格式

```java
class Outer {
    class Inner {
        ...
    }
}
Outer.Inner oi = new Outer().new Inner() //定义一个内部类对象
```

- 内部类的访问特点

  - 内部类可直接访问外部类的成员，包括私有成员，此时内部类相当于一个外部类的方法；外部类不能直接访问除静态公有成员以外的内部类成员，但可在外部类方法内创建内部类对象。

- 内部类私有的访问情况

  - 当内部类的权限为私有时，不能通过直接创建对象的形式访问内部类的成员，应当通过在外部类中创建公有方法并在方法内创建内部类对象的方式访问

- 内部类为静态成员

  - 内部类为静态，但内部类成员为非静态时，调用格式为

  ```java
  class Outer {
      static class Inner {
          public void method() {
              ...
          }
      }
  }
  Outer.Inner oi = new Outer.Inner(); /*这里其实是Outer.new 	Inner(),因为内部类为静态成员，不需要先创建外部类对象即可访问，只    创建了一个内部类对象以访问内部类非静态成员方法*/
  oi.method();
  ```

  - 内部类与内部类成员都为静态时，调用格式为

  ```java
  class Outer {
      static class Inner {
          public static void method() {
              ...
          }
      }
  }
  Outer.Inner.lethod(); //一路类名调用，不需要创建内外类对象
  ```

- 面试案列

```java
/*分别输出10,20,30*/
class Outer {
	public int num = 10;
	class Inner {
		public int num = 20; 
		public void method() {
			int num = 30;
			System.out.println(Outer.this.num);
            System.out.println(this.num);
            System.out.println(num);
		}
	}
}
/*内部类可通过使用 外部类名.this 引用来访问外部类成员*/
```

- 局部内部类的定义及概述

  - 定义：在外部类成员方法内定义的类称为局部内部类
  - 局部内部类只能在其所定义的方法内部访问
  - 局部类在访问它所在的方法的局部变量时，局部变量必须用final修饰，但在JDK1.8取消了该设定

- 匿名内部类

  - 局部内部类的简化写法，使用前提是已经存在一个类或者接口，可以是具体类也可以是抽象类
  - 匿名内部类定义格式

  ```java
  new 类名或接口名() {
      重写方法;
  }.重写方法名();
  ```

  - 重写多个方法调用

    - 匿名内部类对号只针对只重写一个方法时的实现，多个方法时用有名内部类
    - 可以使用多态，即新建父类引用指向匿名类即可调用多个方法

    ```java 
    接口或父类名 类名 = new 父类名或接口名() {
        重写方法;
    };
    类名.方法名1();
    类名.方法名2();
    ...
    ```

### API概述

- API(Application Programming Interface)
  
  - 应用程序编程接口
- Java API
  
  - Java提供给我们使用的类，这些类将底层的实现封装了起来，我们不需要关心如何实现这些类，只需学习如何使用
  
  - 使用Java API
  
    > **1**：首先要找到相关类：**1**：通过索引去找 **2**：通过目录去找
    >
    > **2**：看清其中文定义
    >
    > **3**：查看类->abstract ,interface,final
    >
    > **4**：查看其类的特点
    >
    > **5**：如果当前类可以被实例化，则查看其构造函数
    >
    > **6**：点近相应构造方法查看具体参数表示
    >
    > **7**：根据需求查看普通方法

### Object类的概述

- Object类概念
  - 类层次结构的根类
  - 所有类方法都直接或间接继承自该类
  
- 构造方法
  
  ```java
  public Object();
  ```
  
- 成员方法
  
  ```java
  int hashcode(); //返回hash值
  Class<T> getClass(); //返回运行时类
  boolean equals(Object obj); //比较两个对象是否一致
  String toString(); //返回对象的字符串形式，重写该方法以实现自定义输出对象的属性
  ```
  

> **Native** **：**java native interface: **本地应用接口** **调用本地由其他语言书写方法**

### 对象克隆

> 创建出一个与当前对象属性及方法完全一致的对象副本

```java
protected native Object clone(); //方法声明 
```

#### 实现方式

1. 实现`Cloneable`接口
2. 重写`clone()`方法

#### 浅克隆和深克隆

- 浅克隆：只复制基本数据类型，引用数据类型的引用不变。
- 深克隆：对象内的基本数据和引用数据都被拷贝一份。
- 深克隆实现流程：
  1. 先实现对象的浅克隆；
  2. 在克隆方法内对对象内的引用对象进行克隆。



### String类的概述

> 字符串类，其被final所修饰，不能被继承。

> 字符串不能被改变，当创建一个字符串时，会先到常量区找有无相同的字符串，若没有则在常量区中新建一个。若以实例化方式新建字符串，其会在堆内和常量区创建对象。空串""也会被分配内存。

- String类的获取功能

  ```java
  int length(); //获取字符串长度
  char charAt(int index); //获取对应位置的字符
  boolean isEmpty();//字符串长度为0时返回true
  char charAt(int index); //获取索引对应位置的字符
  int indexOf(char ch); /*返回指定字符在字符串中第一次出现处的索引，若字符不存在，返回 -1。*/
  int indexOf(String str);/*获取指定字符串中第一个字符在该字符串中第一次出现处的索引，若不存在，返回 -1。*/
  int indexOf(String str,int fromIndex); /*获取指定字符串在对应索引之后第一次出现的位置的索引*/
  int indexOf(char ch，int fromIndex); /*获取指定字符在指定索引后第一次出现处的索引*/
  int lastIndexOf(char ch); /*从字符串最后向前查找指定字符第一次出现的位置*/
  String substring(int start);  /*从指定位置开始截取字符串，默认到行尾*/
  String substring(int start，int end);  /*从指定位置开始到指定位置前结束截取字符串 （包含头，不包含尾）*/
  boolean endsWith(String str); //判断是否以指定字符串结尾
  boolean startsWith(String str); //判断是否以指定字符串开头
  ```

- String类的转换功能

  ```java
  byte[] getBytes(); //把字符串转换成字节数组
  char[] toCharArray(); //把字符串转换为字符数组
  static String valueOf(Object); //把任意类型数据转换为字符串
  String toLowerCase(); //把字符串转换成小写
  String toUpperCase(); //把字符串转换成大写
  String concat(String str); //拼接字符串
  String trim();//去除首尾空格
  ```

- 各种不同的声明方式所在内存位置

  ```java
  String string = "Hello"; //常量区
  String str2 = "Hello"; //常量区
  String str4 = "He" + "llo"; //常量区
  String s5 = "He"; //常量区
  String s6 = "llo"; //常量区
  String str3 = new String("Hello"); //堆
  String s7 = s5 + s6; //堆
  String s8 = s5 + "llo"; //堆
  ```

### StringBuffer类

- StringBuffer类的定义

  一个线程安全的可变序列，类似于String的字符串缓冲区，不可更改（指不可像String那样随意连接），但可调用方法改变其长度和内容(append()等方法)

- String和StringBuffer的区别

  - String是一个不可变的字符序列
  - StringBuffer是一个可变的字符序列 

- StringBuffer的构造函数

  ```java
  public StringBuffer();  //无参构造，默认创建16字符容量
  public StringBuffer(int capacity);  //指定容量的StringBuffer对象
  public StringBuffer(String str);  //指定字符串的StringBuffer对象
  ```


- StringBuffer的方法

  ```java
  int capacity(); //返回缓冲区的容量
  int length(); //返回长度(字符数)
  StringBuffer append(String str); //将任意字符串添加进缓冲区并返回StringBuffer本身
  StringBuffer insert(int offset, String str); //在指定位置将任意类型的数据插入缓冲区并返回其本身
  StringBuffer deleteCharAt(int index); //删除索引指向的字符
  StringBuffer delete(int start,int end); //删除两个索引之间的内容,包含头不包含尾
  StringBuffer replace(int start,int end,String str); //将索引区间的内容用str替换,包含头不包含尾
  StringBuffer reverse(); //字符串反转
  String substring(int index); //从索引位置截取字符串至末尾
  String substring(int start,int end); //从索引开始截取到索引结束，包括头不包括尾
  ```


### StringBuilder类

- 成员方法：与StringBuffer一致

- 与StringBuffer的区别：StringBuffer是jdk1.0版本的，线程安全，效率低

  ​					 StringBuilder是jdk1.5版本的，线程不安全，效率高

### Arrays类的概述和方法

- 概述：针对数组进行操作的工具类，提供排序，查找等方法

- 成员方法：

  ```java
  public static String toString(T[] arr); //数组转字符串
  public static void sort(T[] arr); //数组排序,只能升序排列
  public static int binarySearch(int[] arr, int key); //查找元素
  public static List<T> asList(T ... a); //返回由数组元素生成的集合
  public static void fill(T[] arr, T t); //使用指定的值填充整个数组
  ```


### 基本数据类型包装类

- 概述：将基本数据类型包装成对象以便于在其中定义更多的功能方法以更好地使用该数据

- 基本数据类型包装类有八种，其中七种有`parse`方法可以将其字符串表现形式解析为基本数据类型，`Character`没有该方法，原因是`char`无法存储多个字符

- 基本数据类型与包装类对应关系

  | 基本数据类型 |  包装类   |
  | :----------: | :-------: |
  |     byte     |   Byte    |
  |    short     |   Short   |
  |     int      |  Integer  |
  |     long     |   Long    |
  |    float     |   Float   |
  |    double    |  Double   |
  |     char     | Character |
  |   boolean    |  Boolean  |

- Integer常用方法

  ```java
  int intValue(); //以int形式返回该Integer对象的值
  static int parseInt(String s); //将字符串解析成有符号十进制整数
  static String toString(int i,int radix); //以指定进制(radix)输出对应整数的字符串表示
  static Integer valueOf(String s, int radix); //将指定进制(radix)整数的字符串表示转换成Integer对象
  static int max(int a,int b); //返回两数最大值
  static int min(int a,int b); //返回两数最小值
  static int compare(int a,int b); //比较a,b；若大于，返回1，等于返回0，小于返回-1
  ```

- JDK1.5新特性

  - 自动装箱与拆箱：将基本数据类型自动包装成包装类，或将包装类自动拆箱成基本数据类型
  
  - 如果数据的范围在byte的取值范围(-128,127之间)，自动装箱不会新创建对象，而是从常量池中获取，超过byte取值范围则会在堆中新创建对象
  
  - 缓存值
  
    | 数据类型  |   缓存值    |
    | :-------: | :---------: |
    |  Boolean  | true, false |
    |   Byte    |  -128~127   |
    |   Short   |  -128~127   |
    |  Integer  |  -128~127   |
    |   Long    |  -128~127   |
    | Character |    0~127    |
    |   Float   |  无缓存值   |
    |  Double   |  无缓存值   |
  
    

### 时间和日期类

#### Data 类概述与使用

> Data类是Java.util提供的封装当前日期和时间的类

------

- `Date`的构造方法

  ```java
  Date(); //创建当前时间的Date类对象
  Date(long date); //参数为1970年1月1日以来的毫秒数，即时间戳
  ```

- 

#### SimpleDateFormat的概述与使用

> 格式化时间和日期类

#### Calendar类的概述与使用

> Calendar：日历类，用于完成日期和时间的操作。是一个抽象类，单例模式，可以获取唯一的一个系统时间。

- 获取`Calendar`实例

  ```java
Calendar calendar = Calendar.getInstance();
  ```

- 常用方法

  ```java
  void add(int field,int offset); //给对应的字段增加对应的偏移量，自动计算增加后的日期
  void get(int field); //根据日期字段返回对应的日期值
  void set(int ... args); //手动设置日期和时间
```
  
- `Calendar`类中字段表

  |             字段              |                         含义                         |
  | :---------------------------: | :--------------------------------------------------: |
  |         Calendar.YEAR         |                      日期中的年                      |
  |        Calendar.MONTH         |                 日期中的月，需要加1                  |
  |         Calendar.DATE         |                      日期中的日                      |
  |         alendar.HOUR          |                日期中的小时(12小时制)                |
  |     Calendar.HOUR_OF_DAY      |                日期中的小时(24小时制)                |
  |        Calendar.MINUTE        |                     日期中的分钟                     |
  |        Calendar.SECOND        |                      日期中的秒                      |
  |     Calendar.WEEK_OF_YEAR     |                    当前年中星期数                    |
  |    Calendar.WEEK_OF_MONTH     |                    当前月中星期数                    |
  |     Calendar.DAY_OF_YEAR      |                   当前年中的第几天                   |
  |     Calendar.DAY_OF_MONTH     |                   当前月中的第几天                   |
  |     Calendar.DAY_OF_WEEK      | 当前星期的第几天(星期天表示第一天，星期六表示第七天) |
  | Calendar.DAY_OF_WEEK_IN_MONTH |                 当前月中的第几个星期                 |
  |                               |                                                      |

- 

### 枚举

> 定义枚举类是通过关键字`enum`实现的，我们只需依次列出枚举的常量名。

定义语法：

```java
enum <枚举类名>{
    枚举成员1, 枚举成员2...
}
```



### 正则表达式

> 正则表达式以`^`开头，以`$`结束的一个字符串。

- 正则表达式符号

  |  符号   |           作用            |                         用例                         |
  | :-----: | :-----------------------: | :--------------------------------------------------: |
  |   []    |       代表单个字符        |                   [abc]     a,b或c                   |
  |    .    |       任意一个字符        |                  .    任何一个字符                   |
  |   \d    |           数字            |            [\d]     0到9中的任何一个数字             |
  |   \D    |          非数字           |              [\D]   任何一个非数字字符               |
  |   \s    |         空白字符          |                                                      |
  |   \S    |        非空白字符         |                                                      |
  |   \w    |         单词字符          |             [0-9,a-z,A-Z,_ ]属于单词字符             |
  |   \W    |        非单词字符         |                                                      |
  |   X?    |      X出现一次或零次      |        [abc]？  abc中的任何字母出现一次或零次        |
  |   X*    |      X出现零次或多次      |        [abc]*  abc中的任何字母出现零次或多次         |
  |   X+    |      X出现一次或多次      |        [abc]+  abc中的任何字母出现一次或多次         |
  |  X{n}   |       X恰好出现n次        |      [abc]{5}   abc中的任何字符总共恰好出现5次       |
  | X{n，}  |       X至少出现n次        |       [abc]{5，}   abc中的任意字符至少出现5次        |
  | X{n，m} | X至少出现n次，但不超过m次 | [abc]{5,8}   abc中的任意字符整数出现5次，但不超过8次 |
  
- 正则表达式中的方法

  ```java
  String[] split(String reg); //根据给定的正则表达式切割字符串
  static replaceAll(String reg,String replacement); //根据正则表达式替换字符串中的元素
  ```

- 正则表达式的分组功能

  - （）可以将某一个或几个元素合成为一个组，在匹配时当成一个整体看待，\\ \\ n表示第n组又出现一次，比如 (.)\\\\ 1匹配 “哈哈” 这样的词，(.)\\\\1(.)\\\\2 匹配 ”高高兴兴“这样的词，(..)\\\\1 匹配 “高兴高兴”。
  - \$符号可以取得前面组的内容，通常用于replaceAll 方法中，\$n 代表取得第n组的内容，例 replaceAll("(.)\\\\1+","$1") 

- Pattern和Matcher的概述

  - 典型调用顺序：

    ```java
    Pattern p = Pattern.compile("a*b");  //获取正则表达式
    Matcher m = p.matcher("abbbbb");  //获取匹配器
    boolean b = m.matches();  //看是否匹配
    ```

  - 获取功能：

    ```java
    /*获取电话号码实例*/
    Pattern p = Pattern.compile(regex);  //获取电话号码正则表达式
    Matcher m = p.matcher(s);     //匹配源字符串
    while(m.find())
      System.out.print(m.group());
    /*
    find()   匹配源字符串，若找到匹配的子串，返回true
    group()  返回上一次匹配成功的子串，用于获取
    
    find和group必须搭配使用并且find要先于group执行
    */
    ```

### 常用工具类

#### Math类的概述和方法使用

- 概述：用于基本数学运算的工具类

- 成员方法

  ```java
  static int abs(int a); //返回绝对值
  static double ceil(double a); //对小数向上取整
  static double floor(double a); //对小数向下取整
  static int max(int a,int b);  //返回两数中的最大值
  static double pow(double a,double b); //返回a的b次方
  static double random(); //生成一个随机数
  static int round(float a); //四舍五入
  static double sqrt(double a); //返回a的开平方
  ```

#### System类的概述

- 成员：

  ```java
  System.in //标准键盘输入流
  System.out //标准输出流
  
  static void gc(); //运行垃圾回收器
  static void arraycopy(Object src,int srcPos,Object dest,int destPos,int length);
  /*数组拷贝*/
  ```

### Collection集合

- 集合的概述：

  集合是接口;数组的长度是固定的，因此java提供了集合可以存储任意对象，并且长度可变，随着对象数量增减

- 数组与集合的区别：

  - 数组可以存储基本数据和引用数据，基本数据存储值，引用数据存储指针
  - 集合只能存储引用数据(对象)，当存储基本数据时，会自动装箱
  - 数组长度固定，不能自动增长；集合长度可变，能自动增减

- 集合的体系

  - 根接口Collection
    - List(子接口，有序，存取顺序一致，有索引，可以存储重复数据)
      - ArrayList
        - 底层由数组实现
      - LinkList
        - 底层由链表实现
      - Vector
        - 同ArrayList，但时间较早，是线程安全的。
    - Set(子接口，无序，存取顺序不一致，无索引，不可存储重复数据)
      - HashSet

        - 由哈希算法实现

        ```java
        HashSet<E> hs = new HashSet();  
        ```

        - HashSet的存取顺序是不一致的，存入顺序和取出顺序不一定相同
        - 存入时先调用对象的hashCode()方法，计算并比较Hashcode，若相同，再调用equls()方法比较对象的属性，若相同，则属于同一对象；在存储自定义对象时，应重写这两个方法

      - TreeSet

        - 由二叉树实现，可以对元素进行排序
        - TreeSet不能直接存储自定义对象，若要存储自定义对象，对象所属类必须实现Comparable<T>接口，并重写compareTo()方法，以确保该类可比较。当此对象小于，等于或大于指定的比较对象时，compareTo方法返回一个负整数、零、正整数。

- 集合的方法

  ```java
  boolean add(E e) //将任意对象存进collection
  boolean remove(Object o) //删除指定元素
  void clear() //清空整个集合
  boolean contains(Object o) //如果包含指定元素，返回true
  boolean isEmpty()  //判断是否为空
  int size()  //返回集合长度，即集合内元素个数
  Object[] toArray(T []) //返回包含集合所有元素的数组
  boolean addAll(Collection c) //将集合c中的所有元素添加进当前集合
  boolean removeAll(Collection c) //
  boolean containsAll(Collection c) //
  boolean retainAll(Collection c) //取集合c与当前集合的交集，若调用的集合改变，返回true，若不                                   变，返回false；即当前集合为c的同集或子集时返回false
  ```

- 迭代器的使用（集合遍历）

  ```java
  Iterator iterator() //返回一个当前集合的迭代器
  Boolean hasNext() //是否有下一个元素
  Object next() //返回下一个元素
  ```

- List的特有方法

  ```java
  void add(int index,E element) //在指定的索引处添加一个元素，其后元素依次向后移一个单位;当使用									不存在的索引时，将出现索引越界异常;index小于等于size
  E remove(int index) //删除索引对应处的元素,并返回被删除的元素
  E get(int index) //返回索引对应处的元素
  E set(int index,E element) //修改指定位置的元素 ,并返回更改前的元素
  ListIterator listIterator() //返回一个ListIterator
  ```

  - 并发修改：使用迭代器遍历的同时集合在增减元素，称为并发修改,并发修改在普通的迭代器中是不被允许的，因为在开始生成迭代器时就已告知迭代器元素的总数，开始迭代后元素总数不可变。此时，可用ListIterator，此为List专有的迭代器，可以实现迭代的同时增减元素

  - LinkList特有的方法

    ```java
    void addFirst(E e) //从开头插入元素
    void addLast(E e) //从结尾插入元素
    E getFirst() //取得第一个元素
    E getLast() //取得最后一个元素
    E removeFirst() //删除第一个元素
    E removeLast() //删除最后一个元素
    ```

- Set
### 泛型的概述和使用

- 集合泛型

​       定义：集合泛型是指在定义集合时，在集合名前类型名后以<>标注此后集合内将存储的数据的类型，加了泛型的集合   将只能存储泛型内指定的对象。泛型内必须是引用数据类型。

```java
  Collection<String> arr = new ArrayList<>();
```

  泛型的优点：1、提高安全性，将运行期错误转到编译期

​			 2、省去强转麻烦

  - 泛型类的概述和定义

    将泛型定义在类上：

    ```java
    public class 类名<泛型类型>
    ```

    泛型必须是引用类型 ,泛型可以替代类中定义的成员变量数据类型，使之可以在创建对象时再定义类内的成员变量数据类型

- 泛型接口的概述和定义



### 反射

> 将类的各个部分(成员变量，构造方法，成员方法)封装为其他对象，称为反射机制。

反射的优点：

1. 可以在程序运行过程中操作这些对象
2. 可以解耦合，提高程序的可扩展性

反射机制将类的字节码文件封装为一个`Class`对象，其中有三个属性

|    属性     |             作用             |
| :---------: | :--------------------------: |
|    Field    | 将类中的成员变量封装为此对象 |
| Constructor |  将类的构造函数封装为此对象  |
|   Method    |    将成员方法封装为此对象    |

获取一个类的`Class`对象的三种方法

```java
<类名>.class //返回一个指定类名的类的Class对象
Class.forName(<包名+类名>)
object.getClass() //返回一个此对象所属类的Class对象
```

三种方法的使用场景:

      1. 常用于开发中的参数传递；
         2. 常用于配置文件中，例如数据库连接池中配置JDBC驱动
         3. 常用于开发中。

`Class`类中的成员方法

| 方法                                 |                作用                |            备注            |
| :----------------------------------- | :--------------------------------: | :------------------------: |
| Field[]  getDeclaredFields();        |     获取所有成员变量，返回数组     | 可以获取所有权限的成员变量 |
| Field[]  getFields();                | 获取所有public的成员变量，返回数组 |  只能获取public的成员变量  |
| Field  getField(String);             |       获取指定名称的成员变量       |  只能获取public的成员变量  |
| Method  getMethod(String, Obj.class) |  根据方法名和参数列表类型获取方法  |    只能获取public的方法    |
| Constructor[] getConstructors()      |          获取所有构造函数          |    只能获取public的构造    |

### 注解

- jdk内置的注解：

  ```java
  @Deprecated //表示资源已被取代
  @Override  //表示重写父类方法
  @SuppressWarnings("all") //忽略所有警告
  ```

- 自定义注解

  - 格式

    ```java
    元注解
    public @interface anno_name{}
    ```

  - 注解本质上是一个接口，它继承自`Annotation`接口

  - 元注解：用于描述注解的注解、

    - @Target：描述注解的作用位置
    - @Retention：描述注解被保留的阶段
    - @Document：描述注解是否被抽取到API文档中
    - @Inherited：描述注解是否被子类继承

  - 

- 

### Map的概述及用法

- 一个可变长度的键值对的双列集合
- HashMap：以哈希算法实现的Map
- TreeMap：以二叉树实现的Map，和TreeSet一样可以自动排序
- LinkedHashMap：按插入顺序排序的HashMap
- Map接口的方法

```java
V put(K key,V value) //根据键值对添加元素，如果键不存在，则直接存储并返回null,若键存在，则覆盖原值，并返回原来的值
V get(Object key) //根据提供的键来返回值，若键不存在，则返回null
void clear()  //移除所有的元素，清空集合
V remove(Object key)  //根据键移除键值对元素，并返回被移除的值
boolean containsKey(Object key)  //判断对应的键是否在集合中存在
boolean containsValue(Object value) //判断对应的值是否在集合中存在
boolean isEmpty()  //判断集合是否为空
Set<K> KetSet()  //获取Map中所有键的Set集合
Collection<V> values() //获取Map中所有值得Collection集合
Set<Map.Entry<K,V>> entrySet() //将Map中的键值对作为一个对象，获取Map的键值对Set
int size()  //返回Map的长度，即键值对个数
```

- HashMap和Hashtable的区别
  - HashMap是线程不安全的，效率高，出现在JDK1.2版本；Hashtable是线程安全的，效率低，出现在JDK1.0
  - HashMap中的键值可以为null；Hashtable不可以

### Collections工具类的方法

```java
public static <T> void sort(List<T> list)  /*对传入的List进行排序，要求传入的List中所存的对象
    										的类已实现Comparable接口，即对象具备可比较性*/
public static <T> int binarySearch(List<T> list,T key) /*以二分查找的算法查找List中对应元素														并返回其索引，若不存在该元素，则返回														其可以插入的点的负索引-1(-插入点-1)*/
public static <T> T max(collection<?> coll) //获取集合元素的最大值
public static void reverse(List<?> list)  //反转集合顺序
public static void shuffle(List<?> list)  //随机打乱集合中元素顺序
```



---

### 异常

>  

### Lambda表达式



### 多线程

#### 概念

> 并发：指两个或多个任务在同一时间段内执行（交替执行）
>
> 并行：指两个或多个任务在同一时刻执行（同时执行）

> 进程：一个在内存中运行的程序，每个进程都有独立的内存空间，一个应用可以同时运行多个进程；进程也是程序的一次执行过程，是系统运行程序的基本单位；系统运行一个进程即是一个进程从创建，运行到消亡的过程。
>
> 线程：线程是进程中的一个执行单元，负责当前进程中程序的执行；一个进程中可以有多个线程，这样的应用称为多线程程序。

#### 线程调度

- 分时调度

  所有线程轮流使用CPU，平均分配每个线程占用CPU的时间

- 抢占式调度

  优先级高的线程先使用CPU，如果优先级相同，则随机选择一个线程。(Java为抢占式)

#### 创建多线程程序的方式

##### 1.Thread类

> 继承Thread类，重写run()方法，并通过start()方法调用。

```java
public class MyThread extends Thread{
    @Override
    public void run() {
        int i = 0;
        for (i = 0; i < 10; i++) {
            System.out.println("run:"+i);
        }
    }
}

MyThread mt = new MyThread();
mt.start();
```

##### 2. Runable接口

> 实现Runable接口，并重写run()方法

```java
public class MyRunable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("runable:" + i);
        }
    }
}
```

> 使用Thread类调用以上

```java
Thread t = new Thread(new MyRunable());
t.start();
```

#### 线程安全问题

> 单线程程序不会出现线程安全问题；多线程程序，若没有访问共享数据，则不会有线程安全问题，若访问了共享数据，则将产生线程安全问题。

##### 线程同步机制

###### 1.同步代码块

> 将可能出现线程安全问题的代码块放进同步代码块中

```java
Object o = new Object()
synchronized (o){ ... }
```

同步代码块使用锁对象，所有线程执行抢占锁对象，抢到的线程进入执行，未抢到的线程进入阻塞等待状态，等待前进程归还锁对象，然后开始新一轮抢占。同步代码块保证了只有一个线程在同步中访问共享数据。程序频繁地判断锁，获取锁，释放锁，程序的效率会降低。

###### 2. 同步方法

> 使用`synchronized`修饰的方法，保证A线程在方法内执行时，其他线程在方法外等候。

```java
public synchronized void method(){ ... }
```

将可能出现线程安全问题的代码放入方法中。

###### 3. 锁机制

> Lock接口提供了锁机制，使用lock()和unlock()方法对出现线程安全问题的代码进行加锁和释放锁。

```java
Lock lock = new ReentrantLock();
lock.lock()
try{
   //有线程安全问题的代码块
}finally{
	lock.unlock();
}
```

#### 网络编程

##### Java中实现网络通信

> Java中提供了两个类用于实现TCP通信

1. 客户端：`java.net.socket`类。实现Socket对象，向服务端发送请求，服务端响应，两者建立连接开始通信。
2. 服务端：`java.net.serverSocket`类。创建ServerSocket对象，开启一个服务，等待连接。

## Java EE 

### JDBC的使用

- 代码示例

  ```java
  try {
       //注册JDBC驱动
  	 DriverManager.registerDriver(new Driver()); //非必须步骤
      
       //建立连接
       //url = "jdbc:mysql://localhost/student"  //连接用的协议，地址及数据库名
       Connection conn = DriverManager.getConnection(url,user,password); 
       //创建一个statement对象
       Statement state = conn.createStatement();
       //执行查询，得到结果集
       String sql = "select * from user"; //查询用的sql语句
  	 ResultSet rs = state.executeQuery(sql);	
  	 //遍历结果集
  	 while (rs.next()) {
  		String id = rs.getString("id");
  		String name = rs.getString("name");
  		int age = rs.getInt("age");
  		String birth = rs.getString("birth");
  		System.out.println("ID:" + id + " NAME:" + name + " age:" + age + "       birth:" + birth);	
  			}
  	 //关闭各连接对象
  		rs.close();
  		state.close();
  		conn.close();
  	} catch (SQLException e) {
  		e.printStackTrace();
  	   }
  ```

  - Statement：Java执行数据库操作的一个接口，用于向数据库发送要执行的静态SQL语句并返回查询得到的结果集。

  - JDBC工具类：在最后关闭对象释放资源时，通常将关闭代码单独建立一个工具类以提高代码复用，

    ```java
    public class JDBCutil {
    	
    	private JDBCutil() {
    		
    	}
    	//关闭各对象，释放资源
    	public static void release(ResultSet rs,Statement state,Connection conn) {
    		closeRs(rs);
    		closeStatement(state);
    		closeConnection(conn);
    	}
    	
    	private static void closeRs(ResultSet rs) {
    		try {
    			if (rs != null) {
    				rs.close();
    			}
    			
    		} catch (SQLException e) {
    			e.printStackTrace();
    		}finally {
    			rs = null;
    		}
    		
    	}
    	
    	private static void closeStatement(Statement state) {
    		try {
    			if (state != null) {
    				state.close();
    			}
    		} catch (SQLException e) {
    			e.printStackTrace();
    		}finally {
    			state = null;
    		}
    		
    	}
    	
    	private static void closeConnection(Connection conn) {
    		try {
    			if (conn != null) {
    				conn.close();
    			}
    		} catch (SQLException e) {
    			e.printStackTrace();
    		}finally {
    			conn = null;
    		}
    		
    	}
    }
    ```


  - 注册驱动不是必须的，JDBC4以后的版本，驱动将自动注册。

### Properties文件使用

- properties文件记录了jdbc的连接数据，用于直接读取以方便连接文件格式如下

  ```java
  url = <url>
  user = <username>
  password = <passwd>
  //字段名 = 数值
  ```

- 使用properties文件：在代码中新建properties对象并用文件中的key获取对应的值

  ```java
  Properties pro = new Properties(); //新建pro对象
  InputStream is = 
      <类名>.class.getClassLoder().getResourceAsStream("jdbc.properties"); /*
      将properties文件读取为输入流
      */
  pro.load(is); //pro对象加载输入流
  url = pro.getString("url"); //获取文件中的各值
  
  ```

  

### DAO模式

> Data Access Object：数据库访问规则

1. 新建一个dao接口，里面声明数据库访问规则

2. 新建dao实现类,实现上面的接口

### PreparedStatement类使用

1. 为了解决sql注入的问题引入PreparedStatement类，与之前Statement类的区别在于，前者为先拼接SQL语句再执行，后者为先预处理SQL语句再拼接执行

2. 代码示例

   ```java
   String sql = "select * from <表名> where <字段名> = ？"; //在需要用变量替换的地方用？占位
   PreparedStatement ps = connection.prepareStatement(sql);//创建ps对象并传入sql语句预处理
   ps.setString(1,id); //传入变量名设置相应字段
   resultSet = ps.executeQuery(); //执行查询操作获取结果集
   num = ps.executeUpdate(); //执行更新获取影响行数
   ```

### JavaWeb介绍

#### XML文件介绍

1. XML文件用途
   1. 用来保存数据
   2. 做配置文件
   3. 传递数据的载体

2. 文件格式

   ```xml
   <? xml version = "1.0" encoding = "UTF-8" ?>
   <一级标签>
       <二级标签>
           <三级标签>数据</三级标签>
           <三级标签>数据</三级标签>
       </二级标签>
   </一级标签>
   ```

   XML文件第一行为文档声明，通常声明文档的版本和编码。声明下的第一个标签为根标签，所有的标签和数据必须包含在根标签内。

3. 标签属性：标签中可以定义属性，属性名不限可自由指定

   ```xml
   <stu id = "10086">
       <name>张三</name>
       <age>23</age>
   </stu>
   ```

4. 注释：<!--这里是一条注释 -->，注释必选在文档声明下方。

5. 转义字符

   |  \&lt;  |  <   |  小于  |
   | :-----: | :--: | :----: |
   |  \&gt;  |  >   |  大于  |
   | \&amp;  |  &   |  和号  |
   | \&apos; |  .   | 省略号 |
   | \&quot; |  "   |  引号  |

6. CDATA区，用于传递数据，区内的标签将被认为是普通字符串，很少用到

   ```xml
   <decs><![CDATA[
   <a href = "www.baidu.com">lalala</a>
       ]]></decs>
   ```

7. XML的解析方式

   1. SAX：simple API for XML；基于事件驱动，读取一行解析一行。不会造成内存溢出，不能增删改，只能查询。

   2. DOM：Document Object Model；将整个xml文档读到内存中，形成树状结构，整个文档称之为document对象，标签称为element对象，属性称为attribute对象，数据称为Text对象。若文件过大，可能造成内存溢出，可以进行增删改操作。

   3. 解析方案：jaxp，jdom，dom4j
#### Tomcat的安装与使用

   1. Tomcat目录介绍

      1. bin:Tomcat的可执行文件目录
      2. conf：配置文件目录：server.xml  web.xml
      3. lib：运行所需的jar文件
      4. logs：运行日志
      5. webapps：发布到Tomcat服务器上的项目存放目录
      6. work：jsp翻译成class文件存放目录

   2. 如何把项目发布到Tomcat

      1. 将要发布的文件拷贝到webapps下，新建一个文件夹并存放要发布的web文件，浏览器访问路径为

         <地址>:8080/<新建文件夹名>/<文件名>

      2. 用虚拟路径发布：在conf/server.xml中找到host元素节点，并加入以下内容

         ```xml
         <Context docBase = "" path=""></Context>
         <!-- docBase:要发布的文件实际存储路径 path:url中用于访问的虚拟路径-->
         ```

#### Nginx按使用



#### Http简介

1. Http协议介绍

   

2. Http请求数据介绍

   http请求数据结构分为请求行，请求头，请求体

   1. 请求行格式:

   ```http
   POST /examples/servlets/servlet/RequestParamExample HTTP/1.1
   
   POST:请求方式  
   /examples/servlets/servlet/RequestParamExample :请求的地址路径
   HTTP/1.1 :HTTP协议版本
   ```

   2. 请求头内容

      ```http
      accept : 客户端向服务端表示自己能接受的数据类型
      Referer : 请求的全路径地址
      User-Agent : 向服务端表明当前客户端的信息（浏览器内核版本，操作系统内核版本、位数等信息）
      content—type : 提交的数据类型
      accept-encoding : 压缩算法
      Host : 主机地址
      Content-lenght : 数据长度
      Connection : <keep-alive> 是否保持连接
      Cache-Control : 对缓存操作
      ```

   3. 请求体内容

      浏览器真正发送给服务器的内容,以 key=value 的形式,如果存在多组数据, 键值对间以 & 连接

      ```http
      请求体例:
      firstname=sasa&lastname=sdsd 
      ```

3. Http响应数据

   响应数据包括响应行,响应头,响应体

   1. 响应行结构

      ```http
           HTTP/1.1  200    OK
      结构:(协议版本) (状态码) (对应状态码)
      ```

   2. 响应头结构

      ```http
      Server : 服务器类型
      Content-Type : 返回给客户端的数据类型及编码格式
      Content-Length : 返回数据的长度
      Date : 响应的日期
      ```

4. GET和POST请求的区别

   1. 请求路径不同,post请求在url后面不跟任何数据,get请求,在url后面跟上请求数据

   2. 带上的数据不同,post使用流的方式写数据,  get在url中拼接请求数据

   3. 由于post使用流的方式写数据,所以一定要有一个content-length的头来说明数据的长度,没有长度限制,

      get在url后面拼接数据,有安全隐患,一般在从服务端获取数据同时客户端不上传数据时使用,能带的数据有限,限制1kb大小

5. Web资源

   在http协议中规定了响应和请求双方,客户端与服务端与web相关的资源

   1. 静态资源

      包括 html , css , js 

   2. 动态资源

      包括 jsp

#### Servlet介绍

1. Servlet定义: Servlet是一个运行在web服务器上的 Java 程序,用于响应客户端的HTTP请求, 配合动态资源来使用, 静态资源也需要,但是静态资源通常使用Tomcat自带一个 defaultServlet. 

2. Servlet是一个Java接口,需要有一个类实现,但通常不直接实现Servlet,而是继承其实现类HttpServlet

3. Servlet配置

   ```xml
   1.新建一个类并继承HttpServlet抽象类,并重写doGet()和doPost()方法
   2.在web.xml中写入以下配置
   <!--该配置用于向web服务器注册一个Servlet-->
   <servlet>
     	<servlet-name>{实现Servlet接口的类名}</servlet-name>
     	<servlet-class>{包名.类名}</servlet-class>
     </servlet>
   
   <!--该配置用于创建一个指向Servlet的url映射 -->
     <servlet-mapping>
     	<servlet-name>{类名}</servlet-name>
     	<url-pattern>/{自定义url名}</url-pattern>
     </servlet-mapping>
   ```

   - 注册Servlet的简易方法，在实现类的前面加@WebServlet注解

      ```java
     @WebServlet("/aaa") //注解内为url链接后缀
     public class Servlet2 extends HttpServlet{
         ...
     }
     ```

     

4. Servlet生命周期

   1. init() 方法: 在创建该servlet 实例时就会执行该方法, 一个servlet只会初始化一次, init()方法只会执行一次,默认情况下,初次访问该servlet时,才会创建实例，若要提前创建实例，可在web.xml中写入配置

      ```xml
      <servlet>
          <load-on-startup>1</load-on-startup> <!--该数字越小，启动优先级越高-->
      </servlet>
      ```

      

   2. service() 方法: 只要客户端来了一个请求, 就执行该方法, 可以被执行多次,一次请求,对应一次该方法调用

   3. destroy() 方法: servlet被销毁时执行该方法
      - 该项目从服务器中移除
      - 正常执行服务器关闭程序

5. ServletContext类

   1. 用于获取全局设定，一个web工程中只含有一个ServletContext对象，无论在何处声明该对象，均指向同一对象，用于获取在web.xml中设定的全局配置，任何一个servlet都可以获取该参数

   2. 先在web.xml中设定以下参数

      ```xml
      <context-param>
        	<param-name>name</param-name>
        	<param-value>value</param-value>
        </context-param>
      ```

      再在servlet类中获取该对象

      ```java
      ServletContext sc = getServletContext();
      ```
   3. sc对象的各成员方法
      

      - 使用以下方法可获取到xml文件中的param-value值
      
      ```java
String getInitParameter("<param-name>") //该方法返回上面的param-value值
      ```

      - 使用以下方法可以获取指定文件的绝对路径
      
      ```java
String getRealPath("<指定文件的相对路径>") //以指定文件的相对路径获取绝对路径
      ```
      
      - 使用以下方法可以将指定文件转成流
      ```java
      InputStream getResourceAsStream("<指定文件的相对路径>")
      ```
      
   
6. HttpRequest与HttpResponnse

   1. doGet和doPost参数列表中的两个形参，request和response

   2. request：浏览器传给服务端的数据，里面通常包含要提交的表单信息

      ```java
      request.setCharacterEncoding("utf-8"); //解决post中文数据乱码
      String request.getParameter("<输入框name>"); //使用该方法提取request中的表单信息
   String[] getParameterValues(String name); //获取多个参数值
      Enumeration<String> getParameterNames(); //获取所有的请求参数key
   Map<String,String[]> getParameterMap(); //获取所有参数键值的map集合
      ```

      - 请求转发：在服务器内部的资源跳转，将当前请求转发到其他servlet。
   
        ```java
        request.getRequestDispatcher("要跳转的Servlet").forward(request,response);
        ```
   
        特点：

        1. 浏览器路径不发生变化
   
           2. 只能转发到当前服务器内部资源
   
           3. 转发是一次请求
   
              
   
   3. response：服务端返回给客户端的信息
   
      ```java
      PrintWriter response.getWriter(); //返回一个PrintWriter对象
      pw.write(<要返回的字符串>)；
      response.getWriter().write(<要返回的字符串>); //或者直接这样返回
      response.setCharacterEncoding(); //设置返回的字符集
      response.setContentType("text/html;charset=UTF-8"); //设置浏览器以什么字符集解析页面
      ```
   

#### Cookie和Session

##### 重定向和请求转发

1. 重定向方法

   ```java
   response.sendRedirect("<重定向的HTML文件名>");
   ```

2. 请求转发方法

   ```java
   request.getRequestDispatcher("<重定向的HTML文件名>").forward(request, response);
   ```

##### Cookie介绍

> 服务器发送给客户端并存储在客户端上的一份数据,记录了用户的登录数据，浏览记录等。

1. Cookie的设置和获取

   1. 向客户端添加cookie

      ```java
      Cookie c = new Cookie("key","value");
      response.addCookie(c);
      ```

   2. 获取客户端请求中的cookie

      ```java
      Cookie[] cookies = request.getCookies();
      if (cookies != null) {    //当第一次请求时，cookie可能为空，要先判断 
      			for (Cookie c : cookies) {
      				String nameString = c.getName();
      				String valString = c.getValue();
      				System.out.println(nameString + "..." + valString);
      			}
      		}
      ```

2. Cookie的生存周期

   > 默认情况下，关闭浏览器后Cookie即失效，但可以设置Cookie的有效期

   通过以下方法可设置有效期

   ```java
   cookie.setMaxAge(expiry); /* expiry取值：
                              * 正值x：cookie将在x秒后过期
                              * 负值：保存到浏览器关闭时即删除cookie
                              *
                              */
   ```

3. Cookie的其他方法

   ```java
   cookie.setValue(newValue); //设置新的值
   cookie.setDomain(pattern); //用于指定只有请求了指定的域名才能带上该cookie
   cookie.setPath("/CookieDemo"); //只有访问该域名下的CookieDemo这个路径才会带cookie
   ```


##### Session

> Session,会话。Session是基于Cookie的一种会话机制，Cookie是存放在客户端的一小份数据，Session是存放在服务端的数据。会在cookie中添加一个sessionID，由服务器生成。

1. Session的获取和常用方法

   ```java
   HttpSession s = request.getSession(); //获取一个Session
   s.getID(); //得到会话ID
   s.setAttribute(key,value); //设置值
   s.getAttribute(key); //获取值
   s.removeAttribute(key); //移除值
   ```

2. Session生存周期

   - 创建：当调用了`request.getSession()`，即创建了一个Session。
   - 销毁：Session是存放在服务器内存中的一份数据，销毁Session的途径有
     	          1. 关闭服务器
               2. 会话时间过期，默认为30分钟
   - Session可以用Redis进行持久化

3. Session强制终结

   ```java
   session.invalidate(); //强制总结当前会话
   ```


#### JSP

> JSP，java server page；继承自servlet的一个java类，用于显示动态的网页信息。HTML只适合显示静态的网页。

##### JSP的三大指令

> 指令的写法：<%@ 指令名 指令参数=...%>

1. Page指令：用于配置JSP页面
   
   该指令各参数的意义：
   
   - language：表明jsp文件中可以写java代码
   
   - contentType：向浏览器表明文件的类型以及使用的编码，告诉浏览器该如何打开该文件。
   
   - extends：用于指定jsp翻译成java文件后，继承的父类是谁，一般不用改。
   
   - import：导包用，一般不用手写。
   
   - session：
   
     - 可选的值为true或false
     - 用于控制在这个session页面内，是否可以直接使用session对象
   
   - errorPage：
   
     用于控制当前页面出现错误时，跳转到下一个jsp页面。值是下一个页面的路径。
   
   - isErrorPage：
   
     用于声明某一个页面是不是错误跳转页面
   
2. Include指令：导入页面的资源文件

   用于包含另一个jsp文件的内容进来。

3. taglib指令：标签库 ，即外置的jar包

##### JSP动作标签

##### JSP内置对象

>可以在jsp页面中直接使用的对象，不用创建。

- PageContext【PageContext 类】

  作用域仅限于当前页面

- request【HttpServletRequest 类】

  作用域仅限于一次请求，只要服务器对该请求做出响应，域中存的值就没有了。

- session【HttpSession】

  作用域限于一次会话当中（多次请求与响应）。

- application 【ServletContext】

  整个工程都可以访问，服务器关闭后不能访问。

以上四个是作用域对象。即这些对象可以存值，其取值范围有限定。

- out 【JspWriter】

- exception 【Throwable】：只有在isErrorPage为ture时该对象才能使用。

- config 【ServletConfig】

- page 【Object】

  负责将jsp翻译成java的实例对象

- response 【HttpServletResponse】

#### EL表达式

> 作用：为了简化在JSP里写的Java代码。用于运算或者获取值。

- EL表达式的运算符：

  >1.算术运算符
  >
  >2.逻辑运算符
  >
  >3.比较运算符
  >
  >4.空运算符：empty
  >
  >​	用于判断字符串，集合，数组对象是否为null并且长度是否为零。
  >
  >​	例：${empty list}

- 

写法： `${表达式}`，例输出四个作用域中的值：

```jsp
${pageScope.name} //输出pageContent中key为'name'的值
${array[0]}  //取出域中存的数组中的值
${map.name}  //取出域中所存的map中key为name的值
${map[address.aa]} //取出map中key为"address.aa"的值
${pageContext.request.contextPath} //动态获取虚拟目录
```

#### JSTL

> Jsp Standard Tag Library，Jsp标准标签库。用于替换<%%>的写法，一般与EL表达式组合。

常用标签：

```jsp
<c:set></c:set>
<c:if test="${EL表达式}" var="" scope=""></c:if> <!--检查EL表示是否为真，以此执行标签中的语句--><!--var:定义一个变量存储前面表达式的值，存储到scope指定的域中-->  
<c:foreach begin="" end="" var="" step="" item=""></c:foreach> <!--begin：开始遍历 end：结束遍历 step：步进 var：遍历的结果会赋值到该处定义的中间变量中 item:从session中获取可遍历的对象-->
```

使用步骤：

```jsp
<!--使用前，现在jsp文件中导入jar文件-->
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!--使用以上标签来对数据进行操作-->
```



#### 事务，数据库连接池

##### 事务

> 一组操作的合集，其中的操作语句要么都执行，要么都不执行

- 在Java中使用事务

  ```java
  conn.setAutoCommit(false); //首先关闭自动提交
  ...； //业务逻辑
  conn.commit(); //提交事务，使修改生效
  //如果出现异常
  conn.rollback(); //回滚事务
  ```

  事务只针对当前连接，不针对表。

##### 数据库连接池

- 开源连接池 Druid，C3P0

- C3P0的使用

  1. 导入jar包
  2. 定义配置文件：c3p0.properties 或者 c3p0.xml，将配置文件放置于Source Root路径下。
  3. 创建连接池对象 ComboPooledDataSource
  4. 获取连接对象 getConnection()

- Druid使用

  1. 导入jar以及jdbc驱动：druid.jar

  2. 定义配置文件：

     1. 配置文件为propertites
     2. 名称不限，放在任意目录下，需手动加载

     ```properties
     #配置文件内容
     driverClassName=com.mysql.jdbc.Driver
     url=jdbc:mysql://localhost:3306/test?serverTimezone=UTC
     username=root
     password=admin
     initialSize=5
     maxActivate=10
     maxWait=3000
     ```

  3. 通过工厂类获取连接池对象  DruidDataSourceFactory

     ```java
     Properties profile = new Properties();         profile.load(JDBCutils.class.getClassLoader().getResourceAsStream("druid.properties"));
     ds = DruidDataSourceFactory.createDataSource(profile);
     ```

  4. 获取连接

     ```java
     ds.getConnection();
     ```

##### JDBCutils

```java
public class JDBCutils {

    public static DataSource ds;

    static {

        try {

            Properties profile = new Properties();
            profile.load(JDBCutils.class.getClassLoader().getResourceAsStream("druid.properties"));
            		            
            ds = DruidDataSourceFactory.createDataSource(profile);

        } catch (Exception e) {
            e.printStackTrace();
        }

    }

    public static Connection getConnection() throws SQLException {
        return ds.getConnection();
    }

    public static DataSource getDataSource() {
        return ds;
    }

    public static void close(Statement stmt,Connection conn){
        close(null,stmt,conn);
    }


    public static void close(ResultSet rs, Statement stmt, Connection conn){

        if(rs != null){
            try {
                rs.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (stmt != null){
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        
        if(conn != null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

##### JDBC Template

> Spring框架对JDBC的简单封装，提供了一个JDBC template对象。简化执行数据库操作过程，让开发者专注于SQL语句和执行。

使用步骤：

1. 导入jar

2. 创建jdbc template对象，依赖于数据源

   ```java
   JdbcTemplate jt = new JdbcTemplate(ds);
   ```

   调用JdbcTemplate方法来完成操作。

   ```java
   update(sql); //执行增删改语句
   queryForMap(sql,args...); //查询结果封装为map 只适用于结果为一条记录，将列名作为key，值为                               value
   queryForList(sql,args...); //查询结果封装为List 将单条记录封装为Map，并将所有Map封装为List
   queryForObject(sql,Integer.class); //结果封装为基本数据类型对象,一般用于聚合函数查询
   query(sql,new BeanPropertyRowMapper<T>(T.class)); //结果封装为javaBean对象,返回                                                           javaBean对象的List集合
   ```
   
   注意：查询返回的结果集即使为空，返回的`List`也不为`null`，而只是一个空集合，要用`size()`来判断其是否为空，而不能单纯判断其是否为`null`。

#### Filter

- 过滤器细节

  - web.xml配置

    ```xml
    <!--该配置用于向web服务器注册一个Filter-->
    <filter>
      	<filter-name>{实现filter接口的类名}</filter-name>
      	<filter-class>{包名.类名}</filter-class>
      </filter>
    
    <!--该配置用于创建一个指向Filter的拦截url -->
      <filter-mapping>
      	<filter-name>{类名}</filter-name>
      	<url-pattern>/{自定义url名}</url-pattern>
      </filter-mapping>
    ```

  - 过滤器的执行流程

    1. 过滤器拦截请求
    2. 过滤器放行请求
    3. 请求到达服务器申请资源
    4. 请求返回过滤器，执行放行代码后的操作。

  - 过滤器的生命周期方法

    - init()：服务器启动后，会创建Filter对象，然后调用init()方法，只执行一次
    - doFilter()：每一次请求拦截时都执行
    - destory()：服务器关闭后，Filter对象被销毁，若服务器正常关闭，则执行destory方法，只执行一次。

  - 过滤器配置详解

    - 拦截路径配置

      1. 具体拦截路径：/index.jsp   只有访问jsp资源时，过滤器才执行
      2. 拦截目录：/user/*               访问user目录下的资源时过滤器执行
      3. 后缀名拦截：*.jsp                访问所有jsp资源时，过滤器执行
      4. 拦截所有资源：/*

    - 拦截方式配置：资源被访问的方式拦截

      1. 注解配置：

         - 设置dispatchTypes属性
           1. REQUEST：默认值。浏览器直接请求资源
           2. FORWARD：转发访问资源
           3. INCLUDE：包含访问资源
           4. ERROR：错误跳转资源
           5. ASYNC：异步访问资源

      2. web.xml配置：

         配置<dispatcher></dispatcher>标签即可

  - 过滤器链(多个过滤器)

    - 执行顺序：
      1. 过滤器1
      2. 过滤器2
      3. 资源执行
      4. 过滤器2
      5. 过滤器1
    - 过滤器执行优先级
      - 注解配置：按照过滤器类名的字符串比较规则，类名中的字符逐个比较，值小的先执行
      - web.xml配置：定义在上面的先执行

    

#### Listener

> 监听器，wen三大组件之一

- 事件监听机制：
  1. 事件：一件事情
  2. 事件源：事件发生的地方
  3. 监听器：一个对象
  4. 注册监听：将事件，事件源，监听器绑定在一起。当事件源上发生某个事件后，执行监听器
- `ServletContextListener`：监听`ServletContext`对象的创建和销毁

#### Ajax和JQuery

##### JQuery

> 一个Js的方法库

1. 获取元素：

   ```js
   var obj = $("选择器"); //返回一个jq对象，可以看做一个数组
   ```

2. Js和Jq对象相互转换

   - Js -> Jq：`$(js对象)`
   - Jq -> Js：`Jq对象.get(index)`

3. 事件绑定&&入口函数

   

4. 选择器

   1. 基本选择器

      1. 标签选择器（元素选择器）

         ```js
         $("htmlTag")
         ```

      2. id选择器

         ```js
         $("#id")
         ```

      3. 类选择器

         ```js
         $(".classname")
         ```

      4. 并集选择器

         ```js
         $("选择器1,选择器2 ...")
         ```

         

   2. 层级选择器

      1. 后代选择器

         ```js
         $("A B") //选择A元素内部的所有B元素
         ```

      2. 子选择器

         ```js
         $("A > B") //选择A元素内部所有B元素的子元素
         ```

   3. 属性选择器

      1. 属性名称选择器

         ```js
         $("A[属性名]") //包含指定属性的选择器
         ```

      2. 属性选择器

         ```js
         $("A[属性名=值]") //包含指定属性等于指定值的选择器
         ```

      3. 复合属性选择器

         ```js
         $("A[属性名=值][]") //包含多个指定属性条件的选择器
         ```

   4. 过滤选择器

      1. 首元素选择器

         ```js
         :first //获取第一个元素 
         ```

      2. 尾元素选择器

         ```js
         :last //获取最后一个元素
         ```

      3. 非元素选择器

         ```js
         :not(selector) //不包含指定内容的元素
         ```

      4. 偶数选择器

         ```js
         :even //偶数，从零开始计数
         ```

      5. 奇数选择器

         ```js
         :odd //奇数，从零开始计数
         ```

      6. 等于索引选择器

         ```js
         :eq(index) //指定索引元素
         ```

      7. 大于索引选择器

         ```js
         :gt(index) //大于指定元素
         ```

      8. 小于索引选择器

         ```js
         :lt(index) //小于指定元素
         ```

      9. 标题选择器

         ```js
         :header //获得标题元素，固定写法
         ```

   5. 表单过滤选择器

      1. 可用元素选择

         ```js
         :enabled //获得可用元素
         ```

      2. 不可用元素选择器

         ```js
         :disabled //不可用过滤选择器
         ```

      3. 选中选择器

         ```js
         :checked //获得单选(复选框)选中的元素
         ```

      4. 选中选择器

         ```js
         :selected //获得下拉框选中的元素
         ```

5. DOM操作

   1. 内容操作

      1. html()：

         ```javascript
         .html() //获取标签体内容
         ```

      2. text()：

         ```js
         .text() //
         ```

      3. val()

         ```js
         .val() //获取输入框中的内容
         ```

   2. 属性操作

      1. 通用属性操作

         1. attr()：获取/设置元素的属性

            ```js
            $("#id").attr("属性") //获取属性
            $("#id").attr("属性","值") //修改属性
            ```

         2. removeAttr()：删除元素的属性

         3. prop()：获取/设置元素的属性

         4. removeProp()：删除元素的属性

      2.  对class属性操作

         1. addClass()：添加class属性值

            ```js
            $("#id").addClass("值") //给指定id的元素的class属性添加指定的值
            ```

         2. removeClass()：删除class属性值

            ```js
            $("#id").removeClass("值") //给指定id的元素的class属性删除值
            ```

         3. toggleClass()：切换class属性值

            ```js
            $("#id").toggleClass("one") //若指定id的元素存在class=one，则删除该class，若没                               有，则添加该class
            ```

   3. CRUD操作

      1. append()：父元素将子元素追加到末尾

      2. remove()：移除元素

         ```js
         对象.remove() //将对象删除掉
         ```

      3. empty()：清空元素的所有后代元素

         ```js
         对象.empty() //将对象的后代元素清空，但保留该对象及其属性节点
         ```

6. 动画效果和遍历方式

   -  动画效果

      1. 默认显示和隐藏方式

         1. show([speed,[easing],[fn]])
      
            参数：

            1. speed：动画的速度，三个预定义的值(“slow”,”normal”,”fast”)或动画的毫秒值(1000)
            2. easing：用来指定切换效果：默认是“swing”，可用参数“linear”
            3. fn：一个函数，在方法执行完后执行该函数
      
            ```js
      $("#id").show();
            ```

         2. hide([speed,[easing],[fn]])

         3. toggle([speed],[easing],[fn])

      2. 滑动显示和隐藏方式

         1. slideDown([speed],[easing],[fn])
         2. slideUp([speed],[easing],[fn])
         3. slideToggle([speed],[easing],[fn])
      
      3. 淡入淡出显示和隐藏
      
         1. fadeIn([speed],[easing],[fn])
      2. fadeOut([speed],[easing],[fn])
         
         3. fadeToggle([speed],[easing],[fn])
      
   - 遍历方式
   
     1. jq对象.each(callback)
   
        ```js
        cities.each(function(index,element){
            alert(index + " " + element);
        });
        ```
   
     2. $.each(obj,callback)
   
        ```js
        $.each(cities,function(){
            alert($(this).html());
        });
        ```
   
     3. for ... of
   
        ```js
        for(li of cities){
            alert(li.innerHTML);
        }
        ```
   
   -  事件绑定
   
      1. jquery标准的绑定方式
   
         ```js
         jq对象.事件方法(回调函数);
         ```
   
      2. on绑定对象/off解除绑定
   
         ```js
         jq对象.on("事件名称",回调函数)
         jq对象.off("事件名称")
         ```
   
      3. 事件切换：toggle 
   
         ```js
         jq对象.toggle(fun1,fun2) //单击对象后，会交替执行fun1和fun2
         ```
   
7. JQuery插件机制

   > 用于增强JQuery的功能

   - 实现方法

     1. $.fn.extend(obj)

        用于增强jq所获取的DOM对象，仅DOM对象可用

        ```js
        $.fn.extend({
            //定义一个check()方法，所有JQ对象都可以调用该方法 
            check:function(){
               ...
            }
        });
        ```

     2. $.extend(obj)

        用于增强jq对象本身，用于全局可调用该方法

##### Ajax

> Ajax可以实现在不加载整个网页的情况下，更新部分网页的技术。

- 实现方式：

  - 原生的`JS`实现：

    ```js
    //创建核心对象
    var xmlhttp;
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    //发送请求
    /*
    参数1：请求方式(GET || POST)
        * GET方式，请求参数在URL后面拼接，send方法为空参。
        * POST方法，请求参数在send方法中定义
    参数2：URL
    参数3：同步(false)或异步(true)
    */
    xmlhttp.open("GET","test1.txt",true);
    xmlhttp.send(string); //若请求方法为POST，则在该方法中定义请求参数
    //接受响应信息
    xmlhttp.onreadystatechange=function()
      {
        //判断readyState就绪状态是否为4，Status响应状态码是否为200
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
            //获取服务器响应结果
        	document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
      }
    ```

  - `JQuery`实现方式：

    1. `$.ajax()`：

       ```js
       $.ajax({
           url:"" , //请求链接
           type:"" , //请求方式，GET或POST
           data:{"key":"value"} , //请求参数
           success:function(){} , //响应成功后自动执行的回调函数
           error:function(){} ,  //响应失败后的回调函数
           dataType:"" , //设置接收到的响应数据格式
       });
       ```

    2. `$.get()`：专用于`GET`请求的实现

       ```js
       $.get(url, [data], [callback], [type])
       //参数列表:请求URL，请求参数，回调函数，响应数据格式
       //例
       $.get("",  //请求URL
             {},  //请求参数
             function(){}, //回调函数
             "");   //响应数据格式
       ```

    3. `$.post()`：专用于实现`POST`请求

##### JSON

>  JSON：JavaScript 对象表示法(JavaScript Object Notation)

- 语法：

  JSON 语法是 JavaScript 对象表示法语法的子集。

  - 数据在键值对中
  - 数据由逗号分隔
  - 花括号保存对象
  - 方括号保存数组

  JSON 值可以是：

  - 数字（整数或浮点数）
  - 字符串（在双引号中）
  - 逻辑值（true 或 false）
  - 数组（在方括号中）
  - 对象（在花括号中）
  - null

- JSON和Java对象相互转换

  - JSON解析器：Jsonlib，Gson，Fastjson，jackson

  - Java对象转Json：

    - jackson实现：

      ```java
      //创建jackson核心对象 ObjectMapper
      ObjectMapper mapper = new ObjectMapper();
      //序列化为json字符串
      String json = mapper.writeValueAsString(obj);
      ```

      注解：将注解加在要作用的属性上方以使其生效

      1. @JsonIgnore：排除属性

      2. @JsonFormat：属性格式化

         > 例：@JsonFormat(“yyyy-MM-dd”)  格式化日期

  - Json字符串转Java对象：

    ```java
    Obj obj = mapper.readValue(json,Obj.Class);
    ```

### Mybatis

> 一个java编写的持久层框架，封装了jdbc操作的细节，使用了ORM思想实现了结果集封装，使开发者可以着眼于SQL语句本身。

#### 配置过程

- 配置Mybatis主配置文件

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE configuration  
    PUBLIC "-//mybatis.org//DTD Config 3.0//EN"  
    "http://mybatis.org/dtd/mybatis-3-config.dtd">
  <!--Mybatis的主配置文件-->
  <configuration>
      <!--配置环境-->
      <environments default="mysql">
          <!--配置Mysql环境-->
          <environment id="mysql">
              <!-- 配置事务的类型-->
              <transactionManager type="JDBC"></transactionManager>
              <!--配置数据源（连接池）-->
              <dataSource type="POOLED">
                  <!--配置连接参数-->
                  <property name="driver" value="com.mysql.jdbc.Driver"/>
                  <property name="url" value="jdbc:mysql://localhost:3306/eesy_mybatis?serverTimezone=UTC&characterEncoding=UTF-8"/>
                  <property name="username" value="root"/>
                  <property name="password" value="admin"/>
              </dataSource>
          </environment>
      </environments>
      <!--指定映射配置文件的位置，映射配置文件是指每个dao独立的配置文件-->
  	<mappers>
          <mapper resource="info/fangou/dao/UserDao.xml"/>
      </mappers>
  </configuration>
  ```

- 配置DAO映射配置文件

  每一个dao一个映射配置文件，映射配置文件的路径必须与dao的包结构一致

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <!--namespace为dao接口的全限定类名-->
  <mapper namespace="info.fangou.dao.UserDao">
      <!-- 配置查询所有 -->
      <!-- id为dao内定义的方法名 resultType为返回的实体类全限定类名-->
      <select id="findAll" resultType="info.fangou.domain.User">
          select * from user;
      </select>
  
      <!-- 配置模糊查询，parameterType为传入参数类型，CONCAT为SQL字符串拼接函数-->
      <select id="findByName" resultType="info.fangou.domain.User" parameterType="String">
          select * from user where username like CONCAT('%',#{name},'%')
      </select>
  
      <delete id="deleteUser" parameterType="int">
          delete from user where id = #{id}
      </delete>
  
      <update id="updateUser" parameterType="info.fangou.domain.User">
          update user set username = #{username},birthday = #{birthday},sex = #{sex},address = #{address} where id=#{id}
      </update>
  
      <insert id="saveUser" parameterType="info.fangou.domain.User">
          insert into user(username, birthday, sex, address) value (#{username}, #{birthday}, #{sex}, #{address})
      </insert>
  
  </mapper>
  ```

- Mybatis执行过程案例

  ```java
  		//1.读取配置文件
          InputStream is = Resources.getResourceAsStream("SqlMapConfig.xml");
          //2.创建SqlSessionFactory工厂
          SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
          SqlSessionFactory factory = builder.build(is);
          //3.使用工厂创建Sqlsession对象
          SqlSession sqlSession = factory.openSession();
          //4.使用SqlSession对象创建dao的代理对象
          UserDao userDao = sqlSession.getMapper(UserDao.class);
          //5.使用代理对象执行方法
          List<User> userList = userDao.findAll();
          for (User user : userList) {
              System.out.println(user);
          }
          //6.释放资源
          sqlSession.close();
          is.close();
  ```
  
- 数据库列名与实体类属性名不对应

  > 使用resultMap可以解决以上不对应的问题

  ```xml
  <!--id为该resultMap的唯一标识，type为Java实体类全限定类名-->
  <resultMap id="userMap" type="info.fangou.domain.User">
      <!--主键的对应关系，property为实体类中的属性，column为数据库中的字段-->
      <!--javaType:实体类中的数据类型，jdbcType:数据库中的数据类型-->
      <id property="" column="" javaType="" jdbcType=""></id>
      <!--非主键属性对应关系--> 
      <result property="" column="" javaType="" jdbcType=""></result>
  </resultMap>
  ```

  在SQL语句中启用以上`resultMap`：

  ```xml
  <select id="findAll" resultMap="userMap">
     select * from user
  </select>
  ```

#### 使用注解开发

1. 修改主配置文件

   ```xml
       <!--指定映射配置文件的位置，映射配置文件是指每个dao独立的配置文件-->
       <!--若使用注解，则使用class属性指定dao的全限定类名-->
       <mappers>
           <mapper class="info.fangou.dao.UserDao"/>
       </mappers>
   </configuration>
   ```

2. 删除dao映射配置文件，并在dao方法上加注解

   ```java
   @Select("select * from user")
   List<User> findAll();
   ```

3. 注解实现CRUD操作

   在Dao接口内做如下编写

   ```java
   public interface UserDao {
   
       @Select("select * from user")
       List<User> findAll();
   
       @Insert("insert into user(username,birthday,sex,address) values(#{username},#{birthday},#{sex},#{address})")
       void saveUser(User user);
   
       @Update("update user set username=#{username},birthday=#{birthday},sex=#{sex},address=#{address} where id=#{id}")
       void updateUser(User user);
   
       @Delete("delete from user where id = #{id}")
       void deleteUser(Integer id);
       
       //模糊查询的实现
       @Select("SELECT * FROM `user` WHERE username LIKE CONCAT('%',#{name},'%')")
       List<User> findByName(String name);
       
    //使用聚合函数
       @Select("select count(id) from user")
       int findTotal();
   }
   ```
   
4. 注解解决列名与实体类名不对应问题

   ```java
   @Results(value = {
         @Result(id = false,column = "",property = "")//id：是否为主键，column：数据库字段名，property：实体类名
   })
   ```

   以上为基本的增删改查实现。



#### 连接池以及事务控制

- Mybatis中的连接池配置

  - mybatis提供了三种连接池配置方式

    1. 主配置文件中的`dataSource`标签，`type`属性表示采用何种连接方式

       `Type`的取值：

       - POOLED：采用连接池的思想，实现`javax.sql.DataSource`规范。
       - UNPOOLED：采用传统获取连接的思想，没有连接池，实现`javax.sql.DataSource`规范。
       - JNDI：采用服务器的`JNDI`技术获取`DataSource`对象，非`web`或`maven`的`war`工程不能使用。

- Mybatis的事务特点

  - 事务实现：通过`sqlsession`对象的`commit`方法和`rollback`方法实现事务的提交和回滚。

  - 设置事务自动提交：

    ```java
    //传入一个true值
    SqlSession sqlSession = factory.openSession(true);
    ```

#### 动态SQL

> 可以实现不同个数的条件执行查找

- `where`标签：加在SQL语句之后，用来包裹其他标签

- `if`标签：条件选择标签，用于选择哪一个删选条件成立

- `foreach`标签：用于子查询，查询条件为一个集合

  ```xml
  <!--查询条件为多个，并且不一定同时成立-->
  <select id="findByContent" parameterType="info.fangou.domain.User" resultType="info.fangou.domain.User">
          select * from user
          <where>
              <if test="username != null">
                  and username = #{username}
              </if>
  
              <if test="sex != null">
                  and sex = #{sex}
              </if>
          </where>
      </select>
  <!--查询条件为一个集合，需要调用子查询-->
      <select id="findEach" resultType="info.fangou.domain.User" parameterType="info.fangou.domain.QueryVo">
          select * from user
          <where>
              <if test="ids != null and ids.size() != 0">
                  <foreach collection="ids" open="id in (" close=")" item="idi" separator=",">
                      #{idi}
                  </foreach>
              </if>
          </where>
      </select>
  ```

- 抽取重复的SQL语句

  ```xml
  <!--用于包裹需要抽取的重复sql语句-->
  <sql id="defaultSql">
          select * from user <!--此处不能加分号-->
  </sql>
  <!--在需要引用以上sql语句的地方使用该标签-->
  <include refid="defaultSql"></include>
  ```



#### Mybatis中的多表操作

- ONGL表达式

  > 对象图导航语言，可以通过`对象名.属性名`来直接获取属性值

- 左外连接获取双表数据

  `resultMap`配置，现在要输出的实体类中加入另一实体类的声明。

  ```xml
  <resultMap id="userMap" type="info.fangou.domain.User2">
          <id property="id" column="id" ></id>
          <result property="username" column="username"></result>
          <result property="birthday" column="birthday"></result>
          <result property="sex" column="sex"></result>
          <result property="address" column="address"></result>
  		<!--配置user实体类中account集合的映射-->
      	<!--property：user实体类中集合的对象标识符，ofType：account实体类的全限定类名-->
          <collection property="accounts" ofType="info.fangou.domain.Account">
              <id property="ID" column="ID" ></id>
              <result property="UID" column="UID"></result>
              <result property="MONEY" column="MONEY"></result>
          </collection>
  </resultMap>
  ```

  SQL语句编写

  ```xml
  <select id="findAll2" resultMap="userMap">
          SELECT * FROM `user` LEFT JOIN `account` ON `user`.id = `account`.UID;
  </select>
  ```

#### 延迟加载与立即加载

### Spring框架

#### IOC的概念和作用

> 控制反转，将创建对象的权利交给框架，是框架的重要特征。包括依赖注入和依赖查找。
>
> 作用：削减程序的耦合。

##### Spring配置使用过程

1. 配置文件

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd">
   	<!--配置javabean-->
       <!--id为唯一识别字段，自定义；class为javabean的全限定类名-->
       <bean id="..." class="...">
           <!-- collaborators and configuration for this bean go here -->
       </bean>
   
       <bean id="..." class="...">
           <!-- collaborators and configuration for this bean go here -->
       </bean>
   
       <!-- more bean definitions go here -->
   
   </beans>
   ```

2. 调用`Spring`获取Bean对象

   ```java
   //获取核心容器对象 
   ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");//配置文件名
   //获取Bean对象                      //配置文件中的id
   AccountDao accountDao = ac.getBean("accountDao", AccountDao.class);
   ```

   - `ApplicationContext`的三个实现类

     ```java
     //只能加载类路径下的配置文件
     ClassPathXmlApplicationContext("");
     //可以加载任意路径下的配置文件
     FileSystemXmlApplicationContext("");
     //用于读取注解创建容器
     AnnotationConfigApplicationContext("");
     ```

   - `BeanFactory`和`ApplicationContext`的区别

     - 前者在创建对象策略上采用延迟创建，在对象使用时才创建，适用于多例对象创建；
     - 后者策略采用立即创建，一读取完配置文件马上创建配置文件中的对象，适用于单例对象创建。

##### Spring中Bean对象的生命周期

1. 单例对象：随着容器的创建而创建，随容器的销毁而消亡，生命周期与容器相同。
2. 多例对象：当使用对象时由`Spring`框架为我们创建，当长时间不使用且没有其他对象引用时由`Java`垃圾回收机制回收。

##### Spring依赖注入

> 依赖关系：当前类中需要用到其他类对象。由Spring管理对象间的依赖关系。
>
> 依赖注入：依赖关系的维护称之为依赖注入

- 能够注入的数据类型：
  1. 基本类型和`String`
  2. 在配置文件中或注解配置过的其他`Bean`
  3. 复杂类型 / 集合类型
  
- 注入的方式：

  1. 使用构造函数注入
  2. 使用`set`方法注入
  3. 使用注解注入

- 构造函数注入

- `Set`方法注入

  

##### Spring的注解配置与使用

- 注解的作用

  1. 用于创建对象

     > 等同XML配置中的<bean>标签

     - @Component()

       作用：将当前类存入容器

       属性：value：用于指定bean的id，若不写则默认为类名首字母改小写。

     - @Controller：通常用于表现层

     - @Service：通常用于业务层

     - @Repository：通常用于持久层

       以上三个注解作用与`Component`相同，分别用在三层不同位置

  2. 用于注入数据

     > 等同XML配置中在<bean>标签内的<property>标签

     - @autowired

       作用：自动按照类型注入，只要容器中有唯一一个`bean`对象类型与要注入的变量类型匹配，就可以注入成功，当有两个或以上类型匹配的对象，则先根据类型划出匹配的范围，再将变量名作为`id`，寻找`id`匹配的对象，若找不到，则报错。
       
     - @qualifier

       作用：按照类型注入的基础之上再按照名称注入，在给类成员注入时不能单独使用，给方法参数注入时可以单独使用。

       属性：value：用于指定注入`bean`的`Id`。

     - @resource

       作用：直接按照`bean`的`id`注入，可独立使用。

       属性：name：用于指定注入`bean`的`Id`。

     - @value

       作用：用于注入基本类型和`String`类型

       属性：value：用于指定数据的值，也可以使用`SpEL`。

  3. 用于改变作用范围

     > 等同XML配置中在<bean>标签中的`scope`属性

     - @scope

       作用：用于指定`bean`的作用范围

       属性：

       ​	value：

       ​		常用取值：`singleton`，`prototype`，单例模式或多例模式。

  4. 生命周期相关

     > 等同XML配置中在<bean>标签中的`init-method`和`destory-method`属性
     
     - @PreDestory：用于指定销毁方法
     - @PostConstruct：用于指定初始化方法

- 使用注解配置

  1. 修改主配置文件

     ```xml
     <?xml version="1.0" encoding="UTF-8"?>
     <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         <!--添加context命名空间-->
         xmlns:context="http://www.springframework.org/schema/context"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
             http://www.springframework.org/schema/beans/spring-beans.xsd
             http://www.springframework.org/schema/context
             http://www.springframework.org/schema/context/spring-context.xsd">
     
         <context:annotation-config/>
     	<!--在此处写明使用接口的类的包名-->
     	<context:component-scan base-package=""></context:component-scan>
     </beans>
     ```

  2. 在类名上加注解

     ```java
     @Component("accountService")//注解内写明id，如不写明则id默认为类名首字母改小写(accountServiceImpl)
     public class AccountServiceImpl implements AccountService {
         
     }
     ```

  3. 使用容器获取类对象

     ```java
     public class Main {
         public static void main(String[] args) {
     
             ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");
             
             AccountService accountService = ac.getBean("accountServiceImpl", AccountService.class);
             
         }
     }
     ```

##### Spring的配置类与配置注解

- 配置注解

  - @Configuration

    > 应用于一个类上，注明该类为Spring配置类

    ```java
    @Configuration
    public class SpringConfig {
        
    }
    ```

  - @ComponentScan

    > 用于通过注解指明Spring容器在创建时要扫描的包

    ```java
    @Configuration
    @ComponentScan("") //通过属性指定创建容器时要扫描的包
    @ComponentScan({"",""}) //如果有多个包，将包名用大括号包含
    public class SpringConfig {
    
    }
    ```

  - @Bean

    > 用于将当前方法的返回值作为bean对象存入Spring容器
    >
    > 属性：name  用于指定bean的id值。默认为当前方法名

  - @Import

    > 用于在配置类中导入其他配置类
    >
    > 属性：value  指定其他配置类的字节码文件数组(类名.class)

  - @PropertySource

    > 用于指定properties文件的路径
    >
    > 属性：value  指定文件的路径和文件名
    >
    > ​			关键字：classpath  表示类路径下

    ```java
    @PropertySource("classpath:profile.properties")
    ```

##### Spring整合Junit

- 导入`Spring-test`

  ```xml
  <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>5.0.2.RELEASE</version>
  </dependency>
  ```

- 使用注解替换原有的运行器

  - @RunWith：指定运行器

  - @ContextConfiguration：指定配置文件或配置类

    属性：classes：若使用注解配置，则指定配置类的字节码文件

    ​            locations：若使用配置文件，则指定配置文件类路径

  ```java
  @RunWith(SpringJUnit4ClassRunner.class)
  @ContextConfiguration(classes = SpringConfig.class)
  public class Test1 {
      @Autowired
      private AccountService accountService;
      @Test
      public void test1(){
          accountService.save();
      }
  }
  ```

#### AOP的概念

> 通过配置的方式，实现动态代理
>
> Joinpoint：连接点。指的是被拦截的点，在Spring中指方法，因为Spring只支持方法类型的连接点。
>
> Pointcut：切入点。指的是对哪些Joinpoint进行拦截的定义。
>
> Advice：通知/增强。通知是指拦截到Joinpoint后所要做的事情。
>
> ​				通知类型：前置通知，后置通知，异常通知，最终通知，环绕通知。
>
> Introduction：引介。引介是一种特殊的通知。在不修改类代码的前提下，其可以在运行期为类动态的添加一							些方法或Field。
>
> Target：目标对象。

##### 配置AOP

- 配置文件修改

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      <!--配置AOP命名空间-->
      xmlns:aop="http://www.springframework.org/schema/aop"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/aop
          http://www.springframework.org/schema/aop/spring-aop.xsd">
  
      
  </beans>
  ```

- 



### SpringMVC

> 是一个基于MVC设计思想的表现层框架。

#### SpringMVC框架配置

##### 一、前端控制器配置

> 前端控制器是一个servlet，要在web.xml中配置

```xml
<web-app>
  <display-name>Archetype Created Web Application</display-name>
  <!--配置前端控制器并拦截所有请求-->
  <servlet>
    <servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
       
      <!--配置加载Spring配置文件-->
      <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:springmvcConfig.xml</param-value>
    </init-param>
    
      <!--配置在服务器启动时加载servlet-->
    <load-on-startup>1</load-on-startup>  
  </servlet>
  <servlet-mapping>
    <servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>  
</web-app>
```

##### 二、SpringMVC控制器类配置

```java
@Controller //使用注解将类加入Spring容器
@RequestMapping("/param") //设定访问路径
public class ParamController {
    
    @RequestMapping("/saveAccount")
    public String saveAccount(Account account){
        System.out.println(account);
        return "success";
    }
}
```

##### 三、Spring容器配置

> 配置Spring配置文件

```xml
<!--Spring配置文件 springmvcConfig.xml-->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/mvc
       http://www.springframework.org/schema/mvc/spring-mvc.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd">

    <context:component-scan base-package="info.fangou"/>
    
</beans>
```

##### 四、视图解析器配置

> 配置Spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       ...
       
    <context:component-scan base-package="info.fangou"/>

<!--配置视图解析器-->
    <bean id="internalResourceViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <!--配置视图存放的路径-->
        <property name="prefix" value="/WEB-INF/pages/"/>
        <!--配置后缀名-->
        <property name="suffix" value=".jsp"/>
    </bean>
	<!--开启SpringMVC框架注解支持-->
	<mvc:annotation-driven/>
</beans>
```

#### 请求参数绑定

##### 1. 请求参数绑定实体类型

以Account和User实体类为例

```java
public class Account implements Serializable {
    private String username;
    private String password;
    private Double money;
    private User user;
}
public class User implements Serializable {
    private String uname;
    private Integer age;
}
```

控制器方法：

```java
@RequestMapping("/saveAccount")
public String saveAccount(Account account){
     System.out.println(account);
     return "success";
}
```

JSP页面：

页面中`name`属性的值必须与实体类中的属性名相对应。

```jsp
<form action="param/saveAccount" method="post">
            姓名：<input type="text" name="username"/><br>
            密码：<input type="text" name="password"/><br>
            金额：<input type="text" name="money"/><br>
            用户姓名：<input type="text" name="user.uname"/><br>
            用户年龄：<input type="text" name="user.age"/><br>
            <input type="submit" value="提交"/>
</form>
```

##### 2. 解决中文乱码

> 通过配置过滤器的方式设置字符集编码，解决中文乱码

在`web.xml`中设置过滤器，并设置字符集为`utf-8`。

```xml
<filter>
    <filter-name>characterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>UTF-8</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>characterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
```

##### 3.请求参数绑定集合类型

实体类代码

```java
public class Account implements Serializable {

    private String username;
    private String password;
    private Double money;
   
    private List<User> list;
    private Map<String,User> map;

}
```

JSP页面

```jsp
<form action="param/saveAccount" method="post">
            姓名：<input type="text" name="username"/><br>
            密码：<input type="text" name="password"/><br>
            金额：<input type="text" name="money"/><br>
    <!--将umane和age封装到一个User对象中并存到list[0]位置-->
            用户姓名：<input type="text" name="list[0].uname"/><br>
            用户年龄：<input type="text" name="list[0].age"/><br>
	<!--将umane和age封装到一个User对象中并存到map中，key为one-->
            用户姓名：<input type="text" name="map['one'].uname"/><br>
            用户年龄：<input type="text" name="map['one'].age"/><br>
            <input type="submit" value="提交"/>
</form>
```

##### 4.自定义数据类型转换

> 主要用于日期格式的转换，以日期为例

1. 编写转换类

   ```java
   //实现Converter转换接口
   public class StringToDateConverter implements Converter<String, Date> {
       @Override
       public Date convert(String s) {
           if (s == null) {
               throw new RuntimeException("空");
           }
           DateFormat df = new SimpleDateFormat("yyyy-MM-dd");
           try {
               return df.parse(s);
           } catch (ParseException e) {
               e.printStackTrace();
           }
           return null;
       }
   ```

2. 在Spring配置文件中配置转换器对象并开启

   ```xml
   <!--配置自定义转换器对象-->
   <bean id="conversionService" class="org.springframework.context.support.ConversionServiceFactoryBean">
           <property name="converters">
               <set>
                   <bean class="info.fangou.utils.StringToDateConverter"/>
               </set>
           </property>
       </bean>
   
       <!--开启自定义转换器对象-->
       <mvc:annotation-driven conversion-service="conversionService"/>
   ```

##### 5.获取原生Servlet API

> 用于在控制器中获取HttpServletRequest和HttpServletResponse。

```java
@RequestMapping("/test")
//直接在参数列表中添加需要获取的对象
public String servletTest(HttpServletRequest request, HttpServletResponse response){
    HttpSession httpSession = request.getSession();
    System.out.println(httpSession);
    return "success";
}
```

#### SpringMVC注解作用

##### 1. RequestMapping

用法：@RequestMapping(path = "/hello")

作用：定义控制器方法的访问路径，当加在方法上时，定义方法的访问路径，当加在类上时，定义类的访问路径。

属性：value：用于指定请求的URL，作用等同于path；

​            method：用于指定请求的方法。

​			例：@RequestMapping(path = "/hello",method = {RequestMethod.GET}) 

​            params：用于指定限制请求参数的条件。他支持简单的表达式，要求请求参数的key和value必须和配置一模一样。

​            headers：用于限制请求消息头的条件。

##### 2. RequestParam

> 用于修饰控制器方法中的变量，将变量名与请求参数名对应。

```java
@RequestMapping("/testAnno")
                       //填请求参数名
public String testAnno(@RequestParam(name = "username") String name){
     System.out.println(name);
     return "success";
}
```

### SSM框架整合

> 用Spring整合SpringMVC和Mybatis

1. 整合思路
   1. 先搭建整合环境
   2. 把Spring搭建配置完成
   3. 使用Spring整合SpringMVC
   4. 使用Spring整合Mybatis
2. 

### Maven使用简介

> Maven是java的项目管理软件，可以自动处理jar包的依赖，类似于python的conda

1. Maven项目结构

   | 目录                               | 目的                                                         |
   | :--------------------------------- | ------------------------------------------------------------ |
   | ${basedir}                         | 存放pom.xml和所有的子目录                                    |
   | ${basedir}/src/main/java           | 项目的java源代码                                             |
   | ${basedir}/src/main/resources      | 项目的资源，比如说property文件，springmvc.xml                |
   | ${basedir}/src/test/java           | 项目的测试类，比如说Junit代码                                |
   | ${basedir}/src/test/resources      | 测试用的资源                                                 |
   | ${basedir}/src/main/webapp/WEB-INF | web应用文件目录，web项目的信息，比如存放web.xml、本地图片、jsp视图页面 |
   | ${basedir}/target                  | 打包输出目录                                                 |
   | ${basedir}/target/classes          | 编译输出目录                                                 |
   | ${basedir}/target/test-classes     | 测试编译输出目录                                             |
   | Test.java                          | Maven只会自动运行符合该命名规则的测试类                      |
   | ~/.m2/repository                   | Maven默认的本地仓库目录位置                                  |

2. Maven字段意义

   所有 POM 文件都需要 project 元素和三个必需字段：groupId，artifactId，version。

   | 节点         | 描述                                                         |
   | ------------ | ------------------------------------------------------------ |
   | project      | 工程的根标签。                                               |
   | modelVersion | 模型版本需要设置为 4.0。                                     |
   | groupId      | 这是工程组的标识。它在一个组织或者项目中通常是唯一的。例如，一个银行组织 com.companyname.project-group 拥有所有的和银行相关的项目。 |
   | artifactId   | 这是工程的标识。它通常是工程的名称。例如，消费者银行。groupId 和 artifactId 一起定义了 artifact 在仓库中的位置。 |
   | version      | 这是工程的版本号。在 artifact 的仓库中，它用来区分不同的版本。例如：com.company.bank:consumer-banking:1.0                                    com.company.bank:consumer-banking:1.1 |

3. Maven仓库的种类

   

4. Maven命令

   |    命令     |       作用       |
   | :---------: | :--------------: |
   |  mvn clean  | 清除项目编译信息 |
   | mvn compile |     编译项目     |
   |  mvn test   |     测试项目     |
   | mvn package |     打包项目     |
   | mvn install |     安装项目     |
   | mvn deploy  |     发布项目     |

5. pom文件中依赖的作用域

   <scope>标签可以设定依赖的作用范围，其取值为`provided`：只在编译时作用；`test`：只在测试时作用

6. 

    