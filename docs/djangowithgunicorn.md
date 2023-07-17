## Django with Gunicorn

[Gunicorn](https://gunicorn.org/) (‘Green Unicorn’) is a pure-Python WSGI server for UNIX. It has no dependencies and can be installed using pip.

Installing Gunicorn
```
pip install gunicorn
```

### Running Django in Gunicorn as a generic WSGI application
Command to run Django project using Gunicorn app server
```
guncorn myproject:wsgi
```

_Note: Application server doesn't serve static files except in development server which means we can't able to access css, js, images... files_
