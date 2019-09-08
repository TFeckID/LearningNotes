# Lua随便学学

## 运算符

### 算术运算符

下表列出了 Lua 语言中的常用算术运算符，设定 A 的值为10，B 的值为 20：

| 操作符 | 描述 | 实例               |
| :----- | :--- | :----------------- |
| +      | 加法 | A + B 输出结果 30  |
| -      | 减法 | A - B 输出结果 -10 |
| *      | 乘法 | A * B 输出结果 200 |
| /      | 除法 | B / A w输出结果 2  |
| %      | 取余 | B % A 输出结果 0   |
| ^      | 乘幂 | A^2 输出结果 100   |
| -      | 负号 | -A 输出结果   -10  |

---

### 关系运算符

下表列出了 Lua 语言中的常用关系运算符，设定 A 的值为10，B 的值为 20：

| 操作符 | 描述                                                         | 实例                  |
| :----- | :----------------------------------------------------------- | :-------------------- |
| ==     | 等于，检测两个值是否相等，相等返回 true，否则返回 false      | (A == B) 为 false。   |
| ~=     | 不等于，检测两个值是否相等，相等返回 false，否则返回 true<   | (A ~= B) 为 true。    |
| >      | 大于，如果左边的值大于右边的值，返回 true，否则返回 false    | (A > B) 为 false。    |
| <      | 小于，如果左边的值大于右边的值，返回 false，否则返回 true    | (A < B) 为 true。     |
| >=     | 大于等于，如果左边的值大于等于右边的值，返回 true，否则返回 false | (A >= B) is not true. |
| <=     | 小于等于， 如果左边的值小于等于右边的值，返回 true，否则返回 false | (A <= B) is true.     |

---

### 逻辑运算符

下表列出了 Lua 语言中的常用逻辑运算符，设定 A 的值为 true，B 的值为 false：

| 操作符 | 描述                                                         | 实例                   |
| :----- | :----------------------------------------------------------- | :--------------------- |
| and    | 逻辑与操作符。 如果两边的操作都为 true 则条件为 true。       | (A and B) 为 false。   |
| or     | 逻辑或操作符。 如果两边的操作任一一个为 true 则条件为 true。 | (A or B) 为 true。     |
| not    | 逻辑非操作符。与逻辑运算结果相反，如果条件为 true，逻辑非为 false。 | not(A and B) 为 true。 |

---

### 其他运算符

下表列出了 Lua 语言中的连接运算符与计算表或字符串长度的运算符：

| 操作符 | 描述                               | 实例                                                         |
| :----- | :--------------------------------- | :----------------------------------------------------------- |
| ..     | 连接两个字符串                     | a..b ，其中 a 为 "Hello " ， b 为 "World", 输出结果为 "Hello World"。 |
| #      | 一元运算符，返回字符串或表的长度。 | #"Hello" 返回 5                                              |

---

###  运算符优先级

从高到低的顺序：

```lua
^
not    - (unary)
*      /
+      -
..
<      >      <=     >=     ~=     ==
and
or
```

## 循环

### while循环

语法

```lua
while(condition)
do
   statements
end
```

### for循环

for语句有两大类：

- 数值for循环

  数值for循环语法格式:

  ```lua
  for var=exp1,exp2,exp3 do  
      statement  
  end  
  ```

  var从exp1变化到exp2，每次变化以exp3为步长递增var，并执行一次"执行体"。exp3是可选的，如果不指定，默认为1。

  for的三个表达式在循环开始前一次性求值，以后不再进行求值。

- 泛型for循环

  泛型for循环通过一个迭代器函数来遍历所有值，类似java中的foreach语句。

  Lua 编程语言中泛型for循环语法格式:

  ```lua
  --打印数组a的所有值  
  for i,v in ipairs(a) do 
  	print(v) 
  end  
  ```

  i是数组索引值，v是对应索引的数组元素值。ipairs是Lua提供的一个迭代器函数，用来迭代数组

### repeat...until 循环

> repeat...until 循环语句不同于 for 和 while循环，for 和 while循环d的条件语句在当前循环执行开始时判断，而 repeat...until 循环的条件语句在当前循环结束后判断。

Lua 编程语言中 repeat...until 循环语法格式:

```lua
repeat
   statements
until( condition )
```

repeat...until 是条件后行,所以repeat...until 的循环体里面至少要运行一次。

## 流程控制

### if语句

if 语句语法格式如下：

``` lua
if (condition) then
	statement
end
```

### elseif 语句

```lua
if (condition) then
	statement
  else
    statement
end
```

```lua
if (condition1) then
	statement
elseif (condition2) then
	statement
else
	statement
end
```

