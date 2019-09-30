# 安装mysqlclient出现的问题
1. 首先安装mysql驱动，
    brew install mysql-connector-c
2. 然后发现homebrew未安装又去安装homebrew
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
3. 再安装mysql驱动时，缺少setuptools又挂了,安装setuptools
    curl https://bootstrap.pypa.io/ez_setup.py -o - | python
4. 安装mysqlclient
    pip3 install mysqlclient


#Django.db.utils.OperationalError: (1045, "Access denied for user 'root'@'localhost' (using password: NO)")
1. 今天我在Django 链接 Mysql 数据库 的时候出现了一个错误：

2. Django.db.utils.OperationalError: (1045, "Access denied for user 'root'@'localhost' (using password: NO)")
3. 利用ALTER USER 'root'@'127.0.0.1' IDENTIFIED WITH mysql_native_password BY 'password';

    在Mysql 8.0 中，利用上述语句可以更新用户的加密方式为过去版本的方式。执行命令如下：

    mysql -u root -p

    use mysql；

    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'newpassword'; 

    FLUSH PRIVILEGES; 

    修改密码以后，重新执行

    python manage.py makemigrations

    python manage.py migrate

# url包
1. from django.conf.urls import include, url
    urlpatterns = [
    url(r'^admin/', include(admin.site.urls)),
    url(r'^', include('booktest.urls')) # 包含应用booktest的urls文件
]

# AttributeError at /admin/'WSGIRequest' object has no attribute 'user'

1. 解决方法：修改settings.py文件中的MIDDLEWARE为MIDDLEWARE_CLASSES

# Q对象    &|~
1. 使用之前需要先导入：
    from django.db.models import Q

 2. 用法
 BookInfo.objects.filter(Q(id__gt=3)&Q(bread__gt=30))BookInfo.objects.filter(Q(id__gt=3)|Q(bread__gt=30))BookInfo.objects.filter(~Q(id=3))

 # F对象
 1. 使用之前需要先导入:
    from django.db.models import F

2. 用法
BookInfo.objects.filter(bread__gt=F('bcomment'))
BookInfo.objects.filter(bread__gt=F('bcomment'))

# 聚合函数
1. 使用前需先导入聚合类:
    from django.db.models imoport Sum,Count,Max,Min,Avg

2. 用法
BookInfo.objects.aggregate(Count('id'))
BookInfo.objects.aggregate(Sum('bread'))
BookInfo.objects.filter(id__gt=3).count()

# 查询相关函数
1. get: 返回一条且只能有一条数据，返回值是一个对象，参数可以写查询条件
    all: 返回模型类对应表的所有数据，返回值是QuerySet。
    filter: 返回满足条件的数据，返回值是QuerySet，参数可以写查询条件
    exclude: 返回不满足条件的数据，返回值是QuerySet，参数可以写查询条件。
    order_by: 对查询结果进行排序，返回值是QuerySet，参数中写排序的字段

    F对象：用于类属性之间的比较。
    Q对象：用于条件之间的逻辑关系。

    aggregate: 对于聚合操作，返回值是一个字典，进行聚合的时候需要先导入聚合类
    count: 返回结果集中数据的数目，返回值是一个数字。

2. 注意：
    对于一个QuerySet实例对象，可以继续调用上面的所有函数。


# 查询集
1. all, filter, exclude, order_by调用这些函数会产生一个查询集，
    QuerySet类对象可以继续调用上面所有函数

2. 查询集特性：
 1）惰性查询：只有在实际使用查询集中的数据的时候才会发生对数据库真正的查询
 2）缓存：当使用的是同一个查询集时，第一次的时候回发生实际数据库的查询，
    然后把结果缓存起来，之后再使用这个查询集时，使用的是缓存中的结果。

3. 限制查询集：
    可以对一个查询集进行取下标或者切片操作来限制查询集的结果。
    对一个查询集进行取下标或者切片操作会产生一个新的查询集，下标不允许为负数

4. 用法
    b[0:1].get()
    exists:判断一个查询集中是否有数据。True False 

# 模型类关系
1. 一对多关系
    models.ForeignKey() 定义在多的类中。

2. 对多对关系
    models.ManyToManyFiled() 定义在哪个类中都可以

3. 一对一关系
    models.OneToOneField() 定义在哪个类中都可以

# 关联查询（一对多）
1. 在一对多关系中，一对应的类我们把它叫做一类，多对应的那个类我们把它叫做多类
    我们把多类中定义的建立关联的类属性叫做关联属性。

2. 用法
    查询id为1的图书关联的英雄的信息。
    b = BookInfo.objects.get(id=1)
    b.heroinfo_set.all()
    通过模型类来差
    HeroInfo.objects.filter(hbook__id=1)

    查询id为1的英雄关联的图书信息
    h = HeroInfo.objects.get(id=1)
    h.hbook
    BookInfo.objects.filter(heroinfo__id=1)


3. 通过模型类实现关联查询：
    注意：
    1. 通过模型类实现关联查询时，要查哪个表中的数据，就需要通过哪个类来查
    2. 写关联查询条件的时候，如果类中没有关系属性，条件需要哪些对应类的名字，
        如果类中有关系属性，直接写关系属性

    查询图书信息，要求图书关联的英雄的描述包含'八'
    BookInfo.objects.filter(heroinfo__hcomment__contains='八')
    查询图书信息，要求图书中的英雄大于3
    BookInfo.objects.filter(heroinfo__id__gt=3)
    查询书名为”天龙八图“的所有英雄
    HeroInfo.objects.filter(hbook__btitle='天龙八部')

# 插入、更新和删除
    调用一个模型类对象的save方法的时候就可以实现对模型类对应数据表的插入和更新
    调用一个模型类对象的delete方法的时候就可以实现对模型类对应数据表数据的删除





