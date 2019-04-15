# 开发过程中的一些记录

## 数据库的配置
参考官方文档：[https://docs.djangoproject.com/en/2.2/ref/databases/](https://docs.djangoproject.com/en/2.2/ref/databases/)
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'OPTIONS': {
            'read_default_file': os.path.join(BASE_DIR, 'my.cnf'),
        },
    }
}
```
OPTIONS的优先级高于配置里面的NAME，PORT
my.cnf内容：
```
[client]
database = NAME
user = USER
password = PASSWORD
default-character-set = utf8
```
无法导入MySQLdb的问题是由于Django默认使用MySQLdb去连接MySQL数据库，可以选择安装MySQLdb或者使用pymysql替换。
如果使用pymysql的话，可以在project包的__init__.py或者settings.py中添加
```
import pymysql
pymysql.install_as_MySQLdb()
```
源码里面是：
```
  sys.modules["MySQLdb"] = sys.modules["_mysql"] = sys.modules["pymysql"]
```
其实就是用pymysql模块替换MySQLdb模块