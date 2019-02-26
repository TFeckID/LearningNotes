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
      - TreeSet
        - 由二叉树实现

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

  

