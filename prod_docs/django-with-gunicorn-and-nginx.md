# DJANGO PRODUCTION SETUP WITH GUNICORN & NGINX
### Prerequisites
- Gunicorn
- Nginx &
Required packages for your project

_Note: Please make sure your project running correctly and 
Be sure to include localhost as one of the options in allowed hosts since you will be proxying connections through a local Nginx instance._ 

### settings.py

```
ALLOWED_HOSTS = ['your_server_domain_or_IP', 'second_domain_or_IP', . . ., 'localhost']

```
```
STATIC_URL = 'static/'

# Default primary key field type
# https://docs.djangoproject.com/en/4.0/ref/settings/#default-auto-field

DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'

import os
STATIC_ROOT = os.path.join(BASE_DIR, 'static/')
```
## Completing initial project setup
```
python manage.py makemigrations
python manage.py migrate
```
You can collect all of the static content into the directory location that you configured by typing:
```
python manage.py collectstatic
```
You will have to confirm the operation. The static files will then be placed in a directory called static within your project directory.
