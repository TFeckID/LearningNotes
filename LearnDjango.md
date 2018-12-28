### Django简介

- django是基于MVT设计模式的框架，即M，model模型，与MVC中的model功能相同，负责数据处理，内嵌ORM框架；V，view视图，与MVC中的C功能相同，接受HttpRequest,业务处理，返回HttpResponse；T，template模版，与MVC中的V功能相同，复制构造封装要返回的html模版，内嵌了模版引擎
- MTV中的Model只能访问关系型数据库，如果要访问非关系型数据库，需引用第三方库

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
