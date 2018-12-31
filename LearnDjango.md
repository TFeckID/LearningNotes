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

- 模型实例方法

  ```python
  __str__()  #将对象转换为字符串时会调用 ##相当于java的toString()
  sava()	   #将模型对象保存在数据表中
  delete()   #将模型对象从数据表中删除
  ```

- 模型类的属性

  - 属性objects：管理器，是Manage类型的对象，用于与数据库进行交互

  - 当没有为模型类定义管理器时，Django会自动生成一个名为objects的管理器，若有自定义管理器，则Django不再自动生成

  - 为模型类BookInfo定义管理器books的语法如下

    ```python
    class BookInfo(models.Model):
        ...
        books = models.Manager()
    ```

- 管理器Manager

  - 管理器时Django的模型进行数据库操作的接口，Django应用的每个模型都至少拥有一个管理器

  - Django支持自定义管理器类，继承自models.Manager

  - 自定义管理器主要用于两种情况：

    - 修改原始查询集，重写get_queryset()方法

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
            books = BookInfoManager()
        ```

    - 想管理器类中添加额外的方法，比如创建对象

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

### 模版

- 模版中的标签

  ```html
  {{<变量名>}}    <!--输出大括号中的变量名-->
  {%  %}    <!--在大括号中写代码段-->
  ```


