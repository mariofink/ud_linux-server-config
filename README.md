# Linux Server Configuration Project

IP address: 18.219.142.131

Url: http://18.219.142.131/

**Connecting via SSH:**

    ssh -i ~/.ssh/<key> ubuntu@18.219.142.131 -p 2200

## Software

* PostgreSQL
* Apache
* mod_wsgi

## Configuration

### PostgreSQL

Add a database user for the catalog application:

    postgres=# CREATE DATABASE catalog;
    postgres=# CREATE USER catalog WITH PASSWORD 'catalog';
    CREATE ROLE
    CREATE DATABASE
    postgres=# GRANT ALL PRIVILEGES ON DATABASE "catalog" to catalog;
    
### Python application

Create a virtual environment in /var/www/fullstack-nanodegree-vm/vagrant/catalog/

    virtualenv venv

Install dependencies via pip in  /var/www/fullstack-nanodegree-vm/vagrant/catalog/

    pip install -r requirements.txt

### Apache

Site configuration:
**/etc/apache2/sites-available/000-default.conf**

    WSGIPythonHome /var/www/fullstack-nanodegree-vm/vagrant/catalog/venv
    <VirtualHost *:80>
            ServerAdmin webmaster@localhost
            DocumentRoot /var/www/html
            ErrorLog ${APACHE_LOG_DIR}/error.log
            CustomLog ${APACHE_LOG_DIR}/access.log combined
            WSGIScriptAlias / /var/www/fullstack-nanodegree-vm/vagrant/catalog/catalog.wsgi
    </VirtualHost>


## Random notes
When using pip there were some strange errors popping up surrounding locales.
I found a fix for this here: https://stackoverflow.com/questions/14547631/python-locale-error-unsupported-locale-setting#36257050

    export LC_ALL="en_US.UTF-8"
    export LC_CTYPE="en_US.UTF-8"
    sudo dpkg-reconfigure locales
        
        
