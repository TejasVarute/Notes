# 📘 Python, Django & Frontend IMP Questions (with Answers)

## **Python Core**

### 1. Mutable vs Immutable Types

- **Mutable** → can be changed after creation.
  Examples: `list`, `dict`, `set`, `bytearray`.

  ```python
  l = [1, 2, 3]
  l[0] = 100
  print(l)  # [100, 2, 3]
  ```

- **Immutable** → cannot be changed after creation.
  Examples: `int`, `float`, `str`, `tuple`, `frozenset`.

  ```python
  s = "hello"
  s2 = s.replace("h", "y")
  print(s)   # "hello"
  print(s2)  # "yello"
  ```

---

### 2. Difference between `==` and `is`

- `==` → checks **value equality**.
- `is` → checks **object identity**.

```python
a = [1, 2]
b = [1, 2]
print(a == b)  # True
print(a is b)  # False
```

---

### 3. Decorator

- Function that takes another function and extends/modifies its behavior.

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before function")
        result = func(*args, **kwargs)
        print("After function")
        return result
    return wrapper

@my_decorator
def say_hello():
    print("Hello")

say_hello()
```

---

### 4. `with` Statement / Context Manager

- Manages setup and teardown automatically.

```python
with open("test.txt", "w") as f:
    f.write("Hello")
# File closed automatically
```

- Custom context manager:

```python
class MyContext:
    def __enter__(self):
        print("Enter")
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Exit")
```

---

### 5. Generators vs Iterators

- **Iterator**: has `__iter__()` and `__next__()`.
- **Generator**: created with `yield`, special kind of iterator.

```python
def gen():
    yield 1
    yield 2
g = gen()
print(next(g))  # 1
print(next(g))  # 2
```

- Use: memory-efficient, lazy evaluation.

---

### 6. List Comprehension vs Generator Expression

```python
lst = [x*x for x in range(5)]   # list, stores all values
gen = (x*x for x in range(5))   # generator, lazy
```

---

### 7. `*args` and `**kwargs`

- `*args` → positional arguments (tuple).
- `**kwargs` → keyword arguments (dict).

```python
def func(*args, **kwargs):
    print(args)
    print(kwargs)

func(1, 2, 3, a=10, b=20)
# (1, 2, 3)
# {'a': 10, 'b': 20}
```

---

### 8. GIL (Global Interpreter Lock)

- Only one thread runs Python bytecode at a time.
- Good for I/O-bound tasks, bad for CPU-bound tasks.
- Use `multiprocessing` for CPU-heavy tasks.

---

### 9. Threading vs Multiprocessing

- **Threading**: lightweight, share memory, GIL-limited, best for I/O.
- **Multiprocessing**: separate processes, bypass GIL, best for CPU-bound.

---

### 10. Lambda Function

- Small anonymous function.

```python
add = lambda x, y: x + y
print(add(2, 3))  # 5
```

---

### 11. Exception Handling

```python
try:
    x = 1 / 0
except ZeroDivisionError:
    print("Error")
else:
    print("No error")
finally:
    print("Always runs")
```

---

### 12. Modules & Packages

- **Module** → `.py` file.
- **Package** → directory of modules with `__init__.py`.
- Used to organize code.

---

### 13. Garbage Collection

- Python uses **reference counting**.
- Also has cyclic GC for objects referencing each other.

---

### 14. Map, Filter, Reduce

```python
nums = [1, 2, 3, 4]

squares = list(map(lambda x: x*x, nums))   # map
evens = list(filter(lambda x: x%2==0, nums))  # filter

