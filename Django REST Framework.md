# Django-REST API

---

## HTTP (Hyper Text Transfer Protocol) methods

- The GET method requests a representation of the specified resource. Requests using GET should only retrieve data.
- The HEAD method ask for a response identical to that of the GET request, but without the response body.
- The POST method is used to submit an entity to the specified resource, often causing a change in state or side effect on the server.
- The PUT method repalces all current representations of the target resource with the request payload.
- The DELETE method deletes the specified resource.
- The CONNECT method established a tunnel to the server identified by the target resource.
- The OPTIONS method is used to describe the communication options for the target resouce.
- The TRACE method performs a message loop-back test along the path to the target resource.
- The PATCH method is used to apply partial modifications to a resource.

## HTTP Status Codes

### Response range

1. Information responses - (100 - 199)
2. Successful responses - (200 - 299)
3. Redirects (300 - 399)
4. Client errors (400 -499)
5. Server errors (500 -599)

---

## API (Application Program Interface) -

- - Provider: The compony or developer who provide the API
  - Comsumer: The compony or person who use the API

    ### Types of API -


    - Private : It can be used within organization.
    - Partner : It can be used within business and business partners.
    - Public : It can be used any third party developers.

    ### API Key -

    - While Register/sign up with API, it provides Unique key as API key.
    - This key is used while communicating, API shares the API key for validation.

    ### How API works -

    - Client device make requests to API.
    - API will communicate with Application/Database.
    - Application/Database provides required data to API.
    - API return the requests to Client.

---

## REST API -

- It stands for Representational State Transfer.
- It is an architecheral design for develop web API.
- The API which developed using **REST** is known as **REST API/RESTful API**.
- REST API Crud operations:

  - POST : Create
  - GET : Read
  - PUT, PATCH : Update : PUT - Complete Update, PATCH - Partial Update
  - DELETE : Delete

---

## Django REST framework -

- Django REST Framework is a powerful and flexible toolkit for building web APIs.

  - The web browsable API is a huge usability win for your developers.
  - Authentication policies including packages for OAuth1 and OAuth2.
  - Serialization that supports ORM and non-ORM data sources.
  - Customizable all the way down - just use regular function-based views if you don't need the more powerful features.
  - Extensive documentation and great community support.
  - Used and trusted by internationally recognized componies including Mozilla, Red Hat, Heroku and Eventbrite.
- Packages:

  - ***djangorestframework*** - REST Framework libraries.
  - ***pyYAML***, ***uritemplate*** - Schema generation support.
  - ***Markdown*** - Markdown support for browsable API.
  - ***pygments*** - Add syntax highlighting to Markdown processing.
  - ***django-filter*** - Filtering support.
  - ***django-guardian*** - Object level permissions support.

## Django ORM (Object-Relational-Mapper)

- It provides an abstraction layer for interacting with relational databases using Python code instead of SQL queries.
- Eg.

  - SQL Query:

    ```sql
    CREATE TABLE customer (
        ID INT(10), First_Name VARCHAR(20) PRIMARY KEY,
        Middle_Name VARCHAR(20) NOT NULL,
        Last_Name VARCHAR(20) NOT NULL,
        Department VARCHAR(20) NOT NULL,
        Joining_Date DATETIME NOT NULL);
    ```
  - Django ORM:

    ```python
    class customer(models.Model):
        ID = models.IntegerField(max_length=10)
        First_Name = models.CharField(max_length=20)
        Middle_Name = models.CharField(max_length=20)
        Last_Name = models.CharField(max_length=20)
        Joining_Date = models.DateTimeField()

        def __str__(self):
            return self.ID
    ```

---

## Django REST Framework

### 1. Connect REST Framework with Django-

- Add `rest_framework` in `INSTALLED_APPS` list inside the settings.py file.

### 2. Serializers -

- Serializers are responsible for converting complex data such querysets and model instance to native Python datatypes (called serialization) that can then easily rendered into JSON or XML or other context types which understandable by Front end.
- It also provide Deserialization.
- `Serialization` - `Complex DataType` (querysets) to `Python native DataType` (dictionary).
- `Render into JSON` - `Python native DataType` (dictionary) to `JSON Data`.
- **Serializer class**: It gives a powerful, generic way to control the output of your responses, as well as a ModelSerializer class which provides a useful shortcut for creating serializers that deal with model instances and querysets.
- Steps to create serializer class

  - Create a separate `seriealizers.py` file to write all serializers
  - import serializers from rest_framework `from rest_framework import serializers`
  - create class inherited with serializer.
    ```python
    class _Serializer(serializers.Serializer):
       name = serializers.CharField(max_length = 20)
       roll = serializers.IntegerField()
       city = serializers.CharField(max_length = 20)
    ```
- Serialization:

  - For single tuple:
    - Query set instance : `obj = Dataset.objects.get(id=1)`
    - Converting into Dict : `serializer = _Serializer(obj)`
  - For whole Query Set:
    - Query set instance : `obj = Dataset.objects.all()`
    - Converting into Dict : `serializer = _Serializer(obj, many=True)`
  - Get serialized data: `print(serializer.data)`
- JSON Renderer:

  - importing JSONRender : `from rest_framework.renderers import JSONRenderer`
  - Render the Data into Json : `json_data = JSONRenderer().render(serializer.data)`
- JSON Response:

  - Syntax : `JsonResponse(data, encoder=DjangoJSONEncoder, safe=True, json_dumps_params=None, **kwargs)`
  - An HttpResponse subclass that helps to create a JSON-encoded response. It inherits most behavior from its superclass.

### 3. Viewsets -

- Django REST Framework allows you to combine the logic for a set of related views in a single class, called Viewsets.

---
