# FSND - Linux Configuration

This documentation attempts to list down everything needed to access the Linux server and use the catalog app. Included in this document are also all known installations and configurations done to achieve a working server.

## Accessing the website

The public IP address is **52.221.206.188**. The web site can thus be accessed by any browser using HTTP (port 80) in that address. However, due to Google OAuth2 limitations, logging in is not possible from that IP. In the Google developer console, the permission has been set for the following site only:

```
http://mysite.52.221.206.188.xip.io
```

This will allow the server to use Google credentials and handle redirects. However, browsing the item catalog should be fine with just the IP address.

## Accessing the server

To directly access the Linux server, the IP is the same as above (52.221.206.188), and the SSH port is 2200. The server is configured to only allow key based authentication, so a private key is needed. The account name is "grader" without the quotation marks.

## Summary of software installed

* Apache
* PostgreSQL
* Git
* Python libraries:
  - Flask
  - SQLAlchemy
  - oauth2client
  - passlib
  - httplib2
  - mod_wsgi

## Summary of configuration changes made

### General configuration

* Disabled remote root login (file: /etc/ssh/sshd_config, line: PermitRootLogin no)
* Forced key based login
* Set up a firewall to only allow incoming traffic from ports 80, 2200 and 123. All outgoing traffic is allowed
* Changed server time to UTC
* Made a PostgreSQL user named cataloguser (password catalog) with less privileges
* Verified that PostgreSQL remote connections are disabled

### App deployment configuration

* The catalog app is located at /var/www/catalog
* Created a WSGI script (located at /var/www/catalog/catalog.wsgi)
* Configured a sites-enabled file (located at /etc/apache2/sites-available/catalog.conf)
* Configured a virtual environment (located at /var/www/catalog/catalog/venv)

### Catalog app changes

* Database changed from SQLite to PostgreSQL
* client_secrets.json file path specified

## Summary of third-party resources used

* Google OAuth2: configured it to allow authentication requests from this site
* xip.io: to create proper URI for Google authentication
* Udacity Linux Configuration videos
* Udacity discussions
* Main info on WSGI: http://flask.pocoo.org/docs/1.0/deploying/mod_wsgi/
* General flow for the setup: https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
* Some random tidbits: https://www.fullstackpython.com/wsgi-servers.html
* Some more random info: http://www.bogotobogo.com/python/Flask/Python_Flask_HelloWorld_App_with_Apache_WSGI_Ubuntu14.php
* For help with creating PostgreSQL databases and users: https://www.a2hosting.sg/kb/developer-corner/postgresql/managing-postgresql-databases-and-users-from-the-command-line
* Database help: https://www.postgresql.org/docs/9.1/static/manage-ag-createdb.html
* Virtual environments: https://modwsgi.readthedocs.io/en/develop/user-guides/virtual-environments.html
* Debugging help: https://serverfault.com/questions/239614/wsgi-and-python-print-statements
* For help with disabling remote logins in PostgreSQ: https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps
* + random websites for minor details that cannot be traced back anymore


