python setup.py install
sudo apt-get install -y npm
npm install -g bower

# Aplicación flask 

Aplicación que integra flask con el tema gentellela utilizando MongoDB como base de datos

## Getting Started

Permite tener una versión inicial de la aplicación

### Prerequisites


```
mongoDB
npm
virtualenv

```

### Installing

Instalar bower

```
npm install -g bower
```
Instalar las librerias Js, correr el comando en la raiz del proyecto.


```
bower install
```

Generar el archivo de configuración de la aplicación


```
cp config.ini.template config.ini
```

Crear ambiente de la aplicación


```
mkvirtualenv flask-app
```

Instalar aplicación


```
python setup.py install
```

Correr aplicación


```
python run.py
```

## Adicionales

Configuraciones adicionales en caso de ser necesarias

### Supervisord

Archivo de configuración para supervisord y se añade formula para utilizar con gunicorn

```
[program:flask-app.domain.com]
;command=/home/<user>/.virtualenvs/flask-app/bin/gunicorn -w 4 -b 0.0.0.0:6001 --timeout 180 --error-logfile /var/www/flask-app.domain.com/gunicorn_error.log --log-level info run:app
command=/home/<user>/.virtualenvs/flask-app/bin/python /var/www/flask-app.domain.com/run.py
autorestart=false
user=jano
autostart=false
directory=/var/www/flask-app.domain.com/
logfile=/var/log/supervisor/flask-app.domain.com.log
redirect_stderr=true
stopasgroup=true
exitcodes=1

```

### Nginx

Archivo de configuración para nginx

```
server {
  listen   80;
  server_name  flask-app.domain.com;
  access_log  /var/log/nginx/flask-app.domain.com.access.log;
  error_log  /var/log/nginx/flask-app.domain.com.error.log notice;
  rewrite_log on;
  index index.php index.html;

  location / {
     client_max_body_size 50M;
     proxy_pass http://localhost:<port>;
  }
  location /static/ {
      root /var/www/flask-app.domain.com/app;
      autoindex off;
  }

}

```

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```



## Acknowledgments

* Hat tip to anyone who's code was used
* Inspiration
* etc