from functools import reduce
sum_all = reduce(lambda a, b: a+b, nums)   # reduce
```

- Alternative: list comprehensions.

- Explain `*args` and `**kwargs`

  - The `*args` is positional args. Where the args are accessed at function by its position.
  - The `**kwargs` is keyword args. Where the args are accessed at function by its keywords.

- Difference between threading and multiprocessing.

  - Threading is a single processing concept. Here we execute a thread/task at a time and for multiple threads we set priority and conditional statement to process it.
  - The multiprocessing means executing multiple threads at a time parallel.

- What is a lambda function ?

  - Python have a bult in single line function.
  - Eg. lambda x, y : x+y

- Exception handling ?

  - Python has try, except, finally, else.

- What are modules and packages in python.

  - The multiple classes or functions defined in a file is called modules where we can use them in somewhere else.
  - Multiple modules in a folder creates a package.

- What are map, filter, reduce ?
  - The map is a bultin function in python which iterate the give dataset.
  - The filter is used to filter the data and get required data from dataset.
  - reduce is also same like filter but it.

---

## **Django**

### 1. What is Django? (MVT)

- **Model** → database layer.
- **View** → business logic.
- **Template** → presentation.

---

### 2. FBV vs CBV

- **FBV**: simple, explicit.
- **CBV**: reusable, OOP-based, built-in generic views.

---

### 3. Models & Migrations

- **Model**: Python class → DB table.
- **Migration**: schema version control.
- Create with `makemigrations` + `migrate`.

---

### 4. ORM

- Converts Python → SQL.

```python
User.objects.filter(is_active=True)
```

---

### 5. ORM Queries

- `.filter()`, `.get()`, `.exclude()`, `.annotate()`, `.order_by()`.

```python
Book.objects.filter(price__gt=500).order_by("title")
```

---

### 6. `select_related` vs `prefetch_related`

- **select_related** → JOIN, good for FK/One-to-one.
- **prefetch_related** → extra query, caches, good for Many-to-many.

---

### 7. Signals

- Hooks on events (like `post_save`, `pre_delete`).

---

### 8. Middleware

- Process request/response globally.

```python
class MyMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response
    def __call__(self, request):
        response = self.get_response(request)
        return response
```

---

### 9. Forms & ModelForms

- **Form** → custom validation.
- **ModelForm** → auto-generated from model.

---

### 10. Authentication & Authorization

- Built-in `User`, `Permissions`, `Groups`.
- Custom user model → extend `AbstractUser`.

---

### 11. Static & Media Files

- **Static** → CSS, JS, images.
- **Media** → user uploads.

---

### 12. Template Tags & Filters

- `{% for %}`, `{% if %}`, `{% block %}`.
- Custom filters with `@register.filter`.

---

### 13. Deployment

- Use WSGI/ASGI (Gunicorn, uWSGI, Daphne).
- Static files → Whitenoise, Nginx.

---

### 14. Security

- **CSRF** → token.
- **XSS** → escaping.
- **SQL Injection** → ORM prevents.

---

### 15. Django REST Framework (DRF)

- Build APIs.
- `APIView`, `ViewSet`, `Serializer`.

---

### 16. Testing

- Use `TestCase`.
- Test models, views, forms, APIs.

---

## **Frontend Basics**

### 1. HTML vs HTML5

- HTML5 → semantic tags (`<header>`, `<footer>`), audio/video, canvas.

### 2. CSS

- **Box model** (margin, border, padding, content).
- **Flexbox, Grid** for layout.

### 3. JavaScript

- `var`, `let`, `const`.
- ES6: arrow functions, promises, async/await.
- Event handling, DOM manipulation.

### 4. Async vs Sync JS

- **Sync** → blocking.
- **Async** → non-blocking (callbacks, promises, async/await).

### 5. AJAX / Fetch

- Used to call backend APIs.

```js
fetch("/api/data")
  .then((res) => res.json())
  .then((data) => console.log(data));
