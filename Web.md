# HTML

### What is HTML?

**H**yper **T**ext **M**arkup **L**anguage, using markup tag to describe website.

CSS stands for Cascading Style Sheets.

### HTML Basic

1. HTML document = website (almost)

2. HTML label is not case sensitive.

3. The attribute value should always be enclosed in quotation marks. 

4. The browser will remove extra spaces and blank lines in *source code*
5. Responsive web design

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### Document

| Tag       | description                              |
| --------- | ---------------------------------------- |
| html      | document                                 |
| body      | body                                     |
| h1 to h6  | heading                                  |
| hr /      | horizontal rule                          |
| <!-- -->  | comments                                 |
| a href="" | link                                     |
| br /      | line break                               |
| title     | extra information displayed as a tooltip |
| img       | image                                    |
| pre       | preformatted text                        |
| style     | CSS style                                |
| link      | external CSS                             |

### Formatting

| Tag            | Description      |
| -------------- | ---------------- |
| b              | bold             |
| strong / small | important /small |
| i              | italic           |
| em             | emphasized       |
| mark           | marked           |
| del            | deleted          |
| sub / sup      | sub / sup        |
| ins            | inserted         |

### Quotations

| Tag        | Description      |
| ---------- | ---------------- |
| abbr       | abbreviation     |
| address    | address          |
| bdo        | text direction   |
| blockquote | quote            |
| cite       | title            |
| q          | inline quotation |

### List

| Tag  | Description               |
| ---- | ------------------------- |
| ul   | unordered list            |
| ol   | ordered list              |
| li   | list item                 |
| dl   | description list          |
| dt   | description term          |
| dd   | describe description term |

### Block & Inline

| Tag    | Description                        |
| ------ | ---------------------------------- |
| div    | section in a document(block-level) |
| span   | section in a document(inline)      |
| iframe | define a inline frame              |

### Class & Id

| Tag   | Description                                      |
| ----- | ------------------------------------------------ |
| class | specify a class for an HTML element. use `.`     |
| id    | specify a unique id for an HTML element. use `#` |

### Image

| Tag     | Description                      |
| ------- | -------------------------------- |
| map     | image map                        |
| area    | click able area inside image map |
| picture | container for image resource     |

### Table

| Tag     | Description   |
| ------- | ------------- |
| table   | table         |
| tr      | table row     |
| th      | table header  |
| td      | table data    |
| caption | table caption |

### Head

| Tag    | Description                                                |
| ------ | ---------------------------------------------------------- |
| head   | information about the document                             |
| title  | title of document                                          |
| base   | default address / target                                   |
| link   | external resource                                          |
| meta   | meta data: charset, keywords, description, author,viewport |
| script | client-side script                                         |
| style  | style                                                      |

### Semantics

| Tag        | Description                            |
| ---------- | -------------------------------------- |
| article    | independent, self-contained content    |
| header     | content for navi and introduct content |
| footer     | footer for ducument or section         |
| nav        | navi links                             |
| aside      | sidebar                                |
| figure     | images                                 |
| figcaption | caption for image                      |

### Forms

| Tag      | Description                     |
| -------- | ------------------------------- |
| form     | form                            |
| input    | imput type: text, radio, submit |
| label    | label for form element          |
| action   | sent to a page                  |
| target   | _blank / _self                  |
| method   | get / post ...                  |
| select   | drop-down list                  |
| textarea | multi-line input                |
| button   | clickable button                |
| legend   | caption                         |
| datalist | pre-defined input data          |
| output   | result of calculation           |



# CSS

CSS: Cascading Style Sheets

| name      | description |
| --------- | ----------- |
| id        | #           |
| class     | .           |
| universal | *           |


### Background

| Tag                   | Example        |
| --------------------- | -------------- |
| background--color     | green          |
| opacity               | opacity 0.3    |
| background-image      | url(.....)     |
| background-repeat     | no-repeat      |
| background-position   | right top      |
| background-attachment | fixed / scroll |

### Border

| Tag           | Description                        |
| ------------- | ---------------------------------- |
| border-style  | solid / dotted / none / hidden     |
| border-width  | 5px / medium / thick (上右下左4个) |
| border-color  | red (上右下左4个)                  |
| border-radius | 5px (圆形框)                       |



# FastAPI 

### Run the code

```
uvicorn [name]:app --reload
```

### First Steps

```python
from fastapi import FastAPI # 1.Import FastAPI.
app = FastAPI()             # 2.FastAPI instance
@app.get("/")				# 3.operation decorator
async def root():			# 4.operation function
    return {"message": "Hello World"} # 5.return content

@app.get("/items/{item_id}")
async def read_item(item_id):
    return {"item_id": item_id}
```

### Predefined Value

```python
class ModelName(str, Enum):
    pass  # 预先定义的可选项
@app.get("/model/{model_name}")
def get_model(model_name: ModelName):
```

### Path parameters containing paths

```python
# /files/{file_path:path}
@app.get("/files/{file_path:path}")
```

### Query Parameters



# Django

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

添加Form，meta是employee对象，

在view和html中修改employee_form 使得返回form

add crispy forms in setting.py

change label and mandatory field