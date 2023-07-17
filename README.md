# Django Deployment

### Django currently supports two interfaces: WSGI and ASGI.
- [WSGI](https://wsgi.readthedocs.io/en/latest/) is the main Python standard for communicating between web servers and applications, but it only supports synchronous code.
- [ASGI](https://asgi.readthedocs.io/en/latest/) is the new, asynchronous-friendly standard that will allow your Django site to use asynchronous Python features, and asynchronous Django features as they are developed.

## Deploy with WSGI
- [How to use Django with Gunicorn](https://github.com/Antony-M1/django-production-setup/blob/dev/docs/How-to-use-Django-with-Gunicorn.md)
- [How to use Django with uWsgi](url)
- [How to use Django with Apache & mod_wsgi](url)
- [How to authenticate against Django’s user database from Apache](url)
- [The application object](url)
- [Configuring the settings module](url)
- [Applying WSGI middleware](url)

## Deploy with ASGI
- [How to use Django with Daphne](url)
- [How to use Django with Hypercorn](url)
- [How to use Django with Uvicorn](url)
- [The application object](url)
- [Configuring the settings module](url)
- [Applying ASGI middleware](url)

## Deployment checklist
The below checklist needs to be done once the deployment is done
- [Run manage.py check --deploy](url)
- [Critical settings](url)
- [Environment-specific settings](url)
- [HTTPS](url)
- [Performance optimizations](url)
- [Error reporting](url)
