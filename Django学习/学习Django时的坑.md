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

