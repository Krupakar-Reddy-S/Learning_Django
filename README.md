# Learning Django

## Introduction to Django

Django is a high-level Python web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source.

It is used by many big companies like Instagram, Pinterest, Mozilla, The Washington Times, and the Public Broadcasting Service.

## Getting Started With Django

### Installation and Setup

1. **Virtual Environment**: It is recommended to use a virtual environment to keep your project dependencies separate from your system dependencies. To create a virtual environment, run the following command:

    ```bash
    python3 -m venv .venv
    ```

    To activate the virtual environment, run the following command:

    ```bash
    source myenv/bin/activate
    ```
2. **Django Installation**: To install Django, run the following command:

    ```bash
    pip install django
    ```

3. **Create a Django Project**: To create a new Django project, run the following command:

    ```bash
    django-admin startproject <project_name>
    ```

    This will create a new directory with the project name and the following files:

    - `manage.py`: A command-line utility that lets you interact with this Django project.

    - `<project_name>/`: The actual Python package for your project. It is the primary container for the project.
    - `<project_name>/__init__.py`: An empty file that tells Python that this directory should be considered a Python package.
    - `<project_name>/settings.py`: Settings/configuration for this Django project.
    - `<project_name>/urls.py`: The URL declarations for this Django project.
    - `<project_name>/wsgi.py`: An entry-point for WSGI-compatible web servers to serve your project.
    - `<project_name>/asgi.py`: An entry-point for ASGI-compatible web servers to serve your project.

4. **Run the Server**: To run the server, navigate to the project directory and run the following command:

    ```bash
    python manage.py runserver
    ```

    This will start the development server at `http://127.0.0.1:8000/` by default.

### Apps in Django

1. **What is an App?**:
    Django projects are composed of multiple apps. An app is a web application that does something – e.g., a blog system, a database of public records, a small poll app, etc. An app can be in multiple projects, and you can package and distribute them for use by others in their projects.

2. **Create a Django App**: To create a new Django app, run the following command:

    ```bash
    python manage.py startapp <app_name>
    ```

    This will create a new directory with the app name and the following files:

    - `<app_name>/`: The actual Python package for your app.

    - `<app_name>/__init__.py`: An empty file that tells Python that this directory should be considered a Python package.
    - `<app_name>/admin.py`: A configuration file for the Django admin interface.
    - `<app_name>/apps.py`: A configuration file for the app itself.
    - `<app_name>/models.py`: The database schema for this app.
    - `<app_name>/tests.py`: A package for the app's tests.
    - `<app_name>/views.py`: The views for this app.

3. **Include the App in the Project and connect URLs**:

    To include the app in the project, add the app name to the `INSTALLED_APPS` list in the `settings.py` file.

    We also need to include the app's URL configuration in the project's URL configuration. This is done by including the app's URL configuration in the `urlpatterns` list in the `urls.py` file for each app and then including the app's URL configuration in the project's URL configuration.
    
    ```python
    # project/urls.py
    from django.urls import include, path

    urlpatterns = [
        path('app/', include('app.urls')),
    ]
    ```

    ```python
    # app/urls.py
    from django.urls import path
    from . import views

    urlpatterns = [
        path('', views.index, name='index'),
    ]
    ``` 

## Architecture of Django

Django follows the Model-View-Template (MVT) architecture. The MVT architecture is a variation of the Model-View-Controller (MVC) architecture. In Django, the MVT architecture consists of the following components:

1. **Model**: The model is the data access layer. It handles the data access and is responsible for the data-related logic. This is similar to the `model` in the MVC architecture.

2. **View**: The view is the business logic layer. It handles the user interaction and is responsible for processing the user requests. This is similar to the `controller` in the MVC architecture.

3. **Template**: The template is the presentation layer. It handles the user interface and is responsible for rendering the data. This is similar to the `view` in the MVC architecture.

In the MVT architecture, the view is responsible for processing the user requests and returning the response. It interacts with the model to fetch and store the data. The template is responsible for rendering the data and presenting it to the user.

## Jinja Templating Engine

Django uses the Jinja templating engine to render the templates. Jinja is a fast, expressive, and extensible templating engine. It is similar to the Django template engine but provides more features and flexibility.

Jinja templates are HTML files with special syntax for inserting variables, expressions, and control structures. Jinja templates can include template inheritance, macros, filters, and other advanced features.

1. **Variables and Expression**: Jinja templates can include variables and expressions enclosed in double curly braces `{{ ... }}`. For example:

    ```html
    <h1>Hello, {{ name }}!</h1>

    <p>{{ 2 + 2 }}</p>
    ```

2. **blocks**: Jinja templates can include blocks enclosed in curly braces `{% ... %}`. For example:

    ```html
    {% block content %}
        <h1>Hello, {{ name }}!</h1>
    {% endblock %}
    ``` 

3. **Control Structures**: Jinja templates can include control structures like `if`, `for`, and `block`. For example:

    ```html
    {% if user.is_authenticated %}
        <p>Welcome, {{ user.username }}!</p>
    {% else %}
        <p>Please log in to continue.</p>
    {% endif %}
    ```

4. **Template Inheritance**: Jinja templates can include template inheritance using the `extends` and `block` tags. For example:

    ```html
    {% extends "base.html" %}

    {% block content %}
        <h1>Hello, {{ name }}!</h1>
    {% endblock %}
    ```

5. **Filters**: Jinja templates can include filters to modify the output. For example:

    ```html
    <p>{{ text|capitalize }}</p>
    ```

6. **Macros**: Jinja templates can include macros to define reusable blocks of code. For example:

    ```html
    {% macro hello(name) %}
        <p>Hello, {{ name }}!</p>
    {% endmacro %}
    ```

7. **Include**: Jinja templates can include other templates using the `include` tag. For example:

    ```html
    {% include "header.html" %}
    ```

## Static Files in Django

Static files are files that are served directly to the user without any processing by the server. These files include CSS files, JavaScript files, images, fonts, and other assets that are used to style and enhance the user interface.

In Django, static files are stored in the `static` directory of each app. The `static` directory can contain subdirectories for organizing the static files. For example:

```plaintext
app/
└── static/
    ├── css/
    │   └── style.css
    ├── js/
    │   └── script.js
    └── img/
        └── logo.png
```

To include static files in a template, use the `{% static %}` template tag. For example:

```html
{% load static %}
<link rel="stylesheet" href="{% static 'css/style.css' %}">
<script src="{% static 'js/script.js' %}"></script>
<img src="{% static 'img/logo.png' %}" alt="Logo">
```

To serve static files during development, add the followign to `settings.py`:

```python
# settings.py
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static'),
]
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
```

Use the `collectstatic` command to collect the static files into the `STATIC_ROOT` directory:

```bash
python manage.py collectstatic
```

Now, the static files will be served from the `STATIC_ROOT` directory, and the `{% static %}` template tag will generate the correct URLs for the static files directly.

