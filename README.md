# Access AWS RDS with Python 3


```python
# DB instance identifier: database-1
# username: admin
# pass: 12345678
# host: database-1.c5jhk7wvcn9a.us-east-2.rds.amazonaws.com
# port: 3306
```


```python
!pip install PyMySQL
```

    Requirement already satisfied: PyMySQL in c:\programdata\anaconda3\lib\site-packages (0.9.3)
    


```python
import pymysql
```


```python
db = pymysql.connect('database-1.c5jhk7wvcn9a.us-east-2.rds.amazonaws.com', 'admin', '12345678')
```


```python
cursor = db.cursor()
```


```python
cursor
```




    <pymysql.cursors.Cursor at 0x25826aeb948>




```python
cursor.execute("select version()")
```




    1




```python
data = cursor.fetchone()
```


```python
data
```




    ('8.0.17',)



## Create a table 


```python
sql = '''drop database kgptalkie'''
cursor.execute(sql)
```




    0




```python
sql = '''create database kgptalkie'''
cursor.execute(sql)
```




    1




```python
cursor.connection.commit()
```


```python
sql = '''use kgptalkie'''
cursor.execute(sql)

```




    0




```python
sql = '''
create table person (
id int not null auto_increment,
fname text,
lname text,
primary key (id)
)
'''
cursor.execute(sql)

```




    0




```python
sql = '''show tables'''
cursor.execute(sql)
cursor.fetchall()
```




    (('person',),)




```python
sql = '''
insert into person(fname, lname) values('%s', '%s')''' % ('laxmi', 'kant')
cursor.execute(sql)
db.commit()

```


```python
sql = '''select * from person'''
cursor.execute(sql)
cursor.fetchall()
```




    ((1, 'laxmi', 'kant'), (2, 'laxmi', 'kant'))




```python

```


```python
sql = '''desc person'''
cursor.execute(sql)
cursor.fetchall()
```




    (('id', 'int(11)', 'NO', 'PRI', None, 'auto_increment'),
     ('fname', 'text', 'YES', '', None, ''),
     ('lname', 'text', 'YES', '', None, ''))

