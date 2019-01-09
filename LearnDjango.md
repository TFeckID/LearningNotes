### Django简介

- django是基于MVT设计模式的框架，即M，model模型，与MVC中的model功能相同，负责数据处理，内嵌ORM框架；V，view视图，与MVC中的C功能相同，接受HttpRequest,业务处理，返回HttpResponse；T，template模版，与MVC中的V功能相同，复制构造封装要返回的html模版，内嵌了模版引擎
- MTV中的Model只能访问关系型数据库，如果要访问非关系型数据库，需引用第三方库

### 项目建立和管理

- 项目建立：在安装好django后，使用以下命令在当前目录自动创建一个django项目

  ```python
  django-admin startproject <project_name>
  ```

  也可使用pycharm等IDE自动创建项目

- 项目结构及文件：

  |---project_name

  ​        |——\__init__.py 

  ​	|——setting.py

  ​	|——urls.py

  ​	|——wsgi.py

  |---app_name

  ​	|——admin.py

  ​	|——\__init__.py

  ​	|——view.py	

  ​	|——model.py

  ​	|——test.py

  ​	|——migrations

  ​	             |——\__init__.py

  - 文件解析：

    - setting.py：项目配置文件，用于管理项目所有的设置属性

    - urls.py：路由文件，通过正则匹配url指定view来响应请求

    - wsgi.py：用于对服务器发布
    - Manage.py：程序入口
    - admin.py：后台管理文件，注册要管理的模型类
    - view.py：视图，用于处理和返回请求
    - model.py：模型文件，用于和数据库交互
    - test.py：测试文件，但不常用
    - migrations：数据迁移文件所处的文件夹

- 应用创建

  - 使用一个应用开发一个业务模块

    ```python
    python manage.py startapp <app_name>  //使用该命令创建一个应用
    ```

- Django常用命令

  ```django
  #创建数据库
  #Django 1.7.1以上版本
  # 1. 创建转移文件
  python manage.py makemigrations
  # 2. 将生成的py文件应用到数据库
  python manage.py migrate
  
  #Django 1.6及以下
  python manage.py syncdb
  
  #清空数据库
  python manage.py flush   
  
  #创建超级管理员
  python manage.py createsuperuser   # 按照提示输入用户名和对应的密码就好了邮箱可以留空，用户名和密码必填
   
  # 修改 用户密码可以用：
  python manage.py changepassword username
  
  #导入导出数据
  python manage.py dumpdata appname > appname.json
  python manage.py loaddata appname.json
  
  #数据库命令行
  python manage.py dbshell 
  #Django 会自动进入在settings.py中设置的数据库，
  #如果是 MySQL 或 postgreSQL,会要求输入数据库用户密码。
  #在这个终端可以执行数据库的SQL语句。
  ```

### 模型的使用

- 定义及作用：模型是数据表结构的抽象，用于与数据库交互

- ORM简介：ORM是“对象-关系-映射”的简介，主要任务是：

  - 根据对象的类型生成表结构
  - 将对象，列表的操作转换为SQL语句
  - 将SQL查询到的结果转换为对象，列表

- Django中的模型包含存储数据的字段和约束，对应数据库中唯一的表

