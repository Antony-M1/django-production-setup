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

## Testing Gunicorn’s Ability to Serve the Project
You can test this by entering the project directory and using gunicorn to load the project’s WSGI module:
```
gunicorn --bind 0.0.0.0:8000 myproject.wsgi
```
This will start Gunicorn on the same interface that the Django development server was runnig on. You can go back and test the app again in your browser

_Note: The admin interface will not have any of the styling applied since **Gunicorn does not know how to find the static CSS content** responsible for this_

## Creating systemd Socket and Service Files for Gunicorn
We have tested that Gunicorn can interact with our Django application, but we should now implement a more robust way of starting and stopping the application server.
To accomplish this, We'll make [systemd](https://chat.openai.com/share/35085535-9f16-4ade-ad28-24371e24d94d) service and socket files

Start by creating and opening a systemd socket file for Gunicorn with sudo privileges:
```
sudo nano /etc/systemd/system/gunicorn.socket
```

Inside, you will create a [Unit] section to describe the socket, a [Socket] section to define the socket location, and an [Install] section to make sure the socket is created at the right time:

### gunicorn.socket
```
[Unit]
Description=gunicorn socket

[Socket]
ListenStream=/run/gunicorn.sock

[Install]
WantedBy=sockets.target
```
Save and close the file when you are finished

Next, Create and open a systemd service file for Gunicorn with sudo privileges in your text editor. The service filename should match the socket filename with exception of the extension
```
sudo nano /etc/systemd/system/gunicorn.service
```
### gunicorn.service
```
[Unit]
Description=gunicorn daemon
Requires=gunicorn.socket
After=network.target

[Service]
User=ubuntu
Group=www-data
WorkingDirectory=/home/ubuntu/myprojectdir
ExecStart=/home/ubuntu/myprojectdir/myprojectenv/bin/gunicorn \
          --access-logfile - \
          --workers 3 \
          --bind unix:/run/gunicorn.sock \
          myproject.wsgi:application

[Install]
WantedBy=multi-user.target
```
With that, your systemd service file is complete. Save and close it now.

You can now start and enable the Gunicorn socket. This will create the socket file at /run/gunicorn.sock now and at boot. When a connection is made to that socket, systemd will automatically start the gunicorn.service to handle it:
```
sudo systemctl start gunicorn.socket
sudo systemctl enable gunicorn.socket
```
You can confirm that the operation was successful by checking for the socket file.






