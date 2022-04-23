# Docker LAMP
LAMP stack with phpMyAdmin, Mailhog (for e-mail debugging), composer version
 2, xdebug, git and WP CLI.

## Setup
The following instructions are for the Linux operating system.  
To start using this development environment you have to:  

1. get the id, the group and the group id of your current Linux user, 
for example if your current user is `giancarlo` the commands are:  
get the user id: `id -u giancarlo`  
get the group name: `id -gn giancarlo`  
get the group id: `id -g giancarlo`  

2. fill in the `.env` file with the information above
3. change the MySql password in the `.env` file (optional)
4. run the command `docker-compose up -d` to have the docker images 
built and the containers running.

## Website installation
The website must be installed in the `site` directory, the `site/public`
directory is the public directory.

### WordPress installation
If your website is a WordPress site, you can install it with the 
following procedure:
```bash
cd site/public
wget http://wordpress.org/latest.tar.gz
tar xfz latest.tar.gz --strip 1
rm -f latest.tar.gz
```
Then: 
1. open phpMyAdmin at [http://localhost:5000/](http://localhost:5000/) 
2. create a new database
3. run the WordPress installation from [http://localhost/](http://localhost/) 
4. set  
DB host = `dbserver`  
DB user = `root`  
DB password =  password defined in the `.env` file.  
DB name = name of the database created at step 2

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
