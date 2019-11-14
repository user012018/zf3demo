Blog Sample
==================================================

This sample is based on the Hello World sample and it shows how to:

  * Integrate your web site with the Doctrine library
  * Initialize the database schema
  * Use the entity manager
  * Create entities and define relationships between entities
  * Create repositories


    │   composer.json    
    │   composer.lock    
    │   composer.phar    
    │   docker-compose.yml    
    │   Dockerfile    
    │   LICENSE.md    
    │   phpunit.xml.dist    
    │   README.md    
    │   Vagrantfile    
    │       
    ├───config    
    │   │   application.config.php    
    │   │   development.config.php.dist    
    │   │   modules.config.php    
    │   │       
    │   └───autoload    
    │           .gitignore    
    │           development.local.php.dist    
    │           global.php    
    │           local.php.dist    
    │           README.md    
    │           zend-developer-tools.local-development.php    
    │               
    ├───data    
    │   │   schema.mysql.sql    
    │   │       
    │   ├───cache    
    │   │       .gitignore    
    │   │           
    │   └───Migrations    
    │           Version20160901114333.php    
    │           Version20160901114938.php    
    │               
    ├───module    
    │   └───Application    
    │       ├───config    
    │       │       module.config.php    
    │       │           
    │       ├───src    
    │       │   │   Module.php    
    │       │   │       
    │       │   ├───Controller    
    │       │   │   │   IndexController.php    
    │       │   │   │   PostController.php    
    │       │   │   │       
    │       │   │   └───Factory    
    │       │   │           IndexControllerFactory.php    
    │       │   │           PostControllerFactory.php    
    │       │   │               
    │       │   ├───Entity    
    │       │   │       Comment.php    
    │       │   │       Post.php    
    │       │   │       Tag.php    
    │       │   │           
    │       │   ├───Form    
    │       │   │       CommentForm.php    
    │       │   │       PostForm.php    
    │       │   │           
    │       │   ├───Repository    
    │       │   │       PostRepository.php    
    │       │   │           
    │       │   ├───Service    
    │       │   │   │   PostManager.php    
    │       │   │   │       
    │       │   │   └───Factory    
    │       │   │           PostManagerFactory.php    
    │       │   │               
    │       │   └───View    
    │       │       └───Helper    
    │       │               Breadcrumbs.php    
    │       │               Menu.php    
    │       │                   
    │       ├───test    
    │       │   └───Controller    
    │       │           IndexControllerTest.php    
    │       │               
    │       └───view    
    │           ├───application    
    │           │   ├───index    
    │           │   │       about.phtml    
    │           │   │       index.phtml    
    │           │   │           
    │           │   ├───partial    
    │           │   │       paginator.phtml    
    │           │   │           
    │           │   └───post    
    │           │           add.phtml    
    │           │           admin.phtml    
    │           │           edit.phtml    
    │           │           view.phtml    
    │           │               
    │           ├───error    
    │           │       404.phtml    
    │           │       index.phtml    
    │           │           
    │           └───layout    
    │                   layout.phtml    
    │                       
    └───public    
        │   .htaccess    
        │   index.php    
        │       
        ├───css    
        │       bootstrap-theme.css    
        │       bootstrap-theme.css.map    
        │       bootstrap-theme.min.css    
        │       bootstrap-theme.min.css.map    
        │       bootstrap.css    
        │       bootstrap.css.map    
        │       bootstrap.min.css    
        │       bootstrap.min.css.map    
        │       style.css    
        │           
        ├───fonts    
        │       glyphicons-halflings-regular.eot    
        │       glyphicons-halflings-regular.svg    
        │       glyphicons-halflings-regular.ttf    
        │       glyphicons-halflings-regular.woff    
        │       glyphicons-halflings-regular.woff2    
        │           
        ├───img    
        │       favicon.ico    
        │       zf-logo.png    
        │           
        └───js    
                bootstrap.js    
                bootstrap.min.js    
                jquery-2.2.4.min.js









## Installation

You need to have Apache 2.4 HTTP server, PHP v.5.6 or later and MySQL v.5.6 or later.

Download the sample to some directory (it can be your home dir or `/var/www/html`) and run Composer as follows:

```
php composer.phar install
```

The command above will install the dependencies (Zend Framework and Doctrine).

Enable development mode:

```
php composer.phar development-enable
```

Adjust permissions for `data` directory:

```
sudo chown -R www-data:www-data data
sudo chmod -R 775 data
```

Create `config/autoload/local.php` config file by copying its distrib version:

```
cp config/autoload/local.php.dist config/autoload/local.php
```

Edit `config/autoload/local.php` and set database password parameter.

Login to MySQL client:

```
mysql -u root -p
```

Create database:

```
CREATE DATABASE blog;
GRANT ALL PRIVILEGES ON blog.* TO blog@localhost identified by '<your_password>';
quit
```

Create tables and import data to database:

```
mysql -u root -p blog < data/schema.mysql.sql
```

Alternatively, you can run database migrations:

```
./vendor/bin/doctrine-module migrations:migrate
```

Then create an Apache virtual host. It should look like below:

```
<VirtualHost *:80>
    DocumentRoot /path/to/blog/public
    
	<Directory /path/to/blog/public/>
        DirectoryIndex index.php
        AllowOverride All
        Require all granted
    </Directory>

</VirtualHost>
```
After creating the virtual host, restart Apache.

Now you should be able to see the Blog website by visiting the link "http://localhost/". 
 
## License

This code is provided under the [BSD-like license](https://en.wikipedia.org/wiki/BSD_licenses). 

## Contributing

If you found a mistake or a bug, please report it using the [Issues](https://github.com/olegkrivtsov/using-zf3-book-samples/issues) page. Your feedback is highly appreciated.