```

### 6. CORS

- Browser security → restricts cross-origin requests.
- Django → use `django-cors-headers`.

### 7. Responsive Design

- Use **media queries**.

```css
@media (max-width: 600px) {
  body {
    font-size: 14px;
  }
}
```

## ⚛️ React Questions (Fresher-Friendly)

**1. What is React and why is it used?**

- A JavaScript library for building UI components.
- Efficient with Virtual DOM, component-based architecture, reusable UI.

---

**2. Difference between functional and class components?**

- Class components use lifecycle methods (`componentDidMount`, etc.).
- Functional components use **hooks** (`useState`, `useEffect`).

---

**3. What are React Hooks? Give examples.**

- Special functions to use state and lifecycle in functional components.
- Example:

  ```jsx
  import React, { useState } from "react";

  function Counter() {
    const [count, setCount] = useState(0);
    return (
      <div>
        <button onClick={() => setCount(count + 1)}>Click {count}</button>
      </div>
    );
  }
  ```

---

**4. What is JSX?**

- JavaScript XML → allows writing HTML-like syntax in JS.

---

**5. What is the difference between state and props?**

- **Props**: Read-only, passed from parent to child.
- **State**: Local to component, can be updated via `setState` / `useState`.

---

**6. What is the Virtual DOM?**

- A lightweight copy of real DOM. React updates virtual DOM first, then reconciles differences with real DOM (diffing algorithm) → faster updates.

---

**7. How to handle forms in React?**

- Controlled components (input value linked to state).
- Example:

  ```jsx
  const [text, setText] = useState("");
  <input value={text} onChange={(e) => setText(e.target.value)} />;
  ```

---

**8. How do you make API calls in React?**

- Use `fetch` or libraries like Axios inside `useEffect`.

  ```jsx
  useEffect(() => {
    fetch("/api/data")
      .then((res) => res.json())
      .then((data) => setData(data));
  }, []);
  ```

---

**9. What is useEffect used for?**

- Side effects: fetching data, timers, subscriptions.

---

**10. How do React and Django/DRF connect?**

- React (frontend) makes **API requests (fetch/axios)** → Django REST Framework (backend) responds with JSON.

---

---

## 🐍 Django REST Framework (DRF) Questions

**1. What is Django REST Framework?**

- A Django library to build RESTful APIs easily with serializers, viewsets, routers.

---

**2. What is a Serializer in DRF?**

- Converts Django models → JSON (and back).

  ```python
  from rest_framework import serializers
  from .models import Post

  class PostSerializer(serializers.ModelSerializer):
      class Meta:
          model = Post
          fields = '__all__'
  ```

---

**3. What is the difference between APIView and ViewSet?**

- **APIView**: You write each HTTP method (`get`, `post`, `put`).
- **ViewSet**: Less code; uses actions (`list`, `create`, `retrieve`) with routers.

---

**4. How do you define a simple API in DRF?**

```python
from rest_framework import viewsets
from .models import Post
from .serializers import PostSerializer

class PostViewSet(viewsets.ModelViewSet):
    queryset = Post.objects.all()
    serializer_class = PostSerializer
```

- Then map using `DefaultRouter`.

---

**5. What are authentication methods in DRF?**

- SessionAuthentication, TokenAuthentication, JWT.

---

**6. How do you handle permissions in DRF?**

- Use `permission_classes` → e.g., `IsAuthenticated`, `IsAdminUser`.
- Example:

  ```python
  from rest_framework.permissions import IsAuthenticated

  class PostViewSet(viewsets.ModelViewSet):
      permission_classes = [IsAuthenticated]
  ```

---

**7. Difference between `Serializer` and `ModelSerializer`.**

- `Serializer`: Define fields manually.
- `ModelSerializer`: Auto-generates fields from Django model.

---

**8. What is pagination in DRF?**

- Breaking large API results into pages. Configured via `settings.py`.

---

**9. How do you test a DRF API?**

- Using DRF’s APIClient or tools like Postman/Insomnia.

---

**10. Example: How would React fetch data from a DRF API?**
Frontend React:

```jsx
useEffect(() => {
  fetch("http://127.0.0.1:8000/api/posts/")
    .then((res) => res.json())
    .then((data) => setPosts(data));
}, []);
```

Backend DRF (urls.py):

```python
from rest_framework.routers import DefaultRouter
from .views import PostViewSet

router = DefaultRouter()
router.register(r'posts', PostViewSet)
urlpatterns = router.urls
```
