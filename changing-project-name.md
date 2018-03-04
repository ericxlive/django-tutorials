
### Rename directories

First rename your project directory "yourprojectname" and the following inside. 

```
              yourprojectname/
                   |-- manage.py 
                   |-- yourprojectname/ 
                          |-- __init__.py 
                          |-- settings.py 
                          |-- urls.py 
                          |-- wsgi.py
```



### settings.py ###

ROOT_URLCONF = 'NewProjectName.urls'
WSGI_APPLICATION = 'NewProjectName.wsgi.application'

### manage.py ###

os.environ.setdefault("DJANGO_SETTINGS_MODULE", "NewProjectName.settings")

### wsgi.py ###

os.environ.setdefault("DJANGO_SETTINGS_MODULE", "NewProjectName.settings")
