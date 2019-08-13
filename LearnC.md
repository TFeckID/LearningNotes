# C：从入门到入土

### 枚举类

> 枚举类型为c语言的基本数据类型，他可以限定枚举变量的取值为规定的值。第一个枚举成员的值默认为整型的0，后面的枚举成员依次加1，可以在枚举定义时给任意成员赋值，赋值必须为整型，赋值之后的枚举成员依次在赋的值上加1，之前的成员值不变。

- 枚举定义格式

  ```c
  enum 枚举名 {枚举元素1, 枚举元素2, ...};
  ```

- 遍历枚举

  当枚举元素的值为连续的，可以对枚举进行遍历；当元素的值为离散时，无法对其进行遍历

  ```c
  enum DAY
  {
        MON=1, TUE, WED, THU, FRI, SAT, SUN
  } day;
  int main()
  {
      // 遍历枚举元素
      for (day = MON; day <= SUN; day++) {
          printf("枚举元素：%d \n", day);
      }
  }
  ```

### 指针

- 从函数返回指针

  函数默认不允许返回内部局部变量的地址，若要返回一个指针，必须在函数体内将变量以`static`关键字修饰

- 函数指针

  指向一个函数的指针称为函数指针，

### 字符串

> c/c++中的字符串其实是一个以` '\0' `或`null`结尾的一堆字符组成的字符数组 

- C中提供的操作字符串的函数，使用前必须先包含头文件`string.h`

  ```c
  void strcpy(s1,s2); //复制字符串s2到s1
  void strcat(s1,s2); //连接字符串s2到s1末尾
  int strlen(s1); //返回字符串s1的长度
  int strcmp(s1,s2); //比较s1和s2，若两者相同，则返回0；若s1<2s，则返回负数；反之，返回正数
  char * strchr(s1,ch); //返回一个指针指向字符ch在s1中第一次出现的位置
  char * strstr(s1,s2); //返回一个指针指向字符串s2在s1中第一次出现的位置
  ```

### 结构体

- 如果两个结构体相互包含，则需要对其中一个结构体进行不完整声明

  ```c
  struct B;    //对结构体B进行不完整声明
   
  //结构体A中包含指向结构体B的指针
  struct A
  {
      struct B *partner;
      //other members;
  };
   
  //结构体B中包含指向结构体A的指针，在A声明完后，B也随之进行声明
  struct B
  {
      struct A *partner;
      //other members;
  };
  ```

### 位域

- 

### 文件操作

- 