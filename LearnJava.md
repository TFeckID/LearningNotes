# Java从入门到问灵

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

###四种权限修饰符的作用

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

### Object类的概述

- Object类概念
  - 类层次结构的根类
  - 所有类方法都直接或间接继承自该类
- 构造方法
  - public Object()
- 成员方法
  - hashCode()方法，返回对象的哈希码值
  - getClass()方法，返回此对象的运行时类(取得字节码文件)

### String类的概述

- String类的获取功能

  ```java
  int length() //获取字符串长度
  char charAt(int index) //获取对应位置的字符
  int length() //获取字符串的长度
  char charAt(int index) //获取索引对应位置的字符
  int indexOf(int ch) /*返回指定字符在字符串中第一次出现处的索引，                       若字符不存在，返回 -1。*/
  int indexOf(String str) /*获取指定字符串中第一个字符在该字符串中                       第一次出现处的索引，若不存在，返回 -1。*/
  int indexOf(String str,int fromIndex) /*获取指定字符串在对应                                         索引之后第一次出现的                                         位置的索引*/
  int indexOf(char ch，int fromIndex) /*获取指定字符在指定索引后                                      第一次出现处的索引*/
  int lastIndexOf(char ch) /*从字符串最后向前查找指定字符第一次出                            现的位置*/
  String substring(int start)  /*从指定位置开始截取字符串，默认到                                行尾*/
  String substring(int start，int end)  /*从指定位置开始到指定                     位置前结束截取字符串 （包含头，不包含尾）*/
  ```

- String类的转换功能

  ```java
byte[] getBytes() //把字符串转换成字节数组
char[] toCharArray() //把字符串转换为字符数组
static String valueOf(Object) //把任意类型数据转换为字符串
String toLowerCase() //把字符串转换成小写
String toUpperCase() //把字符串转换成大写
String concat(String str) //拼接字符串
  ```

### StringBuffer类

- StringBuffer类的定义

  一个线程安全的可变序列，类似于String的字符串缓冲区，不可更改（指不可像String那样随意连接），但可调用方法改变其长度和内容(append()等方法)

- String和StringBuffer的区别

  - String是一个不可变的字符序列
  - StringBuffer是一个可变的字符序列 

- StringBuffer的构造函数

  ```java
  public StringBuffer()  //无参构造，默认创建16字符容量
  public StringBuffer(int capacity)  //指定容量的StringBuffer对象
  public StringBuffer(String str)  //指定字符串的StringBuffer对象
  ```

- StringBuffer的方法

  ```java
  public int capacity() //返回缓冲区的容量
  public int length() //返回长度(字符数)
  public StringBuffer append(String str) //将任意字符串添加进缓冲区并返回StringBuffer本身
  public StringBuffer insert(int offset, String str) //在指定位置将任意类型的数据插入缓冲区并返回其本身
  public StringBuffer deleteCharAt(int index) //删除索引指向的字符
  public StringBuffer delete(int start,int end) //删除两个索引之间的内容,包含头不包含尾
  public StringBuffer replace(int start,int end,String str) //将索引区间的内容用str替换,包含头不包含尾
  public StringBuffer reverse() //字符串反转
  public String substring(int index) //从索引位置截取字符串至末尾
  public String substring(int start,int end) //从索引开始截取到索引结束，包括头不包括尾
  ```

### StringBuilder类

- 成员方法：与StringBuffer一致

- 与StringBuffer的区别：StringBuffer是jdk1.0版本的，线程安全，效率低

  ​					 StringBuilder是jdk1.5版本的，线程不安全，效率高

### Arrays类的概述和方法

- 概述：针对数组进行操作的工具类，提供排序，查找等方法

- 成员方法：

  ```java
  public static String toString(int[] arr) //数组转字符串
  public static void sort(int[] arr) //数组排序
  public static int binarySearch(int[] arr, int key) //查找元素
  public static List<T> asList(T ... a) //返回由数组元素生成的集合
  ```

### 基本数据类型包装类

- 概述：将基本数据类型包装成对象以便于在其中定义更多的功能方法以更好地使用该数据

- 基本数据类型有八种，其中七种有parse方法可以将其字符串表现形式解析为基本数据类型，Character没有该方法，原因是char无法存储多个字符

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
  public int intValue() //以int形式返回该Integer对象的值
  public static int parseInt(String s) //将字符串解析成有符号十进制整数
  ```

- JDK1.5新特性

  - 自动装箱与拆箱：将基本数据类型自动包装成包装类，或将包装类自动拆箱成基本数据类型
  - 如果数据的范围在byte的取值范围(-128,127之间)，自动装箱不会新创建对象，而是从常量池中获取，超过byte取值范围则会在堆中新创建对象

### 正则表达式

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
  |         |                           |                                                      |

- 正则表达式中的方法

  ```java
  public String[] split(String reg) //根据给定的正则表达式切割字符串
  public static replaceAll(String reg,String replacement) //根据正则表达式替换字符串中的元素
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

- Math类的概述和方法使用

  - 概述：用于基本数学运算的工具类

  - 成员方法

    ```java
    public static int abs(int a) //返回绝对值
    public static double ceil(double a) //对小数向上取整
    public static double floor(double a) //对小数向下取整
    public static int max(int a,int b)  //返回两数中的最大值
    public static double pow(double a,double b) //返回a的b次方
    public static double random() //生成一个随机数
    public static int round(float a) //四舍五入
    public static double sqrt(double a) //返回a的开平方
    ```

- System类的概述

  - 成员：

    ```java
    System.in //标准键盘输入流
    System.out //标准输出流
    
    public static void gc() //运行垃圾回收器
    public static void arraycopy(Object src,int srcPos,Object dest,int destPos,int length)
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
        - 同ArrayList，但时间较早
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

  - 并发修改：使用迭代器遍历的同时集合在增减元素，称为并发修改,并发修改在普通的迭代器中是不被允许的，因为在开始生成迭代器时就已告知迭代器元素的总数，开始迭代后元素总数不可变。此时，可用ListIterator，此为List专有的迭代器，可以实现迭代的同时增加元素

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

### Map的概述及用法

- 一个可变长度的键值对的双列集合
- HashMap：以哈希算法实现的Map
- TreeMap：以二叉树实现的Map，和TreeSet一样可以自动排序
- Map接口的方法

```java
V put(K key,V value) //根据键值对添加元素，如果键不存在，则直接存储并返回null,若键存在，则覆盖原                        值，并返回原来的值
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

### JDBC的使用

- 代码示例

  ```java
  try {
       //注册JDBC驱动
  	 DriverManager.registerDriver(new Driver()); 
      
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
      request.getParameter("<输入框name>") //使用该方法提取request中的表单信息
      ```

      

   3. response：服务端返回给客户端的信息

      ```java
      PrintWriter response.getWriter(); //返回一个PrintWriter对象
      pw.write(<要返回的字符串>)；
      response.getWriter().write(<要返回的字符串>); //或者直接这样返回
      response.setCharacterEncoding(); //设置返回的字符集
      response.setHeader("Content-Encoding", "UTF-8"); //设置浏览器以什么字符集解析页面
      ```

   4. 


#### Cookie和Session



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