- Django与MySQL数据库连接

  - 主机上安装MySQL数据库与mysql的python包

    ```python
    pip install mysql-python #python2安装此包
    pip install MySQLClient  #python3安装此包
    ```

  - 在settings.py文件中修改如下代码

    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',  #使用mysql的引擎
            'NAME': 'test2',    #连接的数据库名
            'USER': 'root',		#数据库用户
            'PASSWORD': 'mysql',  #数据库密码
            'HOST': 'localhost',  #数据库所在主机地址
            'PORT': '3306',		  #数据库端口
        }
    }
    ```

- 定义模型

  - 在模型中定义属性会生成表中字段
  - Django根据属性的类型确定以下信息：
    - 当前选择的数据库支持字段的类型
    - 渲染管理表单时使用的默认html控件
    - 在管理站点最低限度的验证
  - django会为表创建自动增长的主键列，每个模型只能有一个主键列，如果使用选项设置某属性为主键列后django不会再创建自动增长的主键列
  - 默认创建的主键列属性为id，可以使用pk代替，pk全拼为primary key
  - 字段中不能有 \__（双下划线，因为在Django QuerySet API中有特殊含义（用于关系，包含，不区分大小写，以什么开头或结尾，日期的大于小于，正则等）,也不能有Python中的关键字，name 是合法的，student_name 也合法，但是student__name不合法，try, class, continue 也不合法，因为它是Python的关键字( import keyword; print(keyword.kwlist) 可以打出所有的关键字)

- 模型类实例方法

  ```python
  __str__()  #将对象转换为字符串时会调用 ##相当于java的toString()
  sava()	   #将模型对象保存在数据表中
  delete()   #将模型对象从数据表中删除
  ```

- 管理器Manager

  - 管理器是模型类的一个属性，用于将对象与数据表进行映射，是Django的模型类进行数据库操作的接口，Django应用的每个模型类都至少拥有一个管理器

  - Django支持自定义管理器类，继承自models.Manager；若未自定义管理器，Django将自动生成一个管理器object

  - 自定义管理器主要用于两种情况：

    - 修改默认查询集，重写get_queryset()方法

      ```python
      #在model.py中编写如下代码
      class BookInfoManager(models.Manager):
          def get_queryset(self):
              #默认查询未删除的图书信息
              #调用父类的成员语法为：super(子类型, self).成员
              return super(BookInfoManager, self).get_queryset().filter(isDelete=False)
      ```

      * 在模型类中BookInfo中定义控制器

        ```python
        class BookInfo(models.Model):
            ...
            booksManager = BookInfoManager()
        ```

    - 向管理器类中添加额外的方法，比如创建对象

      ```python
      class BookInfoManager(models.Model):
          def create(self,btitle,bpub_date):
              b=BookInfo()
              b.btitle=btitle
              ...
              return b
      '''
      	定义该方法后，以后新建bookInfo对象时可以使用以下语法：
      	b=BookInfo.booksManager.create(<属性值>)
      '''
      ```

- 查询

  - 查询集
    - 查询集表示从数据库中获取的对象的集合

    - 查询集可以包含任意个过滤器

    - 查询集为惰性执行，创建查询集不会访问数据库，调用数据时才会访问数据库

    - 何时对查询集求值：迭代，序列化，与if合用

    - 返回查询集的方法，即如何获取查询集：
      - all()             返回所有对象
      - filter()         过滤器，按一定的规则过滤满足条件的数据并返回查询集
      - exclude()    过滤器，按一定规则过滤不满足条件的数据
      - order_by()  排序
      - values()      将查询结构一个对象构成一个字典并排成列表，类似于json

    - 返回单个结果的方法

      ```python
      get()       #返回单个结果
      			#如果未找到会引发"模型类.DoesNotExist异常"
        			#如果返回多条结果会引发"模型   类.MultipleObjectsRetrned"异常
      count()     #返回当前查询结果的总条数
      first()     #返回第一个结果
      last()      #返回最后一个结果
      exists()    #判断查询集中是否返回有数据，如果有则返回True
      ```

  - 字段查询

    - 用字段与一个常量值比较，相当于SQL里的where语句，作为方法filter(),exclude(),get()的参数

    - 语法：属性名称__比较运算符=常量值

    - 对于外键，使用“属性名_id”表示外键的原始值

    - 转义：like语句中使用了%与，匹配数据中的%与，在过滤器中直接写，例如：filter(title__contains="%")，表示 where title like '%\%%'

      表示查找标题中含有%的

    - 比较运算符

      - exact：表示判等，大小写敏感；如果没有写比较运算符，默认为判等

        ```python
        filter(isDelete = False)
        filter(isDelete__exact = False)
        ```

      - contains：是否包含，大小写敏感

        ```python
        exclude(btitle__contains = '传')
        ```

      - startswith,endswith：以value开头或结尾，大小写敏感

        ```python
        exclude(btitle__endswith = '传')
        ```

      - isnull，isnotnull：是否为null

        ```python
        filter(btitle__isnull = False)
        ```

      - 在比较运算符的前面加个i表示不区分大小写，如istartwith

      - in：是否包含在范围内

        ```python
        filter(id__in = [1,2,3,4,5])
        ```

      - gt，gte，lt，lte：大于，大于等于，小于，小于等于

        ```python
        filter(id__gt = 3)
        ```

      - year，month，day，week_day，hour，minute，second：对时间日期间的类型进行运算

        ```python
        filter(bpub_date__year = 1990)
        filter(bpub_date__gt = date(1990,12,31))
        ```

      - 跨关联关系的查询，处理join查询

        - 语法：模型类名<属性名><比较>，可以没有__<比较>的部分，表示等于，结果等同

          inner join

        - 可反向使用，即在关联的两个模型中都可使用

          ```python
          filter(hero_info__hcontent__contains = "八") #查询书中英雄的描述包含"八"的书名
          ```

        - 查询的快捷方式：pk，pk表示primary key，默认主键是id

          ```python
          filter(pk__lt = 6)
          ```

- 聚合

  - 使用aggregate()函数返回聚合函数的值

  - 聚合函数有：Avg，Count，Max，Min，Sum

     ```python
      from django.db.models import Max
      maxDate = list.aggregate(Max('bpub_date')) #查询最大的日期
     ```

  - Count的一半用法

    ```python
    count = list.Count()
    ```

- F对象

  - 可以使用模型的字段A与字段B进行比较，如果字段A出现在等号的左边，则字段B出现在等号右边，需要F对象构造

    ```python
    list.filter(<字段名A>__gte=F('<字段名B>'))
    ```

- Q对象

  - 过滤器的方法中的关键字查询会合并为And进行

  - 要进行or查询时，需要使用Q()对象

  - Q对象用于封装一组关键字参数，这些参数与“比较运算符中的相同”

    ```python
    from django.db.models import Q
    list.filter(Q(pk__lt = 6))
    ```

  - Q对象可以使用&，|操作符组合使用

  - 当操作符用于两个Q对象时，会产生一个新的Q对象

    ```python
    list.filter(pk__lt = 6).filter(bcomment__gt = 10)
    list.filter(Q(pk__lt = 6)|Q(bcomment__gt = 10))
    ```

  - 使用～在Q对象前面表示取反

    ```python
    list.filter(~Q(pk__lt = 4))
    ```

  - 过滤器函数可以使用多个Q对象与关键字参数，所有参数将and在一起，Q对象必须在关键字参数前面

- 模型使用步骤

  - 定义模型类

  - 创建迁移文件：根据模型类生成类SQL代码

    ```python
    python manage.py makemigrations
    ```

  - 执行迁移：根据迁移文件在数据库内生成表

    ```python
    python manage.py migrate
    ```

  - 使用模型操作数据：

    - 使用以下命令打开django的shell

      ```java
      python manage.py shell
      ```

    - 在shell中创建对象并使用

      ```python
      #创建模型对象，相当于insert操作
      from booktest.models import BookInfo
      book = BookInfo()  #创建对象
      book.title = ''    #给对应的属性赋值
      book.save()        #保存
      
      #修改对象属性，相当于update操作
      book = BookInfo.object.get(id=*)  #获取之前的对象
      book.title = ""     #修改相关属性
      book.save()         #保存
      
      #删除操作
      book.delete()
      
      #查询操作
      
      BookInfo.objects.all()   #查询所有
      BookInfo.objects.get(id=*)   #查询某一个
      ```

- 元选项

  - 在模型类中定义类Meta，设置元信息

    ```python
    class BookInfo(models.Model):
        ...
        class Meta():
            db_table = ''   #定义数据表名称
            ordering = ['id']  #对象的默认排序字段，获取对象的列表时使用，接受属性构成的列表
            				   #字符串前加-，即'-id'表示倒序，不加表示正序
    ```


### 后台管理站点

- Django自带有后台管理界面，在url后加上／admin打开后台管理界面，在使用之前要用以下命令新建超级管理员账户

  ```python
  python manage.py createsuperuser
  ```

- 要管理模型，需要在admin.py中注册该模型类

  ```python
  #在admin.py中编写如下代码以注册要管理的模型
  from model import *   #在python3  需用 from .model import *
  admin.site.register(model_name)
  ```

- 要在管理页面显示详细信息，需在admin.py中添加自定义显示方式的类

  ```python
  class model_nameAdmin(admin.ModelAdmin):
    list_display = ['<字段名>']
  '''
  列表页属性
  list_display  显示字段，点击列头进行排列
  list_filter   过滤字段，过滤框会出现在右侧 list_filter = ['<字段名>'] 
  search_fields 搜索字段，搜索框会出现在上侧 search_fields = ['<字段名>']
  list_per_page 分页，分页框会出现在下侧 list_per_page=10
  '''
  admin.site.register(model_name,model_nameAdmin)
  ```

- 布尔值的显示

  发布时性别的布尔值并不直观，可以使用方法进行封装

  ```python
  #在相应的模型类中定义如下方法
  def gender(self):
    if self.hgender:
      return '男'
    else:
      return '女'
  gender.short_description = '性别'
  # 在admin中注册时用gender代替hgender
  class model_nameAdmin(admin,ModelAdmin):
    list_display = ['<字段名>','gender']
  ```

### 视图与url

#### 视图

- 视图接受web请求并返回web响应
- 视图就是一个python函数，被定义在view.py内
- 响应可以是一张网页的HTML内容，一个重定向或404错误

### 模版

- 模版中的标签

  ```python
  {{<变量名>}}    #输出大括号中的变量名
  {%  %}         #在大括号中写代码段
  {{<字典名>.<字段名>}}   #在模版中显示字典内容
  {% for key, value in <字典名>.items %}   #遍历字典
      {{ key }}: {{ value }}
  {% endfor %}
  ```

- 在for循环中判断是否为最后一项

  ```python
  {% for item in List %}
      {{ item }}
    	{% if not forloop.last %},{% endif %} 
  {% endfor %}
  ```

  forloop.last为应用在for循环中的一个变量，作用是判断当前是否为最后一项，当为最后一项是该值为true

  - 循环中的一些变量

    ```python
    forloop.counter	         #索引从 1 开始算
    forloop.counter0	       #索引从 0 开始算
    forloop.revcounter	     #索引从最大长度到 1
    forloop.revcounter0	     #索引从最大长度到 0
    forloop.first	           #当遍历的元素为第一项时为真
    forloop.last	           #当遍历的元素为最后一项时为真
    forloop.parentloop	     #用在嵌套的 for 循环中，获取上一层 for 循环的 forloop
    ```

  - 当列表中可能为空值时用for empty

    ```python
    <ul>
    {% for athlete in athlete_list %}
        <li>{{ athlete.name }}</li>
    {% empty %}
        <li>抱歉，列表为空</li>
    {% endfor %}
    </ul>
    ```

- 在模版中获得视图对应的变量

  ```python
  # views.py
  def add(request, a, b):
      c = int(a) + int(b)
      return HttpResponse(str(c))
  
  # urls.py
  urlpatterns = patterns('',
      url(r'^add/(\d+)/(\d+)/$', 'app.views.add', name='add'),
  )
   
  # template.html
  {% url 'add' 4 5 %}
  ```

- 在模版中获取当前用户

  ```python
  {{ request.user }}
  ```

  如果登陆就显示内容，不登陆就不显示内容

  ```python
  {% if request.user.is_authenticated %}
      {{ request.user.username }}，您好！
  {% else %}
      请登陆，这里放登陆链接
  {% endif %}
  ```

- 获取当前网址

  ```python
  {{ request.path }}
  ```

- 获取当前GET参数

  ```python
  {{ request.GET.urlencode }}
  ```
