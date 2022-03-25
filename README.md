# Docker LAMP
LAMP stack with phpMyAdmin, Mailhog (for e-mail debugging), composer version
 2, xdebug and WP CLI.

## Website installation
The website must be installed in the `site` directory, the `site/public`
directory is the public directory.

## Tools
### phpMyAdmin
[http://localhost:5000/](http://localhost:5000/)

### Email debugging

To debug emails you can use MailHog, you can reach it at: [http://localhost:8025/](http://localhost:8025/)

## PHP and Apache customization
Apache Virtualhost can be customized in the file `config/apache/000.default.conf`  
php.ini settings can be overriden with the file `config/php/override-php.ini`

## Common commands
Start and stop:  
`docker-compose up -d`  
`docker-compose stop`

Open a terminal inside the webserver container:  
`docker-compose exec -u $USER phpapache bash`  

Open a terminal inside the database container to use MySQL CLI:  
`docker-compose exec dbserver bash`  
`mysql -u root -p`  
The mySQL password is defined in the `.env` file.

Rebuild the phpapache container after a change to the Dockerfile:  
`docker-compose build`

## Error logs

### Apache

They are in `/var/log/apache2` with name `docker-lamp\*.log`

### PHP

File: `/var/log/apache2/php-errors.log`  
The location can be changed in the file `config/php/override-php.ini`, parameter `error_log`
