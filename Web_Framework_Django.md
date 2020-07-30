### Django Tips



```python
#创建project
django-admin startproject projectname

#创建app
python manage.py startapp polls

#每次改变models时候运行
python manage.py makemigrations
python manage.py migrate

#在交互式中创建新的object
python manage.py shell 

# 创建管理员
python manage.py createsuperuser



# 新建model
python manage.py makemigrations [project]
python manage.py sqlmigrate [project] [0001]
python manage.py migrate [project]

```



Django MVT pattern:

Developer provides model, view, template and map it to URL and Django does the magic to serve it to user.



过程



添加Form，meta是employee对象，

在view和html中修改employee_form 使得返回form

add crispy forms in setting.py

change label and mandatory field



