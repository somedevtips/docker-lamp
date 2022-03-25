# Docker lamp

## Tools
### phpMyAdmin
[http://localhost:5000/](http://localhost:5000/)

### Email debugging

To debug emails you can use MailHog, you can reach it at: [http://localhost:8025/](http://localhost:8025/)

## Common commands
Open a terminal inside the webserver container:  
`docker-compose exec -u $USER phpapache bash`  
  
Rebuild the phpapache container after a change to the Dockerfile:  
`docker-compose build`

## Error logs

### Apache

They are in `/var/log/apache2` with name `docker-lamp\*.log`

### PHP

File: `/var/log/apache2/php-errors.log`  
The location can be changed in the file `config/php/override-php.ini`, parameter `error_log`
