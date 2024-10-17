# [Django Dynamic API](https://app-generator.dev/docs/developer-tools/dynamic-api.html)

Simple tool that **Generates Secure APIs** on top of `DRF` with minimum effort - actively supported by **[App-Generator](https://app-generator.dev/)**.

- [Dynamic API Features](https://www.youtube.com/watch?v=nPQMUafTrNY) - video presentation

<br />

---

> For a **complete set of features** and long-term support, check out **[Dynamic Django](https://app-generator.dev/docs/developer-tools/dynamic-django/index.html)**, a powerful starter that incorporates:

- [Dynamic DataTables](https://app-generator.dev/docs/developer-tools/dynamic-django/datatables.html): using a single line of configuration, the data saved in any table is automatically managed
- [Dynamic API](https://app-generator.dev/docs/developer-tools/dynamic-django/api.html): any model can become a secure API Endpoint using DRF
- [Dynamic Charts](https://app-generator.dev/docs/developer-tools/dynamic-django/charts.html): extract relevant charts without coding all major types are supported
- [CSV Loader](https://app-generator.dev/docs/developer-tools/dynamic-django/csv-loader.html): translate CSV files into Django Models and (optional) load the information
- Powerful [CLI Tools](https://app-generator.dev/docs/developer-tools/dynamic-django/cli.html) for the GIT interface, configuration editing, updating the configuration and database (create models, migrate DB)

<br />

## `Dynamic API Features` 

- `API engine` provided by `DRF`
- `Minimal Configuration` (single line in config for each model)
- `Handles any model` defined across the project

<br />

![Django Dynamic API - DRF Interface (open-source tool).](https://user-images.githubusercontent.com/51070104/197181145-f7458df7-23c3-4c14-bcb1-8e168882a104.jpg)

<br />

## How to use it

<br />

> **Step #1** - `Install the package` 

```bash
$ pip install django-dynamic-api
// OR
$ pip install git+https://github.com/app-generator/django-dynamic-api.git
```

<br />

> **Step #2** - `Update Configuration`, include the new APPs

```python
INSTALLED_APPS = [
    'django_dyn_api',            # Django Dynamic API  # <-- NEW
    'rest_framework',            # Include DRF         # <-- NEW 
    'rest_framework.authtoken',  # Include DRF Auth    # <-- NEW   
]
```

<br />

> **Step #3** - `Register the model` in `core/settings.py` (DYNAMIC_API section)

This sample code assumes that `app1` exists and model `Book` is defined and migrated.

```python

DYNAMIC_API = {
    # pattern: 
    # API_SLUG -> Import_PATH 
    'books'  : "app1.models.Book",
}

REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.TokenAuthentication',
    ],
}

```

<br />

> **Step #4** - `Migrate DB` and create the tables used by `DRF` 

```bash
$ python manage.py makemigrations
$ python manage.py migrate
```

<br />

> **Step #5** - `Update routing`, include APIs 

```python
from django.contrib import admin
from django.urls import path, include                        # <-- UPD: 'include` directive
from rest_framework.authtoken.views import obtain_auth_token # <-- NEW

urlpatterns = [
    path("admin/", admin.site.urls),
    path('', include('django_dyn_api.urls')),     # <-- NEW
    path('login/jwt/', view=obtain_auth_token),   # <-- NEW
]    
```    

<br />

> **Step #6** - `Use API` 

If the managed model is `Books`, the API interface is `/api/books/` and all CRUD methods are available. 

> Note: for mutating requests, the `JWT Token` is provided by `http://localhost:8000/login/jwt/` route (the user should exist). 

<br />

![Django API Generator - POSTMAN Interface (open-source tool).](https://user-images.githubusercontent.com/51070104/197181265-eb648e27-e5cf-4f3c-b330-d000aba53c6a.jpg)

<br />

### Links & resources 

- [DRF](https://www.django-rest-framework.org/) - HOMEpage
- More [Developer Tools](https://appseed.us/developer-tools/) provided by `AppSeed`
- Ask for [Support](https://appseed.us/support/) via `Email` & `Discord` 

<br />

---
[Django Dynamic API](https://app-generator.dev/docs/developer-tools/dynamic-api.html) - Open-source library provided by **[App-Generator](https://app-generator.dev/)**
