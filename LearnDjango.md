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

  - 

### 模型的使用

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
  from model import *   #在Django 2.*版本以上需用 from .model import *
  admin.site.register(model_name)
  ```

### 视图与url



