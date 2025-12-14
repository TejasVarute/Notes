# FastAPI

---

# About FastAPI

- **FastAPI** is modern python web framework, very efficient in building API's. It is based on Python's type hints feature. It is one of the fastest web frameworks on python.

  - As it works on the functionality of starlette and pydantic libraries, its performance is amongst the best and on par with that of NodeJS and Go.
  - In addition to offering high performance, FastAPI offers significant speed for development, reduces human-induced errors in the code, is easy to learn and is completely production-ready.
  - FastAPI is fully compatible with well-known standards of APIs, namely **OPENAPI** and **JSON** schema.

- Required libraries

  - `fastapi` : FastAPI lib
  - `uvicorn/uvicorn[standard]` : (Asynchronous Server Gateway Interface) Server lib
  - `typing` [built-in] : Contains built-in Data Structures [List, Set, Tuple, Dict]
  - `pydantic` [built-in] : Contains BaseModel [acts as base class for creating user defined models].
  - `python-multipart` : To access Form.
  - `aiofiles` : Used for handle static files
  - `jinja2` : Used for templates
  - `sqlalchemy` : It is an interface between python code and database [SQL toolkit & ORM]

  ```shell
  > pip install fastapi uvicorn[standard] aiofiles jinja2 sqlalchemy
  ```

---

# Getting Started with FastAPI

- Check OpenAPI docs,
- Enter url as `http://localhost:8000/docs`.
- To collect API schema (Help to create RESTful APIs based on standards) - use `openapi.json` on docs page.

### . Form in FastAPI

- Text input from Form.
- Eg.

```html
<!-- Form.html -->

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      rel="stylesheet"
      href="{{ url_for('static', path='css/styles.css') }}"
    />
    <title>Login Form</title>
  </head>
  <body>
    <form
      action="http://localhost:8000/auth"
      method="POST"
      enctype="multipart/form-data"
    >
      <h1>Login Form</h1>
      <input
        type="text"
        id="username"
        name="username"
        placeholder="Enter Username Here"
      />
      <input
        type="password"
        id="password"
        name="password"
        placeholder="Enter Password Here"
      />
      <button type="submit">Submit</button>
    </form>
  </body>
</html>
```

```python
@app.get("/login", response_class=HTMLResponse)
async def login(request:Request):
    return template.TemplateResponse('form.html', context={'request' : request})

@app.post("/auth", response_class=HTMLResponse)
async def authentication(username:str=Form(...), password:str=Form(...)):
    if username == 'username' and password == 'password':
        return HTMLResponse("""
                            <h1>Login Successful</h1>
                            """)
    else: return HTMLResponse("""
                              <h1>Login Failed</h1>
                              """)
```

- File input from Form.
- Eg.

```html
<!-- File.html -->

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      rel="stylesheet"
      href="{{ url_for('static', path='css/styles.css' ) }}"
    />
    <title>File Uploaded</title>
  </head>
  <body>
    <form
      action="http://localhost:8000/uploaded"
      method="POST"
      enctype="multipart/form-data"
    >
      <h1>Upload File</h1>
      <input type="file" id="file" name="file" placeholder="Select File" />
      <button type="submit">Submit</button>
    </form>
  </body>
</html>
```

```python
@app.get("/upload_file", response_class=HTMLResponse)
async def file_form(request:Request):
    return template.TemplateResponse("file.html", context={'request' : request})

@app.post('/uploaded', response_class=HTMLResponse)
async def uploaded(file:UploadFile=File(...)):
    if file:
        with open("static/file.png", "wb") as buffer:
            shutil.copyfileobj(file.file, buffer)
        return HTMLResponse("""
                            <h1>File Uploaded Successfully</h1>
                            """)
    else :
        return HTMLResponse("""
                            <h1>Failed to Upload File</h1>
                            """)
```

### . Store Cookie on Client side.

- A **cookie** is one of the HTTP headers. The web server sends a response to client, in addition to the data requested, it also inserts one or more cookies.
- A **cookie** is a very small amount of data, that is stored in client's machine.
- On subsequent connection requests from the same client, this cookie data is also attached along with the HTTP protocol.
- In FastAPI, the cookie parameter is set on the response object with the help of set_cookie() method

```python
response.set_cookie(key, value)
```

- Eg.

```python
from fastapi import FastAPI, Cookie
from fastapi.responses import JSONResponse

app = FastAPI()
@app.post("/cookie/")
async def create_cookie():
    content = {"message" : "cookie set"}
    response = JSONResponse(content=content)
    response.set_cookie(key="username", value="admin")
    return response

@app.get("/readcookie/")
async def read_cookie(username: str = Cookie(None)):
    return {"username" : username}

```

