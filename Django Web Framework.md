# Django

- Django is based on MVT (model, view, template) pattern
- Django is high-level python web framework
- It gives rapid development and clean, pragmatic design
- Its free and open source
- Model : Structure and manipulating the data of web application
- View : Encapsulate the logic responsible for processing a user's request and for returning the response.
- Template : Provides designer friendly syntax for rendering the information to be presented to the user.

## Steps to install Django

- `pip install django`
- `pip install djangorestframework`
- `pip install pillow`

## Setup django project

- django-admin startproject `project_name`
- cd `project_directory`
- python manage.py startapp `app_name`
- python manage.py makemigrations
- python manage.py migrate
- python mange.py runserver

## Project Directory

```apache
  |-- App1/
  |-- App2/
  |-- templates/
  |-- static/
  |-- media/
  |-- project/
  |-- manage.py
  |-- sqlite.db
```

## GET and POST method

- GET Method does not require CSRF token.
- GET Method shows all the attribute in url box with assigned value.
- POST Method requires CSRF token.
- POST Method does not show attributes in url box.

---

## Essential changes

### 1. Setup the templates folder

- Create `templates` folder inside the project directory
- In `project_directory/settings.py` file, add `'DIRS' : [os.path.join(BASE_DIR, 'templates')],` inside the `TEMPLATES` list

### 2. Setup the static folder

- Create `static` folder inside the project directory
- In `project_directory/settings.py` file, add `'STATICFILES_DIRS' : [os.path.join(BASE_DIR, 'static')],` next line to `STATIC_URL = '/static/'`

### 3. Connect APPs with Project

- Add `APP_Name` inside the `INSTALLED_APPS` list

### 4. Setup urls

- Import `path` and `include` from `django.urls`
- Add `APP.urls` in `urlpatterns` list

```python
    from django.urls import path, include

    urlpatterns = [
        path("", include("APP_NAME.urls")),
    ]
```

### 5. Setup urls in APP

- Create `urls.py` file inside the APP directory
- Import `path` and `views`

```python
    from django.urls import path
    from . import views

    urlpatterns = [
        path('site_name', views.function_name, name='site-name'),
    ]
```

### 6. Setup Views in APP

- Import `render`, `redirect`, `HttpResponse`
- Define function

  ```python
  from django.shortcuts import render, redirect, HttpResponse

  def Home(request):
      return render(request, 'html_file')
  ```

### 7. Setup Models in APP

- Import `model`
- Setup fields as Following Example

```python
   from django.db import models

   class Database(models.Model):
       char = models.CharField()
       text = models.TextField()
       date = models.DateField()
       time = models.TimeField()
       datetime = models.DateTimeField()
       int = models.IntegerField()
```

## Create Form

- Create `forms.py` file inside the App
- Import `forms`
- Setup form
- Eg.

  ```python
  from django import forms

  class Form(forms.Form):
      char = forms.CharField(label = '', widget=forms.TextInput(attrs = {'class' : ''}))
      url = forms.URLField(label = '', widget=forms.URLInput(attrs= {'class' : ''}))
      key = forms.CharField(label='password', widget=forms.PasswordInput(attrs={'class' : ''}))
  ```

## Create 404 error handle page

- Create `page_not_found` function inside `APP\views.py` file
  ```python
  def page_not_found(request, exception):
      return render(request, 'page_not_found.html')
  ```
- Add this view in `APP\urls.py` file
  ```python
  urlpatterns = [
      path('error', views.page_not_found, name="404_handler")
  ]
  ```
- Link this file with `projects_dir\urls.py`
  ```python
  handler404 = 'APP.views.page_not_found'
  ```
- Restart the server

---
