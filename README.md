# Docker lamp

## Email debugging

To debug emails you can use MailHog, you can reach it at: [http://localhost:8025/](http://localhost:8025/)

## Error logs

### Apache

They are in /var/log/apache2 with name docker-lamp\*.log

### PHP

File: /var/log/apache2/php-errors.log  
The location can be changed in the file config/php/override-php.ini, parameter error_log