### . Header Parameters

- In order to read the values of an **HTTP header** that is a part of the client request, import the Header object from the FastAPI library, and declare a parameter of Header type in the operation function definition. The name of the parameter should match with the HTTP header converted in `camel_case`.
- Eg.

```python
from typing import Optional
from fastapi import FastAPI, Header

app = FastAPI()
@app.get("/headers/")
async def read_header(accept_lang : Optional[str] = Header(None)):
    return {"Accept-Language" : accept_lang}
```

- Creating Custom header.
- In order to set a custom header, its name should be prefixed with **X**.
- Eg.

```python
from fastapi import FastAPI
from fastapi.responses import JSONResponse

app = FastAPI()

@app.get("/getheaders/")
def set_rsp_headers():
    content = {"message" : "Hello World"}
    headers = {"X-Web-Framework" : "FastAPI", "Content-Language" : "en-US"}
    return JSONResponse(content=content, headers=headers)
```

### . Response Model

- An operation function return A JSON response to the client.
- The response can be in the from of Python primary types, i.e, **numbers**, **string**, **list** or **dict**, etc.
- It can also be form of **Pydantic model**.
- For a function to return a model object, the operation decorator should declare a `response_model` parameter.
- Eg.

```python
from fastapi import FastAPI
from pydantic import BaseModel, Field

app = FastAPI()

class Student(BaseModel):
    id : int
    name : str = Field(None, name="Student Name", max_length=20)
    marks : list[int] = []
    per_marks = float

class Percent(BaseModel):
    id : int
    name : str = Field(None, name="Student Name", max_length=20)
    per_marks = float

@app.post("/marks/", response_model=Percent)
async def get_percent(s1: Student):
    s1.per_marks = sum(s1.marks)/2
    return s1
```

### . Nested Models

- Each attribute of a **pydantic** models has a type.
- The type can be a built-in Python type or model itself.
- Hence, it is possible to declare nested JSON "objects" with specific attribute names, types and validations.
- Eg.

```python
from fastapi import FastAPI
from pydantic import BaseModel
app = FastAPI()

class supplier(BaseModel):
    supplier_id : int
    supplier_name : str

class Product(BaseModel):
    product_id = int
    product_name : str
    price : float
    supplier : Supplier

class Customer(BaseModel):
    customer_id = int
    customer_name : str
    product : tuple[Product]

@app.post("/invoice/")
async def getInvoice(c1:Customer):
    return c1
```

### . Dependencies

- The built-in dependency injection system of FastAPI makes it possible to integrate components easier when building API.
- In programming, **Dependency injection** refers to the mechanism where an object receives other objects that it depends on.
- Advantages,
  - Reuse the same shared logic
  - Share database connections
  - Enforce authentication and security features
- Eg.

```python
from fastapi import FastAPI
app = FastAPI()

########## Dependency function

async def dependency(id: str, name:str, age:int):
    return {"id" : id, "name" : name, "age" : age}

@app.get("/user")
async def user(dep : dict = Depends(dependency)):
    return dep

@app.get("/admin")
async def admin(dep: dict = Depends(dependency)):
    return dep

########## Dependency class
class Dependency:
    def __init__(self, id:str, name:str, age:int):
        self.id = id
        self.name = name
        self.age = age

@app.get("/user")
async def user(dep: Dependency = Depends(Dependency)):
    return dep

@app.get("/admin")
async def admin(dep: Dependency = Depends(Dependency)):
    return dep
```

### . CORS

- Cross-Origin Resource Sharing (CORS) is a situation when frontend application that is running on one client browser tries to communicate with backend through JavaScript code and the backend is in a different **origin** than the frontend.
- The origin here is a combination of protocol, domain name and port numbers.
- As a results, http://localhost and https:localhost have different origins.
- If the browser with a URL of one origin sends a request for the execution of JavaScript code from another origin, the browser sends an **OPTIONS HTTP** request.
- If the backend authorizes the communication from the different origin by sending the appropriate headers it will let the JS in frontend send it requests to the backend. For that, backend must have a list of **allowed origins**.
- To specify explicitly,

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware
app = FastAPI()

origins = ["http://localhost", "http://localhost:8080",]
app.add_middleware(CORSMiddleware, allow_origins=origins, allow_credentials=True, allow_methods=["*"], allow_headers=["*"])

@app.get("/")
async def main():
    return {"message" : "Hello World"}
```

---
