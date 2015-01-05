# Optimized Nginx configuration for Wordpress

## Introduction 

   Nginx configuration for [WordPress](http://wordpress.org "WordPress").
   

## Features

   1. Invalid headers filtering.

   2. Access restriction: `install`, and `readme.html` files  

   3. Directory access restriction: `svn`, `git`, and much more.

   4. Secure and fast `PHP-FPM` handling.

   5. Apache as a backend support for PHP handling.
      
   6. [FLV](http://wiki.nginx.org/HttpFlvStreamModule), [H264/AAC](http://nginx.org/en/docs/http/ngx_http_mp4_module.html) streaming support

## Basic Auth for access to restricted files like install.php

   `install.php` is protected using Basic Auth. 
   To create username/password for that file:
   
   - Install `apache2-utils`.
   
   - Excute `htpasswd -d -b -c .htpasswd-users user password`

   - REMEMBER to delete the command from your bash history.

   You have to create the `.htpasswd-users` file with the user(s) and
   password(s). For that, if you're on Debian or any of its
   derivatives like Ubuntu you need the
   [apache2-utils](http://packages.debian.org/search?suite%3Dall&section%3Dall&arch%3Dany&searchon%3Dnames&keywords%3Dapache2-utils)
   package installed. Then create your password file by issuing:

          htpasswd -d -b -c .htpasswd-users <user> <password>


## Installation

   1. Move the old `/etc/nginx` to `/etc/nginx.old`.
   
   2. Clone the git repository from github:
   
      `git clone https://github.com/azoughbi/Wordpress.git`
   
   3. Edit `sites-available/example.dev.conf` and read the 2nd line
   
   4. Configure PHP-FPM:
      
      + [PHP FPM](http://www.php-fpm.org "PHP FPM"), You're required to
        configure php-fpm setup, this is can be done in
        `/etc/php5/fpm` directory.
        
        Get my [php-fpm example](https://github.com/azoughbi/wp-php-fpm-config) for
        an **example** of `php-fpm`.
        
      Check the socket if created and listening. 
      
      For unix sockets:

          netstat --unix -l
         
      For TCP sockets:   
         
          netstat -t -l
   
      It should display the PHP CGI socket.
   
      Note: the default socket listening to for php-fpm is:  
      
      `unix:/var/run/php-fpm.sock`
      
      update`upstream_phpcgi.conf` accordingly.
   
   
   5. Create the `/etc/nginx/sites-enabled` by excuting:
      `ln -s /etc/nginx/sites-available /etc/nginx/sites-enabled`

   6. Reload Nginx:
   
      `/etc/init.d/nginx reload`
   
   7. Check that your config is working by visiting the website
      in your browser.
   
   8. If everything is working, you can remove the `/etc/nginx.old` directory.
   
   9. Done.