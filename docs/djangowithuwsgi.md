## Django with uWSGI
[uWSGI](https://uwsgi-docs.readthedocs.io/) is a fast, self-healing and developer/sysadmin-friendly application container server coded in pure C.

### Prerequisite: uWSGI¶
command to install uWSGI
```
pip install uwsgi
```

### uWSGI model
uWSGI operates on a client-server model. Your web server (e.g., nginx, Apache) communicates with a django-uwsgi “worker” process to serve dynamic content.