---

## 字符串

> 字符串或串(String)是由数字、字母、下划线组成的一串字符。

Lua 语言中字符串可以使用以下三种方式来表示：

- 单引号间的一串字符。
- 双引号间的一串字符。
- `[[`和`]]`间的一串字符。

### 字符串操作

Lua 提供了很多的方法来支持字符串的操作：

| 序号 | 方法 & 用途                                                  | 例子                                                         |
| :--- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| 1    | **string.upper(argument):** 字符串全部转为大写字母。         |                                                              |
| 2    | **string.lower(argument):** 字符串全部转为小写字母。         |                                                              |
| 3    | **string.gsub(mainString,findString,replaceString,num)** 在字符串中替换，mainString为要替换的字符串， findString 为被替换的字符，replaceString 要替换的字符，num 替换次数（可以忽略，则全部替换） | `>string.gsub("aaaa","a","z",3); zzza 3 `                    |
| 4    | **string.find (str, substr, [init, [end]])** 在一个指定的目标字符串中搜索指定的内容(第三个参数为索引)，返回其具体位置。不存在则返回 nil。 | `> string.find("Hello Lua user", "Lua", 1)  7 9 `            |
| 5    | **string.reverse(arg)** 字符串反转                           | `> string.reverse("Lua") auL`                                |
| 6    | **string.format(...)** 返回一个类似printf的格式化字符串      | `> string.format("the value is:%d",4) the value is:4 `       |
| 7    | **string.char(arg) 和 string.byte(arg[,int])** char 将整型数字转成字符并连接， byte 转换字符为整数值(可以指定某个字符，默认第一个字符)。 | `> string.char(97,98,99,100) abcd  string.byte("ABCD",4) 68 string.byte("ABCD") 65 ` |
| 8    | **string.len(arg)**  计算字符串长度。                        | `> string.len("abc") 3 `                                     |
| 9    | **string.rep(string, n))**  返回字符串string的n个拷贝。      | `> string.rep("abcd",2) abcdabcd `                           |



## 函数

### 函数定义

Lua 编程语言函数定义格式如下：

```lua
optional_function_scope function function_name( argument1, argument2, argument3..., argumentn)
   function_body
 return result_params_comma_separated
end
```

解析：

- **optional_function_scope**
- : 该参数是可选的制定函数是全局函数还是局部函数，未设置该参数默认为全局函数，如果你需要设置函数为局部函数需要使用关键字 `local`。

- **function_name:**
- 指定函数名称。

- **argument1, argument2, argument3..., argumentn:**
- 函数参数，多个参数以逗号隔开，函数也可以不带参数。

- **function_body:**
- 函数体，函数中需要执行的代码语句块。

- **result_params_comma_separated:**
- 函数返回值，Lua语言函数可以返回多个值，每个值以逗号隔开。

---

### 函数作为参数传递给变量

- Lua 中我们可以将函数作为参数传递给函数，如下实例：

- ```lua
  myprint = function(param)
     print("这是打印函数 -   ##",param,"##")
  end
  
  function add(num1,num2,functionPrint)
     result = num1 + num2
     -- 调用传递的函数变量
     functionPrint(result)
  end
  myprint(10)
  -- myprint 函数作为参数传递
  add(2,5,myprint)
  ```

---

### 多返回值
Lua函数可以返回多个结果值，比如string.find，其返回匹配串"开始和结束的下标"（如果不存在匹配串返回nil）。
```lua
  > s, e = string.find("www.w3cschool.cn", "w3cschool") 
  > print(s, e)
  5	13
```
Lua函数中，在return后列出要返回的值得列表即可返回多值，如：
```lua
  function maximum (a)
      local mi = 1             -- 最大值索引
      local m = a[mi]          -- 最大值
      for i,val in ipairs(a) do
         if val > m then
             mi = i
             m = val
         end
      end
      return m, mi
  end
  
  print(maximum({8,10,23,12,5}))
```
以上代码执行结果为：

```lua
  23   3
```
### 可变参数

> Lua函数可以接受可变数目的参数，和C语言类似在函数参数列表中使用三点（...) 表示函数有可变的参数。
> Lua将函数的参数放在一个叫arg的表中，**#arg** 表示传入参数的个数。

例如，计算几个数的返回值：

```lua
function average(...)
   result = 0
   local arg={...}
   for i,v in ipairs(arg) do
      result = result + v
   end
   print("总共传入 " .. #arg .. " 个数")v
   return result / #arg
end
  
print("平均值为",average(10,5,3,4,5,6))
```
以上代码执行结果为：
```lua
总共传入 6 个数
平均值为 5.5
```