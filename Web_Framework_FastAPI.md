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